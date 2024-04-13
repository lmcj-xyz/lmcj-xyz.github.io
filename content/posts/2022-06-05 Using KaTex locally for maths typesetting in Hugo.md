---
title: "Using KaTex Locally for Maths Typesetting in Hugo"
date: 2022-06-05T12:53:26+02:00
slug: 2022-06-05-using-katex-locally-for-maths-typesetting-in-hugo
type: posts
draft: false
maths: true
categories:
  - Tutorial
tags:
  - Software
  - Mathematics
toc: true
---

If you work or study on mathematics related fields and have a website, you might often want to share your knowledge with the world.
Of course, doing it is rather easy with many website creation tools, and there are also many tutorials to do it with any tool you can think of.

So, I want to tell you how to do it using the static site generator
[Hugo](https://gohugo.io/)
and the JavaScript library
[KaTeX](https://katex.org/).

I will tell you how to do it sourcing locally the scripts (the *kind of* difficult way), because most tutorials only show you how to do it with remote files.
If instead you want to know how to do it with remote files (the easy way) because you clearly don't care about saving precious miliseconds while your website loads, there are many tutorials to do it, some of them are:

* [the official documentation](https://katex.org/docs/browser.html),

* [this blog entry by Mert Bakir](https://mertbakir.gitlab.io/hugo/math-typesetting-in-hugo/),

* and [this one by Edwin Kofler](https://hyperupcall.github.io/blog/posts/render-latex-with-katex-in-hugo-blog/)

Jokes aside, bear in mind that KaTeX is really fast, so using the remote files is already great, but it can always be faster and also I like to have things locally.

Additionally I will give you a script (tested on Linux, but might work in other OS if you tweak it properly) to update KaTeX if you use the local version of them.

Just for reference of how KaTeX renders stuff here is a small mathematical sentence:

Let
$b(t, \cdot) \in \mathcal{C}^{-\beta}$,
for
$0 < \beta < 1/2$
i.e.
$b$
belongs to a Hölder-Zygmund space with negative order, then let us define, formally, the following SDE

$$X_t = X_0 + \int_0^t b(s, X_s) ds + W_t$$

Now that you saw how beatiful this is, let us start.

> **Disclaimer:** I am breaking down the process step by step, and that is why it looks very long, in reality it won't take you more than 10 mins to do the hardest version, so don't be discouraged if this looks too long.

## My Hugo directory tree

First let me quickly lay the ground about the folder structure I have, and in this way you can extrapolate it for your own case:

    .
    |__archetypes/
    |__config.toml
    |__content/
    |__data/
    |__katex/
    |__layouts/
       |__partials/
    |__public/
    |__resources/
    |__static/
       |__css
       |__scripts
    |__themes/

> **Attention:** the `katex/` directory is not necessary to have from the beginning since it is where your downloaded scripts will be, and it will be created when you extract the archive.

> **Attention again:** Also, of course the folder structure is more complex, but only the relevant parts are listed here.

We will only work on the directories
`layouts/`
`static/`
`katex/`
and
`themes/`,
although to be honest, most of what we will do is on the first two.

## Download the scripts

To download the scripts, you have two options:

* Fire up the terminal and type
`wget https://github.com/KaTeX/KaTeX/releases/download/v0.15.6/katex.tar.gz`
(as far as I am concerned, you can use `wget` on any OS)

* Go to
[the releases page of KaTeX](https://github.com/KaTeX/KaTeX/releases)
and download the either the
`tarball`
or the
`zip`
file, depending with what thing you are more comfortable, both archiving formats work on any OS.

> **Attention:** For the first option you **must** check what version is the most recent, so you anyway should go to the releases page from option 2.

Make sure the
`katex`
directory is in your main Hugo folder.

Once you download it you will unpack your archive, in Linux you can use (in the terminal):

* `tar -xvf <tarball file>` where the options for `tar` mean `-x` extract, `-v` is verbose output (you can totally exclude it but I like verbose commands) and `-f` tells `tar` to use the file you are giving.

* `unzip <zip file>`

Or if you don't want to use the terminal, just open your graphical file browser and extract the archive from there.

## Move the files

Now you will have a folder called
`katex`
with the following contents

    katex/
    |__contrib/
    |__fonts/
    |__katex.css
    |__katex.js
    |__katex.min.css
    |__katex.min.js
    |__katex.mjs
    |__README.md

The important parts from there are
`fonts/`,
`katex.js`
and
`katex.css`.
The
`contrib/`
directory can be important if you want to add some extra functionality, which by the way we will do here.

So, for the sake of this tutorial you will move the files like this

* The directory `fonts/` and the file `katex.css` go inside `static/css/`,

* the file `katex.js` go inside `static/scripts/katex/`, and

* optionally (but mandatory if you follow exactly this particular tutorial) the file `contrib/auto-render.js` will go in `static/scripts/katex`

> **Attention:** You can also use the `katex.min.js` and `katex.min.css` which are "minimal" version of the files.

## Make your website use the files you just moved

First, on the `layouts/partials/` directory you need one [partial template](https://gohugo.io/templates/partials/)
and you can name it `katex.html`, add the following content to that file

    <link rel="stylesheet" href="{{ "css/katex.css" | relURL }}">
    
    <script defer src="{{ "scripts/katex/katex.js" | relURL }}"></script>
    
    <script defer src="{{ "scripts/katex/auto-render.js" | relURL }}" onload="renderMathInElement(document.body);"></script>
    
    <script>
        document.addEventListener("DOMContentLoaded", function() {
            renderMathInElement(document.body, {
                delimiters: [
                    {left: "$$", right: "$$", display: true},
                    {left: "$", right: "$", display: false}
                ]
            });
        });
    </script>

If you moved the files where I mentioned above this will work.

The first line loads the stylesheet `katex.css`, the second the script `katex.js`, the third the extension `auto-render.js`, which renders all the math inside of text, and the last chunk will make possible inline equations, which most likely you want to have.

The third line is optional if you are not interested in using [auto-render.js](https://katex.org/docs/autorender.html).

Now, depending on where do you want to load your scripts, this can be a little tricky; but the way I like adding scripts to an `HTML` file, is on the `head`. So if you want to do it like that, then in `layouts/partials/` you will create (unless you already have it) a template called `head.html` and you will add there the following:

    {{ if .Params.maths }}{{ partial "katex.html" . }}{{ end }}

> **Attention:** You can add scripts in the `footer` or `header` or `body`, do it as you prefer I am just following the current advice about where to load scripts, because it is no longer the 17th century and we have things like `async` and `defer`, which I am using here. For more info about those things see [this SO answer](https://stackoverflow.com/a/24070373).

This will check in the frontmatter if you enabled `maths` in that post, therefore from now on whenever you want to add maths in a post you must add, in the frontmatter, the line
    
    ---
    maths: true
    ---

Because of that I would, of course, suggest to add it in your [archetypes](https://gohugo.io/content-management/archetypes/), and if you don't need it for a certain post you just make it `false`.

> **Attention:** The reason we are doing this, is so that no unnecessary `js` code is loaded everywhere and it is only used where needed, if you are not interested in that, then go and add all the scripts into the base template. Which I strongly disapprove and won't tell you how to do it (it might depend on your theme), you might be able to figure that out on your own.

Finally, there is kind of a tricky part, which depending on how you have your Hugo project can or cannot be neccessary, it might also depend on your theme.
The thing is that the `head.html` file that we created, might not be loaded into your base `html` template, and you will have to look for your main template file and add the line

    {{ partial "head" . }}

**In my particular case** (and be very mindful that this is a particular case), I am using a modified version of the theme [smol](https://themes.gohugo.io/themes/smol/) and have kept some of the structure of the theme, so I added the line above in the file `themes/smol/layouts/_default/baseof.html` inside the `<head>` section. But this will depend on your own project.

> **Update at 6 Jun 2022:** Turns out the above is not as dependant of the theme, since most themes have the same structure and you can very safely go and add the line to your `themes/<your theme>/layouts/_default/baseof.html` file. You just need to add it according to the file that loads scripts.

> **Update at 25 Feb 2024:** It's best if you don't touch your theme folder ever again unless necessary, but instead copy the `baseof.html` to your website's `layouts` directory and edit the one there, Hugo will override the theme's setting if it finds a file with the same name in the base directory, this applies to any file from your theme. So this is for instance a better way to change your `style.css` as well.

## Final words

There you go, you must now be able to use KaTeX on you Hugo website, of course syntax is like LaTeX and you will use `$ $` for inline equations and `$$ $$` for blocks.

Have fun!

## Bonus: Script to update KaTeX (Linux)

This is only tested on Linux, but might as well work in any other OS with the appropriate modifications, for that reason I will explain what each command does, and you can look for the commands that do the same in your OS (in MacOS might even work as it is).

* Create a file named as you want to name it, I want it to be `update_katex`,

* make it executable by running `chmod +x update_katex`,

* add the following content

    ```
    #!/bin/sh
    curl -s https://api.github.com/repos/KaTeX/KaTeX/releases/latest \
    | grep "browser_download_url.*tar.gz" \
    | cut -d : -f 2,3 \
    | tr -d \" \
    | wget -qi -

    tar -xf katex.tar.gz
    rm katex.tar.gz
    cp -r katex/fonts/ static/css/
    cp katex/katex.css static/css/
    cp katex/katex.js static/scripts/katex/
    cp katex/contrib/auto-render.js static/scripts/katex/
    ```

Let me explain the code above, first the pipelines sequence:

* `curl` retrieves the `json` file with the releases information, and the option `-s` is to make it silent,

* `grep` looks for the pattern in quotes and returns the line that contains it,

* `cut` deletes/keeps fragments of a string, the option `-d :` makes it look for the character `:` and make it the delimitator, so that with `-f` we chose the fragments with respect to the delimitator, in this case `2,3`,

* `tr -d \"` deletes the quotes

* we used `wget` before but now we give it the option `-q` for it to be quiet and `-i` to give it a file, `-` makes it take the value of that comes from the pipeline.

And then the rest of the commands are:

* `tar -xf katex.tar.gz` extracts file,

* `rm katex.tar.gz` deletes the compressed archive,

* And then you copy stuff with `cp`.
