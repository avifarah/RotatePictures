# Rotate.Pictures
2020-05-21

## Installation Instructions
If you prefer not to compile the code then retrieve the zipped file [Rotate.Pictures.zip](https://github.com/avifarah/RotatePictures/commit/97244916585071e4207366c8cee07f00a46a34f8).  Unzip it and make the appropriate modifications to the configuration file (Rotate.Pictures.config).  That's it.  The code will work on the .Net Framework 4.8.  So if you prefer to use the code without compiling it and you do not have the .Net Framework 4.8 then you will need to install the .Net Framework 4.8 (see: [.Net Framework 4.8](https://dotnet.microsoft.com/download/dotnet-framework/net48)).

On the other hand if you wish to compile the source code yourself, then get the source code and compile it, preferably in Release mode.

### Remarks
Code targets .Net Framework 4.8.  You may change the target framework if you do not have or do not wish to install the .Net Framework 4.8

Now that your code is compiled copy the contents of the bin/Release (or bin/Debug) into the machine/directory where you wish to run it from.

Your last step is the modify the configuration file, Rotate.Pictures.exe.config:

In the appSettings section of the configuration file, change the following entries:
- key="Initial Folders"
```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	<configSections>
		<section name="log4net" type="log4net.Config.Log4NetConfigurationSectionHandler, log4net" />
	</configSections>
	<appSettings>
		<!-- Directories where the system will look for pictures to display.
					Directories are semicolon separated.  Ex: value="g:\pic;m:\pic" -->
		<add key="Initial Folders" value="M:\Pictures" />
```

The value part of the entry should contain the directory where the pictures are.  Do not worry about subdirectories, the software will crawl through the subdirectories and look for pictures, then display them in a random rotating fashion.

If your pictures are spread over multiple directories, then separate them with a semicolon.  So, if you have pictures in the following directories: “C:\MyPictures”, “D:\YourPictures” and “C:\RandomDirectory\FarOut\FunnyPics” then the **Initial Folders** entry will look like:

```<add key="Initial Folders" value=" C:\MyPictures;D:\YourPictures;C:\RandomDirectory\FarOut\FunnyPics" />```

- **Max picture tracker depth**

```
<!-- Depth of stack keeping the displayed pictures, meaning you may go 
			back up to "Max picture tracker depth" of displayed pictures -->
<add key="Max picture tracker depth" value="1000" />
```

![Example of running program](https://github.com/avifarah/RotatePictures/blob/master/Annotation%202020-05-21%20003603.png)
