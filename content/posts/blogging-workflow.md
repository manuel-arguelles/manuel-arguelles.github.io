+++
title = "Blogging workflow"
date = 2021-01-09T18:55:00-05:00
tags = ["blog"]
draft = false
+++

I'm still trying to figure out the best workflow for me, for now I'm using [Emacs](https://www.gnu.org/software/emacs/) with [Org mode](https://orgmode.org/), the package that generates the Markdown from the org files is called [ox-hugo](https://ox-hugo.scripter.co/). I'm using the development version of [Spacemacs](https://www.spacemacs.org/) and the installation was super easy. My configuration looks like this:

```emacs-lisp
dotspacemacs-configuration-layers
'(
  (org :variables
       org-want-todo-bindings t
       org-enable-hugo-support t)
 )
```

All the posts (blogs entries) are in one file, as recommended by ox-hugo, each entry is a todo. The reason for that is that once the status changes to done, the date is recorded. This is quite handy to date the entries once you are done writing them.

For the hosting I'm using two repositories, the output which is basically the HTML part (that's the public/ directory in the Hugo structure) and the rest in a separate repository.
