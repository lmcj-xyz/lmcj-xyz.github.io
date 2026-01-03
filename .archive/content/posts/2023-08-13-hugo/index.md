---
title: "Setting Up a Website Using Hugo, GitHub Pages and a Custom Domain"
date: 2023-08-13T11:19:39+01:00
draft: true
tags:
- software
categories:
- tutorial
---
So you have a brand new domain name to show off your stuff on the internet and now want to build a website eh?
Whats that?
So...you say you don't want to pay for and manage your own server and have heard of this things called
[GitHub pages](https://pages.github.com/)
that all the cool kids are using?
Well...not ideal but okay.
Oh and also you don't want to deal with HTML and CSS as much because *iT'S hArD* and some techy friend told you about a framework called
[Hugo](https://gohugo.io/)
which makes the creation of static websites quite fun and easy?
Well hopefully after you read this blog post you will have your shiny new website up and running.

Why another tutorial?
You might ask.
Well for the same reason everyone else makes tutorials, to learn stuff and flex about it.
And how come you will tell us how to use GitHub pages if you don't even use it? Well I just happen to kind of know.

## Prerequisites {#prerequisites}
- Your own domain name (I use [orangewebsite](https://www.orangewebsite.com/) but you use whatever you want)
- A GitHub account ([sign up](https://github.com/signup) if you don't have one)
  - And I guess [git](https://git-scm.com/) or [the GitHub desktop client](https://desktop.github.com/), *although I have to say that I won't use the latter and if you use it you better know how to because I have no idea and I won't provide you with any guidance on that regard*
- Hugo installed ([follow the instructions](https://gohugo.io/installation/) for yor platform)

*You do what you are missing and come back here.
I'll wait.*

![Waiting for you](relax.gif)

**Oh god, finally!
Okay let's get to work!**
![Let's start](work1.gif)

## Create a Hugo website {#create-site}

Since you want to host your website in GitHub, let us make this a git repository

{{< highlight bash >}}
git init
{{< / highlight >}}

and add the following text
(which I took from [here](https://github.com/github/gitignore/blob/main/community/Golang/Hugo.gitignore))
into a file called `.gitignore`

{{< highlight text >}}
# Generated files by hugo
/public/
/resources/_gen/
/assets/jsconfig.json
hugo_stats.json

# Executable may be added to repository
hugo.exe
hugo.darwin
hugo.linux

# Temporary lock file while building
/.hugo_build.lock
{{< / highlight >}}

and then make your first commit

{{< highlight bash >}}
git add .gitignore
git commit -m "First commit"
{{< / highlight >}}

After this is your responsibility to track the cahnges in the repository, so I would imagine you know how ot use `git`.
If not, then go run
`man gittutorial`
on your terminal or check
[the gittutorial online](https://git-scm.com/docs/gittutorial),
or I guess any other tutorial like 
[this article from freeCodeCamp](https://www.freecodecamp.org/news/learn-the-basics-of-git-in-under-10-minutes-da548267cc91/)
or
[this video by Colt Steele](https://www.youtube.com/watch?v=USjZcfj8yxE).
If you use the GitHub desktop client you are on your own, god bless your soul.

> Oh one more thing:
> if you go to the
> [get started guide for Hugo](https://gohugo.io/getting-started/quick-start/)
> you will note that they suggest you to use a theme from the
> [many Hugo themes available](https://themes.gohugo.io/),
> **I will not do that**.
> Instead I will teach you how to create a theme. If you don't care about that then you can skip the section
> [Create your own theme](./#your-theme)
> and just follow the instructions to clone a theme as mentioned
> [here](https://gohugo.io/getting-started/quick-start/#explanation-of-commands).

### Running hugo
We are going to be using the terminal, but it's fine, nothing scary.

You will first locate yourself on a directory where you want to create the directory for your website.
Say for instance your `Documents` directory, or if you have some `Repositories` directory where you place your software projects then use that I guess, anywhere is fine your `home` directory is also fine, it doesn't really matter.

Then on your terminal you will run

{{< highlight bash >}}
hugo new site mywebsite
{{< / highlight >}}

this will create a directory called 
{{< highlight bash "hl_inline=true" >}}
mywebsite
{{< / highlight >}},
if you want you can give any other name instead of `mywebsite`, I personally will run

{{< highlight bash >}}
hugo new site mathsposer
{{< / highlight >}}

because I will use the domain name
[mathsposer.com](https://mathsposer.com),
so feel free to use your domain name.

Once you do that you will receive a message congratulating you for your sucessful creation of a new website and giving you some more instructions, don't listen to them, they want you to download a theme.
Or listen to them, I don't really care.

If you have successfully ignored them and listened to me, then let us explore the directory structure of the project, run

{{< highlight bash >}}
cd mathsposer # to change to said directory
{{< / highlight >}}

and you will see the following structure:

- **archetypes/**
  - *default.md*
- *config.toml*
- **content/**
- **data/**
- **layouts/**
- **public/**
- **static/**
- **themes/**

> Whenever i mention I have a directory structure **bold-with-slash-at-the-end/** represent directories, whereas *italic-characters* represent files.

And the only thing I will edit for the moment is the
`config.toml`
file, which as you might guess is where we configure our website.
You will have by default the following

{{< highlight toml >}}
baseURL = 'http://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
{{< / highlight >}}

but I will change it to

{{< highlight toml >}}
baseURL = 'http://mathsposer.com/'
languageCode = 'en-gb'
title = 'The website of a Maths Poser'
theme = 'nothing'
{{< / highlight >}}

whereas ideally you will use your own domain name in the
`baseURL`
parameter, change the
`languageCode`
to something that suits you, and modify the
`title`
to reflect the title of your own website, perhaps is your name or something.
And I added one more thing, which is the
`theme`,
I gave it the value
`nothing`
because that is what I will call my theme, you use the name of the theme of your preference.

Now before explaining what to do with the files and directories above, we actually need a theme.
Silly, isn't it?
But it has its reasons...don't ask what are the reasons please.

### Create your own theme {#your-theme}

I will repeat this...if you don't care about learning how themes work and want a precooked theme then do as in
[this guide](https://gohugo.io/getting-started/quick-start/#explanation-of-commands)
(which is what you should have done anyway...)

As many things with Hugo, you start by doing some command line trickery:

{{< highlight bash >}}
hugo new theme nothing
{{< / highlight >}}

where 
{{< highlight bash "hl_inline=true" >}}
nothing 
{{< / highlight >}}
is the name of the theme, mine is called
{{< highlight bash "hl_inline=true" >}}
nothing 
{{< / highlight >}}
(remember my `config.toml` file?)
because that's what I am going to do,
*nothing*.

Then the following folder structure will appear inside the directory
`nothing`:
- **archetypes/**
  - *default.md*
- **layouts/**
  - *404.html*
  - **_default/**
    - *baseof.html*
    - *list.html*
    - *single.html*
  - *index.html*
  - **partials/**
    - *footer.html*
    - *header.html*
    - *head.html*
- *LICENSE*
- **static/**
  - **css/**
  - **js/**
- *theme.toml*

Now, all the files here are going to be empty or almost empty, except for *baseof.html* which, as the name suggests, is the basic structure of pages
(or at least the default structure, we'll taltk about that in a second)
contains the following

{{< highlight html >}}
<!DOCTYPE html>
<html>
    {{- partial "head.html" . -}}
    <body>
        {{- partial "header.html" . -}}
        <div id="content">
        {{- block "main" . }}{{- end }}
        </div>
        {{- partial "footer.html" . -}}
    </body>
</html>
{{< / highlight >}}

If you have used HTML before you might be wondering what those cursed curly brackets are? 
Ahhh!!! 
Behold the Hugo template.
![Behold!!!](behold.gif)

So, what do we do now?
Basically the way this works is that in between
`{{  }}`
you can put some
[Go code](https://go.dev/)
or template variables.
Above we can see two functions being called
`partial`
and 
`block`, let us explain partial.
In the directory structure above you have a directory called 
`partials`
in this one we have partial 
`.html`
documents
which are used to build our website, so I presume you can guess that the function `partial` will include the partial documents into the document is being called.
The sintax is then
`{{ partial "<PATH>/<PARTIAL>.<EXTENSION>" . }}`

We are including here three partials into our
`baseof.html`
document, might as well add something into them.

First the
`head.html`
document.
The HTML tag
`head`
is used to include metadata from the file, and we will include only two very simple but important things

{{< highlight html >}}
<head>
	<title>{{ .Site.Title }}</title>
	<link rel="stylesheet" href="/css/style.css" type="text/css" media="all" />
</head>
{{< / highlight >}}

The
`title`
tag gives the title of the website
(duh)
but the way you visualise it is on the tab name of your browser, and you can see that we are using the power of templates here by setting
`{{ .Site.Title }}`
this instructs Hugo to go search the name of the website in the config file and this is going to be whatever you put under the parameter
`title`
in the
`config.toml`,
in my case it looks like this on the tab

{{< figure src="title-tag.png" title="The title tag I set on the head tag" >}}

The next one is the standard way to include your CSS file to style the website, nothing fancy.
But keep this in mind because we will have to create the
`style.css`
sheet
under the directory
`static/css/`
of our theme.

Now let's do something about the
`header.html`
document, what is the header of a website?
This is normaly the stripe on top which has navigation links and the title of the site.
By default the file is empty and we will only include one thing:

{{< highlight html >}}
<header>
	<a href="{{ .Site.BaseURL }}">{{ .Site.Title }}</a>
</header>
{{< / highlight >}}

Namely, the link to the website invoked with a template and the template variable
`.Site.BaseURL`
with the displayed text invoked with another variable
`.Site.Title`.
These two variables will search in
`config.toml`
for the
`baseURL`
and
`title`
parameters, and this will be wrapped with the
`header`
tag because we are creating the header of the file.

Now let us add something to the
`footer.html`
documet, people tend to add contact and attribution information, we will just add

{{< highlight html >}}
<footer>
	by lm
</footer>
{{< / highlight >}}

which tells people who is making this thing.

And now
**what about the block function**
on
`baseof.html`?
Well, this basically adds whatever thing you define, in our case we have to define the block
`main`.
We can do this in different places, in particular for this first example we will do it in the
`layouts/index.html`
document by adding

{{< highlight html >}}
{{ define "main" }}  
{{ .Content }}  
{{ end }}
{{< / highlight >}}

This bit is a usage of templates a bit more complicated than what we have seen, but the gist is that we define something by using
`{{ define "something" }}`
and it ends with
`{{ end }}`
and whatever we type in the middle of that is going to be the content of
`something`,
in this case we have the variable
`.Content`
and that basically calls the content from some file in the
`content`
file of the Hugo project.

And now let's create the landing page for our website by running the following

{{< highlight bash >}}
hugo new content/_index.md
{{< / highlight >}}

Note the underscore before the name, this is just to indicate this is the landing page.

And for this I just added the text

{{< highlight markdown >}}
This is a website.

And you don't need any more than this.

But you probably want something else, don't you?
{{< / highlight >}}

And the result is this

{{< figure src="website.png" title="The result of the modifications to the HTML documents" width="90%" >}}

For a complete read on templates go to
[read the docs on Hugo templating](https://gohugo.io/templates/)
and in
[Go templates](https://pkg.go.dev/text/template)

One last thing about the theme is to style it a bit by using CSS, for that let us go to the
`style.css`
sheet of our theme, and I will add the following, which I will not explain because you can check for yourself.

{{< highlight css >}}
header {
	background-color: black;
}
header a {
	color: red;
}
footer {
	color: white;
	background-color: black;
}
{{< / highlight >}}

{{< figure src="website-styled.png" title="The result of the modifications to the HTML documents" width="90%" >}}

So now go and explore this and create your own theme.

## Create a GitHub website

Now let us take this baby into the world (wide web).

This whole thing is naturally based mainly on the documentation from
[GitHub](https://pages.github.com/),
[Hugo](https://gohugo.io/hosting-and-deployment/hosting-on-github/),
and
[the custom domain guidance for GitHub pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages).

> Note that the hosting in
> `git`
> based platforms isvery popular and you can do it in some other platforms like
> [Codeberg](https://codeberg.page/)
> and
> [GitLab](https://docs.gitlab.com/ee/user/project/pages/),
> the procedure might be a bit different but you can just read the docs.

### Add your repo to GitHub

Remember that initially you made the Hugo project into a git repository?
Now let us commit all the changes by running the following

{{< highlight bash >}}
git add .
git commit -m "Website ready for the world"
{{< / highlight >}}

Presumably, you know how to use
`git`
and you have been tracking changes while you were following the tutorial
(yeh sure...),
then the next step is to create a GitHub repository for your website.

### Use your own domain name
