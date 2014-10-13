# Install forked-daapd on the Raspberry Pi

Based on http://www.raspberrypi.org/forums/viewtopic.php?f=66&t=49928
but you can use `apt-get`

## How to install with apt-get
1. Decide if you want the server to support displaying artwork embedded in media files. Support for this means that the install process will upgrade your standard Wheezy libav package to the newer version 9 - and that might be a problem if you have other stuff that depends on the stock version of libav.
2a. So, do you want embedded artwork and libav 9? Then add this line to /etc/apt/sources.list:
deb http://www.gyfgafguf.dk/raspbian wheezy-backports/armhf/
2b. Or do you not want embedded artwork and libav 9? Then add this line to /etc/apt/sources.list:
deb http://www.gyfgafguf.dk/raspbian wheezy/armhf/
3. Run sudo apt-get update and then sudo apt-get install forked-daapd
4. Edit the config file /etc/forked-daapd.conf and (re)start the server with sudo /etc/init.d/forked-daapd restart


```bash
$ sudo vi /etc/apt/sources.list
$ cat /etc/apt/sources.list
deb http://archive.raspbian.org/raspbian wheezy main contrib non-free
deb http://www.gyfgafguf.dk/raspbian wheezy/armhf/

$ sudo apt-get update
$ sudo apt-get install forked-daapd
$ cd /etc/forked-daapd.conf 
$ vi /etc/forked-daapd.conf 
```

Enter in `/etc/fstab`

```
//192.168.xxx.yyy/Private /media/mybooklive cifs uid=1002,gid=1000,file_mode=0644,dir_mode=0755,rw,credentials=/root/mybooklive-credentials 0 0
```

Enter in /etc/mtab

```
//192.168.xxx.yyy/Private /media/mybooklive cifs rw,relatime,vers=1.0,sec=ntlm,cache=loose,unc=\\192.168.xxx.yyy\Private,username=linux,uid=1002,forceuid,gid=1000,forcegid,addr=192.168.xxx.yyy,file_mode=0644,dir_mode=0755,nounix,serverino,rsize=61440,wsize=65536,actimeo=1 0 0
```

Enter in /root/mybooklive-credentials

```
$ sudo cat /root/mybooklive-credentials
username=linuxxx
password=xxxxxxx
```

```bash
$ sudo vi /root/mybooklive-credentials
$ sudo chmod 400 /root/mybooklive-credentials
$ sudo mkdir /media/mybooklive
$ sudo mount /media/mybooklive
```


Enter in /etc/forked-daapd.conf

```
$ cat forked-daapd.conf

general {
	# Username
	uid = "root"
	logfile = "/var/log/forked-daapd.log"
	# Database location
#	db_path = "/var/cache/forked-daapd/songs3.db"
	# Available levels: fatal, log, warning, info, debug, spam
	loglevel = log
	# Admin password for the non-existent web interface
	admin_password = "unused"
	# Enable/disable IPv6
	ipv6 = no
}

# Library configuration
library {
	# Name of the library as displayed by the clients
	# %h: hostname, %v: version
	name = "My Music on %h"
	# TCP port to listen on. Default port is 3689 (daap)
	port = 3689
	# Password for the library. Optional.
#	password = ""

	# Directories to index
	directories = {
            "/media/mybooklive/Musikarchiv/FLAC/Stefan",
            "/media/mybooklive/Musikarchiv/FLAC/Katja",
            "/media/mybooklive/Musikarchiv/FLAC/Carina",
            "/media/mybooklive/Shared Music/Stefan",
            "/media/mybooklive/Shared Music/Katja",
            "/media/mybooklive/Shared Music/Carina"
        }

	# Directories containing podcasts
	# For each directory that is indexed the path is matched against these
	# names. If there is a match all items in the directory are marked as 
	# podcasts. Eg. if you index /srv/music, and your podcasts are in
	# /srv/music/Podcasts, you can set this to "/Podcasts".
	# (changing this setting only takes effect after rescan, see the README)
	podcasts = { "/Podcasts" }

	# Directories containing audiobooks
	# For each directory that is indexed the path is matched against these
	# names. If there is a match all items in the directory are marked as 
	# audiobooks.
	# (changing this setting only takes effect after rescan, see the README)
	audiobooks = { "/Audiobooks" }

	# Directories containing compilations (eg soundtracks)
	# For each directory that is indexed the path is matched against these
	# names. If there is a match all items in the directory are marked as 
	# compilations.
	# (changing this setting only takes effect after rescan, see the README)
	compilations = { "/Compilations" }

	# Compilations usually have many artists, and if you don't want every
	# artist to be listed when artist browsing in Remote, you can set
	# a single name which will be used for all music in the compilation dir
	# (changing this setting only takes effect after rescan, see the README)
	compilation_artist = "Various artists"

	# There are 5 default playlists: "Library", "Music", "Movies", "TV Shows"
	# and "Podcasts". Here you can change the names of these playlists.
#	name_library    = "Library"
#	name_music      = "Music"
#	name_movies     = "Movies"
#	name_tvshows    = "TV Shows"
#	name_podcasts   = "Podcasts"
#	name_audiobooks = "Audiobooks"

	# Artwork file names (without file type extension)
	# forked-daapd will look for jpg and png files with these base names
#	artwork_basenames = { "artwork", "cover", "Folder" }
	artwork_basenames = { "artwork", "cover", "Folder", "folder" }

	# File types the scanner should ignore
	# Non-audio files will never be added to the database, but here you
	# can prevent the scanner from even probing them. This might improve
	# scan time. By default .db and .ini are ignored.
#	filetypes_ignore = { ".db", ".ini" }

	# Disable startup file scanning
	# When forked-daapd starts it will do an initial file scan of your
	# library (and then watch it for changes). If you are sure your library
	# never changes while forked-daapd is not running, you can disable the
	# initial file scan and save some system ressources. Disabling this scan
	# may lead to forked-daapd's database coming out of sync with the
	# library. If that happens read the instructions in the README on how
	# to trigger a full rescan.
#	filescan_disable = false

	# Should iTunes metadata override ours?
#	itunes_overrides = false

	# Formats: mp4a, mp4v, mpeg, alac, flac, mpc, ogg, wma, wmal, wmav, aif, wav
	# Formats that should never be transcoded
#	no_transcode = { "alac", "mp4a" }
	# Formats that should always be transcoded
#	force_transcode = { "ogg", "flac" }
}

# Local audio output
audio {
	# Name - used in the speaker list in Remote
	nickname = "AirPlay aus"
	# Audio device name for local audio output
#	card = "default"
	# Mixer channel to use for volume control - ALSA/Linux only
	# If not set, PCM will be used if available, otherwise Master.
#	mixer = ""
}

# AirPlay/Airport Express device settings
# (make sure you get the capitalization of the device name right)
#airplay "My AirPlay device" {
	# forked-daapd's volume goes to 11! If that's more than you can handle
	# you can set a lower value here
#	max_volume = 11
	# AirPlay password
#	password = "s1kr3t"
#}

# Spotify settings (only have effect if Spotify enabled - see README/INSTALL)
spotify {
	# Directory where user settings should be stored (credentials)
#	settings_dir = "/var/cache/forked-daapd/libspotify"
	# Cache directory
#	cache_dir = "/tmp"
	# Set preferred bitrate for music streaming
	# 0: No preference (default), 1: 96kbps, 2: 160kbps, 3: 320kbps
#	bitrate = 0
}
```
