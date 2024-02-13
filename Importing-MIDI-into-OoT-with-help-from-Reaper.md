# Importing MIDI into Ocarina of Time with help from Reaper

There are various MIDI editors and MIDI capable DAWs (Digital audio workstations). This guide presumes that you want to use Reaper as your DAW of choice. Reaper is professional music production software but has a tolerable nag-ware trial (similar to Sublime Text) and *only* a $60 personal license if you get super into this music production thing.

This guide is written for a Windows user, but Reaper works on Mac and Linux.

## Background 
MIDI is both the name of the protocol that electronic instruments speak and the file format of songs produced with these electronic instruments in mind. A MIDI file (.mid) is like sheet music for a computer. However, you do not need to be able to read or play sheet music to work with MIDI files. More specifically, a MIDI file is a sequence of commands telling a program how to play back a song.

The General MIDI 1 (GM1) standard defines a set of virtual instruments that should generally be supported for MIDI files you'll find on the internet and try to play in Windows Media Player or whatever are designed with this instrument set in mind.

Ocarina of Time does not use MIDI, but it uses a sequenced format that we can convert to. OoT doesn't use GM1 instruments. Instead it has its own set of instruments that has some custom effects not in GM1, but it also doesn't have every instrument in GM1. Notably it doesn't have a drum kit.

OoT has bunches of instruments, bunch each song only uses a fixed set of instruments. The set of instruments used in a specific song is referred to as the audio bank. For now lets assume we need to use an existing audio bank... IDK how to do anything else yet.

## Downloads

* Reaper https://www.reaper.fm/download.php - The subject of this guide.

* TX16Wx https://www.tx16wx.com/download/ - A free DAW plugin to play back virtual instruments. This is literally the first one I came across. Others might be better. IDK.

* DezZival's OoT Sound Font https://www.youtube.com/watch?v=qpPzR-FodYc - Link in the description. This is a set of virtual instruments based on those used in OoT and MM.

* seq64 1.5 https://github.com/sauraen/seq64/releases/tag/V1.5 - The tool to convert MIDIs into OoT's seq format and inject them into a ROM. V2.0 and is different and existing guides assume 1.x versions of the software.

* ROM Decompressor https://github.com/OoTRandomizer/OoT-Randomizer/raw/Dev/bin/Decompress/Decompress.exe - seq64 needs an uncompressed rom. The utility used by OoT Rando works.

* Sekaiju https://openmidiproject.opal.ne.jp/Sekaiju_en.html - A GM 1 compatible MIDI editor. People seem to recommend it for setting loop points. IDK if Reaper can export loop points yet.

* Anvil Studio 64-bit for Windows https://www.anvilstudio.com/ - An alternative basic MIDI editor. People seem to hate on it but out of the box it is easier to use than Sekaiju. I'm only using it to playback GM 1 MIDIs.



## Setup

> You will need an OoT ROM. ***DO NOT*** ask me or OoT Rando related discords for a rom. You just can't do that. 

For this guide I'm creating a folder on my desktop called `OoT Music Demo`.  I made a `Downloads` folder in there and placed everything above in there.

### Install Downloads

These are the files I have. You may have newer versions downloaded.
* `asinstall.exe`
* `Decompress.exe`
* `Ocarina of Time Soundfont 2.0.1.zip`
* `reaper711_x64-install.exe`
* `Sekaiju8.0.zip`
* `seq64_v1.5.zip`
* `TX16Wx Software Sampler 3.6.0h x64.msi`

Double click `reaper711_x64-install.exe` and follow the wizard. If Reaper opens after the install finishes, **close it** for now.

Double click `TX16Wx Software Sampler 3.6.0h x64.msi` and follow the wizard.

(Optional) Double click `asinstall.exe` (anvil studio) and follow the wizard. 

(Optional) Double click `Sekaiju8.0.zip`. Drag `Sekaiju8.0` into `OoT Music Demo` to extract it.

![Drag to unzip](Importing-Midi-into-OoT-with-help-from-Reaper/drag_unzip_sekaiju.png)

Right click `seq64_v1.5.zip`. Select *`Extract All...`*. Press the **`Extract`** button without changing the path. Now drag the `seq64_v1.5` folder into `OoT Music Demo` to move it.

![Right click extract all](Importing-Midi-into-OoT-with-help-from-Reaper/extract_all_seq64.png)

Drag `Decompress.exe` into `OoT Music Demo` to move it.

Double click `Ocarina of Time Soundfont 2.0.1.zip`. Drag the `Soundfonts` folder into `OoT Music Demo` to extract it. Go back to `OoT Music Demo`. Do a slow double click or right click → *`Rename`* `Soundfonts` and change its name to `OoT_Soundfonts_2.0.1`.

### Decompress ROM

> *Don't make me tap the sign!*

In `OoT Music Demo` I made the folder `rom`. I made a copy of my rom and placed it in this folder.

Press <kbd>win</kbd>+<kbd>r</kbd> to open the Windows Run dialogue. Type `cmd` and press enter. A black terminal window should appear. *DON'T PANIC*. Drag `Decompress.exe` onto this window. Type a space (` `) into the window. Drag your rom onto the window. Press the <kbd>enter</kbd> key. This should create a `-decomp` (decompressed not decompiled) rom next to your original rom.

![Decompress rom](Importing-Midi-into-OoT-with-help-from-Reaper/decompress_rom.png)

We will need this decompressed rom later.

### Getting a MIDI
For this demo I will be using `town.mid` that comes with Windows. Paste `C:\Windows\Media` into the Windows Explorer address bar and press enter.

![Explorer Address Bar](Importing-Midi-into-OoT-with-help-from-Reaper/explorer_address_bar.png)

Find `town.mid` and copy it into `OoT Music Demo`. Rename the copy to `town_original.mid`.

Double clicking it should open it in Windows Media Player for playback. You could also open it in Sekaiju or Anvil Studio and hit play in there.

## Importing a MIDI into Reaper

### Open Reaper
The first time you launch it, it may take a small bit. If you have not closed Reaper since installing TX16Wx, close Reaper and then open it again.

### Make a new project
Make sure you're starting with a new project. *`File → New project`*

![new project](Importing-Midi-into-OoT-with-help-from-Reaper/new_project.png)

**Immediately** save the new empty project. <kbd>ctrl</kbd>+<kbd>s</kbd>. I'm saving my project to `OoT Music Demo` and calling it `town_oot_port`. **CHECK** the *`Create subdirectory for project`* box! Also **CHECK** the *`Copy all media into project directory`* box!

![Save Project](Importing-Midi-into-OoT-with-help-from-Reaper/save_project.png)

Continue to save regularly.

### Import the MIDI
Drag `town_original.mid` onto the start of the timeline.

![](Importing-Midi-into-OoT-with-help-from-Reaper/drag_midi.png)

Leave the *`Expand 11 MIDI tracks to new REAPER tracks`* and *`Import MIDI tempo map to project tempo map at 1.1.00`* boxes checked. Press the **`OK`** button.

![](Importing-Midi-into-OoT-with-help-from-Reaper/midi_file_import.png)

Your timeline Reaper window should now look like this:
![](Importing-Midi-into-OoT-with-help-from-Reaper/first_timeline.png)

<kbd>ctrl</kbd>+<kbd>s</kbd>.

### Reopening your project
After saving you can close Reaper. Launching Reaper again will open the last used project. You can also double click the `OoT Music Demo\town_oot_port\town_oot_port.rpp` project file from Windows Explorer or find it in the *`File → Open project...`* menu inside Reaper.

### Reaper Basics
https://www.reaper.fm/guides/REAPER%20Quick%20Start.pdf

### Assigning playback instruments