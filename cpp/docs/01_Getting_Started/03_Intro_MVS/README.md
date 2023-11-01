## Introduction
Welcome to the C++ bootcamp module on downloading, installing, and running Microsoft Visual Studio! In this module, we will guide you through the process of setting up one of the most popular integrated development environments (IDEs) for C++ programming. Microsoft Visual Studio provides a robust set of tools and features that can greatly enhance your coding experience and productivity.

So, let's get started on this exciting journey of learning C++ and harnessing the power of Microsoft Visual Studio to develop robust and efficient applications. By the end of this module, you'll be equipped with the tools and knowledge to embark on your C++ programming adventure. Let's dive in and begin the process of downloading, installing, and running Microsoft Visual Studio!

Here's how you can download, install, and run Microsoft Visual Studio (the free version) for C++ development:

## Step 1: Download Visual Studio
1. Open a web browser and navigate to the official Visual Studio website: [https://visualstudio.microsoft.com/](https://visualstudio.microsoft.com/).
2. Click on the "Download Visual Studio" button, the "Community" version. Make sure to select the "Visual Studio Community" edition, as it is the free version and supports C++ development. You may need to scroll down to find it.
3. The download will automatically starts.

## Step 2: Run the Installer
1. Once the installer is downloaded, locate the file (typically in your Downloads folder) and run it.
2. The installer will begin preparing the necessary files for installation. This may take a few moments.
3. After the preparation is complete, the Visual Studio Installer will launch.

## Step 3: Select Workload and Components
1. In the Visual Studio Installer, you will be presented with various options for workloads and components to install. A workload is a set of tools and features tailored to a specific type of development.
2. Since you're interested in C++ programming, select the "Desktop development with C++" workload. This workload includes the necessary tools and libraries for C++ development.
3. You can also customize the installation by selecting individual components if needed. However, the selected workload should cover most of your C++ development requirements.
4. Once you've made your selection, click the "Install" button at the bottom right.

## Step 4: Installation
1. The installer will now download and install the selected components. This process may take some time depending on your internet connection and the components you chose.
2. During the installation, you may be prompted to accept the license terms and authorize the installer to make changes to your system. Follow the on-screen instructions and click "Continue" or "Next" as needed.
3. Once the installation is complete, you will see a "Success" message.

## Step 5: Launch Visual Studio
1. After the installation, you can launch Microsoft Visual Studio from the Start menu or desktop shortcut. It may take a moment to initialize the first time you run it.
2. On the initial startup, you might be prompted to sign in with a Microsoft account or create a new one. You can choose to sign in or skip this step by clicking the "Not now, maybe later" option at the bottom.

For more information, take a look at its official website at [here](https://learn.microsoft.com/en-us/cpp/build/vscpp-step-0-installation?view=msvc-170).

## Online C++ Compilers
Online C++ compilers provide an alternative way to run and test C++ programs without the need for a local development environment. Here's an overview of online C++ compilers, along with their pros and cons.

### Important Online C++ Compiler Websites:
1. [OnlineGDB](https://www.onlinegdb.com/online_c++_compiler): OnlineGDB offers a C++ compiler with an interactive IDE, allowing you to write, compile, and run C++ code online.
2. [Repl.it](https://replit.com/languages/cpp): Repl.it provides a wide range of programming languages, including C++. It offers an online coding environment where you can write, compile, and run your C++ programs.
3. [Ideone](https://ideone.com/): Ideone is an online compiler and debugging tool supporting various programming languages, including C++. It allows you to write and execute code snippets online.
4. [JDoodle](https://www.jdoodle.com/online-compiler-c++/): JDoodle offers an online C++ compiler where you can write and execute code, with options to customize the input and output.

Remember, while online C++ compilers can be useful for quick tests or simple programs, for more extensive development projects, it is recommended to set up a local development environment using dedicated C++ IDEs.

### Pros of Online C++ Compilers
* **Accessibility**: Online C++ compilers can be accessed from any device with an internet connection, making them convenient for quick coding tasks or when you don't have access to a local C++ development environment.
* **Easy Setup**: Online compilers eliminate the need for installation or configuration, which can be time-consuming for beginners or in certain environments where installing software is restricted.
* **Rapid Prototyping**: Online C++ compilers enable you to quickly prototype and test small snippets of code, making them useful for experimenting with new ideas or troubleshooting specific programming issues.
* **Sharing Code**: Many online C++ compilers provide options to share your code with others through a URL, allowing for easy collaboration or seeking assistance from programming communities.

### Cons of Online C++ Compilers:
* **Limited Features**: Online compilers may not offer the full range of features available in dedicated local IDEs like Microsoft Visual Studio or Code::Blocks. They might lack advanced debugging tools, project management capabilities, or integration with other development tools.
* **Dependency on Internet**: As online C++ compilers require an internet connection, programming in environments with unstable or no internet access can be challenging or impossible.
* **Security and Privacy**: When using online compilers, there might be concerns about the security and privacy of your code, especially if it contains sensitive or proprietary information. Make sure to review the terms and conditions and privacy policies of the online compiler platform.
* **Performance Limitations**: Online compilers may have limitations on program size, execution time, or available system resources. Complex or resource-intensive C++ programs might not run optimally or at all on these platforms.

### Running C++ Linux Programs on Windows using WSL and Microsoft Visual Studio

If you're using a Windows machine and want to run the above C++ code that requires a Linux environment, don't worry! With the Windows Subsystem for Linux (WSL) and Microsoft Visual Studio, you can seamlessly develop and run Linux-based C++ applications on your Windows computer. Here's a step-by-step guide to get you started:

#### 1. Installing the Windows Subsystem for Linux (WSL):

1. **Enable WSL**: Before installing any Linux distributions on Windows, you must enable the "Windows Subsystem for Linux" optional feature. Open PowerShell as Administrator and run:
   ```bash
   wsl --install
   ```

2. **Install a Linux Distribution**: Once WSL is enabled, you can install a Linux distribution of your choice from the Microsoft Store. For our purposes, Ubuntu is a popular choice.

3. **Initialize Your Linux Distribution**: The first time you launch a newly installed Linux distribution, a console window will open, and you'll be asked to wait for a minute for files to de-compress and be stored on your PC. You'll then need to create a user account and password for your new Linux distribution.

For a detailed guide on installing WSL, refer to the official Microsoft documentation: [Install WSL](https://learn.microsoft.com/en-us/windows/wsl/install).

#### 2. Setting Up Microsoft Visual Studio for WSL:

1. **Install Visual Studio**: If you haven't already, download and install Microsoft Visual Studio. Ensure you select the "Desktop development with C++" workload during installation.

2. **Install the Linux Development Workload**: Open Visual Studio Installer and modify your Visual Studio installation. Check the "C++ for Linux development" workload and install it.

3. **Create a New Linux Project**: Launch Visual Studio and create a new "CMake project". This will allow you to write and debug C++ code as if you were on a Linux machine.

4. **Connect to WSL**: In the "Target System" dropdown, select the WSL option. Visual Studio will automatically connect to your WSL instance and use it for building and debugging.

5. **Run Your Code**: Now, you can write your C++ code in Visual Studio, and when you build and run it, it will execute within the WSL environment.

For a comprehensive walkthrough on setting up Visual Studio for WSL2 development, refer to the official Microsoft documentation: [Build and Debug with Visual Studio and WSL2](https://learn.microsoft.com/en-us/cpp/build/walkthrough-build-debug-wsl2).
