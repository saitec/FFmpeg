# Transform

Transform is a video filter that transforms 360 video in equirectangular projection into a cubemap projection

## Building

Transform is implemented as an ffmpeg video filter. To build Transform, follow these steps:

1. Checkout the source for ffmpeg
2. Copy `vf_transform.c` to the libavfilter subdirectory in ffmpeg source
3. Edit `libavfilter/allfilters.c` and register the filter by adding the line: `REGISTER_FILTER(TRANSFORM, transform, vf);` in the video filter registration section
4. Edit `libavfilter/Makefile` and add the filter to adding the line: `OBJS-$(CONFIG_TRANSFORM_FILTER) += vf_transform.o` in the filter section
5. Configure and build ffmpeg as usual

## Results 
The equirectangular video is a 360 video that is laid out flat as below:
![ScreenShot](http://imgur.com/21WobIy)

The Equirectangular to Cubemap filter results in this: 
![ScreenShot](http://imgur.com/9HbcIgz)

## Running

Check out the options for the filter by running `ffmpeg -h filter=transform`
A typical execution would be something like `ffmpeg -i input.mp4 -vf transform=input_stereo_format=MONO:w_subdivisons=4:h_subdivisons=4:max_cube_edge_length=512`
