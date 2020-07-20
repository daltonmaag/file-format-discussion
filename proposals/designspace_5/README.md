# Designspace 5.0 proposal

This is a proposed update to the
[Designspace](https://github.com/fonttools/fonttools/tree/master/Doc/source/designspaceLib)
file format that standardises the following Dalton Maag practices:

* Allow to mix interpolatable sources and some that are not, as long as they're
part of the same "design space". Introduce discrete axes to organize these
sources. Example: uprights and italics. The goal is to have 1 designspace file
for any cohesive font project, with everything listed in one place. This goes
hand-in-hand with the next points.

* Provide STAT table information from the start, and include it in the
Designspace file format. Also allow to provide STAT information for linked
families that are not interpolatable (e.g. Source Sans Roman and Source Sans
Italic) in one single Designspace file. This feature would supersede the
external Stylespace files that Nikolaus developed (see
[statmake](https://github.com/daltonmaag/statmake))
  * Only one copy of the STAT information is maintained, and it is attached to
    the data that it describes (i.e. the usual contents of desispace files).

    Alternative options at the moment don't achieve this:
      * `statmake`'s file is next to the designspace, and needs to be kept
        up-to-date separately
      * Writing STAT information in a feature file is also separate from the
        designspace and needs to be updated separately.
  * We can use the STAT information to provide default lists of named instances
    to be included in the defined variable fonts.

* Define more clearly what can be "produced" from a Designspace by running it
  through a compiler such as `fontmake`, i.e. list explicitly the outputs of
  the build process in the designspace. This achieves two things:
  * We can just feed the designspace to a compiler and get everything we
    expect from it without fiddling with compiler options
  * Because possible outputs are defined explicitly, we can refer to them and
    associate data to them. For example: if the designspace defines two
    variable fonts, and we have two special font tables dumped in TTX format
    to mix into these two fonts, we can express the link between each font
    and each TTX dump.

* Continous and discrete axes will define groups of sources that are
interpolatable. (or maybe we need to explicitly define these groups? To be
discussed). From there:
  * Define several variable fonts from the same set of interpolatable sources.
    This would allow VF projects with several axes such as Aktiv Grotesk to
    have only 1 Designspace file that describes all 5 variable fonts that we
    ship (instead of the current situation where we write 5 Designspace files
    with repeated information).
  * Define several static instances from each group of interpolatable sources.


## Sample files

### [`SourceSans.designspace`](./SourceSans.designspace)

This example file demonstrates how to:
* include STAT table information
* rely on it to get correctly named instances
* mix interpolatable and discrete axes
* define several variable fonts from the "design space"


## Details of proposed changes to the specification

Ideally should be a merge request in fontTools/designspaceLib (once the
modifications described are deemed generally good ideas).

