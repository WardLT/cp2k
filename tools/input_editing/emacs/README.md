# `cp2k-mode.el`

`cp2k-mode.el` provides a major mode in emacs for editing CP2K input files. It has been tested on
emacs 2.1, 2.3 and 2.4.

## Functionalities

- Recognizes and font-locks:
  - the full CP2K input preprocessor syntax
  - the sections and subsections
  - the keywords
  - the comment lines
- Indents lines according to the CP2K input syntax using `<tab>` key
- Input sections can be folded or unfolded, using emacs outline minor mode.
  - `outline-toggle-children` when called on a unfolded section, folds the section recursively; when
    called on a folded section, unfolds the top level tree.
  - `show-all` when called unfolds all sections recursively.
  - `show-subtree` when called unfolds a folded section recursively.
- New interactive functions:
  - `cp2k-indent-line`: indents the line according to CP2K input syntax.
  - `cp2k-beginning-of-block`: goes to the beginning of the subsection, marks the current cursor
    position.
  - `cp2k-end-of-block`: goes to the ending of the subsection, marks the current cursor position.

### Key Bindings

| character |                           |
| --------- | ------------------------- |
| `<tab>`   | `cp2k-indent-line`        |
| C-j       | `newline-and-indent`      |
| C-c ;     | `comment-region`          |
| C-M-a     | `cp2k-beginning-of-block` |
| C-M-e     | `cp2k-end-of-block`       |
| C-c C-c   | `outline-toggle-children` |
| C-c C-a   | `show-all`                |
| C-c C-t   | `show-subtree`            |

## Installation

You need to put `cp2k-mode.el` in one of your local emacs lisp directories, which is in the search
path of your emacs installation.

### Adding to emacs's search path

If you have never installed any packages manually before, and do not know the search path of your
emacs installation, then in your home directory create directory:

```shell
mkdir ~/.emacs.d/lisp/
```

This is the usual place where the local/user defined emacs lisp files are installed. Move
`cp2k-mode.el` to `~/.emacs.d/lisp/`.

Then, add the following in your `.emacs` file (which should be in your home directory, and if it
does not exist, create one):

```emacs
(add-to-list 'load-path "~/.emacs.d/lisp/")
```

This tells emacs to add `~/.emacs.d/lisp/` to its search path for `*.el` files.

### Tell emacs to load `cp2k-mode.el` at startup

Once `cp2k-mode.el` is in the search path, we need to tell emacs to load it at start up, this is
done by adding

```emacs
(require 'cp2k-mode nil 'noerror)
```

to your `.emacs` file.

### Tell emacs to recognize `*.inp` automatically as a cp2k input file

Add

```emacs
(add-to-list 'auto-mode-alist '("\\.inp\\'" . cp2k-mode))
```

to your `.emacs` file.
