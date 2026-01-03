---
title: "Use LaTeX Kids"
date: 2024-11-29T16:19:15Z
draft: false
---

Here is a post in the form of a LaTeX code snippet.

# On the dangers of using plain TeX

```tex
% Let us define a header
%% Starting with some fonts
\font\xmplbx = cmbx10 scaled \magstephalf 
%% Here you define the font named \xmplbx by calling the actual font
%% named cmbx10 and you say that is going to be scaled...how much
%% is the scale, you may ask?
%% \magstep is for magnification, and you magnify by 1.2
%% i.e. cmbx10 scaled \magstep would be the font cmbx10 scaled at 1.2,
%% meaning a 20% increase in the scale.
%% All the `magsteps' are powers of 1.2,
%% \magstep2 for instance would be a magnification of (1.2)^2...
%% which means that \magstephalf is exactly a magnification of
%% \sqrt{1.2} because LOL!
% Same here but with the italics font
\font\xmplbxti = cmbxti10 scaled \magstephalf
% And now you can define the header as a two parameters command
% which you align to the left and use different fonts in different places
% then at the end you add an extra vertical space.
\def\xmpheader#1#2{\leftline{\xmplbx Example #1:\quad\xmplbxti #2}\vglue .5\baselineskip}
%% Pure gore.
% And now you can write a header...
\xmpheader 1 {Simple text}

And this is some actual text which will appear in the document.
% The moral of this is: Kids use LaTeX, there is no point to this.
% Once your life is numb and want to at least feel something
% then go and use TeX.
```
