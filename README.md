# hello-fx

A "Hello World" application in JavaFX that is built using the JavaFX Maven plugin.

## Description

The main goal of this application is to demostrate the ability to build a JavaFX application and build it using Maven rather than the JavaFX Packager directly. In my experience, very few people or companies use Ant anymore; most folks are using Maven or Gradle now.

Through the use of the JavaFX Maven plugin, the build of a JavaFX application is greatly simplified, including being able to quickly create a native application.

Some links for documentation can be found at:

- [JavaFX Maven Plugin](http://zenjava.com/javafx/maven/)
- [Building a Native Application](http://zenjava.com/javafx/maven/native-bundle.html)

## Build a Native App

1. `mvn clean jfx:native` (or `mvn clean install` ... the native packaging has been paired to the verify Maven phase)
2. Look for the the installer, DMG, or RPM in `(project)\target\jfx\bundles`.

This will build an installer for whatever platform you are building on. Building on a Mac will produce a Mac app. Building on a Windows PC will produce a Windows app.

## Building a Windows Installer and Native Application EXE

Building a Mac DMG or Linux RPM works straight of the box. However, Windows requires either WiX for MSI creation or Inno Setup for an EXE-based installer (both install an EXE for the JavaFX application along with a packaged JRE).

Both don't need to be installed, just whichever one gets you to your desired installer format.

### Build an EXE Installer with Inno Setup

Follow the steps below to create an EXE-based installer with Inno Setup and the JavaFX Maven plugin.

1. Download from [Inno Setup's site](http://www.jrsoftware.org/isinfo.php)
2. Install it (I defaulted most of the installation options)
3. Add `C:\Program Files (x86)\Inno Setup 5` to your system `Path` variable.

Once done, run `mvn jfx:native` to create an EXE based installer at `(project)\target\jfx\native\bundles`.

By running the EXE installer, it installs the JavaFX application to the user's local app data folder, as well as an uninstaller entry in the `Programs and Features` control panel. The application is also launched immediately following installation.

### Build an MSI with WiX

To install WiX and have the JavaFX Maven plugin use it during a build, do the following:

1. Download from [WiX's site](http://wixtoolset.org/)
2. Install it.
3. Add `C:\Program Files (x86)\WiX Toolset v3.7\bin` to your system `Path` variable.

Once that is complete, `mvn jfx:native` will create an MSI file in `(project)\target\jfx\native\bundles`.

Running the MSI installs the application to `C:\Program Files (x86)\(project name)` without prompt. Additionally, it creates an uninstaller listing in the `Programs and Features` control panel.