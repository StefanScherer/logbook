# Sync photos on iPad

Apple makes us very hard to sync photos on the iPad, especially if you want them sorted by date. Once upon a time ... there was iOS 3 and everything was fine ;-)

Here is my way to sync my photos.

* Import photos from SD card with Windows Live Photo Gallery.
* If you have photos with a wrong date, you can use `Bearbeiten` -> `Zeit anpassen` and change / shift the date for a bulk of photos.
* Mark good photos with eg. four stars.
* Filter all good photos with eg. four stars.
* Press `Ctrl + A` to select all (good) photos.
* Copy all of these photos in a special folder, eg. `F:\iPad\Fotos\2014\`
* Fix creation date of all these photos with this Perl script `fixdates.pl` and the exiftool

```perl
use Win32API::File::Time qw{:win};
use Image::ExifTool qw(:Public);
use Date::Parse;
opendir(DIR, ".");
@files = readdir(DIR);
close(DIR);
foreach $file (@files) {
  next if $file !~ /.+\.jpe?g$/i;
  my $tag = "CreateDate";
  $values = ImageInfo($file, $tag);
  $value = $$values{$tag};
  # can be a different name !!! # http://search.cpan.org/~exiftool/Image-ExifTool-8.50/lib/Image/ExifTool.pod#ImageInfo
  print "Setting $file file creation date to $value\n";
  $time = str2time($value);
  if (! SetFileTime($file, undef, undef, $time) ) {
    warn "Error occured: $^E\n";
  }
}
print "Done!\n";

* Open a cmd shell, change to the directory

```
cd /D F:\iPad\Fotos\2014
perl ..\..\fixdates.pl
```

* Open iTunes
* Connect your iPad
* Click on the iPad and open the Pictures tab.
* Import all photos of current year (2014). 
* If you append new photos in a folder, remove it first from iPad, then add it again. Otherwise old photos still will be appended at the end and the folder seems to be out of order on iPad.

