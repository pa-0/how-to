
```
ooooo   ooooo   .oooooo.   oooooo   oooooo     oooo         ooooooooooooo   .oooooo.   
`888'   `888'  d8P'  `Y8b   `888.    `888.     .8'          8'   888   `8  d8P'  `Y8b  
 888     888  888      888   `888.   .8888.   .8'                888      888      888 
 888ooooo888  888      888    `888  .8'`888. .8'                 888      888      888 
 888     888  888      888     `888.8'  `888.8'     8888888      888      888      888 
 888     888  `88b    d88'      `888'    `888'                   888      `88b    d88' 
o888o   o888o  `Y8bood8P'        `8'      `8'                   o888o      `Y8bood8P'  
```
A cheat sheet for common data journalism stuff. For details on installing these tools, [see how I work](http://mtdukes.com/work.html).

# Command line tools
A collection of tips and tricks for working with tools executed using bash terminals.

## grep
Search text files for specific character sequences.

### Basic search

```bash
grep "DUKES" absentee.csv
```
Return lines containing a string from a specified file and print to the command line.

### Print to a file
```bash
grep "\"DUKES\",\"MICHAEL\",\"TYLER\"" absentee.csv > dukes.csv
```
Search for a string with quotes and output all lines to a file.

## head/tail
Get a preview of a file.

### See the top
```bash
head absentee.csv
```
Print the first 10 lines of a file to the command line.

### Specify the number of lines

```bash
head -1 absentee.csv > absentee_header.csv
```
Get the first line of a file and save it to a CSV file.

## ffmpeg
A power tool for processing and converting video and audio files.

### Make a GIF
```bash
ffmpeg -ss 5 -t 1.7 -i video.MOV -vf "fps=24,scale=640:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 video.gif
```
Create a high quality GIF 640 pixels wide at 24 frames per second using the specified video file, skipping 5 seconds and lasting 1.7 seconds and save the output.

### MOV to mp4
```bash
ffmpeg -i apple.mov -vcodec h264 -acodec aac apple.mp4
```
Use a codec flag to convert a video file from QuickTime to the more universal mp4 format.

### AVI to mp4
```bash
ffmpeg -i full_video.avi full_video.mp4
```
Convert an AVI file to the more universal mp4 format.

### Combine video clips
```bash
ffmpeg -f concat -safe 0 -i vidlist.txt -c copy full_video.avi
```
Combine all of the files recorded in a text file called `vidlist.txt`, which looks like this:
```
file '/Users/username/directory/vid_seq001.avi'
file '/Users/username/directory/vid_seq002.avi'
```
## pdftk
A power tool for processing and converting PDF files.

### Combine files
```bash
pdftk *.pdf cat output all_documents.pdf
```
Combine all the PDF files in the present directory into a single file. *Note: check to make sure the capitalization of the filetype matches.*

## esridump
[A targeted utility](https://github.com/openaddresses/pyesridump) to pull down geographic data from ESRI maps.

### Download a geojson
```bash
esri2geojson https://services.arcgis.com/iFBq2AW9XO0jYYF7/arcgis/rest/services/Covid19byZIPnew/FeatureServer/0 nc_zipDATE.geojson
```
Download data from the ESRI REST endpoint that powers the N.C. DHHS COVID map of cases by zip code and save it as a geojson file.

## wget
A power tool for recursively downloading files, for example from the Web.

### Download a single file
```bash
wget http://mtdukes.com/work.html
```
Saves the file from the specified URL.

### Download a list of files
```bash
wget -i file_list.txt
```
Saves individual files from URLs specified in a TXT file, one URL on each line.

## file
Tool to do various file formatting things I think.

### Detect encoding of a file
```bash
file -I input.csv
```
Detect encoding of a file.