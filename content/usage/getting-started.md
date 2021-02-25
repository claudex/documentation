---
title: Getting Started
weight: -20
---

This page tells you how to get started with Slides as Code CLI and theme, including installation and basic usage.

{{< toc >}}


## Installation Requirements

There is no “best” way to install Slides as Code and its requirements on your computer.
You should use the method that works best for your use case.

The `sac` command line is a Bash 4.x script targeting Linux, macOS (or WSL) and requires **bash**, **hugo**, **jq**, **yq** and **coreutils**.

To download and install them, [Homebrew](https://brew.sh/) can be used on macOS (or Linux).

``` shell
$ brew install bash hugo jq yq coreutils
```

In order to install these tools with another method, please follow related documentation:

- [**bash**](https://www.gnu.org/software/bash/manual/html_node/Installing-Bash.html) version 4.x and above
- [**hugo**](https://gohugo.io/getting-started/installing/) version 0.80 and above
- [**jq**](https://stedolan.github.io/jq/download/) version 1.6 and above
- [**yq**](https://mikefarah.gitbook.io/yq/) version 4.x and above
- [**coreutils**](https://www.gnu.org/software/coreutils/) version 8.x and above


## CLI Installation

### Homebrew
To download and install the latest version of `sac` command line, [Homebrew](https://brew.sh/) can be used on macOS (or Linux).

``` shell
$ brew install sacproj/sac/sac
```


### Tarball
When installing from the tarball, you have to decide where to install the `sac` script (e.g `/usr/local/bin`).

- Download the tarball `sac-cli.tar.gz` from [releases page](https://github.com/sacproj/sac-cli/releases).
- Unpack the tarball and copy `sac` script where you decide


### Checking Installation
Execute following command to check requirements.

``` shell
$ sac doctor
```

For each tool, `sac doctor` command checks the presence of it and outputs `OK` or `KO` as result. You have to install missing tools in order to get `sac` command line to work as expected.


## Theme Installation
In order to install latest Slides as Code Theme, execute following command:

``` shell
$ sac theme install github sacproj/sac-theme
```

Then, check installed themes by executing following command:

``` shell
$ sac theme installed
/usr/local/share/sac/themes
└── sac
    └── x.y.z
```


## Create new Presentation
Create a new slides Deck with Slides as Code theme in `my-awesome-slides` directory:

``` shell
$ sac desk new my-awesome-slides sac-theme/x.y.z
```

Go to created repository

``` shell
$ cd my-awesome-slides
```

Create a new content files to organize your slide deck:

``` shell
$ sac content new cover.md
my-awesome-slides/content/home/cover.md created
 
$ sac content new intro.md
my-awesome-slides/content/home/intro.md created
 
$ sac content new info.md
my-awesome-slides/content/home/info.md created

$ sac content new qa.md
my-awesome-slides/content/home/qa.md created
```

In fact, slides content could be split into multiple Markdown files.

So, the directory layout is following:

``` text
my-awesome-slides/
├── .gitignore
├── .vscode
│   └── sac.code-snippets
├── config.yaml
├── content
│   └── home
│       ├── cover.md
│       ├── info.md
│       ├── intro.md
│       └── qa.md
└── static
    ├── charts
    ├── codes
    ├── diagrams
    ├── images
    ├── sessions
    ├── sounds
    └── videos
```

- `content/home` directory contains the just created Markdown files.
- Directories inside `static` will contain elements such as images, source code used by the slides deck.
- `config.yaml` contains deck configuration (see [Configuration]({{< ref "reference/configuration" >}}) page).
- `sac.code.snippets` contains VS Code snippets used by selected themes (see [Snippets]({{< ref "reference/snippets" >}}) page).

## Code your Presentation Slides

In order to code (with live update) or present your slides deck, execute following command.

``` shell
$ sac deck code
```


## Content Format
Hugo ❤️ Markdown, but there are times when Markdown falls short.

Instead of writing raw HTML, Hugo created Shortcodes.

A Shortcode is a simple snippet inside a content file
that will be rendered using a predefined template (see [Shortcodes]({{< ref "reference/shortcodes" >}}) page).

```
{{</* shortcode parameters >}}
content
{{< shortcode */>}}
```

VS Code snippets are available in order to ease the use of shortcodes (see [Snippets]({{< ref "reference/snippets" >}}) page).


## Content Source and Rendering
Each content file should contain `markup: html`.
The command `sac content new` is taking care of this for you.

``` text
---
weight: 10
markup: "html"
---
Markdown with Shortcodes content
```

`weight` in content file's front-matter is used to sort content files when concatenating them.
The command `sac content new` is incrementing it by `10` on every execution.

Slides as Code doesn't use Hugo's Markdown renderer, but Reveal.js Markdown renderer.
