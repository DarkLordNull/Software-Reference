# ffmpeg

## .mp4 to .mp3

    ffmpeg -i input.mp4 -f mp3 -vn -ss 00:00:00 -to 00:01:00 output.mp3

* `-f mp3`: sets mp3 as the output file format
* `-vn`: disables video from the output
* `-ss`: start position, in seconds or in `hh:mm:ss[.xxx]` form
* `-to`: stop position, in seconds or in `hh:mm:ss[.xxx]` form (alternatively, use `-t` instead of `-to` to set the duration; `-t` has priority)

`-ss`, `-to`, and -`t` are can be omitted to use the entire duration.

## .mp4 to .gif

Basic command (moderate quality):

    ffmpeg -i input.mp4 -r 20 -s 320x180 -ss 00:00:00 -to 00:01:00 output.gif

* `-r 20`: 20 frames per second (good quality)
* `-s 320x180`: frame size in width x height format

For better quality, use a palette:

    ffmpeg -i input.mp4 -vf fps=20,scale=320:-1:flags=lanczos,palettegen palette.png -ss 0 -to 00:01:00

    ffmpeg -i input.mp4 -i palette.png -ss 0 -to 00:01:00 -lavfi "fps=20,scale=320:-1:flags=lanczos[x];[x][1:v]paletteuse" output.gif

The first command generates `palette.png`, which is used by the second command to generate the .gif. `scale=320:-1` scales the output to 320 pixel width and the required height to maintain the aspect ratio from the input.

## Cropping

    ffmpeg -i input.gif -filter:v "crop=320:180:20:0" output.gif

Here the crop arguments specify the following:

* `320` is the width of the cropped output
* `180` is the height of the cropped output
* `20` is the x-position of the upper left corner of the cropped output
* `0` is the y-position of the upper left corner of the cropped output

## Detecting silence

[How to split an mp3 file by detecting silent parts?](https://askubuntu.com/q/1264779/1114164)

## Merge audio and video files

See [How to merge audio and video file in ffmpeg](https://superuser.com/questions/277642/how-to-merge-audio-and-video-file-in-ffmpeg) on Super User.
