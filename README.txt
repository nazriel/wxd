wxD - wxWidgets bindings for D language

	(c) 2005 BERO <berobero@users.sourceforge.net>
	(c) 2006 afb <afb@users.sourceforge.net>

* About

wxD is wxWidgets bindings for the D programming language.

wxWidgets is a cross-platform GUI toolkit, which supports Windows,
Mac OS X, *nix-like OSs - such as Linux,FreeBSD with X11/Motif/GTK.

wxD is delivered work from wx.NET bindings 0.7.2 (wxWidgets 2.6.1)
It should also work with the later minor versions of wxWidgets 2.6.

It is composed of two parts:
   + wxc is a C++ library which exposes the wxWidgets API as a 
     collection of D friendly functions.
   + wxd is a library written in D which parallels the wxWidgets 
     class hierarchy, ported from wx.NET.


* Status

0.08 (afb)
Added StyledText sample for wxSTC testing
Cleaned up Makefiles, and "DFLAGS" usage
Not build Samples by default ("make test")
Added project files for Code::Blocks / GDC

0.07 (afb)
Updated imports for DMD 0.164 ("public")
Moved all config files to a sub-directory
Fixed MSW issue with Update/UpdateContext
Now compiles with D warnings enabled too

0.06 (afb)
Lots of bugfixes by Matrix, thanks a lot!
Fixed issue with wxValidator* constness
Fixed issue with null GL context on Linux
Added Launcher sample and continued port

0.05 (afb)
Fixed issue with D bool versus C++ bool
Deprecated the new_ struct constructors
Added wxSound class and the Sound sample
Extra documentation comments for the modules

0.04 (afb)
Removed the extra gcc linking for Darwin
Added wxGLCanvas class and the GLCube sample
Added Doxygen documentation (and \cond+\endcond)
Extra configuration files for MinGW32 (Windows)

0.03 (afb)
Update to wx26
Fixed some wxChar issues with Unicode builds
Added support for wxVersion constants
Additionally checked on Linux/Mac OS X platforms.

0.02 (bero)
some bug fix and missing C function implement.
more example works.
fix event
change multiple constructor to single constructor with default args
fix box sizer
 return struct func to void func(struct*)
 in my view, D's extern (C) and C++'s extern "C" is not compatible when return struct
most example work.

0.01 (bero)
Under development.
Currently only checked on Windows platform.
Some example program crashed.


* How to compile

** build wxWidgets

- get wxWidgets-2.6.x
- extract
- regenerate, if needed
windows: (Digital Mars)
    cd build\bakefiles
    bakefile_gen
unix/mac: (GNU)
    ./autogen.sh
- compile and install
windows: (Digital Mars)
  cd build\msw
  make -f makefile.dmc
unix/mac: (GNU)
  ./configure
  make
  sudo make install

** build wxD
- extract
- compile
windows:
  set WXDIR=<path to wxWidgets>
  make all test
unix/mac:
  make all test
freebsd:
  gmake all test


* Naming rules

- constant/enum wxXXXX is wxXXXX
- class/method wxXXX is XXX
- method SetXXX/GetXXX change to property XXX,
  but if XXX is class name, change first character to lower case 
  ex: void SetColour(wxColour)/wxColor GetColour() -> void colour(Color)/Colour colour()

Point,Size,Rect is native D struct instead of wxWidgets struct.
in D, struct can't have constructor.
for convenience, use constructor like function:
 Point Point(int x,int y);
 Size  Size(int w,int h);
 Rect  Rect(int x,int y,int w,int h)
(Rect is an alias of Rectangle)

    C++ API passing array and number of element change to passing array only.
    D array knows number of element.
    ex:

    wxListBox(wxWindow *parent, wxWindowID id,
            const wxPoint& pos = wxDefaultPosition,
            const wxSize& size = wxDefaultSize,
    --->    int n = 0, const wxString choices[] = NULL,
            long style = 0,
            const wxValidator validator = wxDefaultValidator,
            const wxString& name = wxListBoxNameStr)

    ListBox(Window parent, WindowID id,
            Point pos = wxDefaultPosition,
            Size size = wxDefaultSize,
    -->     string choices[] = null,
            long style = 0,
            Validator validator = wxDefaultValidator,
            string name = wxListBoxNameStr)
   
* Platforms

When compiling wxD programs, you need to tell it which version of
wxWidgets that you want (i.e. what platform you are targetting)

If you are using the GNU Makefiles and the wx-config script, then
your platform name should be available in the file "wxc/platform".

Here are the main supported ones:
Windows XP     version=__WXMSW__
Linux/GTK+     version=__WXGTK__
Macintosh      version=__WXMAC__

For checking the wx platform at runtime, see the wxPlatform class.

* Strings

There are two ways to compile wxWidgets, as "ansi" or as "unicode"

In wxD, ANSI means to use UTF-8 and UNICODE means UTF-16 or UTF-32
(depending on the OS, e.g. Windows does UTF-16 and Unix does UTF-32)

wx-config:     DFLAGS:
--unicode=no   version=ANSI
--unicode=yes  version=UNICODE

The alias "string" is used in wxD, for char[] strings (UTF-8 format)

* Licence

wxD is licensed under the wxWindows Licence which is LGPL, with a
special exception to allow distributing as a static linked binary.

For more information, see files:
LICENCE.txt and COPYING.LIB

wxWindows Licence is OSI approved Open Source:
http://www.opensource.org/licenses/wxwindows.php


* Acknowledgements

- wxWidgets [http://www.wxwidgets.org/]
- wx.NET [http://wxnet.sourceforge.net/]
- DMD [http://www.digitalmars.com/d/]
- GDC [http://dgcc.sourceforge.net/]
- gdcmac [http://gdcmac.sourceforge.net/]
- gdcwin [http://gdcwin.sourceforge.net/]