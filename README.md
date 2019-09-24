# File format discussion

Discussion about how we would like to improve current font file formats.

## Why?

An ideal font file format (and matching software) would enable this:

Designers can edit the font in any software that they like, within the same
team, while working together on the same project. Each stage of the project
can use a different editor, each person on the team can use a different
editor. They can use the proprietary power-user features that each editor
provides, while maintaining the ability to work on the font in other editors
that don't have that cool feature (but that provide other cool features of
their own).

They can work in parallel on the same project, including several people
working on the same weight in different scripts, or on the same script across
different weights, or any other distribution of work. They can keep versions
of the project in git and share ongoing work seamlessly. If there's a git
conflict it's an actual conflict in the design, like two people disagreeing
on the shape of a glyph.

The project can span multiple styles that do not necessarily interpolate,
multiple weights and widths, several scripts, and combine all that work into
various outputs: variable fonts, static fonts, interpolated instances, each
including all or part of the designspace, all or part of the glyphset,
features, etc.

Designers can use established workflows to produce currently standardised
outputs like static fonts and "mainstream" variable fonts, but they can also
mix into the output some crazy hand-written tables for experimental results.
Anything that is valid according to the OpenType spec should be possible to
generate from the sources, one way or another.

Whatever work is saved in the source file, the designer can give that file to
a compiler (or click the "generate fonts" button in an editor) and get all
the outputs that are expected, i.e. actual font files that can be QA'd and
sent to clients as-is.

At the moment, some of the goals can be partially achieved and some not at all:

- compatibility between font editors is only partial
- collaboration using UFOS and git has a few issues, most notably conflicts
  that do not concern important bits of the source files
- when a project spans a wide range of styles and scripts, you would want to
  have all of it in the same source file, to allow designing a uniform style
  and sharing for example background layers or comparing interpolations. But
  then you couldn't easily specify subsets to be generated, or different
  fontinfo for each subset.
- Compiling a Designspace + UFOs or a Glyphs file into a variable font and
  some instances is easy enough using fontmake or from within Glyphs, but more
  complicated workflows necessitate custom plumbing.

## Repository contents

To achieve font development bliss, we're designing an ideal source and
interchange format for font data, that would achieve the goals set earlier.
As a long-term goal, we would like to see that file format:

- formally specified and documented.
- implemented for reading and writing in the various languages in use
  by font software (Python first, maybe C/C++/Swift/Rust... depending on uses)
- supported as an `Open` and `Save` option by GUI font editors, in a lossless
  way that "just works" even when switching between platforms and editors.
- supported as an input for font compilation software such as `fontmake` or
  the AFDKO, in such a way that without giving any options, the compiler
  produces the expected output.
- easy to version control, either with git (preferred) or Dropbox, etc.

Because the above goal is a bit idealistic, as a middle term goal, we want
that file format:

- to be at least somewhat specified, maybe by having a reference
  implementation in Python.
- to be "translatable" to existing formats such as UFO + Designspace, or
  proprietary formats such as Glyphs.app, à la glyphsLib.
- to be easy to version control with git.

That would allow us to use that better format as an interchange format between
existing tools, and test and refine the ideas behind it.

Finally, because it will take time to get anywhere and solve actual problems
with a brand new file format, we have a short-term goal of proposing
incremental improvements to existing formats to make them closer to the ideal
format (with future compatibility in mind), and to simplify our lives today,
by standardising emerging good practices. That's why this repository will
also be used to discuss incremental improvements to existing formats, such as
a new version of the Designspace format that includes useful practices
currently implemented "by hand" at Dalton Maag.

### [Ideal file format](ideal_file_format/README.md)

Diagrams and notes about what we would like to have in an ideal font file
format.

![](https://imgs.xkcd.com/comics/standards.png)

### Proposals

List of proposals to improve existing file formats that we use in order to
tend towards the ideal situation above.

- [Designspace 5.0 proposal (work in
  progress)](proposals/designspace_5/README.md)
