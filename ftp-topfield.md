# ftp-topfield

## Introduction

I have an old Topfield TF5000PVR Masterpiece hard disk receiver with only an USB connector.
But behind my TV there is a Raspberry Pi which is some kind of hardware glue for everything.
I have installed the [ftp-topfield](http://www.nslu2-linux.org/wiki/Puppy/FtpdTopfield) tool onto it and connected the USB cable of the Topfield to the Raspberry Pi.

From my Mac or other computer I can connect via FTP over WiFi and download some recorded videos.

## Connect from command line

```
ftp ftp://raspbmc.local:2021
```

## Turbo mode

To speed up the download you can turn on the turbo mode. The USB connector is not quite an USB2 connector, but turning on the turbo mode

```
site turbo
```

## Installation

### xinetd.d/ftp-topfield

```
$ cat /etc/xinetd.d/ftp-topfield 
service ftpd-topfield
{
  type            = UNLISTED
  socket_type     = stream
  protocol        = tcp
  port            = 2021
  server          = /usr/sbin/ftpd-topfield
  server_args     = --port=2021 --logging
  wait            = no
  user            = root
  disable         = no
  instances       = 1
}
```

### bash history
Here is my bash history as I don't remember exactly how to set this up.

```
5  lsusb
6  grep 11db /lib/udev/rules.d/* /etc/udev/rules.d/*
7  sudo addgroup --system toppy
8  sudo adduser pi toppy
9  sudo echo 'ATTRS{idVendor}=="11db", ATTRS{idProduct}=="1000",GROUP="toppy"' >/etc/udev/rules.d/10-topfield-pvr.rules
10  sudo udevadm control --reload
11  sudo udevadm trigger
18  curl http://birdman.dynalias.org/cgi-bin/tdl.cgi/armv5tel/puppy-new_dev_scan-static -o puppy
19  curl http://birdman.dynalias.org/cgi-bin/tdl.cgi/armv5tel/ftpd-new_dev_scan-static -o ftpd
20  which ftpd
21  ls /usr/local/bin/
22  sudo curl http://birdman.dynalias.org/cgi-bin/tdl.cgi/armv5tel/puppy-new_dev_scan-static -o /usr/local/bin/puppy
23  sudo curl http://birdman.dynalias.org/cgi-bin/tdl.cgi/armv5tel/ftpd-new_dev_scan-static -o /usr/local/bin/ftpd
25  chmod +x ftpd puppy 
26  sudo mv ftpd /usr/local/bin
27  sudo mv puppy /usr/local/bin
28  sudo mv /usr/local/bin/ftpd /usr/local/bin/ftpd-topfield
32  ldd /usr/local/bin/puppy 
33  ls -l /usr/local/bin/puppy 
34  sudo curl http://birdman.dynalias.org/cgi-bin/tdl.cgi/armv5tel/puppy-new_dev_scan-static -o /usr/local/bin/puppy
36  ls -l /usr/local/bin/
37  vi /usr/local/bin/puppy 
38  /usr/local/bin/puppy 
39  curl http://birdman.dynalias.org/cgi-bin/tdl.cgi/armv5tel/puppy-new_dev_scan-static -o puppy
40  curl http://birdman.dynalias.org/cgi-bin/tdl.cgi/armv5tel/ftpd-new_dev_scan-static -o ftpd-topfield
42  ./puppy
43  chmod +x puppy ftpd-topfield 
44  ./puppy 
45  ./ftpd-topfield 
46  ls -l
47  file puppy 
48  ./puppy 
49  ldd puppy 
50  uname -a
51  mkdir download
52  cd download
53  curl http://birdman.dynalias.org/Toppy/R2-D2/sources/ftpd-topfield-0.7.7p.tar.gz -o ftpd-topfield-0.7.7p.tar.gz
54  curl http://birdman.dynalias.org/Toppy/R2-D2/sources/puppy_1.14p.tar.bz2 -o puppy_1.14p.tar.bz2
55  ls -l
56  tar tzvf ftpd-topfield-0.7.7p.tar.gz 
57  tar xzvf ftpd-topfield-0.7.7p.tar.gz 
58  ls
59  tar tzvf puppy_1.14p.tar.bz2 
60  tar tJvf puppy_1.14p.tar.bz2 
61  tar tjvf puppy_1.14p.tar.bz2 
62  ls -l
63  tar --help |grep bz
64  tar tjvf puppy_1.14p.tar.bz2 
65  sudo apt-get install bzip2
66  tar tjvf puppy_1.14p.tar.bz2 
67  tar xjvf puppy_1.14p.tar.bz2 
68  sudo apt-get install build-essentials
69  gcc
70  sudo apt-get install build-essential
71  sudo apt-get install libusb-dev
72  ls
73  cd ftpd-topfield-0.7.7p
74  make OLD_DEV_SCAN=1 USE_LIBUSB=1
75  ls
76  ls -ltr
77  sudo make install
78  cd ..
79  cd puppy_1.14p
80  ls
81  make OLD_DEV_SCAN=1 USE_LIBUSB=1
82  ls
83  sudo make install
84  sudo cp puppy /usr/local/bin/puppy
85  ls
86  cd ..
87  puppy
88  cd ..
89  ls
90  rm puppy ftpd-topfield 
91  puppy -c size
92  ls /proc/
93  cd download/
94  ls
95  cd puppy_1.14p
96  ls
97  make clean
98  make OLD_DEV_SCAN=1 
99  ./puppy -c size
100  grep bus *
101  ls /dev/bus/usb/
102  ls
103  grep proc *
104  vi puppy.c 
105  make
106  ./puppy -c size
107  make clean
108  make OLD_DEV_SCAN=1 
109  ./puppy -c size
110  ls /dev/bus/usb/
111  ls /dev/bus/usb/001/00
112  ls -l
113  vi puppy.c 
114  make OLD_DEV_SCAN=1 
115  ./puppy -c size
116  lsusb
117  ./puppy -c size
118  ls -l
119  make clean
120  make
121  ./puppy -c size
122  make clean
123  make OLD_DEV_SCAN=1 USE_LIBUSB=1
124  ./puppy -c size
125  vi puppy.c 
126  ls -l /dev/bus/usb/
127  ls -l /dev/bus/usb/001/
128  ls -l /dev/bus/usb/001/001 
129  ls -l /dev/bus/usb/001/002
130  ls -l /dev/bus/usb/001/003
131  ls -l /dev/bus/usb/001/004
132  ls -l /dev/bus/usb/001/005
133  lsusb
134  ls /dev/bus/usb
135  ls /dev/bus/usb/001
136  ls -l /dev/bus/usb/001
137  ls -l /dev/bus/usb/001/007
138  ls /dev/bus/usb/001/007
139  lsusb
140  vi /etc/udev/rules.d/10-permissions.rules 
141  sudo echo 'ATTRS{idVendor}=="11db", ATTRS{idProduct}=="1000",GROUP="toppy"' >/etc/udev/rules.d/10-topfield-pvr.rules
142  cd 
143  echo 'ATTRS{idVendor}=="11db", ATTRS{idProduct}=="1000",GROUP="toppy"' >10-topfield-pvr.rules
144  sudo cp 10-topfield-pvr.rules /etc/udev/rules.d/10-topfield-pvr.rules
145  ls -l /etc/udev/rules.d/
146  sudo udevadm control --reload
147  sudo udevadm trigger
148  ls -l /dev/bus/usb/001
149  cd download/puppy_1.14p
150  ./puppy -c size
151  make OLD_DEV_SCAN=1 
152  make clean
153  make OLD_DEV_SCAN=1 
154  ls /dev/bus/usb/001/007 
155  cat /dev/bus/usb/001/007 
156  PuTTYPuTTY
157  xxd /dev/bus/usb/001/007 
158  vi puppy.c 
159  ls
160  ls -l
161  ls /usr/local/bin
162  sudo rm /usr/local/bin/ftpd-topfield 
163  sudo rm /usr/local/bin/puppy 
164  sudo cp puppy /usr/local/bin/puppy
165  cd ..
166  puppy
167  puppy -c size
168  rehash
169  puppy -c size
170  cd download/puppy_1.14p
171  ls
172  ./puppy -c size
173  ls -l
174  ls /dev/bus/usb/001
175  ls -l /dev/bus/usb/001/
176  puppy -c size
177  which puppy
178  puppy -c size
179  ./puppy -c size
180  exit
181  passwd
182  df
183  cd download/
184  ls
185  cd puppy_1.14p
186  vi puppy.c 
187  make clean
188  make
189  ls
190  cp puppy.c puppy.c.try-ss
191  cd ..
192  tar xjvf puppy_1.14p.tar.bz2 
193  cd puppy_1.14p
194  make clean
195  make
196  ./puppy -c size
197  cd ..
198  cd ftpd-topfield-0.7.7p
199  ls
200  make clean
201  make
202  cd ..
203  cd puppy_1.14p
204  ls
205  make clean
206  make
207  ./puppy -c size
208  ls -l puppy
209  sudo cp puppy /usr/local/bin/puppy
210  ./puppy -c size
211  strace ./puppy -c size
212  cd ../ftpd-topfield-0.7.7p
213  ls
214  sudo make install
215  exit
216  ftp pi@raspbmc 2021
217  sudo apt-get install ftp
218  ftp pi@raspbmc 2021
219  ftp localhost 2021
220  sudo apt-get install xinetd
221  ftp localhost 2021
222  which ftpd-topfield
223  sudo /etc/init.d/xinetd restart
224  ftp localhost 2021
225  exit
226  puppy -c size
227  ls
228  ls -l
229  ls -l /usr/sbin/ftpd-topfield 
230  sudo ftpd-topfield -D -P 2021 -d
231  sudo vi /etc/xinetd.d/ftp-topfield
232  ls
233  cd
234  mkdir scripts
235  vi scripts/toppy-add.sh
236  chmod +x scripts/toppy-add.sh 
237  vi scripts/toppy-add.sh 
```
