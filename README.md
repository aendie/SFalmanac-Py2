# SFalmanac-Py2

SFalmanac-Py2 is a Python 2.7 script that creates the daily pages of the Nautical Almanac **using the UT1 timescale** :smiley:. Official Nautical Almanacs employ a UT timescale (equivalent to UT1).
These are tables that are needed for celestial navigation with a sextant. Although you are strongly advised to purchase the official Nautical Almanac, this program will reproduce the tables with no warranty or guarantee of accuracy.

SFalmanac-Py2 was developed with the intention of having identical output format as Pyalmanac-Py2. As opposed to the older PyEphem astronomy library, the intention was for it to be based entirely on the newer Skyfield astronomical library: https://rhodesmill.org/skyfield/, however PyEphem is still required to calculate the planet magnitudes.

It uses the star database in Skyfield, which is based on data from the Hipparcos Catalogue. The principal disadvantage is that calculating twilight (actual, civil and nautical sunrise/sunset) and moonrise/moonset is **extremely** slow. As a consequence of this a new hybrid version is available that is four times faster. (The hybrid version uses PyEphem to calculate twilight and moonrise/moonset with only a minimal loss of accuracy.)

NOTE: two scripts are included (both can be run): 'sfalmanac.py' and 'increments.py'  
NOTE: a Python 3 script with identical functionality can be found at:  https://github.com/aendie/SFalmanac-Py3  
NOTE: a 100% [PyEphem](https://rhodesmill.org/pyephem/) version of SFalmanac is available here: https://github.com/aendie/Pyalmanac-Py2  
NOTE: the faster hybrid version is available here: 
https://github.com/aendie/SkyAlmanac-Py2

An aim of this development was to maintain:

* **identical PDF output formatting with a similar control program**  
	 It is then possible to display both generated tables (from PyEphem and Skyfield)
	 and compare what has changed by flipping between the two tabs in Adobe Acrobat Reader DC.
	 Anything that has changed flashes, thereby drawing your attention to it.
	 This crude and simple method is quite effective in highlihgting data that
	 might need further attention.

The results have been crosschecked with USNO data to some extent.  
(However, constructive feedback is always appreciated.)

**UPDATE: Nov 2019**

Declination formatting has been changed to the standard used in Nautical Almanacs. In each 6-hour block of declinations, the degrees value is only printed on the first line if it doesn't change. It is printed whenever the degrees value changes. The fourth line has two dots indicating "ditto". This applies to all planet declinations and for the sun's declination, but not to the moon's declination as this is continuously changing.

This also includes some very minor changes and an improved title page for the full almanac with two star charts that indicate the equatorial navigational stars.

**UPDATE: Jan 2020**

The Nautical Almanac tables now indicate if the sun never sets or never rises; similarly if the moon never sets or never rises. For better performance, the *SunNeverSets* or *SunNeverRises* state is determined only by the month of year and hemisphere. (This is reliable for the set of latitudes printed in the Nautical Almanac tables.) The code also has cosmetic improvements.  
P.S. The *Overfull \hbox in paragraph...* messages can be ignored - the PDF is correctly generated.

**UPDATE: Feb 2020**

The main focus was on cleaning up the TeX code and eliminating the *Overfull/Underfull hbox/vbox* messages. Other minor improvements were included. A Skyfield issue with days that have no moonrise or moonset at a specific latitude was resolved.

**UPDATE: Mar 2020**

A new parameter in *config.py* enables one to choose between A4 and Letter-sized pages. A [new approach](https://docs.python.org/3/whatsnew/3.0.html#pep-3101-a-new-approach-to-string-formatting) to string formatting has been implemented:
the [old](https://docs.python.org/2/library/stdtypes.html#string-formatting) style Python string formatting syntax has been replaced by the [new](https://docs.python.org/3/library/string.html#format-string-syntax) style string formatting syntax. 

**UPDATE: Jun 2020**

The Equation Of Time is shaded whenever EoT is negative indicating that apparent solar time is slow compared to mean solar time (mean solar time > apparent solar time).
It is possible to extend the maximum year beyond 2050 by choosing a different ephemeris in config.py.
Bugfix applied to correct the Meridian Passage times.

**UPDATE: Jul 2020**

A new option has been added into config.py: *moonimg = True* will display a graphic image of the moon phase (making the resulting PDF slightly larger). Use *moonimg = False* to revert to the previous format without the graphic moon image.

**UPDATE: Mar 2021**

&emsp;:smiley:&ensp;***UT is the new timescale employed in the almanac.***&ensp;:smiley:

Two new options have been added into config.py: *useIERS = True* instructs Skyfield (if >= 1.31) to download Earth orientation data from IERS (International Earth Rotation and Reference Systems Service). *ageIERS = 30* instructs Skyfield to download fresh data from IERS if older tham that number of days. This implies greater accuracy for the generated almanacs (if Skyfield >= 1.31).

Note that although you may be using the *de421.bsp* ephemeris (valid from 1900 to 2050), the IERS currently specifies the validity of Earth Orientation Parameters (EOP) from 2nd January 1973 to 
15th May 2022. Refer to the [IERS web site](https://www.iers.org/IERS/EN/Home/home_node.html) for current information.

## Requirements

&emsp;Most of the computation is done by the free Skyfield library.  
&emsp;Typesetting is typically done by MiKTeX or TeX Live.  
&emsp;These need to be installed:

* Python v2.x (2.6 or later)
* Skyfield 1.31 (for best accuracy use 1.31 or higher - see the Skyfield Changelog)
* Pandas 0.24 (to load the Hipparcos catalog; tested: 0.24.2)
* Ephem 3.7.6 or 3.7.7 (required for planet magnitudes)
* MiKTeX&ensp;or&ensp;TeX Live

&emsp;**DEPRECATION: Python 2.7 reached the end of its life on January 1st, 2020.**  
&emsp;**Please upgrade your Python as Python 2.7 is no longer maintained.**  
&emsp;**pip 21.0 dropped support for Python 2.7 in January 2021.**

## Files required in the execution folder:

* &ast;.py
* Ra.jpg
* croppedmoon.png
* A4chart0-180_P.pdf
* A4chart180-360_P.pdf

&emsp;If upgrading from an older version of Skyfield to 1.31 or higher, these files may be deleted:  
&emsp;**deltat.data** and **deltat.preds**

### INSTALLATION GUIDELINES on Windows 10:

&emsp;Install Python 2.7 (do not add python.exe to path)  
&emsp;Install MiKTeX 20.11 from https://miktex.org/  
&emsp;When MiKTeX first runs it will require installation of additional packages.  
&emsp;Run Command Prompt as Administrator; go to your Python folder and execute, e.g.:

&emsp;**cd C:\\Python27\\Scripts**  
&emsp;**pip install wheel**  
&emsp;**pip uninstall pyephem**  
&emsp;**pip install ephem**  
&emsp;**pip install skyfield**  
&emsp;**pip install pandas**  

&emsp;NOTE: if Python 3 is already installed, you need to be in the Scripts folder - otherwise the Py3 version of pip will execute.  
&emsp;NOTE: you may get the following error:  
&emsp;**error: Microsoft Visual C++ 9.0 is required. Get it from http://aka.ms/vcpython27**

&emsp;On Windows 10 Version 2004 and 20H2 there is currently a bug that may cause the following error:  
&emsp;**RuntimeError: The current Numpy installation fails to pass a sanity check due to a bug in the windows runtime.**  
&emsp;The final resolution is expected end of January 2021, however the following workaround will bypass the problem:  
&emsp;**pip uninstall numpy**  
&emsp;**pip install numpy==1.19.3**  

&emsp;Put the SFalmanac files in any folder, run Command Prompt in that folder and start with:  
&emsp;**python.exe sfalmanac.py**  

&emsp;However, if Python 3 is also installed, start with:  
&emsp;**py -2 sfalmanac.py**  


### INSTALLATION GUIDELINES on Ubuntu 18.04:

&emsp;Ubuntu 18 and earlier come with Python 2 preinstalled,  
&emsp;however pip may need to be installed:  
&emsp;**sudo apt install python-pip**  
&emsp;Note: Ubuntu 20.04 comes with Python 3 preinstalled, which is preferable to Python 2.

&emsp;Install the following TeX Live package:  
&emsp;**sudo apt install texlive-latex-extra**

&emsp;Install the required astronomical libraries etc.:  
&emsp;**pip install wheel**  
&emsp;**pip uninstall pyephem**  
&emsp;**pip install ephem**  
&emsp;**pip install skyfield**  
&emsp;**pip install pandas**  

&emsp;Put the SFalmanac files in a folder and start with:  
&emsp;**python sfalmanac.py**  


### INSTALLATION GUIDELINES on MAC:

&emsp;Every Mac comes with python preinstalled.  
&emsp;(Please choose the Python 3 version of SFalmanac if Python 3.* is installed.)  
&emsp;You need to install the PyEphem and Skyfield libraries to use SFalmanac.  
&emsp;Type the following commands at the commandline (terminal app):

&emsp;**sudo easy_install pip**  
&emsp;**pip uninstall pyephem**  
&emsp;**pip install ephem**  
&emsp;**pip install skyfield**  
&emsp;**pip install pandas**  

&emsp;If this command fails, your Mac asks you if you would like to install the header files.  
&emsp;Do so - you do not need to install the full IDE - and try again.

&emsp;Install TeX/LaTeX from http://www.tug.org/mactex/

&emsp;Now you are almost ready. Put the SFalmanac files in any directory and start with:  
&emsp;**python sfalmanac**  
&emsp;or  
&emsp;**./sfalmanac**
