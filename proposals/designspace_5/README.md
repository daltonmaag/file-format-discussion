# Designspace 5.0 proposal

This is a proposed update to the
[Designspace](https://github.com/fonttools/fonttools/tree/master/Doc/source/designspaceLib)
file format that standardises the following Dalton Maag practices:

* Provide STAT table information from the start, and include it in the
Designspace file format. Also allow to provide STAT information for linked
families that are not interpolatable (e.g. Source Sans Roman and Source Sans
Italic) in one single Designspace file. This feature would supersede the
external Stylespace files that Nikolaus developed (see
[statmake](https://github.com/daltonmaag/statmake))

* Define several variable fonts from the same set of interpolatable sources.
This would allow VF projects with several axes such as Aktiv Grotesk to have
only 1 Designspace file that describes all 5 variable fonts that we ship
(instead of the current situation where we write 5 Designspace files with
repeated information).

* Use the STAT information to provide default lists of named instances to be
included in the defined variable fonts.

* Define more clearly what can be "produced" from a Designspace by running it
through e.g. `fontmake`.
