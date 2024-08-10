# This repo is ARCHIVED
Please see the Issues for reasons. We encourage contributions, if you want to contribute to the code base please ask a group moderator to unarchive the repo.







     SSV(1x)                                                    SSV(1x)



     NAME
          ssv - generate an image of an Imperial subsector

     SYNOPSIS
          ssv [-p] filename

     DESCRIPTION
          ssv is an X Window System datafile imaging utility.  ssv
          allows X users to diplay a datafile describing an Imperial
          subsector, add political/military boundaries to it, and to
          write to result to an XImage file which may then be printed
          using the xpr utility.  The '-p' option is used to write an
          output file directly ('ssv.xwd') without ever displaying the
          viewing windows.

     DATAFILE FORMAT
          The format of a sample datafile is shown below:

@SUB-SECTOR: The Narrows  SECTOR: Corridor
#
# Trade routes within the subsector
#src. dst.  X Y dst. offsets
$2710 2511  0 1
$2710 2908  0 0
$2908 2806  0 0
$2806 2906  0 0
$2908 3208  0 0
$3208 3508  1 0
#
# Borders or political boundaries
^0316 1
^0316 2
^0316 3
#
#--------1---------2---------3---------4---------5---------6---------7
#PlanetName   Loc. UPP Code   B   Notes         Z  PBG Al. Star(s)
#----------   ---- ---------  - --------------- -  --- -- ---------
Ackaeck       2502 B586757-9  H Ag Ri              314 Vh K7 V
Kidagir       2503 X242324-5    Lo Ni Po        R  522 Vh M8 V
PLUNGE        2505 B2409CC-E  H Hi In Po De        824 Vh G7 V
Jed           2506 C757863-6  C                    913 Vh M4 V G1 III
Chosen        2603 C534544-8    Ni                 303 Vh M1 V
   .
   .
   .

          Each line is read from the file in turn.  The first charcter
          of the file (the tag) determines what the data on that line
          represents.

          #    The line is a comment.  Ignore it.

          @    The line names the SECTOR/SUB-SECTOR for the file.
               Display this information across the top of the map,
               after dropping the tag.

          $    The line contains a segment in a trade or X-boat route.
               The first 2 fields are the beginning and ending hex
               locations.  The last 2 fields are offsets for the
               the end location if it is outside the border of the
               sector currently being displayed.  If this type of
               segment is being entered, the segment end that is
               INSIDE the subsector must always be listed first.
               The offets indicate in which direction the destination
               is off the map, but are not required to indicate how
               far.  For the X coordinate, -1 is to the left and 1 is
               to the right.  For the Y coordinate, -1 is up (this is
               X Windows, remember?) and 1 is down.  Segments with
               both ends outside the subsector cannot be used.  All
               4 fields MUST appear in the columns shown.

          ^    The line contains a segment of a political, military, or
               cultural boundary.  The first field is the hex location
               and the second field is the edge of the hex.  Hex edges
               are numbered from 0 to 5, clockwise, starting with the
               top edge.

          Any line in the file starting with a character other than
          those listed above is assumed to be an entry for a star system
          within that subsector and must be in the format shown above.
          Each star system entry contains (from left to right) name,
          hex location, UPP code, Base code, system notes, TAS zone code,
          pop. multiplier/asteroid belt/gas giant data, allegiance code,
          and star types.  These field MUST appear in the columns shown.

     BOUNDARY MARKING
          Additional political and/or military boundaries within a sector
          may be entered interactively by the user.  When the program is
          run, 2 windows will appear: the main window showing the subsector
          map, and a smaller control panel with 7 labeled buttons.  To begin
          marking a boundary press the MARK BORDER button.  Each left button
          (button1) press on your mouse (while on the map) will anchor a
          boundary segment at that point on the map.  This will continue
          until the right button (button3) is pressed.  The user may repeat
          this operation as many times as desired to install multiple boundary
          sections.  A boundary section (multiple segments) may be deleted
          by pressing the CLEAR BORDER button.  Only the last section entered
          may be deleted (presumably to correct a mistake).

     PRINTING TO FILE
          Once the appropriate boundaries have been added (if any) the
          entire map may be printed to an XImage file by pressing the
          PRINT MAP button.  The output file will always be 'ssv.xwd'
          and will always be written in the current working directory.
          This file may then be sent to a printer by any print utility
          capable of reading xwd files.  A typical invocation on an HP
          system might be:

      cat ssv.xwd | xpr -device ljet -density 150 -scale 1 -rv | lp -or

     AUTHOR
          ssv was developed by Mark F. Cook, Hewlett-Packard Company
          (markc@hpcvss.cv.hp.com).  Enhanced by Dan Corrin at the
          University of Waterloo (dan@engrg.uwo.ca).

     FILES
          ./ssv.xwd     Output file name for printed maps.

     SEE ALSO
          xpr(1), xwud(1), X(1)
