
[//000000001]: # (tooltip \- Tooltip management)
[//000000002]: # (Generated from file 'tooltip\.man' by tcllib/doctools with format 'markdown')
[//000000003]: # (Copyright &copy; 1996\-2008, Jeffrey Hobbs)
[//000000004]: # (tooltip\(n\) 1\.4\.7 tklib "Tooltip management")

<hr> [ <a href="../../../../toc.md">Main Table Of Contents</a> &#124; <a
href="../../../toc.md">Table Of Contents</a> &#124; <a
href="../../../../index.md">Keyword Index</a> &#124; <a
href="../../../../toc0.md">Categories</a> &#124; <a
href="../../../../toc1.md">Modules</a> &#124; <a
href="../../../../toc2.md">Applications</a> ] <hr>

# NAME

tooltip \- Tooltip management

# <a name='toc'></a>Table Of Contents

  - [Table Of Contents](#toc)

  - [Synopsis](#synopsis)

  - [Description](#section1)

  - [COMMANDS](#section2)

  - [EXAMPLE](#section3)

  - [Bugs, Ideas, Feedback](#section4)

  - [Keywords](#keywords)

  - [Copyright](#copyright)

# <a name='synopsis'></a>SYNOPSIS

package require Tcl 8\.4  
package require msgcat 1\.3  
package require tooltip ?1\.4\.7?  

[__::tooltip::tooltip__ *command* ?*options*?](#1)  
[__::tooltip::tooltip__ *pathName* ?*option arg*? *message*](#2)  

# <a name='description'></a>DESCRIPTION

This package provides tooltips, small text messages that can be displayed when
the mouse hovers over a widget, menu item, canvas item, listbox item or text
widget tag\.

# <a name='section2'></a>COMMANDS

  - <a name='1'></a>__::tooltip::tooltip__ *command* ?*options*?

    Manage the tooltip package using the following subcommands\.

      * __clear__ ?*pattern*?

        Prevents the specified widgets from showing tooltips\. *pattern* is a
        glob pattern and defaults to matching all widgets\.

      * __delay__ ?*millisecs*?

        Query or set the hover delay\. This is the interval that the pointer must
        remain over the widget before the tooltip is displayed\. The delay is
        specified in milliseconds and must be greater than or equal to 50ms\.
        With no argument the current delay is returned\.

      * __fade__ ?*boolean*?

        Enable or disable fading of the tooltip\. The fading is enabled by
        default on Win32 and Aqua\. The tooltip will fade away on Leave events
        instead disappearing\.

      * __disable__

      * __off__

        Disable all tooltips

      * __enable__

      * __on__

        Enables tooltips for defined widgets\.

  - <a name='2'></a>__::tooltip::tooltip__ *pathName* ?*option arg*? *message*

    This command arranges for widget *pathName* to display a tooltip with
    message *message*\. The tooltip uses a late\-binding msgcat call on the
    passed in message to allow for on\-the\-fly language changes in an
    application\. If the widget specified is a menu, canvas, listbox or text
    widget then additional options are used to tie the tooltip to specific menu
    entries, canvas or listbox items, or text widget tags\.

      * __\-index__ *index*

        This option is used to set a tooltip on a menu item\. The index may be
        either the entry index or the entry label\. The widget must be a menu
        widget but the entries do not have to exist when the tooltip is set\.

      * __\-items__ *name*

        This option is used to set a tooltip for canvas widget or listbox items\.
        For the canvas widget, the item must already be present in the canvas
        widget and will be found with a __find withtag__ lookup\. For listbox
        widgets the item\(s\) may be created later but the programmer is
        responsible for managing the link between the listbox item index and the
        corresponding tooltip\. If the listbox items are re\-ordered, the tooltips
        will need amending\.

        If the widget is not a canvas or listbox then an error is raised\.

      * __\-tag__ *name*

        The __\-tag__ option can be used to set a tooltip for a text widget
        tag\. The tag should already be present when this command is called or an
        error will be returned\. The widget must also be a text widget\.

      * __\-\-__

        The __\-\-__ option marks the end of options\. The argument following
        this one will be treated as *message* even if it starts with a \-\.

# <a name='section3'></a>EXAMPLE

    # Demonstrate widget tooltip
    package require tooltip
    pack [label .l -text "label"]
    tooltip::tooltip .l "This is a label widget"

    # Demonstrate menu tooltip
    package require tooltip
    . configure -menu [menu .menu]
    .menu add cascade -label Test -menu [menu .menu.test -tearoff 0]
    .menu.test add command -label Tooltip
    tooltip::tooltip .menu.test -index 0 "This is a menu tooltip"

    # Demonstrate canvas item tooltip
    package require tooltip
    pack [canvas .c]
    set item [.c create rectangle 10 10 80 80 -fill red]
    tooltip::tooltip .c -item $item "Canvas item tooltip"

    # Demonstrate listbox item tooltip
    package require tooltip
    pack [listbox .lb]
    .lb insert 0 "item one"
    tooltip::tooltip .lb -item 0 "Listbox item tooltip"

    # Demonstrate text tag tooltip
    package require tooltip
    pack [text .txt]
    .txt tag configure TIP-1 -underline 1
    tooltip::tooltip .txt -tag TIP-1 "tooltip one text"
    .txt insert end "An example of a " {} "tooltip" TIP-1 " tag.\n" {}

# <a name='section4'></a>Bugs, Ideas, Feedback

This document, and the package it describes, will undoubtedly contain bugs and
other problems\. Please report such in the category *tooltip* of the [Tklib
Trackers](http://core\.tcl\.tk/tklib/reportlist)\. Please also report any ideas
for enhancements you may have for either package and/or documentation\.

# <a name='keywords'></a>KEYWORDS

[balloon](\.\./\.\./\.\./\.\./index\.md\#balloon),
[help](\.\./\.\./\.\./\.\./index\.md\#help), [hover](\.\./\.\./\.\./\.\./index\.md\#hover),
[tooltip](\.\./\.\./\.\./\.\./index\.md\#tooltip)

# <a name='copyright'></a>COPYRIGHT

Copyright &copy; 1996\-2008, Jeffrey Hobbs
