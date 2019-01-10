# SPR_Create_Dotmatics_ADLP_File
Project for processing SPR Data for upload to Dotmatics via ADLP

**Overview**

Takes SPR binding data and reformats the data into an Excel file for upload to Dotmatics through Broad's ADLP data upload portal.

## Environment Setup (Skip this section if done before)
__Follow the steps below for initial setup. If initial setup was conducted previously, skip to next section__.

_Take Note: The following procedure has been tested for Mac OS. Different commands are needed for Windows._

### Setup python on your computer and download script files

1. Create a github.com account by clicking the following link. This is free. (https://github.com)
    - This is necessary in order to copy all of the files needed to run the SPR to ADLP scripts.
    - Another advantage is that any bugs or changes made can be easily synced to your local hard drive.
2. Download and Install Anaconda with Python version 3.7 for Mac by clicking link. (https://www.anaconda.com/download/#macos)
    - Anaconda is a distribution of software packages that are very useful for data science.
    - With the Anaconda download, python version 3 or greater will be automatically installed. Mac OS comes with version 2.7 but this is an older version that may cause issues.
3. Create a new file folder on your hard drive titled "PythonProjects" using the terminal.
    1. Open Terminal.
        - Hold command + space to bring up spotlight search. Type 'terminal' and press 'return'.
    2. In terminal, create a new folder on your hard drive titled "PythonProjects". 
        - Type or copy/paste command: __mkdir PycharmProjects__
        - Press 'return'
    3. In terminal navigate into "PythonProjects" by typing or copy/paste the command: __cd PythonProjects__
        - Press 'enter'
4. Fork this repo by clicking 'Fork' in the upper right corner of this webpage.
    - Forking means that all of the files necessary to run the SPR to ADLP scripts will be copied to your personal github account.
    - Later we will sync these files to your local hard drive in the PythonProjects folder you created above.
5. Once this repo is forked to your github account, navigate to the top project folder on github and click the green button 'Clone or download'. Next, click the button that looks like a clipboard to copy the link to your clipboard.
5. Navigate back to terminal.
6. Type command: __git clone 'paste contents of clipboard'__
7. Press 'return'
    - All the files needed should be copied to your local hard drive in the PythonProjects folder.
8. Navigate *into* the folder containing all of projects files. 
    - Type or copy/paste command: __cd SPR_Create_Dotmatics_ADLP_File__

### Create new Conda environment and install SPR to ADLP script dependencies.

 1. Navigate to terminal.
 2. Make sure you are in the SPR_Create_Dotmatics_ADLP_File file folder.
    - If your are not sure type command: cd ~
    - Press 'enter'
    - Type or copy/paste command: __cd PythonProjects__
    - Type or copy/paste command: __cd SPR_Create_Dotmatics_ADLP_File__
 3. Create and activate Conda Environment
    - Type or copy/paste command: __conda env create --file SRP_ADLP_env.txt__
    - Type or copy/paste command: __source activate SPR_ADLP_env__
    
## Create SPR setup file for dose response experiment

__Important__: For the data processing script to work, you must use the Create_SPR_setup_file.py script described in this section.

__Important__: For the data processing script to work, you must save the Biacore run as: __yy/mm/dd_PROJECT_CODE_affinity__

1. Navigate to the following folder using *Finder*: 
    - /Users/your_user_name/PythonProjects/SPR_Create_Dotmatics_ADLP_File/Example Files
    - Copy the file __181113_Cmpd_Setup_Example_Tbl.xlsx__ to another location your hard drive. You can rename this file to anything you want.
    - Update the file with the information from your experiment.
    - Note:
        - The Files headers must not be changed.
        - The headers in RED are used by the scripts and must be filled out. All others fields can be left blank (Although this is not a best practice).
            
## Create ADLP upload file from Biacore dose response affinity experiment

1. Create both affinity as well as kinetic analysis of the data in the SPR evaluation software.
2. Export both affinity as well as kinetic analysis.
    - Click on *affinity analysis* under 'Screening'
        - Right click on the sensorgram thumbnails and select 'Export All Graphs And Table'.
            - Save on Biacore hard drive.
      Click on *kinetic analysis* under 'Screening'.
        - Right click on the sensorgram thumbnails and select 'Export All Graphs And Table'
            - Save on Biacore hard drive.
3. Transfer both folders from 2. above to SPR image export folder on flynn. 
    - tdts_users/Informatics and computational research/SPR_Image_import/year_month
4. Navigate back to the Biacore evaluation software.
5. Export the 'Report Point Table'
    - Click on 'Report Point Table' under the Report Point Section.
    - Click File --> Export --> Results To Excel
    - Save this file either on flynn or on your hard drive. The name does not matter as long as it's an .xlsx file.
6. Navigate to the following folder using *Finder*: 
    - /Users/your_user_name/PythonProjects/SPR_Create_Dotmatics_ADLP_File/Example Files
    - Copy the Config.txt file to *__another location__* on your hard drive.
7. Update Config.txt for your experiment.
    - Open the Config.txt and replace all the paths as well as variables with those for your experiment.
    - __Trick:__ 
        - To copy file or folder paths, right click on the file or folder and *hold* the option key. 
        - Next, select Copy "File Name" as Pathname.
8. Run SPR_to_ADLP script
    - Navigate to the terminal
    - Make sure the the correct environment is activated.
        - Type or copy/paste command: __source activate SPR_ADLP_env__
        - Press 'enter'
    - Make sure you are in the folder containing the script.
        - If your are not sure type command: cd ~
        - Press 'enter'
        - Type or copy/paste command: __cd PythonProjects__
        - Type or copy/paste command: __cd SPR_Create_Dotmatics_ADLP_File__
     - Run the script
        - Copy the config file path name to the clipboard. See trick in __bold__ above.
        - Type command: __python SPR_to_ADLP "paste config file path name" 
        - press 'enter'
        - The upload file should be created on your desktop.
     - Manual Curation
        - The CURVE_VALID field needs to be fill in with 1 or 0.
            - 1: The data is *valid* and will be uploaded to Dotmatics.
            - 0: The data is *invalid* and will be excluded when uploading the file to Dotmatics through ADLP.
        - Comments
            - Under each cell there is a pull down menu with a list of comments to select from.
        - Other
            - It may be necessary to manually adjust the KD in the KD_SS field 
            __or__ if there is no binding remove the value in the KD_SS field.
            - It may be necessary to remove the stats
            - As a best practice compounds that are *not saturating* should be reported as >top concentration - 1 dilution. e.g. >25
            - As a best practice compounds that are *not saturating* should have all stats removed.
9. Upload file to ADLP
     
    
 
   
