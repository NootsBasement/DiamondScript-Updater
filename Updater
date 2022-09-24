import os
try:
    import requests
except ModuleNotFoundError:
    os.system("pip install requests")
finally:
    import requests

def GetPIDNumber():
    pid = os.getpid()
    print("PID Number of this script:", pid)
    return pid
GetPIDNumber()

def FindHomeDir():
    try:
        home_directory = os.path.expanduser('~')
        start = home_directory
        print("Home Directory Found! Home Directory: " + start)
        return start
    except:
        print("Home Directory can't be found!")
        exit()
HomeUserDirectory = FindHomeDir()

def EstablishDownloadsFolder():
    try:
        DownloadsPath = HomeUserDirectory + "\\Downloads"
        return DownloadsPath
    except:
        print("Error when trying to establish Downloads Folder location?")
DownloadsFolderPath = EstablishDownloadsFolder()

DiamondScriptFolderPath = DownloadsFolderPath + "\\MainDiamondScript"
FullDiamondScriptFolderPath = DiamondScriptFolderPath + "\\DiamondScript.py"
DiamondPIDTxtFile = DiamondScriptFolderPath + "\\DiamondScriptPID.txt"

def UpdateAndRepair():
    try:
        with open(DiamondPIDTxtFile, mode='r') as PIDtxtfile:
            PIDNumber = PIDtxtfile.readlines()
            print(PIDNumber)
        KillPIDCommand = "taskkill /PID " + PIDNumber + " /F"
        os.system(KillPIDCommand)
        print("Killed DiamondScript.py process to check for updates!")
    except:
        try:
            with open(DiamondPIDTxtFile, mode="w+") as PIDtxtfile:
                PIDNumber = PIDtxtfile.read()
            print("PID Text file has been altered or deleted, creating now.")
        except FileNotFoundError:
            print("PID cant be fetched yet!")
            pass
        pass

    def Convert(string):
        list1=[]
        list1[:0]=string
        return list1

    githubvers = requests.get("https://raw.githubusercontent.com/NootsBasement/DiamondScript/main/diamondPublicBuild.py").text
    ConvGitVersToList = Convert(githubvers)

    badchar = '\r'

    EmptyList = []
    for letter in ConvGitVersToList:
        if letter != badchar:
            EmptyList.append(letter)

    FixedGitHubDiamondScript = ''.join(EmptyList)

    try:
        with open(FullDiamondScriptFolderPath, mode='r') as LocalDiamondBuild:
            LocalDiamondBuild.seek(0)
            LocalFileDiamondScript = LocalDiamondBuild.read()
    except FileNotFoundError:
        print("File(s) couldn't be found, Validating Script/Paths...")

        MedieaDirectory = "\MediaStorage"
        SoftwareDirectory = "\SoftwareShortcuts"
        NewPath = DiamondScriptFolderPath

        try:
            os.mkdir(NewPath)
            print("Created Main Path")
        except:
            print("Directory Exists")
            pass

        try:
            MediaPath = NewPath + MedieaDirectory
            os.mkdir(MediaPath)
            print("Created Media Path")

        except:
            print("Directory Exists")
            pass

        try:
            SoftwarePath = NewPath + SoftwareDirectory
            os.mkdir(SoftwarePath)
            print("Created Software Path")
        except:
            print("Directory Exists")
            pass

        try:
            with open(FullDiamondScriptFolderPath, mode='w+') as LocalDiamondBuild:
                LocalDiamondBuild.write(FixedGitHubDiamondScript)
        except:
            print("error")
            pass

    finally:
        with open(FullDiamondScriptFolderPath, mode='r') as LocalDiamondBuild:
            LocalFileDiamondScript = LocalDiamondBuild.read()

    if LocalFileDiamondScript == FixedGitHubDiamondScript:
        UpdateStatusTxtFile = DiamondScriptFolderPath + "\\UpdateStatus.txt"
        print("Local DiamondScript.py is already updated, paths have been restablished if needed.")
        print("Opening DiamondScript.py")
        with open(UpdateStatusTxtFile, mode="w+") as PIDtxtfile:
            PIDtxtfile.write("Updated")
        os.startfile(FullDiamondScriptFolderPath)
        return True

    if LocalFileDiamondScript != FixedGitHubDiamondScript:
        UpdateStatusTxtFile = DiamondScriptFolderPath + "\\UpdateStatus.txt"
        print("Local DiamondScript.py and or paths have been fixed/updated.")
        with open(FullDiamondScriptFolderPath, mode='w+') as LocalDiamondBuild:
            LocalDiamondBuild.write(FixedGitHubDiamondScript)
        with open(UpdateStatusTxtFile, mode="w+") as PIDtxtfile:
            PIDtxtfile.write("Updated")
        os.startfile(FullDiamondScriptFolderPath)
        return False
UpdateAndRepair()
