# Create slideshow from starred pictures
I have a bunch of pictures on my NAS, but only a few of them are starred with Rating with 4 or more.
To show only these pictures from my TV, I thought to create some *.wpl files with a playlist of them.

## Install EXIF Tool
I use the [exiftool](http://www.sno.phy.queensu.ca/~phil/exiftool/) to retrieve the ratings (or tags or anything from EXIF header data).

```bash
brew install exiftool
```

## Create a WPL file
I have written the following bash script to find files with Ratings >= 4 and put them into a WPL file.

First I switch to the directory from where I want to create the WPL file.

```bash
cd /Volumes/Public/Shared\ Pictures/
```

Then start the script with the directory tree to search in, the name of the target WPL file in the current dir and a title text.

```bash
find-starred-photos.sh 2012 2012-rated-pictures.wpl "Bilder 2012"
```

Such a WPL file looks like this:

```xml
<?wpl version="1.0"?>
<smil>
<head>
<meta name="Generator" content="Twonky"/>
<meta name="IsNetworkFeed" content="0"/>
<meta name="IsUserGenerated" content="1"/>
<meta name="Type" content="P"/>
<title>Urlaub 2012 in der Toskana</title>
</head>
<body>
<seq>
<media src="2012/2012-05-26/DSCF0372.JPG"/>
<media src="2012/2012-06-09/DSCF0915.JPG"/>
</seq>
</body>
</smil>
```

## The script find-starred-photos.sh
Here is the bash script code:

```bash
#!/bin/bash

function usage {
  echo "Usage: $0 dirname wplfile \"your title\""
  exit 0
}

if [ "$#" -ne 3 ]; then
  usage
fi

if [ ! -d "$1" ]; then
  usage
fi

tee $2 <<EOF
<?wpl version="1.0"?>
<smil>
<head>
<meta name="Gener$ator" content="Twonky"/>
<meta name="IsNetworkFeed" content="0"/>
<meta name="IsUserGenerated" content="1"/>
<meta name="Type" content="P"/>
EOF
echo "<title>$3</title>" >>$2

tee -a $2 <<EOF
</head>
<body>
<seq>
EOF

# write files in file to avoid problem with blanks in file names
find "$1" -type f -print | sort >/tmp/files$$
while read f; do
  rating=`exiftool "$f" |grep Rating | grep -v Percent | sed -e 's/.*: //'`
  if [ "$rating" != "" ]; then
    if [ "$rating" -ge "4" ]; then
      echo "Picture $f has rating $rating"
      echo "<media src=\"$f\"/>" >>$2
    fi
  fi
done < /tmp/files$$
rm /tmp/files$$

tee -a $2 <<EOF
</seq>
</body>
</smil>
EOF

echo "Done!"
```
