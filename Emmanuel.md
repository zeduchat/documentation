Step 1: Download and Install VS Code
VS Code is the application we will use to open and work on the project.
Download VS Code from the official website:
https://code.visualstudio.com/download

Step 2   Install Git 
Check if git is installed , in your terminal on VS CODE
In the terminal, type  git --version  
and press enter
If Git is installed correctly, you'll see something like: "git version 2.50.1.windows.1

If you see something like: git : The term 'git' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again. 
That error means Git is not installed or Windows cannot find the Git installation. 
What you need to do
1. Download Git and install it
Go to:
Click on the site and install git: https://git-scm.com/download/win

2. Verify Git was installed
Enter this command to yourVS Code terminal: git --version


Step 3: You will use VS Code terminal to download and run the project

Open VS Code 
If you dont have VS Code, download VS Code here: https://code.visualstudio.com/download
Open Vs code after installing


Step 4: Create or Go to Your Projects Folder
This step is simply taking you to a place on your computer where your project files will be stored.

In VS Code
Open Terminal → New Terminal (CLick on view at the top left and click on terminal the last option) and run all three commands at once: 
cd $HOME
mkdir Documents -ErrorAction SilentlyContinue
cd Documents

Check that it worked
Paste this command to your terminal: pwd
If you see this below it means it has worked
Path                   
----
C:\Users\USER\Documents
PS C:\Users\USER\Documents>

STEP 5 Download the Zedu Project 
This step downloads a copy of the Zedu frontend code from GitHub onto your computer 
Don't copy the link and paste it in your browser, do this instead, run this command in your terminal:  
git clone https://github.com/zeduchat/zedu-fe.git
means:
git → Use the Git program.
clone → Make a local copy of a remote repository.
https://github.com/zeduchat/zedu-fe.git → The location of the project on GitHub.
Before you run it
You must have Git installed and working.
Go back to step 2 to check if its installed
If git isn't installed, the clone will fail

After running the command (paste git clone https://github.com/zeduchat/zedu-fe.git  in your VS code terminal), Expected result will be messages similar to:
Cloning into 'zedu-fe'...
Receiving objects...
Resolving deltas…

When it finishes, a new folder named:
zedu-fe  will appear inside your Documents folder

#But if you see this after a period of time
Cloning into 'zedu-fe'...

it means the cloning process has started.
A few possibilities:
It's still downloading — wait 30–60 seconds and see if more messages appear.
The repository is private and Git is waiting for authentication.
The operation completed silently and returned to the prompt.


Check whether the folder was created
Go to file explorer on your task bar and click your documents and check for zedu-fe

You should see some files inside it , if you do it means the clone worked 

OR
In the VS Code terminal, run:
dir
Look for a folder such as:
zedu-fe
If the folder exists
Run:
cd zedu-fe
Then run:
dir
If you see files like package.json, src, public, etc., the clone worked.

If the folder does NOT exist
Run the clone command again and copy the entire output:
git clone https://github.com/zeduchat/zedu-fe.git

Step 6 Enter the Project Folder
If the cloning worked, 
The next step is accessing the Zedu frontend project
Run:  cd zedu-fe   in the terminal
You should see something like this PS C:\Users\USER\Documents\zedu-fe>
If you do, you’re inside Zedu frontend project
Lets go to the next step 

Step 7 Open the Project in VS Code
This step you are trying to access the files in the zedu_fe folder with VS CODE
 If you are using VS CODE already, just continue the process ,  the two ways to go about this
Paste ” code .” into your terminal ( dont copy the apostrophe, just with the code and full stop sign )
It should open a new VS Code with Zedu project files on the left side of VS Code.

OR
Go to file explorer, go to documents and open  zedu-fe folder through vs code

Step 8: Open the VS Code Terminal
A terminal will open at the bottom of VS Code.
Make sure the terminal is inside the zedu-fe folder.
The location should end with:
Zedu-fe

Step 9 Check the Project Requirements
The developers want you to check which versions of software the project needs 
Specifically:
Node.js → Runs JavaScript outside the browser.
pnpm → A package manager used to install project dependencies.
The project requires:
Node.js 22+ (you can download Node.js 22 or any higher version )
pnpm 10.27.0
Check if Node.js is installed
In VS Code Terminal, run:
node -v
Example output:
v22.18.0
If you get:
node : The term 'node' is not recognized
then Node.js is not installed.

Check if pnpm is installed
Run:
pnpm -v
Example output:
10.27.0
If you get:
pnpm : The term 'pnpm' is not recognized
then pnpm is not installed.
We will need to install node.js and pnpm, before we install that lets instal NVM first 

Step 10: Install NVM (Windows)
What is NVM?
NVM stands for Node Version Manager.
It lets you install and switch between different versions of Node.js.
Install NVM for Windows
Go to:
NVM for Windows Releases
On the Releases page
Look for the latest release and download:
nvm-setup.exe
Install it
Important
After installation:
Close VS Code..
Open a new VS Code window .To open the zedu-fe file with VS code, Run: code . on your terminal
This ensures Windows recognizes the new nvm command.

Step 11: Install Node.js 24
If Node.js is missing, download it from:
Node.js Official Website
Install the latest 22.x LTS version or Newer
After installing follow the instructions on the black interface, follow the instructions and press any key 

Step 12: Set Node.js 24 as the Default or any version you downloaded
After installing Node.js 24, run:
nvm use 24
NOTE Your version of node js is checked by the number that comes after the js in our example its 24, if you downloaded  Node.js 22, your version is 22 

Step 13: Verify Node.js
Run:
node -v
You should see something similar to:
v24.x.x
The important part is that it starts with:
V24 (version of node js)


Step 14: Verify npm
This step is checking whether npm was installed correctly.
What is npm?
npm stands for Node Package Manager.
It is installed automatically when you install Node.js.
You'll use npm to install tools and project dependencies

Node.js comes with npm.
Run:
npm -v
You should see an npm version number. 11.6.0   OR   10.8.2

If you get PowerShell error 
If you see:
npm.ps1 cannot be loaded because running scripts is disabled on this system
then npm is installed, but PowerShell is blocking it.
Fix (Recommended)
Open PowerShell as Administrator:
Press Windows Key
Type PowerShell
Right-click Windows PowerShell
Click Run as Administrator
Then run:
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
When asked:
Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No ...
Type:
Y
and press Enter.
.

Step 15: Install pnpm 10.27.0
The project requires:
pnpm 10.27.0
Make sure Node.js 22 is currently active before installing pnpm.
Run:
npm install -g pnpm@10.27.0

Step 16: Verify pnpm
Run:
pnpm --version
The expected output is:
10.27.0

Step 17: Check Everything Before Continuing
At this point, you should have:
Node.js
Run:
node -v
Expected:
V24.x.x or any version 

npm
Run:
npm -v
You should see an npm version.

pnpm
Run:
pnpm --version

Expected:
10.27.0

Git
Run:
git --version

Step 18: Make Sure You Are Inside the Project
This step is simply making sure your terminal is inside the Zedu project folder before you install its dependencies. 
Before installing the project dependencies, make sure you are inside:
Zedu-fe
Check your current location
In your VS Code terminal, run:
pwd
You should see something similar to:
Path
----
C:\Users\USER\Documents\zedu-fe
That's exactly what you want.

If you are not inside the project folder, run:

cd $HOME\Documents\zedu-fe
Then check your location:
Pwd

Step 19: Install the Project Dependencies
Now install everything the project needs.
Run:
pnpm install

This will download all the project's dependencies.
Wait for the process to finish.
Do not close the terminal while the installation is running.
Depending on your internet connection, this may take some time.
When it finishes successfully, continue to the next step.

Step 20: Start the Development Server
This step is where you actually start the Zedu website on your own computer so you can open it in your browser and test/edit it.
Since you're already inside:
PS C:\Users\USER\Documents\zedu-fe>
you're in the correct folder. ✅
1. Run the command
In your VS Code terminal, enter:
pnpm dev
Then press Enter.
2. What will happen?
pnpm will start the Zedu development server.
You'll probably see messages similar to:
> zedu-fe@... dev
> ...
Local: http://localhost:3000/
The important part is the Local URL.
For example:
http://localhost:3000
Or:
http://localhost:3001

Step 21: Open the website
Once you see the URL, Ctrl + Click the URL in the VS Code terminal.
Or copy it and paste it into Chrome:
http://localhost:3000
You should then see the Zedu website running locally.
What does localhost mean?
localhost means your own computer.
So:
http://localhost:3000
doesn't mean the website is publicly online.
It means:
"Open the version of the Zedu website currently running on my computer."
This is useful because you can make changes to the code and see those changes on your local website.
⚠️ Important: Don't close the terminal
Once you run:
pnpm dev
leave the terminal running.
The development server is running inside that terminal. If you close it or press Ctrl + C, the local website will stop.
You can open another terminal in VS Code if you need to run other commands.
