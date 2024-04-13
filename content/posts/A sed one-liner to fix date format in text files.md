---
title: "A Sed One Liner to Fix Date Format in Text Files"
date: 2024-02-24T18:30:54Z
draft: false
tags:
    - Software
categories:
    - Tutorial
---
## TL;DR
This is a *know your tools entry*, although I absolutely don't know my tools as you will see if you read.

The following "one-liner" will change any wiki style link with a date string formatted as "Feb 22nd, 2024" to "2024-02-22", god's intended way to write a date.

Please forgive the search and replace gore of the second `sed`.

```
sed -E 's;([a-zA-Z]{3})\s([0-9]{1,})(st|nd|rd|th),\s([0-9]{4});\4-\1-\2;' "$1" | 
	sed -E 's/-Jan-/-01-/;s/-Feb-/-02-/;s/-Mar-/-03-/;s/-Apr-/-04-/;s/-May-/-05-/;s/-Jun-/-05-/;s/-Jul-/-07-/;s/-Aug-/-08-/;s/-Sep-/-09-/;s/-Oct-/-10-/;s/-Nov-/-11-/;s/-Dec-/-12-/' | 
	sed -E 's;-([0-9])\];-0\1];' > "$1".done
```

## The lore
I had a problem: [Logseq](https://logseq.com/) is my note taking software of choice, it's an [outliner](https://en.wikipedia.org/wiki/Outliner) which stores files in Markdown format so they are *time-proof*. Anyway, I wanted my Logseq wiki to be interoperable with [Obsidian](https://obsidian.md/) because the latter respects the Markdown a bit more than the former.

In Logseq you can create Journals/Daily notes, which are ways to track your daily tasks, meetings, or regular notes; or at least that is what I do.
A Journal is just another Markdown file and you can edit it as any other page, and one of the most convenient things of Logseq are its commands. 
There is a very convenient command called "Date picker", the way to use commands in Logseq is to type "/", then a menu pops up and you can search for the command you need, so if you continue typing "dat..." it will autocomplete to "Date picker", very handy.
However by default Logseq does two things I deeply hate:

1. Journals/Daily notes' filenames are in format "YYYY_MM_DD.md", (yes with underscores), which conflicts with the standard way Obsidian does it.
2. The date picker inserts a wiki style link with the format `[[MMM DDoo, YYYY]]`. If that is not clear,
    - `MMM` means localized month with three letters, e.g. "Aug" for August in english, "ago" for August in Spanish.
    - `DDoo` is the ordinal day of the month, e.g. 14th

I don't think this is standard notation for date formats but that's beyond the point.
So for instance for the 2 February 2024, the date picker will insert the link `[[Feb 2nd, 2024]]`

The first point is easy to fix, just modify either the settings in Obsidian or Logseq for both of them to agree in the way they use Journals/Daily notes.
The second point however, is more difficult, especially if you have been using Logseq for a few years and never bothered about how to configure it until recently (like me).
Why is this a problem? You may ask.
Well, Logseq has absolutely no problem following those links because internally it handles the date conversions or something like that, however when Obsidian sees a wikilink like
`[[The name of the file]]`
it searches the working directory for a file called
`The name of the file.md`,
so, if your link is
`[[Feb 24th, 2024]]`
Obsidian will look for 
`Feb 24th, 2024.md`
not for the actual name of the file
`2024_02_24.md`.

> Oh by the way, to solve the problem of the file names not being the same in Obsidian and Logseq, 
> 
> In Obsidian you go to 
> `Settings->Options->Core plugins->Daily Notes` and then you change the date format to `YYYY_MM_DD`.
> If you want to play by default Logseq rules, or if you want to use a more conventional name then set it to `YYYY-MM-DD`.
> 
> In Logseq go to
> `Settings->General->Custom configuration`
> and then you will edit the configuration file
> `config.edn`
> (you can just search for it and edit it on your preferred text editor of course),
> look for the line which says
> `:journal/file-name-format`
> uncomment it and set the vale to the date format you want, in my case I actually wanted "yyyy-MM-dd", so the line reads
> ```
> :journal/file-name-format "yyyy-MM-dd"
> ```
> additionally you can also set the page title format to
> ```
> :journal/page-title-format "yyyy-MM-dd"
> ```
> so Logseq displays the actual title of the note.

## What to do, what to do...
The obvious solution is to create a small script which changes the date format to what I want, in fact I thought of migrating the whole thing into an Obsidian format and I found [this Python script](https://github.com/NishantTharani/LogSeqToObsidian/tree/main), but then I realized I don't really want to do this, I like Logseq, I just need to tweak it a bit.
But then I did go and read the script and thought I could just steal the function called `update_files_and_tags` in the file [convert_notes.py](https://github.com/NishantTharani/LogSeqToObsidian/blob/main/convert_notes.py).

This seemed overkill, I literally need to edit some files, I am sure I can do it with the standard [Coreutils](https://www.gnu.org/software/coreutils/), so I embarked on the thrilling adventure of learning a bit about `sed`, `date` and `grep`.

## This is what I did
My attempts were relentless...

### Tried using `date`
I thought we can use `date` by either looping over the lines of a file like so
```
while read -r line; do 
    echo $(date -d "$line" +%Y-%m-%d); 
done < filename.md
```
because I went and read the answers to [this StackOverflow question](https://stackoverflow.com/questions/43697746/how-to-change-date-format-in-linux-unix-text-file) and I thought, "oh that looks quite smart" NOOOOOOT. One can simply go an read the manual (literally the first displayed screen) by typing [`man date`](https://www.man7.org/linux/man-pages/man1/date.1.html) and realize that the `-f` flag will save you from doing a silly loop, so you can also do
```
date -f filename.md +%Y-%m-%d
```
Those are more or less equivalent, the `-d` flag reads a string which in the loop will be each line of the file, while the `-f` flag reads the entire file and tries applying the date format to each line.

The problem of those approaches is that they expect you to have exactly the date you want to change in each line, no more no less...or I guess so, I haven't tried extensively, nevertheless this is not what I wanted.
Remember I am applying this to my notes, in the files the dates are within the text.
Besides, if a particular line had a date that I want to change this is always going to be enclosed by `[[` and `]]`, and this makes it not understandable for the command `date`.
And one more thing, `date` doesn't do ordinal numbers, "Feb 2nd, 2024" is not recognizable as a date for the utility `date`.

### Then using `sed` and `date`
Then I found somebody (also in StackOverflow but I cannot find the link any more) suggesting to use `sed` to convert your strings into `date` recognizable dates and then piping into `date`.
At this point I wasn't sure how `date` actually works, it took me a few attempts to learn that `date` is expecting no more than an actual date as the first string in a line as I mentioned above.

This, however gave me an idea...

### Just use `sed`, man
Why don't we just use `sed` to find dates through a regular expression and change it for what we want, at this moment I thought "I will make a very ingenious one-liner to brag about on the internet", just to realize that piping will just work.
Embrace the [gruging](https://grugbrain.dev/).

> Oh, what is piping?
> Normally a command has an output, for instance
>
> `echo "Hello"`
>
> will print the string "Hello" on your console, if you want to use the output of a command as the argument for other command you can use the pipe operator `|` to redirect the output to another utility, e.g.
>
> `echo "Hello" | grep "H"`
>
> which although this is a silly example it will take the word string "Hello" and feed it to `grep`, which will highlight the match of the letter "H" in the word "Hello".
> If you want, go and read more [here](https://www.redhat.com/sysadmin/pipes-command-line-linux).

First, I went and read this [intro to regular expressions](https://csiro-data-school.github.io/regex/index.html), because obviously I don't remember such things and I need to go and learn every time I need to use them. Really nice tutorial though. And along the way I was implementing my solution.

So I went by steps, let us first find our wikilinks with dates, we can use `grep` just so we can see what we find, and then afterwards use `sed` to substitute.
Both have the same syntax for regex.
```
grep -E '\[\[([a-zA-Z]{3})\s([0-9]{1,})(st|nd|rd|th),\s([0-9]{4})\]\]'
```
The line above will find the wikilinks of this format `[[MMM DDoo, YYY]]` and show them to you, once you are sure it works you can make your substitution by placing that into a search and replace thing in sed, this would be
```
sed -E 's;([a-zA-Z]{3})\s([0-9]{1,})(st|nd|rd|th),\s([0-9]{4});\4-\1-\2;' "$1"
```
There are a few things to notice there, first I realized I don't actually need to match `[[` and `]]` because all the instances where I have dates have been inserted with the date picker and it always creates wikilinks anyway, so it's redundant. 
Second, see that I have some things enclosed in circle brackets, like `([a-zA-Z]{3})`, this is so I can make back-references, so when we encircle our matches we can refer to them within `sed` by typing `\#`, this is backlash and the number of the match.
This is why in the replacement string we have `\4-\1-\2`, we want to substitute our match with the matches 4, 1 and 2 separated by dashes.
Notice that we skipped `\3` this is because `\3` matches the ordinal suffix which we don't want.
I presume if I didn't enclose the suffix in circle brackets it wouldn't have matter but then I wouldn't be able to match those strings, although I could have just matched them using `[a-z]{2}`, this is matching any two consecutive lower-case letters.

So let's explain that regex above before going to the next ones which are much simpler.
```
([a-zA-Z]{3})
```
`[a-zA-Z]` matches any letter from the English language, and since this is localized that is enough, then `{3}` is a quantifier which says "whatever is before me, make it three". You can put any positive integer *n* instead of 3 (I guess it could be non-negative but why would you match zero letters?).
I encircle the three letters so I can refer back to it, this will have the reference `\1`
```
\s([0-9]{1,})
```
matches a space with `\s`, then `[0-9]` matches any digit and the quantifier `{1,}` says "whatever is before me, give me at least one", this is because the day will have either one or two digits. I could have used `{1,2}` which limits you to find 1 or 2 or whatever is before, but I just thought about that while writing this entry so I didn't.
I encircle the one or two digits so I can refer back to it, this will have the reference `\2`
```
(st|nd|rd|th)
```
Is an *or* statement, so I am asking for either one of the strings "st", "nd", "rd" or "th", the ordinal suffixes in English.
I encircle the suffix so I can refer back to it, this will have the reference `\3`, although I will not use it but I think for the *or* statement I cannot not encircle it anyway.
```
,\s([0-9]{4})
```
Finally, I want to match a literal comma, a space and four digits.
I encircle the four digits so I can refer back to it, this will have the reference `\3`

Then this matches will be substituted by
```
\4-\1-\2
```
which is the references of the matches before, so if I had the link
`[[Feb 24th, 2024]]`
it will be substituted to
`[[2024-Feb-24]]`.
This is close but it's not quite what I want, because it has first of all the month still as `MMM` and if the day was a single digit `n` the last part of the new date will be a single digit `n` instead of the desired output `0n`.
So, it's time for PIPING.

Oh and at the end I have `$1`, this is just the file argument of a script call, because I wrote this as a [shell/bash](https://www.gnu.org/software/bash/) script and I call it by typing `./ldate filename.md`, so this will call the `sed` command on the file `filename.md`

### The piping
Originally I wanted to call everything together but I realise I actually need the output from the sed above and then I want to substitute the month and the day if it has a single digit.

So I did a big pattern matching sequence for each month of the year which you can see here
```
sed -E 's/-Jan-/-01-/;s/-Feb-/-02-/;s/-Mar-/-03-/;s/-Apr-/-04-/;s/-May-/-05-/;s/-Jun-/-05-/;s/-Jul-/-07-/;s/-Aug-/-08-/;s/-Sep-/-09-/;s/-Oct-/-10-/;s/-Nov-/-11-/;s/-Dec-/-12-/'
```
Yes, it's ugly, but it works. I wanted to do something smarter like the dictionary used by the Logseq to Obsidian migration script I mentioned above, I wanted to solve this quickly so I can write a blog entry about it, five minutes of web browsing didn't give me the answer so here we are.

This just does what it says, first looks for the string "-Jan-" and changes it by "-01-", then for the string "Feb" and replaces it by "-02-", you get the idea.
The dashes were necessary because I may have those strings in other places and I don't want them changed, for one there is a person I know called *Jan* and sometimes I refer to this person in my notes because I may need to remember I have a meeting with him or something, so I don't want his name changed by "01".

Note, that here my search and replace is bookended by forward slashes `/` instead of semi-colons `;` as I did before.
This is for convenience, and readability, you can use any character that you are not going to match.

The final step is the following
```
	sed -E 's;-([0-9])\];-0\1];' > "$1".done
```
Here the match is
```
-([0-9])\]
```
which is one dash `-`, exactly one digit `[0-9]`, and one closing square bracket `\]`, I enclose the digit and refer to it in the substitution as `\1`.
This pattern is easy but it can be dangerous, the trick here is to think that I only care about digits which are between a dash and a closing square bracket.
If I don't account for that, I will be matching digits everywhere and that could be problematic.

Then, at the end I forward the output of the piping into a file which is going to be called `filename.md.done` if I called the script on a file called `filename.md`.
Just to have some backup, doing that you just move all files called `*.md` to where you want them and remove the `.done`.

## Conclusion
And that's it, that's how you do it, or at least one way to do it.
I am sure there are more elegant ways.

The way I applied it was by calling a loop over the files of the directory when I wanted to apply it, i.e.
```
for filename in *;
    do ./ldate "${filename}";
done
```
This calls my script `./ldate` over each file in the current working directory.
You could potentially add the script to a directory on your `PATH` and not have to move your script around, but I didn't do it because most likely I won't need the script ever again, so I just spent a few hours writing a "one-liner" sed to change the date format in files and documenting it on this entry.

It was quite fun.
