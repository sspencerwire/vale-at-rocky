# Rocky vocabularies

Project for creating custom dictionaries for vocabulary words after installing the `vale` linter in NvChad.

## Purpose of the project

The purpose of the project is to create a set of vocabularies for use when writing Rocky Linux documentation. The vocabularies are needed to remove warnings issued by *Vale* for unknown words as in the following example:

> Use correct American English spelling. Did you really mean 'Rocky'?

This term is perfectly fine but not known to `vale` so these messages can clutter up the display, making it difficult to actually see the warnings that you need.

To remove these kinds of warnings, it is necessary to provide *Vale* with a list of words that should be considered correct, and for this purpose Vale's developers introduced *vocabularies*.  
Vocabularies are folders containing two files, the *accept.txt* and *reject.txt* files, which contain the words to be considered correct and those to be considered incorrect, respectively. The words are entered one per line and may have wildcards that affect the choice result.

## Structure of a Vale configuration

In a standard Vale structure the *styles* folder has the selected styles (in this case `RedHat` and `alex`):

```text
styles
├── alex
└── RedHat
```

The configuration file set the search path for the styles, the level the alerts should have (warning, suggestion, and so on) and the styles used:

```ini
StylesPath = ~/.local/share/vale/styles

Vocab = rockydocs, nvchad, terminology

MinAlertLevel = suggestion

Packages = RedHat, alex

[*]
BasedOnStyles = Vale, RedHat, alex
```

## Structure of a dictionary

The dictionary consists of two files, an *accept.txt* file that has the words that Vale should consider as correct, in this case *nvchad/accept.txt*:

```txt
Devicons
formatters
(?i)chadrc
(?i)nvchad
(?i)nvim
[?i]yaml
....
```

The second *reject.txt* file unless there are special needs is usually empty. It is for flagging words not to be used, which in the Rocky documentation is already handled by *RedHat* styles for the technical part and by *alex* for identifying polarizing words in Markdown files.   

Vale allows some dedicated settings for terms:

```text
(?i)linux
[Rr]ocky
```

The entry, (?i)linux, marks the entire pattern as case-insensitive, and the entry [Rr]ocky, provides two acceptable options.

## Conclusion

Using `vale` in NvChad with properly populated dictionaries will help when checking your document with `vale`. It will end the screen clutter that comes from words that `vale` does not know to be correct by default.
