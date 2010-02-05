# bash scripts for doing various file conversions

## File Descriptions

### flac-mp3

- Description: Converts a single flac file into an mp3 file
- Usage: flac-mp3 FLACFILE
- Example: flac-mp3 music.flac
- Dependencies: flac, metaflac, lame

### flac-ogg

- Description: Converts a single flac file into an ogg file
- Usage: flac-ogg FLACFILE
- Example: flac-ogg music.flac
- Dependencies: flac, metaflac, oggenc

### flac2mp3

- Description: Converts an entire directory of flac files into a directory of mp3 files
- Usage: cd DIRECTORY; flac2mp3
- Example: cd album/; flac2mp3
- Dependencies: flac, metaflac, lame

### flac2ogg

- Description: Converts an entire directory of flac files into a directory of ogg theora files
- Usage: cd DIRECTORYPATH; flac2ogg
- Example: cd album/; flac2ogg
- Dependencies: flac, metaflac, oggenc

### dir2wav

- Description: Converts all mp3s in the specified directory into wav files in a wav folder.
- Usage: dir2wav DIRECTORYPATH
- Example: dir2wav ./
- Dependencies: mplayer

#### subsequent CD burning steps

1. Name the audio files in a manner that will cause them to be listed in the desired track order when listed alphabetically, such as 01.wav, 02.wav, 03.wav, etc.
2. Use the following command to burn the wav files as an audio CD: 

		$ wodim -v -pad speed=1 dev=/dev/cdrw -dao -swab *.wav

### mencoder2dvd

- Description: Converts a video playable by mplayer into a DVD compliant MPEG (NTFS)
- Usage: mencoder2dvd VIDEOFILE
- Example: mencoder2dvd my_video_1.avi
- Dependencies: mplayer

#### subsequent DVD burning steps

Use the dvdauthor tool to convert the compliant mpg to a DVD structure. Here's the dvdauthor xml configuration I use (I don't care about chapters or any fancy menus):

		<dvdauthor dest="DVD">
		<vmgm />
		 <titleset>
		   <titles>
		     <pgc>
		       <vob file="my_video_1.mpg" chapters="0"/>
		     </pgc>
		    </titles>
		  </titleset>
		</dvdauthor>

A copy of this can be found in the repository. Put this in the same directory as your mpg file and run:

		$ dvdauthor -x dvd.xml

This will create a DVD/ directory with the appropriate DVD directory structure. To burn, use growisofs:

		$ growisofs -Z /dev/dvd -dvd-video DVD/

And you have a playable DVD!

# Author

All scripts are written by Blake Smith <blakesmith0@gmail.com>

# Sources

[Arch Linux CD Burning Tips](http://wiki.archlinux.org/index.php/CD_Burning_Tips)
[LinuxQuestions.org - AVI to DVD](http://www.linuxquestions.org/questions/linux-software-2/avi-to-dvd-358548/)
A bunch of other places too numerous to remember...

