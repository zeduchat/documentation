Complete Guide: Setting Up the Zedu Frontend on Windows
This guide explains how to set up and run the Zedu frontend locally on a Windows computer.
You will need:

Windows
Git
Visual Studio Code
A GitHub account with access to the Zedu repository
NVM for Windows
Node.js 22+
pnpm 10.27.0


Install Visual Studio Code
Visual Studio Code (VS Code) is the application used to open and work on the project.

Download VS Code from the official website:

https://code.visualstudio.com/download
Installation
Open the VS Code website.
Click Download for Windows.
Wait for the download to finish.
Open the downloaded .exe file.
Follow the installation instructions.
Accept the license agreement.
Continue clicking Next.
Complete the installation.
Open VS Code.


2. Install Git
Git is required to download the Zedu project from GitHub.

Download Git for Windows:

https://git-scm.com/download/win

After installation, open PowerShell, Command Prompt, or Git Bash and run:

git --version

You should see a Git version, for example:

git version 2.55.0.windows.4


3. Open PowerShell
You can use PowerShell, Command Prompt, Git Bash, or the VS Code terminal during setup.

For this guide, use PowerShell.

To open PowerShell:

Click the Windows Start button.
Search for PowerShell.
Open Windows PowerShell.


4. Create the Zedu Projects Folder
Create a folder on your Desktop where the Zedu project will be stored.

In PowerShell, run:

cd Desktop

Then:

mkdir Zedu

Then:

cd Zedu

Your prompt should now look similar to:

PS C:\Users\YourName\Desktop\Zedu>
If PowerShell shows Path[1]:
If PowerShell displays something like:

Path[1]:

press:

Ctrl + C

Then return to the normal PowerShell prompt and run:

cd Desktop

mkdir Zedu

cd Zedu


5. Clone the Zedu Frontend Repository
The Zedu frontend repository is hosted under the zeduchat GitHub organization.

Repository:

https://github.com/zeduchat/zedu-fe

From the Zedu folder, run:

git clone https://github.com/zeduchat/zedu-fe.git

Wait for Git to finish downloading the project.

Important: Your GitHub account must have access to the repository. If GitHub reports that the repository cannot be found or you do not have permission, ask the person managing the Zedu repositories to grant your GitHub account access.

After cloning, enter the project folder:

cd zedu-fe

Then check the project files:

dir

You should see the project's files and folders.

Your PowerShell prompt should look similar to:

PS C:\Users\YourName\Desktop\Zedu\zedu-fe>

Note: If your prompt already ends in zedu-fe>, you are already inside the project folder. Do not run cd zedu-fe again.


6. Open the Project in VS Code
Open VS Code.

If zedu-fe appears under Recent, click it.

If it does not:

Click File at the top-left.
Click Open Folder...
Go to:

C:\Users\YourName\Desktop\Zedu\zedu-fe

Select the zedu-fe folder.
Click Select Folder.

You should now see the Zedu project files in the Explorer panel on the left.

You can also open the project from PowerShell with:

code .


7. Open the VS Code Terminal
Once the project is open in VS Code:

Click Terminal at the top of VS Code.
Click New Terminal.
A terminal should open at the bottom of VS Code.
Make sure the terminal location ends with:

zedu-fe>

For example:

PS C:\Users\YourName\Desktop\Zedu\zedu-fe>
If the VS Code terminal fails with a ConPTY error
You may see an error similar to:

The terminal process failed to launch:

A native exception occurred during launch (Cannot launch conpty).

This is a VS Code/Windows terminal issue and is not caused by the Zedu project.

If the VS Code terminal does not launch, you can continue the setup using normal Windows PowerShell. You do not need the VS Code terminal to install NVM, Node.js, pnpm, or the project dependencies.

You can return to VS Code later for editing the project.


8. Install NVM for Windows
NVM (Node Version Manager) allows you to install and switch between Node.js versions.

Download NVM for Windows from:

https://github.com/coreybutler/nvm-windows/releases
Installation
Open the NVM for Windows releases page.
Find the latest release.
Open the Assets section.
Download the Windows installer, usually named something like:

nvm-setup.exe

Open the downloaded installer.
Follow the installation instructions.
Use the default installation options unless your environment requires otherwise.
Complete the installation.

After installation, close your existing PowerShell windows and open a new PowerShell window.

Verify NVM:

nvm version

You should see an NVM version number, such as:

1.2.2

If NVM is still not recognized immediately after installation, close all PowerShell/Command Prompt windows, open a new one, and try again.


9. Install Node.js 22
The Zedu frontend requires Node.js 22+.

In PowerShell, run:

nvm install 22

Wait for the installation to finish.

Then activate Node.js 22:

nvm use 22

You should see a message indicating that Node.js 22 is now active.


10. Verify Node.js
Run:

node -v

You should see a version beginning with v22, for example:

v22.23.2

If you see a different major version, run:

nvm use 22

Then check again:

node -v


11. Verify npm
npm is installed together with Node.js.

First try:

npm -v
If PowerShell blocks npm.ps1
You may see an error such as:

npm.ps1 cannot be loaded because running scripts is disabled on this system.

If this happens, use:

npm.cmd -v

This bypasses the PowerShell script restriction without requiring you to change the execution policy.

You should see an npm version number.


12. Install pnpm 10.27.0
The Zedu frontend requires:

pnpm 10.27.0

Make sure Node.js 22 is active before installing pnpm.

Run:

npm.cmd install -g pnpm@10.27.0

Do not upgrade pnpm to a newer major version unless the project requirements are changed.


13. Verify pnpm
First try:

pnpm --version

If PowerShell blocks pnpm.ps1, use:

pnpm.cmd --version

The expected version is:

10.27.0


14. Verify Git
Run:

git --version

You should see your installed Git version.

At this point, you should have:

Tool
Required version
Node.js
22+
pnpm
10.27.0
Git
Any current version



15. Make Sure You Are Inside the Project
Before installing dependencies, make sure you are inside:

C:\Users\YourName\Desktop\Zedu\zedu-fe

If you are not, run:

cd C:\Users\YourName\Desktop\Zedu\zedu-fe

Then check your location:

pwd

You should see the zedu-fe path.


16. Install Project Dependencies
With Node.js 22 active and the terminal inside the zedu-fe folder, run:

pnpm.cmd install

This downloads the dependencies required by the project.

The installation may take some time depending on your internet connection.
Slow download warnings
You may see warnings such as:

WARN Tarball download average speed ... is below 50 KiB/s

These warnings usually indicate slow network downloads. They do not necessarily mean the installation failed.

Wait for the process to finish.

A successful installation should end with something similar to:

Done in ... using pnpm v10.27.0
Build script warnings
You may also see a warning about ignored build scripts and a message suggesting:

pnpm approve-builds

Do not automatically approve or change build scripts unless the project maintainers instruct you to do so. If the application later reports a problem related to one of these dependencies, address it based on the project's requirements.


17. Start the Zedu Development Server
Once pnpm.cmd install has completed successfully, start the development server:

pnpm.cmd dev

Next.js should start the local development server.

You should eventually see something similar to:

▲ Next.js 16.2.11 (Turbopack)

- Local: http://localhost:3000

- Network: http://192.168.x.x:3000

✓ Ready

The port may be different depending on the project's configuration.


18. Open Zedu in Your Browser
Once the terminal displays the local URL, open it in your browser.

For example:

http://localhost:3000

Open Chrome, Edge, Firefox, or another browser and enter the URL.

The Zedu frontend should now open locally.


Common Development Messages
While running the development server, you may see messages that look like warnings but do not necessarily prevent the application from running.
Slow filesystem warning
Example:

Slow filesystem detected.

This indicates that Next.js detected slower-than-usual filesystem performance.

If the application works, you can continue developing.
metadataBase warning
Example:

metadataBase property in metadata export is not set

This relates to metadata and social Open Graph/Twitter image URLs. It does not necessarily prevent the application from running.
Invalid DOM property warning
Example:

Invalid DOM property `flood-opacity`. Did you mean `floodOpacity`?

This indicates a React/SVG property naming issue in the project code.

It can be fixed separately if it is part of your assigned task.
Image dimension warning
Example:

Image ... has either width or height modified, but not the other.

This is a Next.js image warning about maintaining image aspect ratio.
Unexpected token '<'
If you see:

Uncaught SyntaxError: Unexpected token '<'

check whether the application actually loads in the browser. If the page is broken or blank, report the error and include the browser console output so it can be investigated.


Stopping and Restarting the Development Server
Keep the PowerShell window open while the development server is running.

To stop the server:

Ctrl + C

To start it again, return to the zedu-fe folder and run:

pnpm.cmd dev


Setup Complete
At this point, the Zedu frontend should be running locally.

Your development environment should have:

Git installed
Zedu zedu-fe repository cloned
Node.js 22+ installed through NVM
pnpm 10.27.0 installed
Project dependencies installed
Zedu development server running
Zedu accessible through http://localhost:3000

You can now proceed with your assigned frontend tasks.

