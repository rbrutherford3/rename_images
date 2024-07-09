# rename_images

Bash script for renaming images to a standard format using dates.

Requires installation of ExifTool ([Install here](https://exiftool.org/install.html#Unix)).

If you want to standardize your image file collection and have your image names match the EXIF data creation date, then this is the tool for you. 

## Install

Manually download the files in this repository to any directory or clone the repository using git. The main file is `rename_images` which calls `rename_file`, which can be used as a standalone file renamer. `chmod` all bash scripts in the repository to be executable.

## Usage

Call `rename_images` with a root directory containing your image files as a parameter like:
```
/path/to/script/rename_images /path/to/root
```
It will then recursively loop through all the files in the directory and:
1. Change the filename if there is an EXIF creation date
2. If there is no EXIF creation date but a date in the filename, then the EXIF date will be updated according ot the perceived date and the filename chanaged like so:

```
IMG_yyyymmdd_HHMMSS.ext
SS_yyyymmdd_HHMMSS.ext (screenshot, if indicated in filename)
VID_yyyymmdd_HHMMSS.ext
```

Example filenames:

```
IMG_20160905_023455.jpg
SS_20240826_120537.png
VID_20001208_223614.mp4
```

## Additional files

### rescue_images

Certain corruptions were found in the filename dates after running `rename_images` that needed to be tended to. The first part of the year ("20") was present but the final two digits were cut off. Further investigation showed that it was from the current year, so this script does the same thing as `rename_images` for those special scenarios. To be used with caution. See comments for more information.

### flatten_directory

This script simply moves all files in the subdirectories of a given root directory to the root without overwriting files, and then deletes all the empty subdirectories. To be used like:
```
/path/to/script/flatten_directory /path/to/root
```

## To-do

1. Modify `rename_images` and `rescue_images` to only process image files by evaluating the file extension.
2. Modify `rename_images` and `rescue_images` to allow custom filename formats.
