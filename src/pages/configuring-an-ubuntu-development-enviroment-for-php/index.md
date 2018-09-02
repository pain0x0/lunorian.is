---
title: Configuring an Ubuntu Development Enviroment for PHP
date: "2018-09-02"
---

Recently I enrolled in a college to gain new technical skills in web application development, computer networking, and cyber security. One course in paticular that I am taking - CTI-110, focuses on web application development in HTML and PHP. Despite promises from the professor for a Virtual Machine configured for Web Develoment after several people complained they were unable to get XAMPP working (XAMPP is some random web server for Microsoft Windows, I've never used XAMPP before so I couldn't say if it's good or bad - you can download and check it out at https://www.apachefriends.org/index.html if you're interested). Unfortunately it seems that the Virtual Machine has still has not been provided (at least not anywhere I could find it in the online course materials), some students who likely do not have prior web development knowledge have no clue on how to get started. So I decided to take this situatation as a learning oppertunity and I am writing this tutorial to share how I setup my own development enviroment for my coursework.

## Recommended System Configuration
This tutorial uses Ubuntu 18.04.1 LTS which uses the GNOME Shell as it's graphical interface. It can be more resource demanding than other Linux distributions are. While the instructions in this tutorial should work on any system which can run Virtualbox, this tutorial was written and tested inside Ubuntu 18.04.1 LTS on Virtualbox running on a macOS High Sierra host operating system with a Intel(R) Core(TM) i5-5257U CPU @ 2.70GHz CPU, I can't promise the information provided in this tutorial will work as is on another system. I shared 2 CPU Cores between macOS and the Guest OS (in our case Ubuntu 18.04.1 LTS) and dedicated 4096Mb of RAM to the Guest. With this short disclaimer out of the way let's get started.

## Why Virtualbox
Outside of the fact that my target audience for this post is CTI-110 students, I think Virtual Machines have several benefits. First things first if you mess up badly inside a Virtual Machine, the host operating system isn't damaged. In a worst case scenario you delete the Virtual Machine and make a new one.

## What if my computer doesn't meet these demanding requirements?
You can still create a Virtual Machine with less available resources, although you may wish to consider an alternate Guest OS such as Xubuntu or Lubuntu which is less straining. Alternatively, there are several cloud providers who would be happy to rent capacity to you for a Virtual Machine you can access remotely at a reasonable price, I recommend [DigitalOcean](https://m.do.co/c/cdc55ee0cd03) (*required dislosure: ordering a virtual machine through this link will give both of us an account credit*). You can configure them remotely, install a graphical enviroment, and use a remote desktop like tool, for example VNCServer is popular in the Linux community, I've heard that SSH can now do X11 forwarding although I've never played with that before. Finally if you are open to change, you could install Ubuntu directly on your computer rather than inside a Virtual Machine. Just make sure to backup your data somewhere safe first.

## Step 1: Install Virtualbox
As previously stated, this tutorial will be focused on creating a development enviroment inside a Ubuntu 18.04.1 LTS Virtual Machine managed by Virtualbox. Your first step should be to download and install Virtualbox.

1) Download Virtualbox from https://www.virtualbox.org/wiki/Downloads for your operating system.
2) Run the installer and follow the prompts.
3) Open Virtualbox.

## Step 2: Download Ubuntu 18.04.1 LTS
You will now need to download an ISO Image of Ubuntu 18.04.1 LTS to install. You have a few options to download the operating system.

* HTTP: The easiest way to download is to visit https://www.ubuntu.com/download/desktop/thank-you?country=US&version=18.04.1&architecture=amd64 and download the ISO directly from their website. Of course depending on your internet connection speed among other factors, a Bittorrent Download may be faster.
* BitTorrent: A faster way to download the ISO is through a peer to peer file sharing application called BitTorrent. You can a torrent link in the Alternative Downloads section at https://www.ubuntu.com/download/alternative-downloads
* NetBoot: This isn't necessarily "faster" although it is a smaller ISO to download and downloads the more important stuff as needed.

The method you use is really personal preference. Whichever method you choose will still result in you downloading and installing Ubuntu. Once the ISO file is done downloading proceed to the next step.

## Step 3: Create a Virtual Machine from Virtualbox
It's now time to jump into the fun stuff and create your own Virtual Machine.

1) Click new and pick a name for your new Virtual Machine

![alt](/static/images/configuring-an-ubuntu-development-enviroment-for-php/screenshot-1.png)

2) Choose a good amount of memory for your new Virtual Machine. I recommend 4096Mb although there are several factors. Addatioally keep in mind this is not magic memory - Virtualbox is reserving that much memory from the host computer's available memory. This means if you have 32 Gb of RAM you now have 28Gb and so forth.

![alt](/static/images/configuring-an-ubuntu-development-enviroment-for-php/screenshot-2.png)

3) Create a Virtual Hard Disk. I would recommend at least 16Gb of disk space, 32Gb is preferable. I recommend dynamically allocated, although fixed size may be slighter faster. This depends on several factors however, you'll need to do your research and find what works best for your specific system.

![alt](/static/images/configuring-an-ubuntu-development-enviroment-for-php/screenshot-3.png)

## Step 4: Install Ubuntu inside your Virtual Machine
You can now press start and Virtualbox will start your Virtual Machine. It will prompt you to select an ISO file to boot. Select the Ubuntu ISO you downloaded earlier.

It may take up to a minute for it to completely boot. Once it's done booting, follow the on screen prompts to install Ubuntu. The only option you should see for disk configuration is "erase disk and install ubuntu" - this is "erasing" the Virtual Hard Disk, not your real hard drive. It will ask you to choose a username and password as part of the process. It may take a little bit for the installer to finish up. Afterwards just reboot the Virtual Machine and it'll boot into Ubuntu.

## Step 5: Configure Ubuntu
Once you are at your desktop, Ubuntu may ask you to enroll in Canoncial Live Patch, it's an optional service to sign-up for allowing you to avoid reboots. It's up to you whether to install it or not.

This is also a good time to go ahead and install the Virtualbox Guest Additions. Just run `sudo apt-get install virtualbox-guest-dkms virtualbox-guest-utils virtualbox-guest-x11` inside terminal, let the installer run, and reboot the virtual machine. Afterwards Ubuntu will be optimized for running inside Virtualbox. It's worth the extra configuration time.

## Step 6: Install your development tools

You can run the following commands in terminal for a mostly automatic install of the necessary tools.

**Step 1:** Run `sudo apt-get install php php-mysql mysql-server` in terminal.

**Step 2:** Run `snap install vscode --classic` in terminal. This will install the VS Code text editor.

Now you have the bare minimum tools to start writing PHP Code.

## How to use these tools

**Step 1:** Create a folder to store your source code.

**Step 2:** Open the folder in VS Code

**Step 3:** Open terminal, run `cd ~/path/to/your/folder`, then run `php -S localhost:8080`, and open `http://localhost:8080/` in your preferred web browser.

**Step 4:** Create source code files inside your folder, edit them with VS Code, and view the changes in your preferred web browser.

## Suggestions or Feedback?
I’m always open to your suggestions and/or feedback, if you have suggestions or feedback on this blog please send an email to me@lunorian.is I’d love to hear from you :)