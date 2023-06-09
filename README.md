Original source downloaded from https://ftp.gnu.org/gnu/hp2xx/hp2xx-3.4.4.tar.gz
I added solution files for Visual studio 2013 and 2022. The compilation is not perfect and I have a feeling AMIGA shouldn't be included when compiling on windows. Never the less It compiles and runs the basic commands such as 
generate svg file.
```
hp2xx.exe -m svg test.hpg
```
generate eps which can be converted to pdf.
```
hp2xx.exe -m eps test.hpg
```
Show a preview
```
hp2xx.exe test.hpg 
```

## Visual studio
The visual sudio solution files are in ./makes folder no changes are needed to build and run assuming you have the correct SDKs installed or a suitable alternative. You can install Visual Studio 2017 Express from here https://aka.ms/vs/15/release/vs_WDExpress.exe ("Express" is free to use for both commercial and personal projects unlike community editions which don't allow most commercial uses). Visual Studio 2017 Express can run either 2013 or 2022 visual studio solutions. 

## Original README
hp2xx-3.4.4 

This is mainly a bugfix release to correct some problems found in 3.4.3.
In addition, it provides a tentative framework for truetype font support
and a few other minor enhancements.
I would greatly appreciate receiving bug reports, patches or even sample 
HPGL files. (In the latter case, please make sure that no copyright or 
confidentiality agreements are violated before sending any materials.)

Martin Kroeker, 
mk@daveg.com OR martin@ruby.chemie.uni-freiburg.de

Disclaimer: while i currently work for Daveg GmbH and they have generously 
            waived their rights (as per German employment laws) on the code 
            i wrote for hp2xx, this software is totally unrelated to, and 
            not endorsed by, Daveg GmbH. 
See the file 'copying' (i.e. the GNU GPL) for license and warranty
information.



Changes from 3.4.3 to 3.4.4

New features:

- Experimental support for truetype fonts (needs a fixed-width truetype
  font such as the monospace Bitstream Vera from www.gnome.org/fonts,
  fontlib, and '-DSTROKED_FONTS=\"/path/to/this/truetype/font.ttf\"' in the
  DEFINES section of the Makefile). Depending on the font, this should 
  produce better-looking text than the default stick font at the expense
  of higher CPU and memory consumption. Support for non-ASCII characters
  is lacking, and the rendering is at the mercy of the still imperfect
  polygon rasterizer. 
- Support for the rectangle mode of the PE statement (Eugene Doudine)
- NR is now recognized as an image terminator in multi-plot files.
- DXF output provides optional translation of pen number and/or width
  into DXF group 62 line attributes (Georg Viehoever).
- The error handler now tries to report the offending HPGL command sequence,
  not just its position in the input stream
- New option for mapping pen 0 commands to another pen, to avoid changing
  the background color in raster output modes.

Bug fixes:

- penwidth was erroneously set to the default 0.1 mm after drawing a label
- xfig and rgip output did not yet handle the changed pencolor and width
  settings
- polygons sometimes had the wrong sections filled in for some of the 
  scanlines
- forcing penwidth via the -p commandline option no longer worked for 
  the conventional values between 1 and 9 
- PJL parser now handles input lines of up to 256 characters 
- polygon sides could escape clipping in some circumstances
- WG support was broken in 3.4.3 (coordinate error resulted in odd shapes)
- simplified HPGL output would write very small numbers in exponential
  notation, which is not allowed by any HPGL standard.
- DT handling was both incorrect and incomplete
- pdf and eps modes were using much too large miter limits
- exporting to raster modes could fail in some circumstances due to 
  wrong linewidth corrections being applied in the raster buffer.
- arcs drawn with 'deviation distance' chord tolerance parameter were
  drawn as acute angles or even crashed hp2xx
- PNG export of color graphics was broken in 3.4.3
- SP command in PE mode did not update the internal pencount, potentially
  leading to use of a reduced color palette in the raster modes.
- Using -h,-? or even -help no longer generates an error message before the
  usage text is shown.
