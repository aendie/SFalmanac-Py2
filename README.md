# SFalmanac-Py2

SFalmanac-Py2 is a Python 2.7 script that creates the daily pages of the Nautical Almanac. These are tables that are needed for celestial navigation with a sextant. Although you are strongly advised to purchase the official Nautical Almanac, this program will reproduce the tables with no warranty or guarantee of accuracy.

SFalmanac-Py2 was developed with the intention of having identical output format as Pyalmanac-Py2. As opposed to the older PyEphem astronomy library, the intention was for it to be based entirely on the newer Skyfield astronomical library: https://rhodesmill.org/skyfield/, however PyEphem is still required to calculate the planet magnitudes.

It uses the star database in Skyfield, which is based on data from the Hipparcos Catalogue. The principal disadvantage is that calculating twilight (actual, civil and nautical sunrise/sunset) and moonrise/moonset is **extremely** slow. As a consequence of this a new hybrid version is available that is four times faster. (The hybrid version uses PyEphem to calculate twilight and moonrise/moonset with only a minimal loss of accuracy.)

NOTE: two scripts are included (both can be run): 'sfalmanac.py' and 'increments.py'  
NOTE: a Python 3 script with identical functionality can be found at:  https://github.com/aendie/SFalmanac-Py3  
NOTE: a 100% [PyEphem](https://rhodesmill.org/pyephem/) version of SFalmanac is available here:  
https://github.com/aendie/Pyalmanac-Py2  
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

This includes very minor changes and an improved title page for the full almanac with two star charts that indicate the equatorial navigational stars.

## Requirements

&nbsp;&nbsp;&nbsp;&nbsp;Most of the computation is done by the free Skyfield library.  
&nbsp;&nbsp;&nbsp;&nbsp;Typesetting is done by LaTeX or MiKTeX so you first need to install:

* Python v2.x (2.6 or later)
* Skyfield 1.15 (tested version)
* Pandas (to load the Hipparcos catalog; tested: 0.24.2, 0.25.3)
* PyEphem 3.7.6 or 3.7.7 (required for planet magnitudes)
* TeX/LaTeX&nbsp;&nbsp;or&nbsp;&nbsp;MiKTeX

&nbsp;&nbsp;&nbsp;&nbsp;When MiKTeX first runs it will require installation of additional packages.  
&nbsp;&nbsp;&nbsp;&nbsp;Ignore all messages output by pdftex - SFalmanac is running correctly.  

&nbsp;&nbsp;&nbsp;&nbsp;**DEPRECATION:** Python 2.7 will reach the end of its life on January 1st, 2020.  
&nbsp;&nbsp;&nbsp;&nbsp;Please upgrade your Python as Python 2.7 won't be maintained after that date.  
&nbsp;&nbsp;&nbsp;&nbsp;A future version of pip will drop support for Python 2.7.

### INSTALLATION GUIDELINES on Windows 10:

&nbsp;&nbsp;&nbsp;&nbsp;Install Python 2.7 (do not add python.exe to path) 
&nbsp;&nbsp;&nbsp;&nbsp;Install MiKTeX 2.9 from https://miktex.org/  
&nbsp;&nbsp;&nbsp;&nbsp;Run Command Prompt as Administrator; go to your Python folder and execute, e.g.:

&nbsp;&nbsp;&nbsp;&nbsp;**cd C:\\Python27\\Scripts**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pyephem**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install skyfield**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pandas**  

&nbsp;&nbsp;&nbsp;&nbsp;NOTE: if Python 3 is already installed, you need to be in the Scripts folder - otherwise the Py3 version of pip will execute.
&nbsp;&nbsp;&nbsp;&nbsp;Put the SFalmanac files in any folder, go there and start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**python.exe sfalmanac.py**  

&nbsp;&nbsp;&nbsp;&nbsp;However, if Python 3 is also installed, start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**py -2 sfalmanac.py**  


### INSTALLATION GUIDELINES on Linux:

&nbsp;&nbsp;&nbsp;&nbsp;Install your platform's Python- and LaTeX distribution.  
&nbsp;&nbsp;&nbsp;&nbsp;Remember to choose python 2.7 minimum and install all development header files.  
&nbsp;&nbsp;&nbsp;&nbsp;Run at the command line:

&nbsp;&nbsp;&nbsp;&nbsp;**pip install pyephem**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install skyfield**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pandas**  

&nbsp;&nbsp;&nbsp;&nbsp;Put the SFalmanac files in any directory and start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**python sfalmanac**  
&nbsp;&nbsp;&nbsp;&nbsp;or  
&nbsp;&nbsp;&nbsp;&nbsp;**./sfalmanac**


### INSTALLATION GUIDELINES on MAC:

&nbsp;&nbsp;&nbsp;&nbsp;Every Mac comes with python preinstalled.  
&nbsp;&nbsp;&nbsp;&nbsp;(Please choose the Python 3 version of SFalmanac if Python 3.* is installed.)  
&nbsp;&nbsp;&nbsp;&nbsp;You need to install the PyEphem and Skyfield libraries to use SFalmanac.  
&nbsp;&nbsp;&nbsp;&nbsp;Type the following commands at the commandline (terminal app):

&nbsp;&nbsp;&nbsp;&nbsp;**sudo easy_install pip**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pyephem**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install skyfield**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pandas**  

&nbsp;&nbsp;&nbsp;&nbsp;If this command fails, your Mac asks you if you would like to install the header files.  
&nbsp;&nbsp;&nbsp;&nbsp;Do so - you do not need to install the full IDE - and try again.

&nbsp;&nbsp;&nbsp;&nbsp;Install TeX/LaTeX from http://www.tug.org/mactex/

&nbsp;&nbsp;&nbsp;&nbsp;Now you are almost ready. Put the SFalmanac files in any directory and start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**python sfalmanac**  
&nbsp;&nbsp;&nbsp;&nbsp;or  
&nbsp;&nbsp;&nbsp;&nbsp;**./sfalmanac**
