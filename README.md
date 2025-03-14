Custom Template for doing things with colors. 

[![hacs_badge](https://img.shields.io/badge/HACS-Default-41BDF5.svg)](https://github.com/custom-components/hacs)
![Version](https://img.shields.io/github/v/release/SirGoodenough/Color-Multi-Tool)
[![Community Forum](https://img.shields.io/badge/community-forum-orange.svg?style=for-the-badge)](https://community.home-assistant.io/t/color-multi-tool/659958)

[![GitHub issues](https://img.shields.io/github/issues-raw/SirGoodenough/Color-Multi-Tool?style=for-the-badge)](https://github.com/SirGoodenough/Color-Multi-Tool/issues?q=is%3Aopen+is%3Aissue)
[![GitHub closed issues](https://img.shields.io/github/issues-closed-raw/SirGoodenough/Color-Multi-Tool?style=for-the-badge)](https://github.com/SirGoodenough/Color-Multi-Tool/issues?q=is%3Aissue+is%3Aclosed)
[![GitHub contributors](https://img.shields.io/github/contributors/SirGoodenough/Color-Multi-Tool?style=for-the-badge)](https://github.com/SirGoodenough/Color-Multi-Tool/graphs/contributors)

<a href="https://www.buymeacoffee.com/SirGoodenough"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=&slug=SirGoodenough&button_colour=5F7FFF&font_colour=ffffff&font_family=Poppins&outline_colour=000000&coffee_colour=FFDD00" width=auto, height=30/></a>    [![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=SirGoodenough&repository=Color-Multi-Tool&category=template)
<base target="_blank">

# 🧯 Color-Multi-Tool

Custom Template for doing things with colors. It started out by wanting a way to get a random color name off of the official color name list. Then I decided it needed a way to pull random rgb, hs, and xy colors as well. I then decided to build the conversions between all the types.

The conversions are derived from HA's own color conversion code with the exception of rgb2hs. Home Assistant uses the built-in python module to do that in core, so I pulled the code for that from another source.

I followed the conversion code as close as I could, but I find that if you convert a color then convert it back, it drifts quite a bit.

I welcome the PR from anyone that can improve any of this code. It is 'functional' but not optimized at this point. In several cases I don't understand the code, I just ported it over, hopefully successfully. PR's are welcome.

Documentation for this Custom Template can be found at:

- The Description of each of the templates themselves.
- The github readme: https://github.com/SirGoodenough/Color-Multi-Tool/blob/master/README.md.
- Home Assistant Community Forum: https://community.home-assistant.io/t/color-multi-tool/659958.

This requires HomeAssistant version 2023.11.0 or greater due to the use of the list test in the code.

# 🦠 TO-DO List

- ~~Push to HACS Custom.~~
- ~~Error checking inputs for range.~~
- ~~Return a list of all the official color names.~~
- ~~Clean-up code, add shortcuts on redundancies.~~
- ~~Add ```Display closest color name to a given RGB```~~
- ~~Push to Hacs released.~~

# 🔩 Installation

Install this in HACS or download the `color_multi_tool.jinja`. From [this repository](https://github.com/SirGoodenough/Color-Multi-Tool) and place the files into your `config\custom_templates` directory.

[![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=SirGoodenough&repository=Color-Multi-Tool&category=template)

#### If you cannot see templates in your HACS listing

You *may* need to enable 'experimental features' mode. To do this find the HACS section of the Home Assistant Integration page. Click on the '>' arrow to bring you to the custom integration page. Then click on configure, and select 'enable experimental features' check box. click submit, then float out and restart the HA server to make sure it takes. When you come back HACS will look slightly different, but the Templates section is now visible and you will be able to select it. At some point in time HACS will update and the new interface and options will be the only available interface.

#### Other help

Before you report a 'Bug', you need to make sure you have read the accompanying Descriptions on the templates and this README and have followed all the settings required here.
This is important because if these instructions are not followed, you will likely have a bad day and be forced to contact me for help. Not that I don't want to help, but personal interaction takes me a while to respond and is generally non-productive.

Another good thing to do before you ask for help is try testing what you have in the Developer Tools Template Tab in Home Assistant. There you can adjust this and that until you figure out the answer to your question yourself. At the end of the color table in the code is the developer code that I use to test everything. If you provide any PR's make sure you load this and test all the things.

[![Open your Home Assistant instance and show your template developer tools.](https://my.home-assistant.io/badges/developer_template.svg)](https://my.home-assistant.io/redirect/developer_template/)

*********************

# Random Color Name

## `random_name()`

  This will return one of the official color names recognized by Home Assistant lifted directly from the Home Assistant core github November, 2023 at https://github.com/home-assistant/core/blob/dev/homeassistant/util/color.py and the Official CSS3 colors from w3.org: https://www.w3.org/TR/2010/PR-css3-color-20101028/#html4

  Names do not have spaces in them so that we can compare against requests more easily (by removing spaces from the requests as well).

  This lets "dark seagreen" and "dark sea green" both match the same color "darkseagreen".

### SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import random_name %}
    {{- random_name() -}}
  ```

*********************

# Random xy Color

## `random_xy()`

  This will return a CSV string that will convert to a list for a random color in the x,y format.

  SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import random_xy %}
    {% set _rxy = random_xy().split(",") | list -%}
    {{ [_rxy[0]|float|round(3),_rxy[1]|float|round(3)] | list}}
  ```

  REMEMBER:
    Everything returned from a macro template is a string, so for
    conventional usage of colors the result needs to be converted to a
    list as shown in the example above.

*********************

# Random hs Color

## `random_hs()`

  This will return a CSV string that will convert to a list for a random color in the h,s format.

  SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import random_hs %}
    {% set _rhs = random_hs().split(",") | list -%}
    {{ [_rhs[0]|float|round(2),_rhs[1]|float|round(2)] | list}}
  ```

  REMEMBER:
    Everything returned from a macro template is a string, so for
    conventional usage of colors the result needs to be converted to a
    list as shown in the example above.

*********************

# Random rgb Color

## `random_rgb()`

  This will return a CSV string that will convert to a list for a random color in the rgb format.

  SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import random_rgb %}
    {% set _rrgb = random_rgb().split(",") | list -%}
    {{ [_rrgb[0]|int(0),_rrgb[1]|int(0),_rrgb[2]|int(0)] | list}}
  ```

  REMEMBER:
    Everything returned from a macro template is a string, so for
    conventional usage of colors the result needs to be converted to a
    list as shown in the example above.

*********************

# Return the rgb Number for a Provided Color Name

## `name2rgb(color_name)`

  This will return the RGB value for an official color name recognized by Home Assistant lifted directly from the Home Assistant core github November, 2023 at https://github.com/home-assistant/core/blob/dev/homeassistant/util/color.py and the Official CSS3 colors from w3.org: https://www.w3.org/TR/2010/PR-css3-color-20101028/#html4

  Names do not have spaces in them so that we can compare against requests more easily (by removing spaces from the requests as well).

  This lets "dark seagreen" and "dark sea green" both match the same color "darkseagreen".

  Names do not have spaces in them so that we can compare against requests more easily (by removing spaces from the requests as well) 

  This lets "dark seagreen" and "dark sea green" both match the same color "darkseagreen".

  You have to type in her correct name. The text you send me will be set to no spaces and lower case to match the data as described above.

  If the name is not found, it will return "0.0.0", IE black, because then name you provided is not a color.

  SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import name2rgb %}
    {% set _name2rgb = name2rgb(color_name) %}
    {{ [_name2rgb[0]|int(0),_name2rgb[1]|int(0),_name2rgb[2]|int(0)] | list}}
  ```

  REMEMBER:
    Everything returned from a macro template is a string, so for
    conventional usage of colors the result needs to be converted to a
    list as shown in the example above.

*********************

# Return the Color Name for a Provided rgb Number

## `rgb2name(range, rgb_formatted_list)`

  This template will accept a list representing an RGB value plus a range value representing the window size of the 'close enough' color name. It will return the Home Assistant Color name that matches it or is close to it within a +/- range you specify.

- If you want only an exact match, then set the range to 0.
- If you think that +10/-10 is close enough, then set the range to 10.

  For default the color is set to black [0,0,0] and the range is 0, so it will by give you ['black'] for invalid input.

  SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import rgb2name %}
    {{ rgb2name(10,rgbl) }}
  ```

  REMEMBER:
    Everything returned from a macro template is a string.

*********************

# Return the xy Number for a Provided rgb Number

## `rgb2xy(rgb_formatted_list)`

  This will return a CSV string that will convert to a list in the x,y format from the rgb list provided.

  Be sure to convert this to a list when you use it on the other end because it arrives as a CSV string.

  Code lifted directly from the Home Assistant core github November, 2023 at https://github.com/home-assistant/core/blob/dev/homeassistant/util/color.py.

  Brightness is assumed to be 100%

  SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import rgb2xy %}
    {% set _rgb2xy = rgb2xy(rgbl).split(",") | list -%}
    {{ [_rgb2xy[0]|float|round(3),_rgb2xy[1]|float|round(3)] | list}}
  ```

  REMEMBER:
    Everything returned from a macro template is a string, so for
    conventional usage of colors the result needs to be converted to a
    list as shown in the example above.

*********************

# Return the rgb Number for a Provided xy Number

## `xy2rgb(xy_formatted_list)`

  This will return a CSV string that will convert to a list in the rgb format from the xy list provided.

  Be sure to convert this to a list when you use it on the other end because it arrives as a CSV string.

  Code lifted directly from the Home Assistant core github November, 2023 at https://github.com/home-assistant/core/blob/dev/homeassistant/util/color.py.

  Brightness is assumed to be 100%

  SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import xy2rgb %}
    {% set _xy2rgb = xy2rgb(xyl).split(",") | list -%}
    {{ [_xy2rgb[0]|int(0),_xy2rgb[1]|int(0),_xy2rgb[2]|int(0)] | list}}
  ```

  REMEMBER:
    Everything returned from a macro template is a string, so for
    conventional usage of colors the result needs to be converted to a
    list as shown in the example above.

*********************

# Return the rgb Number for a Provided hs Number

## `hs2rgb(hs_formatted_list)`

  This will return a CSV string that will convert to a list in the rgb format from the xy list provided.

  Be sure to convert this to a list when you use it on the other end because it arrives as a CSV string.

  Code lifted directly from the Home Assistant core github November, 2023 at https://github.com/home-assistant/core/blob/dev/homeassistant/util/color.py.

  Brightness is assumed to be 100%

  SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import hs2rgb %}
    {% set _hs2rgb = hs2rgb(hsl).split(",") | list -%}
    {{ [_hs2rgb[0]|int(0),_hs2rgb[1]|int(0),_hs2rgb[2]|int(0)] | list}}
  ```

  REMEMBER:
    Everything returned from a macro template is a string, so for
    conventional usage of colors the result needs to be converted to a
    list as shown in the example above.

*********************

# Return the hs Number for a Provided rgb Number

## `rgb2hs(rgb_formatted_list)`

  This will return a CSV string that will convert to a list in the x,y format from the rgb list provided.

  Be sure to convert this to a list when you use it on the other end because it arrives as a CSV string.

  Code lifted directly from the here November, 2023 at https://www.cs.rit.edu/~ncs/color/t_convert.html#RGB%20to%20HSV%20&%20HSV%20to%20RGB.

  Brightness is assumed to be 100%

  SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import rgb2hs %}
    {% set _rgb2hs = rgb2hs(rgbl).split(",") | list -%}
    {{[ _rgb2hs[0]|float(0)|round(3),_rgb2hs[1]|float(0)|round(3)] | list}}
  ```

  REMEMBER:
    Everything returned from a macro template is a string, so for
    conventional usage of colors the result needs to be converted to a
    list as shown in the example above.

*********************

# Return the xy Number for a Provided hs Number

## `hs2xy(hs_formatted_list)`

  This will return a CSV string that will convert to a list in the hs format from the xy list provided.

  Be sure to convert this to a list when you use it on the other end because it arrives as a CSV string.

  This converter uses other templates provided in this Custom Jinja Template.

  Brightness is assumed to be 100%

  SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import hs2xy %}
    {% set _hs2xy = hs2xy(hsl).split(",") | list -%}
    {{ [_hs2xy[0]|float|round(3),_hs2xy[1]|float|round(3)] | list}}
  ```

  REMEMBER:
    Everything returned from a macro template is a string, so for
    conventional usage of colors the result needs to be converted to a
    list as shown in the example above.

*********************

# Return the hs Number for a Provided xy Number

## `xy2hs(xy_formatted_list)`

  This will return a CSV string that will convert to a list in the hs format from the xy list provided.

  Be sure to convert this to a list when you use it on the other end because it arrives as a CSV string.

  This converter uses other templates provided in this Custom Jinja Template.

  Brightness is assumed to be 100%

  SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import xy2hs %}
    {% set _xy2hs = xy2hs(xyl).split(",") | list -%}
    {{ [_xy2hs[0]|float|round(3),_xy2hs[1]|float|round(3)] | list}}
  ```

  REMEMBER:
    Everything returned from a macro template is a string, so for
    conventional usage of colors the result needs to be converted to a
    list as shown in the example above.
    list as shown in the example above.

*********************

# Test if a list is a valid RGB color list

## `chkRGB(rgb_formatted_list)`

This will test a list to make sure it’s a valid RGB color list.

First we need to make sure it’s a list, and that the list has 3 members.
Then we need to test that each member is a number, an integer, and between 0 & 255.
If all that is true return True.
If any is not true, return False.
Development credit to @Didgeridrew and @jeffcrum on the
[Home Assistant Community Forums](https://community.home-assistant.io/t/help-with-test-of-a-list-of-numbers/664839/3)
for help sorting this out.

  SAMPLE USAGE:

```jinja
    {% from 'color_multi_tool.jinja' import chkRGB %}
    {{ chkRGB([255,165,0]) | bool }}
```

  REMEMBER:
    This always returns text, so cast to bool on the other end to be
    certain of the result.

*********************

# Test if a list is a valid XY color list

## `chkXY(xy_formatted_list)`

This will test a list to make sure it’s a valid XY color list.

First we need to make sure it’s a list, and that the list has 2 members.
Then we need to test that each member is a number, and between 0 & 1.
If all that is true return True.
If any is not true, return False.
Development credit to @123 on the
[Home Assistant Community Forums](https://community.home-assistant.io/t/help-with-test-of-a-list-of-numbers/664839/5)
for help sorting this out.

  SAMPLE USAGE:

```jinja
    {% from 'color_multi_tool.jinja' import chkXY %}
    {{ chkXY([0.497,0.472]) | bool }}
```

  REMEMBER:
    This always returns text, so cast to bool on the other end to be
    certain of the result.

*********************

# Test if a list is a valid HS color list

## `chkHS(hs_formatted_list)`

This will test a list to make sure it’s a valid HS color list.

First we need to make sure it’s a list, and that the list has 2 members.
Then we need to test that each member is a number.
The first one has to be 0 to 100, the second one has to be 0 to 360.
If all that is true return True.
If any is not true, return False.
Development credit to @123 on the
[Home Assistant Community Forums](https://community.home-assistant.io/t/help-with-test-of-a-list-of-numbers/664839/5)
for help sorting this out.

  SAMPLE USAGE:

```jinja
    {% from 'color_multi_tool.jinja' import chkHS %}
    {{ chkHS([38.824,100.0]) | bool }}
```

  REMEMBER:
    This always returns text, so cast to bool on the other end to be
    certain of the result.

*********************

## `chkNAME(color_name)`

Is this color name on the official list?
This will test a provided color name to see if it is on the HA color list.

First we need to make sure it’s a string_like variable.
Then we test that the string is only lowercase letters to match the HA list.
Then we iterate thru the list to make sure it is on the list.
If all that is true return true.
If any is not true, return false.

  SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import chkNAME %}
    {{ chkNAME('orange') | bool }}
  ```

  REMEMBER:
    This always returns text, so cast to bool on the other end to be
    certain of the result.

*********************

## `color_list()`

  This will return all of the official color names recognized by Home Assistant
    lifted directly from the Home Assistant core github November, 2023 at
    https://github.com/home-assistant/core/blob/dev/homeassistant/util/color.py
    and the Official CSS3 colors from w3.org:
    https://www.w3.org/TR/2010/PR-css3-color-20101028/#html4
    Names do not have spaces in them so that we can compare against
    requests more easily (by removing spaces from the requests as well).
    This lets "dark seagreen" and "dark sea green" both match the same
    color "darkseagreen". 
    You also get the RGB color code for each of the color names.

  SAMPLE USAGE:

  ```jinja
    {% from 'color_multi_tool.jinja' import color_list() %}
    {{- color_list().split('\n') | list -}}
  ```

### Other Info

Location of this code: https://github.com/SirGoodenough/Color-Multi-Tool

Home Assistant Community Forum post: https://community.home-assistant.io/t/color-multi-tool/659958

Let me know if you have a suggestion.

If you have any questions, comments or additions be sure to add an issue in the above listed github repo and bring them up on my Discord Server:

### 🤹🏾‍♂️ Contact Links or see my other work

What are we Fixing Today Homepage / Website: https://www.WhatAreWeFixing.Today/

Channel Link URL: (WhatAreWeFixingToday): https://bit.ly/WhatAreWeFixingTodaysYT

What are we Fixing Today Facebook page (Sir GoodEnough): https://bit.ly/WhatAreWeFixingTodaybFB

What are we Fixing Today Twitter Account (Sir GoodEnough): https://bit.ly/WhatAreWeFixingTodayTW

Discord Guild: (Sir_Goodenough#9683): https://discord.gg/Uhmhu3B

BluePrint Library: https://github.com/SirGoodenough/HA_Blueprints/blob/master/README.md

#WhatAreWeFixingToday

#SirGoodEnough

### Disclaimer

⚠️ **DANGER OF ELECTROCUTION** ⚠️

If your device connects to mains electricity (AC power) there is danger of electrocution if not installed properly. If you don't know how to install it, please call an electrician (***Beware:*** certain countries prohibit installation without a licensed electrician present). Remember: **SAFETY FIRST**. It is not worth the risk to yourself, your family and your home if you don't know exactly what you are doing. Never tinker or try to flash a device using the serial programming interface while it is connected to MAINS ELECTRICITY (AC power).
