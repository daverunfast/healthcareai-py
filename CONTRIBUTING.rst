How to set up your dev environment (Windows-specific)
-------------------

Set up git
=============

This is for Windows; see `this`_ for macOS and `this link`_ for linux

.. _this: https://developer.apple.com/xcode/
.. _this link: https://git-scm.com/download/linux

- `Download and install`_ git for Windows:
- Choose "64-bit Git for Windows Setup"
- On the Select Components screen, accept the defaults
- After selecting install location, choose "Use Git from the Windows Command Prompt"
- Checkout using Windows-style
- Choose MinTTy

.. _Download and install: https://git-scm.com/download/

Set up healthcare-ai
====================
- Download Anaconda for Windows (Python 3.5) https://www.continuum.io/downloads
- Open the terminal (i.e., git bash, if using Windows)
- run ``conda install pyodbc``
- run ``pip install https://github.com/HealthCatalystSLC/healthcareai-py/zipball/master``
- Fork this repo (look for the link in the top right corner of the current page)
- At the top of the `repo homepage`_ click the green 'Clone or download' button and copy the https link
- In the terminal type ``git clone [paste_the_link]``
- ``cd`` to healthcareai-py directory

.. _repo homepage: https://github.com/HealthCatalystSLC/healthcareai-py

If you like using virtual environments (not required):

- In terminal, run ``conda env create`` to create the hcconda virtual environment
- To activate your virtual environment, in terminal run ``activate hcconda`` (or ``source activate hcconda`` if using bash)
- You might have to update packages, especially sklearn. The best way to do this is through Settings->Project->Project Interpreter and update scikit-learn

Install the IDE and clone the healthcareai-py repo
=============

1)	Install PyCharm Community Edition

2)	Set path to git.exe via File -> settings -> Version Control -> Git

3)	Clone repo (if you haven't) via PyCharm -> VCS (at top) -> Checkout from version control -> Github
 - Grab .git url from healthcareai-py repo in Github

4)	File -> Open and look for the healthcareai project (if it didn’t come up already)

5) If on Windows, `install both`_ SQL Server Express and SSMS Express
 - Navigate to the `downloads page`_
 - Look for and download ENU\x64\SQLEXPRWT_x64_ENU.exe
 - When installing, be sure to check the box to install SSMS

6) Create tables `(on localhost)`_ within a SAM database to receive predictive output using the code below (use SSMS if on Windows):

.. _install both: http://stackoverflow.com/a/11278818/5636012
.. _downloads page: https://www.microsoft.com/en-us/download/details.aspx?id=29062
.. _(on localhost): https://github.com/HealthCatalystSLC/healthcareai-py/blob/master/localhost_config.md

Note that these will go in the SAM database, if using the Health Catalyst analytics environment

.. code-block:: sql

   CREATE TABLE [SAM].[dbo].[HCPyDeployClassificationBASE] (
          [BindingID] [int] ,
          [BindingNM] [varchar] (255),
          [LastLoadDTS] [datetime2] (7),
          [PatientEncounterID] [decimal] (38, 0),
          [PredictedProbNBR] [decimal] (38, 2),
          [Factor1TXT] [varchar] (255),
          [Factor2TXT] [varchar] (255),
          [Factor3TXT] [varchar] (255))

   CREATE TABLE [SAM].[dbo].[HCPyDeployRegressionBASE] (
          [BindingID] [int],
          [BindingNM] [varchar] (255),
          [LastLoadDTS] [datetime2] (7),
          [PatientEncounterID] [decimal] (38, 0),
          [PredictedValueNBR] [decimal] (38, 2),
          [Factor1TXT] [varchar] (255),
          [Factor2TXT] [varchar] (255),
          [Factor3TXT] [varchar] (255))
       
       
6)	Verify that unit tests pass
 - Right click on tests folder under healthcareai-py/healthcareai
 - Click on Run Nosetest in test

7)	Create test branch and push it to github
 - Note the text ‘Git: master’ in bottom-right of PyCharm
 - Create new test branch via VCS -> Git -> Branches -> New Branch
 - Push branch to github (ie, create origin) via VCS -> Git -> Push (CTRL-SHIFT-K)

Code Housekeeping
=============

1)	Install the following packages via the command line: ``python -m pip install packagename``
 - pylint
 - pyflakes
    
2) Set these up via http://www.mantidproject.org/How_to_run_Pylint#PyCharm_-_JetBrains
 - If your python is installed in ``C:\Pythonxx``, then your parameters will be:
  - Program: ``C:\Python34\Scripts\pylint.exe``
  - Parameters: ``$FilePath$``
  - Working dir: ``C:\Python34\Scripts``
 - If you are using a different Python distribution, you may need to find where Pylint is installed.  For example, the same three parameters from above might be:
  - ``C:\Users\user.name\AppData\Local\Continuum\Anaconda3\Scripts\pylint``
  - Parameters: ``$FilePath$``
  - ``C:\Users\user.name\AppData\Local\Continuum\Anaconda3\Scripts``

 - Instead of using default parameter, use ``$FilePath$``
 - For Anaconda, you may have to use ``C:\Users\user.name\AppData\Local\Continuum\Anaconda3\Scripts\pylint``
 - Check all boxes
    
3) Make sure pylint and pyflakes work
 - Right-click on relevant directory in PyCharm (this will be where you’ve done work)
 - Navigate to external tools
 - Run both pylint and pyflakes
 - Verify that there aren’t any issues with your code; please do this before sending pull requests

4) Set maximum line width to 79 via Settings -> Editor -> Code Style -> Right margin

5) Set tabs as spaces via Edit -> Convert Indents -> To Spaces

6) Click Code -> Inspect code -> Whole project -> Look for section on Package requirements
 - Under the lines related to sklearn, click ‘Ignore Requirement’

Git config
=============
Set up your email and username for git (otherwise no attribution in github)

1) Open the shell (ie, git bash, if on Windows)

2) Set up your email and user name for proper attribution
 - git config user.name "Billy Everyteen"
 -	git config --global user.email "your_email@example.com"

3) Configure line endings for windows: ``git config core.autocrlf true``

4) Make git case sensitive for file names: ``git config core.ignorecase false``

5) Improve merge conflict resolution via ``git config --global merge.conflictstyle diff3``

6) If you use a personal email for github, and would rather have notifications go to your Health Cataylst email
 - See `here`_ -> Notification email -> Custom routing

7) Set up SSH (if desired) so you can push to topic branch without password
 - `Step1`_
 - `Step2`_
 - `Step3`_
 
 .. _Step1: https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/
 .. _Step2: https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/
 .. _Step3: https://help.github.com/enterprise/11.10.340/user/articles/changing-a-remote-s-url/
 .. _here: https://github.com/settings/notifications
 
Create a topic branch that you can work in
==========================================
1) Open the terminal (whether in Git Bash, in Spyder, etc)

2) Type ``git checkout -b nameofbranch``
   - This creates the your local branch for work
   - Note this branch should have your name in it
   
3) Type ``git push origin nameofbranch``
   - This pushes the branch to github (and now it's backed-up)

Getting started with contributions
==================================
When your dev environment is set up, see `click here`_ for the contribution workflow.

.. _click here: README.md#contributing
