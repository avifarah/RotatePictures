# Rotate.Pictures
2020-05-21

If you have any questions then please enter them in the **issues** tab.

## Installation Instructions
If you prefer **not** to compile the code then retrieve the zipped file [Rotate.Pictures.zip](https://github.com/avifarah/RotatePictures/commit/97244916585071e4207366c8cee07f00a46a34f8).  Unzip it and make the appropriate modifications to the configuration file (Rotate.Pictures.config) as per below.  That's it.  

#### Remarks
The code will work with .Net Framework 4.8.  So if you prefer to use the code without the compilation step and if you do not have the .Net Framework 4.8 installed then you will need to install the .Net Framework 4.8, see: [.Net Framework 4.8](https://dotnet.microsoft.com/download/dotnet-framework/net48) for installation instructions.

On the other hand, if you wish to compile the source code yourself, then get the source code and compile it, preferably in Release mode.  Then modify the configuration file (Rotate.Pictures.config).

#### Remarks
The code targets .Net Framework 4.8.  You may change the target framework if you do not have it and do not wish to install it.  I started this project prior to .Net Core and did not attempt to migrate to .Net Core as of yet.

Now that your code is compiled.  Copy the contents of the bin\Release (or bin\Debug) into the machine and directory where you wish to run the program from.

Your last step is the modify the configuration file: ```Rotate.Pictures.exe.config```.

## Modification of the configuration file: ```Rotate.Pictures.exe.config```

Modify the entries in the appSettings section of the configuration file.
- **Initial Folders**
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

The **value** part of the ```<add key="Initial Folders" value="M:\Pictures" />``` entry should contain the directory/directories where the pictures are.  Do not worry about subdirectories, the software will crawl through the subdirectories and look for pictures, then display those pictures in a random order.

### Remarks
If your pictures are spread over multiple directories, then separate the directories with a semicolon.  So, if for example, you have pictures that you wish to rotate through in the following directories: “C:\MyPictures”, “D:\YourPictures” and “C:\RandomDirectory\FarOut\FunnyPics” then the **Initial Folders** entry will look like:

```<add key="Initial Folders" value=" C:\MyPictures;D:\YourPictures;C:\RandomDirectory\FarOut\FunnyPics" />```

- **Max picture tracker depth**
```
<!-- Depth of stack keeping the displayed pictures, meaning you may go 
			back up to "Max picture tracker depth" of displayed pictures -->
<add key="Max picture tracker depth" value="1000" />
```

![Example of running program](https://github.com/avifarah/RotatePictures/blob/master/Annotation%202020-05-21%20003603.png)

Looking at the above depiction of the running Rotating.Pictures display, bottom most, left most "<" button will allow you to go back through the pictures that were just displayed.  The **Max picture tracker depth** will control how many pictures you may go back to, from the current picture.  Default is: 1,000.

- **Still pictures** and **Motion pictures** 
```
<!-- These are the only extensions that the system will consider.  
			Extensions are semicolon separated.
			Extensions must start with a period (".").  -->
<add key="Still pictures" value=".jpg;.bmp;.gif;.png;.psd;.tif" />
<add key="Motion pictures" value=".mov;.avi;.mpg;.mp4;.wmv;.3gp" />
```
Still pictures will display the picture for a fixed amount of time.  Motion pictures will display a video with audio for this same amount of time.  If you need more time to watch the video then select the picture itself (or video), by clicking it, or select the Green circle at the bottom line (see above depiction).  The Green circle will turn Red and you can view the video with no time limit.

Select the picture/video or the Green/Red circle button in order to toggle the between picture/video rotation to stop rotation.  The Green/Red circle button is a visual indicator of the state of rotate/stop-rotate state.

The entries for both **still/motion pictures** are that of the extensions associated with them.  For a file to be considered as either still picture or motion picture it needs to appear in either of the configuration entries.

### Remarks
If an extension appears in both **Still pictures** and in **Motion pictures** configuration entry then the extension will be considered to appear in **Still pictures** only.

- **Image stretch**
```
<!-- Image stretch may be:
			"Fill"		-	Stretch the picture height and width independently
			"None"		-	Original size of height and width is maintained
			"Uniform"	-	Stretches the height and width uniformly until the one of the 
						directions equal the height or the width of the window
			"UniformToFill"	-	Stretches the height and width uniformly passed the
						the first dimension reaching the window height or width
						and until the second dimension reaches the height or 
						width of the window	-->
<add key="Image stretch" value="Uniform" />
```
I believe it to be self-explanatory.

- **Timespan between pictures [Seconds]**
```
<!-- Time to wait between display of one picture to the next.
			Value may contain fraction of a second.  -->
<add key="Timespan between pictures [Seconds]" value="10" />
```
**Timespan between pictures [Seconds]** is the amount of time before the picture will rotate to the next randomly selected picture.

- **First picture to display**
```
<!-- The first picture to be displayed is treated differently than the rest of 
			the pictures.  However, if you leave the value of "First picture to display"
			blank then the system will treat the first picture like it treats the rest 
			of the picture, choose it randomly.  Though not having first picture may 
			mean that your wait for "Timespan between pictures [Seconds]" before the 
			first picture appears. -->
<add key="First picture to display" value="M:\Pictures\Ben\IMG_0840-1.JPG" />
```
The very first picture faces a race condition between the time that the system cycles through all the directories and able to convert a sequential number to picture path, therefore, it is very likely that by the time the system is ready to display the first picture, the system will not finish processing all the files in all directories and subdirectories.  For this reason, having first picture fixed will allow the display to have something to display.  If you leave this value empty then the system may display nothing until it is done cycling through all the files to be displayed.  This time should not last more than one cycle of picture rotation (assuming that it is on the order of 10 seconds).

- **On start image rotating**
```
<!-- The system will start with automatic rotation of picture if the value to 
			"On start image rotating" is true otherwise the first picture will be
			frozen until you change the running status by selecting (click) on the picture or 
			select the forward arrow -->
<add key="On start image rotating" value="True" />
```
I believe it to be self-explanatory

- **Visual heartbeat**
```
<add key="Visual heartbeat" value="400" />
```
This entry controls how often the system should check it needs to do what needs to be done without a user event.  Like rotating to the pictures.  The time is given in milliseconds.  For the majority of the users and under normal circumstances this value may stay as is and you may safely ignore it.

- **Fast Forward [Seconds]** 
```
<add key="Fast Forward [Seconds]" value="10" />
```
![Motion Picture]( https://github.com/avifarah/RotatePictures/blob/master/Annotation%202020-05-21%20190259.png)
Viewing the above depiction showing a video display, you see, at the top of the display and to the left of the **Position** control a **fast forward** and a **fast rewind**.  The **Fast Forward [Seconds]** config entry controls how many seconds to fast-forward or fast-rewind.

- **Pictures Indices To Avoid.  Comma separated**
```
<add key="Pictures Indices To Avoid.  Comma separated" value=""/>
```
While viewing pictures you see a picture that you wish not to view again.  Out of the bottom right icons of the above depiction, select the left icon ![bottom right icons]( https://github.com/avifarah/RotatePictures/blob/master/Annotation%202020-05-21%20200356.png) and your picture index will be added to the list.

### Remark
Since only picture index is added to the list, if you add or remove pictures to the list or to the **Initial Folders**, then you may care to empty this entry out, since it is no longer accurate.

