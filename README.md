# Mono-packaging-for-Mac
This is a **Mono** package (.pkg) for Mac using the amazing Packages app

## Motivation
So you have finished your awesome app using Mono and MonoMac or whatever. But then suddenly you find that distribution becomes a hassle as that your app requires Mono to run and the end user may or may not have it. 9 out of 10, they don't. So you need to distribute your app with Mono. But you also don't want to bloat your app package's size. Mono is no samll thing. It's well over 200MB packaged and over 300MB unpacked. What I did is first to check whether user have Mono installed already. If they do, then great. If they don't, my distribution package will download the custom built Mono packages and install them onto the user's machine. This is as best as I can achieve. Xamarin.Mac does allow you to build self-contained app, but it is attached with a large price tag ($995). So I do think this can be useful to others.

## Get Started
1. Download the amazing, awesome, bullet-proof, silver-lining **Packages** tool, and yes it's that good! If you don't know, Google it, with Bing, of course
2. Use the **Packages** to open the 3 projects in the **setup** folder of the repository
3. That's it

## Overview
There are 3 packaging projects, one is the distribution project - **Mono-packaging**. This is a demo project to show how to use the other two packaging projects - **Mono.pkgproj** and **Mono Shell.pkgproj**. Don't ask me why I don't put the other two pkgproj into one, it is what it is. **Mono.pkgproj** is the pkg project that packages the actual content of **Mono framework**. It points to the Mono.framework folder on your MAC. **Mono Shell.pkgproj** is for packaging all the links of shell scripts of **Mono framework** found in the **usr/bin** folder. 
    
    
   
The distribution project **Mono-packaging** shows how to reference the other two packages. You can use it as a template or a start point for the distribution package of your own fine product. The process is described as below:
   
1. Build the **Mono.pkgproj** and **Mono Sheel.pkgproj** projects, and two files will be generated, **Mono.pkg** and **Mono Shell.pkg.** Rename the latter to **MonoShell.pkg**
2. Upload the two generated files onto your server using some **FTP** tool. Make sure to add .pkg's MIME type to your web server so that it's downloadable
3. Add package reference to the distribution project of your product, the name of the project is the package name, which are **Mono.pkg** and **MonoShell.pkg** respectively.
4. Set the location of each package to the http folder that stores the two **.pkg** files, let's say, http://www.your-web-server.com/downloads. The type should be **HTTP URL**
5. Give the two package references each an **Identifier** and a **Version** No. 
6. Add requirement for the installation of the distribution package in the **presentation** tab of the project for each referenced package so that it only installs when the user don't have **Mono framework** installed already. I included a simple Mono framework check script in the project already. Also please see **Mono-packaging** for details. **Packages** is simple and awesome enough that you can master it in no time.

With that, I'll leave you to explore the repository yourself.
