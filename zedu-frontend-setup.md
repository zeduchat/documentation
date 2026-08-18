Complete Guide: Setting Up the Zedu Frontend For Windows, macOS, and Linux on Local
This guide explains how to download, install, set up, and run the Zedu frontend project on Windows, macOS, and Linux.

Step 1: Download and Install VS Code
VS Code is the application we will use to open and work on the project.
Download VS Code from the official website:
https://code.visualstudio.com/download
VS Code provides installers for Windows, macOS, and Linux.

Windows
Open the VS Code website.
Click Download for Windows.
Wait for the download to finish.
Open the downloaded .exe file.
Follow the installation instructions.
Accept the license agreement.
Continue clicking Next.
Complete the installation.
Open VS Code.

macOS
Open the VS Code website.
Click Download for macOS.
Open the downloaded .dmg file.
Drag Visual Studio Code into the Applications folder.
Open the Applications folder.
Open Visual Studio Code.

Linux
Open the VS Code website.
Choose the Linux version that matches your distribution.
For Ubuntu/Debian, download the .deb package.
For Fedora/RHEL-based systems, download the .rpm package.
Install the downloaded package.
Open VS Code.

Step 2: Install Git
Git is required to download the Zedu project from GitHub.
Windows
Download and install Git from:
https://git-scm.com/download/win
After installation, open Command Prompt, PowerShell, or the VS Code terminal.
Run:
git --version

You should see something similar to:
git version 2.x.x

macOS
Open Terminal.
Run:
git --version

If Git is not installed, macOS may ask you to install the Command Line Developer Tools.
Follow the instructions on the screen and allow the installation to finish.
Then run again:
git --version

Linux
Open Terminal.
For Ubuntu/Debian:
sudo apt update
sudo apt install git

After installation, verify Git:
git --version


Step 3: Open a Terminal
You will use the terminal to download and run the project.

Windows
You can use any of these:
Command Prompt
PowerShell
Git Bash
VS Code Terminal
For beginners, PowerShell or the VS Code Terminal is recommended.
To open PowerShell:
Click the Windows Start button.
Search for PowerShell.
Open Windows PowerShell.

macOS
Open:
Applications → Utilities → Terminal
Or search for Terminal using Spotlight.
Linux
Open your Terminal application.


Step 4: Create or Go to Your Projects Folder
Windows
Open PowerShell and run:
cd $HOME
mkdir Documents -ErrorAction SilentlyContinue
cd Documents

You should now be inside your Documents folder.
You can check your current location by typing this:
pwd

macOS
Open Terminal and run:
cd ~/Documents

Check your current location:
pwd

Linux
Open Terminal and run:
cd ~/Documents

If the Documents folder does not exist, create it first:
mkdir -p ~/Documents
cd ~/Documents

Check your current location:
pwd



Step 5: Download the Zedu Project
The Zedu frontend project is available here:
https://github.com/zeduapp/telex_fe
Run this command:
git clone https://github.com/zeduapp/telex_fe.git

This command works on:
Windows
macOS
Linux
Wait for Git to finish downloading the project.

Step 6: Enter the Project Folder
After the download is complete, run:
cd telex_fe

You are now inside the Zedu frontend project.
Check your current location.
Windows
pwd

macOS/Linux
pwd

The path should end with:
telex_fe


Step 7: Open the Project in VS Code
While you are inside the telex_fe folder, run:
Type “code .”

This should open the project in VS Code.
You should see the Zedu project files on the left side of VS Code.

Step 8: Open the VS Code Terminal

Once the project is open in VS Code:
Click Terminal at the top of VS Code.
Click New Terminal.
A terminal will open at the bottom of VS Code.
Make sure the terminal is inside the telex_fe folder.
The location should end with:
telex_fe

Step 9: Check the Project Requirements

The project requires specific versions of Node.js and pnpm.
Run:
cat package.json | grep '"packageManager"\|"engines"'

Windows PowerShell
If the command above does not work in PowerShell, use:
Select-String -Path package.json -Pattern '"packageManager"','"engines"'

Look for the required versions.
For this project, make sure you have:
Node.js 22+
pnpm 10.27.0

Step 10: Install NVM

NVM allows you to install and switch between different Node.js versions.
The installation is different for Windows and macOS/Linux.

Windows: Install NVM for Windows
Do not use the macOS/Linux NVM installation command on Windows.
Windows uses a separate tool called NVM for Windows.
Download NVM for Windows from:
https://github.com/coreybutler/nvm-windows/releases
Installation
Open the link above.
Find the latest release.
Download the Windows installer.
Extract the downloaded file if necessary.
Run the NVM installer.
Follow the installation instructions.
Complete the installation.
After installation, close your PowerShell or Command Prompt.
Open a new PowerShell window.
Check NVM:
nvm version

If NVM is installed correctly, you should see a version number.
macOS/Linux: Install NVM
For macOS and Linux, use the original NVM project.
Open your terminal and run:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

Wait for the installation to finish.
Then close your terminal.
Open a new terminal.
If NVM is still not recognized, reload your shell.
For Bash:
source ~/.bashrc

For Zsh:
source ~/.zshrc

Then check NVM:
nvm --version

You should see an NVM version number.

Step 11: Install Node.js 22
Now install Node.js 22.
The command is the same for Windows, macOS, and Linux.
Windows
Open PowerShell as Administrator.
Run:
nvm install 22

Then:
nvm use 22

macOS/Linux
Run:
nvm install 22

Then:
nvm use 22


Step 12: Set Node.js 22 as the Default

This prevents you from having to manually select Node.js 22 every time.
macOS/Linux
Run:
nvm alias default 22

Windows
NVM for Windows works slightly differently.
After installing Node.js 22, run:
nvm use 22

Then verify that Node.js 22 is active.
If you install multiple Node.js versions later, run:
nvm use 22

Step 13: Verify Node.js
Run:
node -v

You should see something similar to:
v22.x.x

The important part is that it starts with:
v22

If you see a different major version, run:
Windows
nvm use 22

macOS/Linux
nvm use 22

Then check again:
node -v


Step 14: Verify npm

Node.js comes with npm.
Run:
npm -v

You should see an npm version number.

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

If you see:
10.27.0

Step 17: Check Everything Before Continuing
At this point, you should have:
Node.js
Run:
node -v

Expected:
v22.x.x

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
Before installing the project dependencies, make sure you are inside:
telex_fe

If you are not inside the project folder, run:
cd ~/Documents/telex_fe

Windows
If you created the project inside Documents, run:
cd $HOME\Documents\telex_fe

Then check your location:
pwd

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
Run:
pnpm dev

The project will start running locally.
Wait for the terminal to display a URL.
It may look like:
http://localhost:3000

The port may be different depending on the project's configuration.
For example, it could also be:
http://localhost:3001

Step 21: Open the Project in Your Browser
Copy the localhost URL shown in the terminal.
For example:
http://localhost:3000

Open Chrome, Firefox, Edge, Safari, or another browser.
Paste the URL into the address bar.
Press Enter.
The Zedu frontend should now open.


