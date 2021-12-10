# docs-rosbag2img_exporter
This documentation is prepared to export image files from /image_raw/compressed topic in a rosbag.

## Dependencies
This doc requires that you have previously recorded a bag file which contains compressed image data you would like to export as jpeg images or video. Additionally, this tutorial requires that the image_view package has been built and a few video utilities are installed:
```
roscd image_view
rosmake image_view
sudo apt-get install mjpegtools
```

Run `bag2img_export.launch` file to export individual jpeg files under `.ros` in your home directory.
```
roslaunch bag2img_export.launch
```

The image file can be moved to any desired directory as follows:

```
cd ~
mkdir test
mv ~/.ros/frame*.jpg test/
```

## Converting jpegs into an MP4 video

If your camera was running at 15 frames per second then you would execute the following in a shell for reasonable results.

```
cd ~/test
ffmpeg -framerate 25 -i frame%04d.jpg -c:v libx264 -profile:v high -crf 20 -pix_fmt yuv420p output.mp4
```
