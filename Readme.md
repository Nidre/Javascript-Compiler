# JavaScript Compiler
This project uses **Google Closure**, **WinSCP**, **jpegtran**, **pngquant**, **csso** and **html-minifier** to optimize and upload your project depending on the configuration or command line arguments provided.

# Disclaimer
- This project uses several other projects for some of its features. They are not packaged within this repository and should be downloaded from their own websites, see description below for a step by step explanation of this process.
- I've created this tool for my own needs, some features may or may not make sense, feel free to suggest changes or send a pull-request!
- If you think there is something that I've forgot to give credit or a mistake, feel free to contact me.
- **Contributions are welcome**

# Instructions

- **Download** and **Install** [Python 2.7](https://www.python.org/downloads/)
- **Download** [pngquant](https://pngquant.org/). Needed for **.png** optimizations.
- **Download** [jpegtran](http://jpegclub.org/jpegtran/). Needed for **.jpg** optimizations.
- **Download** [Google Closure](https://developers.google.com/closure/compiler/). Needed for **.js** optimizations.
- **Download** and **Install** [html-minifier](https://github.com/kangax/html-minifier). Needed for **.html** and **.php** optimizations.
- **Download** and **Install** [csso](https://github.com/css/csso). Needed for **.css** optimizations.
- **Copy** **jpegtran.exe**, **pngquant.exe** and **closure-compiler-\<version-number\>.jar** to root folder of python scripts.
- **Rename** **closure-compiler-\<version-number\>.jar** to **compiler.jar**
- **Download** [WinSCP Portable](https://winscp.net/eng/download.php)
- **Copy** **WinSCP.exe** to root folder of python scripts.
- **Configure** the config.ini file. (See below and sample config.ini in the project.)
- **Create** and **configure** the auth.ini file. (See below)
- **Run** **package.py**

See **sample** directory for a working example.

# Configuration Files
## config.ini & command-line

**Command-line Notes**
- Command line options are preferred over config.ini file.
- Add 0 or 1 to toggle options. -o 1 to enable optimizations or -o 0 disable optimizations for example.

**Project Settings**
- **[Project]** = Title for project settings. Required.
  - **itemstocopy, [-i,--itemsToCopy]** = Which Files/Folders should be optimized. Comma separated file name list. Auto rename syntax, **\<file-name\>;\<new-file-name\>**
  - **appname, [-an,--appName]** = Name of the app, used when injecting app name to files with **appnametag**.
  - **appkey, [-ak,--appKey]** = Unique name of the app, works as an id and should not have spaces.
  - **appversiontag, [-avt,--appVersionTag]** = Used to change **appversiontag** for **version** injection. Default = "<app-version>"
  - **appnametag, [-ant,--appNameTag]** = Used to change **appnametag** for **appname* injection. Default = "<app-name>"
  - **projectroot, [-pr,--projectRoot]** = Root path of your JavaScript project.
  - **builddir, [-bd,--buildDir]** = Where should the JavaScript Compiler export the optimized files. Relative to projectroot.
  - **debugitems, [-di,--debugItems]** = Only included if the debug switch is enabled.
  - **debuginjectdata, [-dd,--debugInjectData]** = Replaces the given tag in given file with the given content if debug mode is enabled. Syntax: **\<file-name\>;"\<tag\>";"\<new string\>"**
  - **injectdata, [-id,--injectData]** = Replaces the given tag in given file with the given content. Syntax: **\<file-name\>;"\<tag\>";"\<new string\>"**
  - **version, [-ver,--version]** = Version number/text to be injected to the project. Automatically generated from current date/time with %Y%m%d%H%M%S%f format each time if not provided.
  - **bumpVersion, [-bver,--bumpVersion]** = Should we bump the version number or not.

**Compiler Settings**
- **[Compiler]** = Title for compiler settings. Required.
  - **verbose, [-v,--verbose]** = Should we log more details while running.
  - **debug, [-d,--debug]** = Is debug mode enabled as described above.
  - **zippath, [-zp,--zipPath]** = Where to export the zip file containing the project in the end.
  - **optimize, [-o,--optimize]** = Should we optimize .js, .jpg, .png, .html and .css files. Default = True
  - **optimizehtml, [-oh,--optimizeHtml]** = Should we optimize .html files. Needs optimize to be enabled. Default = True
  - **optimizecss, [-oc,--optimizeCss]** = Should we optimize .css files. Needs optimize to be enabled. Default = True
  - **optimizejs, [-ojs,--optimizeJs]** = Should we optimize .js files. Needs optimize to be enabled. Default = True
  - **optimizejpg, [-oj,--optimizeJpg]** = Should we optimize .jpg files. Needs optimize to be enabled. Default = True
  - **optimizepng, [-op,--optimizePng]** = Should we optimize .png files. Needs optimize to be enabled. Default = True

**Uploader Settings**
- **[Uploader]** = Title for uploader settings. Required.
  - **updatingassets, [-ua,--updatingAssets]** = Assets to be copied to the server while the upload is still going on. An index file saying "Updating..." for example. Files provided here can be renamed automatically with the following Syntax, **\<file-name\>:\<new-file-name\>**.
  - **releaseAssets, [-ra,--releaseAssets]** = Assets to be uploaded once all the assets have been uploaded. Files provided here can be renamed automatically with the following Syntax, **\<file-name\>:\<new-file-name\>**.
  - **targetpath, [-tp,--targetPath]** = Where to upload the project when the compilation is completed. This should be a directory name not the full path. Directory will be created if doesn't exists. Default = ""
  - **uploadzip, [-uz,--uploadZip]** = Should we upload the created zip file.
  - **uploadsource, [-us,--uploadSource]** = Should we uploaded the compiled project.
  - **timeout, [-t,--timeOut]** = Time out for WinSCP. Default = 20

## auth.ini
**FTP Settings**
- **[FTP]** = Title for ftp settings. Required.
  - **username, [.ini file only]** = Username for FTP connection.
  - **password, [.ini file only]** = Password for FTP connection.
  - **domain , [.ini file only]** = Domain for FTP connection.
