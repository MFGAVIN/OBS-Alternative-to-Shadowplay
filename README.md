# Using OBS Studio as an Alternative to NVIDIA Shadowplay


## Table of Contents

- [Introduction](#introduction) 
- [Disclaimer](#disclaimer) 
- Start Here VVV If You Don't Give A Shit
- [Prerequisites](#prerequisites) 
- [Profile & Scene Collection](#profileSceneCollection) 
	- [Profile](#profile) 
	- [Scene Collection](#sceneCollection) 
- [Recording Settings](#recording) 
- [Audio](#audio) 
- [Video](#video) 
- [Replay Buffer](#replayBuffer) 
	- [Settings](#replayBufferSettings) 
	- [Hotkeys](#replayBufferHotkeys) 
- [OBSPlay](#OBSPlay) 
	- [Known Bugs](#knownBugs) 
	- [How to Setup OBSPlay](#setupOBS) 
- [Advanced Settings](#advanced) 
	- [General](#advancedGeneral)
	- [Video](#advancedVideo)
	- [Recording](#advancedRecording)
- [Scene Creation and Automatic Scene Switcher](#scass)  
	- [Scene Creation](#sc)
	- [Automatic Scene Switcher](#ass)
- [Debugging](#debugging)
- [Making OBS Startup on Startup...](#obsStartup)
- [Sources Cited](#citations) 

## Introduction (You Can Skip This)<a name="introduction"><a/>
Hello, my name is MFGAVIN and what sparked this journey was the hatred for NVIDIA Shadowplay, its unreliable video quality, dogshit audio quality annoyed me, so I journey across the lands of OBS Forums to find the knowledge and ingredients to make an alternative.  And I'm happy to say that I think I pieced enough pieces together to it better than Shadowplay and thought others might enjoy it as well.

## Disclaimer <a name="disclaimer"><a/>
Before we dive into this I want to let you guys know that the information I have isn't my own and so whenever we get to certain parts I'll provide links to the places where I got that information.  Also the way I made this was by searching up OBS articles, asking for help in discords, or looking up others setups.

The information presented in this guide is heavily based off [StuckInLimbo's OBS-ReplayBuffer-Setup](https://github.com/StuckInLimbo/OBS-ReplayBuffer-Setup) and in the event they either want this deleted I will comply or edited the information presented in a way it works for both of us.

Also, the settings I give through this guide may have to be altered later on through the [Debugging](#debugging) process.

Lastly, I just want to say that this is my first ever making a article willingly so it might be a shit and a mess but I'll edit it later on to gather my thoughts.

## Prerequisites<a name="prerequisites"><a/>
I don't want to hand hold so take care of this stuff before starting. 

 - An install of **OBS Studio** (se.live is cringe)
 - Download this [script](https://obsproject.com/forum/resources/obsplay-nvidia-shadowplay-alternative.1326/) from OBS Forums called **OBSPlay**.

## Profile & Scene Collection <a name="profileSceneCollection"><a/>
 
This part only really matters if you have a bunch of scenes and stuff already setup and don't want to screw it up.

So in the main window of OBS if you look at the top you will see **Profile** and **Scene Collection** the purpose of these are to make it able to have completely different settings and scenes apart from your usually stuff.

![image](https://user-images.githubusercontent.com/40813002/167230689-87ee6437-2195-4269-b50f-57820e349748.png)


So with this you can start fresh and be able to follow the tutorial, but again it's not really necessary. 

Haven't tested this feature but I'll give you guys my profile and scene collection which I think should give you all the settings I use but might not work.

#### Profile <a name="profile"><a/>
[ClipRecorder - Profile.zip](https://github.com/MFGAVIN/OBS-Alternative-to-Shadowplay/files/8644133/ClipRecorder.-.Profile.zip)
#### Scene Collection <a name="sceneCollection"><a/>
[ClipRecorder - Scene Collection.zip](https://github.com/MFGAVIN/OBS-Alternative-to-Shadowplay/files/8644135/ClipRecorder.-.Scene.Collection.zip)
Unzip them and import them in OBS

 ## Recording Settings <a name="recording"><a/>

### Disclaimer
**This section uses information from** [StuckInLimbo's OBS-ReplayBuffer-Setup](https://github.com/StuckInLimbo/OBS-ReplayBuffer-Setup) 

 Go to **Settings** then skip both **General** and **Stream** since there is nothing there that can help us.  So go to **Output** then **Recording**, these settings are what I use but I'll discuss why.
![image](https://user-images.githubusercontent.com/40813002/167230872-7e3367b5-d869-466a-a8ce-3d077f2bd07f.png)
 
**Set the recording path to the hard drive where you want your clips to be stored**, for me its F:/ but for others it may be C:/ , D:/.  Just select one of those drives as we will be specifying further using OBSPlay script.
![image](https://user-images.githubusercontent.com/40813002/167230916-25a01bb2-a393-44ba-aebf-8d77191d2c5a.png)

 Leave "**Generate File Name without Space**" uncheck
 
 **Recording Format to either MP4 or MKV**.  But remember you cannot utilize the MKV remux to MP4 automatically feature with this script because at the time of writing it makes the MP4 file not show up.
 
**For Audio Tracks**, you can either have both 1 and 2 turned on or just 1 it just depends on your use case since having 2 tracks, one for mic and one for desktop audio allows you to personally customize them later on in editing but its up to you.
 
 **Encoder Options** are going to be slightly varied and so I won't discuss too much about it.  If you have a RTX card go with **NVIDIA NVENC H.264 (new)** since it'd be the preferred use case for me but for you it may be different, so search up if it could be.
 
**Rescale Output**, leave unchecked, but for some people you may have to use it, search up if you may have to because of somethings like monitor resolutions

**Custom Muxer Settings**, leave blank, unless you want to use some of them
  
**Rate Control**, what I've seen others recommend is **CQP**.  
 
**CQ Level**, you should use a range between **14-21**.  A lower CQ Level results in better image quality but a higher file size.
 
**Keyframe Interval** I've seen a couple numbers thrown around so either set it to **0, 2, or 5**.  Though as you can see I set it to 2.
 
 **Preset** can be any of the options beside **Low-Latency** as I was told it was useless but you should cycle around **Performance, Quality, or Max-Quality.**
 
**Profile** it's recommended to use **High** and if you notice problems then to switch to **Main**
 
Leave **Look-Ahead unchecked**
 
Set **GPU to 0**
 
Then lastly for this section, **Max B-Frames to 2**
 
 
 ## Audio <a name="audio"><a/>
### Disclaimer
**This section uses information from** [StuckInLimbo's OBS-ReplayBuffer-Setup](https://github.com/StuckInLimbo/OBS-ReplayBuffer-Setup) 

 So right next to the **Recording** tab, go to **Audio**
 - Set all of the **Audio Track's bitrate to 160** and if you want to name them you can.

Go to the **Audio** tab right below **Output**, here is where the tracks come into hand. 

![image](https://user-images.githubusercontent.com/40813002/167231047-e60a0162-14aa-457d-96b8-505557de7459.png)

Now depending on what your audio devices are set to you should either put the **Sample Rate** to **44.1kHz or 48kHz** and if you don't know what they are then I'll show you a way later.  Also leave **Channels** alone.

Go onto **Global Audio Devices** and select your **Desktop Audio** as well as the **Mic** you use.  See here is where the tracks come in, one track puts both audios into one and 2 splits them.  **After you fill in the ones you use, Disable all others.** Lastly, **ignore the other stuff** since I didn't touch it nor do I know what they do.

Lastly, go back into the **Main Window of OBS** and look at the **Audio Mixer**, and select **Advanced Audio Settings**. After that look at the **tracks** at set it to this.

![image](https://user-images.githubusercontent.com/40813002/167231545-b09c63f3-14b9-443c-b3dd-11e2e1ee209c.png)


## Video Settings <a name="video"><a/>
### Disclaimer
**This section uses information from** [StuckInLimbo's OBS-ReplayBuffer-Setup](https://github.com/StuckInLimbo/OBS-ReplayBuffer-Setup) 

![image](https://user-images.githubusercontent.com/40813002/167231560-b1ea571e-77f8-4af4-bd2e-a9d1acc43dfa.png)
	
Now you shouldn't have to mess with this settings to much a be able to **ignore both Base Resolution and Output Resolution** although issues may occur if you play with resolutions higher than 1080p and maybe don't want to deal with the increase resource use.

**Downscale Filter** can be set to either **Bicubic or Lanczos**, **Lanczos** is better but is more resource intensive but test it yourself and if you see issues maybe change it to **Bicubic**.

**Common FPS Values** leave it at **60**, unless you want to do some weird shit


## Replay Buffer <a name="replayBuffer"><a/>
### Disclaimer
**This section uses information from** [StuckInLimbo's OBS-ReplayBuffer-Setup](https://github.com/StuckInLimbo/OBS-ReplayBuffer-Setup) 

### Settings <a name="replayBufferSettings"><a/>
Go to the **Replay Buffer** inside the **Output** tab and you should see this
![image](https://user-images.githubusercontent.com/40813002/167231579-75f9ab7d-1797-4153-a3da-dff4bf8ec1c5.png)

Now the **Maximum Replay Time** should be set to either **30s to 240s** as suggested by StuckInLimbo, anything more should just be a recording.
Then Maximum Memory should range from **1GB (1024MB) to 4GB (4096MB)** scaling according to the amount of time be replayed of course. 

### Hotkeys <a name="replayBufferHotkeys"><a/>
	
![image](https://user-images.githubusercontent.com/40813002/167231627-83faf902-e41f-4b59-9b11-ff75611cd4a2.png)
	
Go to the **Hotkeys tab** and scroll until you find **"Start Replay Buffer"** and **"Stop Replay Buffer"**, personally I didn't fully set it up because with settings we will discuss later on makes it not too important but if you want to you can set those up.

After those scroll down more until you see **Replay Buffer** with only one hotkey available, **"Save Replay"**, set it to whatever you want maybe **\\** or something with **ALT + __**


## OBSPlay <a name="OBSPlay"><a/>
What the script does is it makes it able to make folders and or files based on the scene names.  Sadly, the person who made the script was last active July 16, 2021.  And so they're two bugs that I found that I want you guys to be aware of.

### Known Bugs <a name="knownBugs"><a/>
 1. The first bug happens if you want to use **MKV** and want to **automatically remux it to MP4**, it'll cause the **MP4 file to mysteriously disappear into the backrooms** for the entities to enjoy.
 2. The second bug is occurs when selecting the settings for the script so I'll go over it more during the setup.
 
### How to Setup OBSPlay <a name="setupOBS"><a/>
 1. Open **OBS**
 2. Click on **Tools**
 3. Click on **Scripts**
 4. Click on the **+ Button**
 5. Add the **OBSPlay script** from where ever you're keeping it
 6. So for the **Base Save Path** you're going to make a folder inside of whatever the hard drive you chose in **C:/** then make a folder inside of it I made my clips so it would be **C:/Clips/**
 
Now if you follow the steps correctly you should be on this portion 
![image](https://user-images.githubusercontent.com/40813002/167231804-c3ef2aa5-33be-421c-a0e2-3c510a8bb2c9.png)
So after making/selected a folder for the clips to be moved to move onto selecting the two modes.

**They're 2 Different Modes**
1. Clips will be prefixed with scene name and then go into a singular folder
	1. If this sounds good to you then **check only "Scene Based File Prefix".**
2. Same as Option 1,  but folders will be made according to scene names and the clips will be placed in their according scene folder.
	2. If this sounds good to you then **check both boxes**

	
## Advanced Settings <a name="advanced"><a/>
We are going to focusing on **General, Video, and Recording,** everything else doesn't matter.

![image](https://user-images.githubusercontent.com/40813002/167231868-7844abd6-70ec-41f2-a602-dd341725f704.png)

### General <a name="advancedGeneral"><a/>
**Process Priority** can be left on either **Normal or Above Normal**
	--- This decides how prioritized you are for resources on your computer.
	
### Video <a name="advancedVideo"><a/>
**Renderer** should already be set to **Direct3D 11** although if something else is there leave it be.
Set **Color Format** to **NV12**
Set **Color Space** to **709**
Lastly, set **Color Range** to **Partial**

### Recording <a name="advancedRecording"><a/>
You can leave all of this as is, but with **Filename Formatting** if you click on it and hover over the text you can see all the possible settings you can set that to.
Lastly, **leave all the other stuff unchecked and blank**

## Scene Creation and Automatic Scene Switcher <a name="scass"><a/>
This portion is one of the vital parts of this guide.

### Scene Creation <a name="sc"><a/>
You must follow this as it's important with OBSPlay because of how the prefixes will work with files and folders.

1. Make One Scene Called "Desktop" and add a **Display Capture** source
2. Add the games you play with **Game Captures** as it's better for performance

For LoL:
	If you're trying to add **League of Legends** and it's not working is because of your overlays as it's really stingy so make sure you check it out, for me it didn't work because of **RTSS Overlay**.  Anything else and explore reasons why on your own.
	
### Automatic Scene Switcher <a name="ass"><a/>
This part's important as it'll optimize the resources when switching to the appropriate from desktop capture and game capture.  

Before I go into more detail, something to note here with this, the replay buffer, and OBSPlay is that whenever you clip something whatever the most recent scene was switched to will result in the file be prefixed to that scene so just remember that when searching for it as it may sometimes be placed somewhere you don't want.

**Go to Tools>Automatic Scene Switcher**
![image](https://user-images.githubusercontent.com/40813002/167231986-1c8f5890-f82d-401a-8934-e94f853eab60.png)

The long box contains all of the programs currently loaded so selected your game's program, the short box contains all the scenes so match up the program names with the scene's name. 

Then look at the **"When no window matches:"** and **select "Switch to:"** and lastly **select "Desktop"**

Leave everything else else as is.
And all that's left is to do that for all the other games you play.



## Debugging <a name="debugging"><a/>
Now, this part is important to help you debug and fix any issues you incur upon testing.  Before I say this, I want you guys to know that in the [OBS Discord Server](https://discord.gg/obsproject) you can ask for support but in my head just in case this blows up I don't want to fill that discord with supports of the same issue, so I want you guys to try and fix the issue yourself, and search up solutions to it yourself, and if it still doesn't work then go straight ahead to the [discord server](https://discord.gg/obsproject). 

The way they recommend to debug is 
1. **Run the Replay Buffer for 30s or longer**
	- Optional/What I Do: **Take a clip**
2. Stop the **Replay Buffer**
	
![image](https://user-images.githubusercontent.com/40813002/167232001-ad45488d-ff45-4dc4-b89b-aad9d595bdd2.png)

3. Follow the image and click on **Upload Current Log File**
4. Click **Analyze**
	- Once you click this it'll take you to a website that'll show the problems that are arising in your use-case as well as stating the fixes.  It's a super useful tool.  And if you still can't solve the issue then go ahead and ask for help in one of the support channels and remember to send a link to your logs so they can actually help you.



## How to make OBS Open on Startup <a name="obsStartup"><a/>
This part is pending since the [guide is pretty straightforward](https://obsproject.com/forum/threads/start-obs-as-administrator-on-startup-in-windows-10-with-startreplaybuffer.116313/), and after discussing with the author I'll see what to do further.


## Sources Used <a name="citations"><a/>
I'd like to give thanks to the [OBS discord server](https://discord.gg/obsproject) and [Epos Vox's discord server](https://discord.gg/eposvox) for helping with questions I had.

Then I'd like to give thanks to [StuckInLimbo's OBS-ReplayBuffer-Setup](https://github.com/StuckInLimbo/OBS-ReplayBuffer-Setup) as I heavily used the information provided to make this guide

Lastly, please check out this [guide by Koala](https://obsproject.com/forum/threads/start-obs-as-administrator-on-startup-in-windows-10-with-startreplaybuffer.116313/)  on how to make OBS open on startup in Administrator mode
