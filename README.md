# Tutorials

## Launch Line
 ` gst-launch-1.0 autovideosrc ! videoconvert ! faceblur ! videoconvert ! autovideosink `
 
 # Running Pipeline
  * source -> tee -> blur -> output -> vertigotv -> output
  
### Tee
  `Tee element` , which allows audio & video streams to be sent to more than one place.
 ### Tee to two local video outputs
Here's a simple example that sends shows video test source twice (using autovideosink)
```
The two windows may overlay on top of each other
gst-launch-1.0 \
    videotestsrc ! tee name=t \
    t. ! queue ! videoconvert ! autovideosink \
    t. ! queue ! videoconvert ! autovideosink
```
 
 ### Vertigotv
 A loopback alpha blending effector with rotating and scaling
 
 # Visualizer 
  
 **Demonstrate audio visualization in GStreamer**
    
  Take any audio file and generate any visualization of your choice.

 - cd into Assignment2 directory
 - Run the following command

       gcc audio_visualisation.c -o audio_visualisation pkg-config --cflags --libs gstreamer-1.0 
 - Run `./audio_visualisation `
 - Choose a visualisation element from the following.
```
1. Synaescope 
2. GOOM 
3. Monoscope
```


# Blur Implementation
* #### Mechanism to add third party or custom algorithms within the reference application by modifying the example plugin (gst-dsexample). The sources for the plugin are in `sources/gst-plugins/gst-dsexample directory` 

To enable OpenCV functionalities , compile dsexample plugin with flag `WITH_OPENCV=1` in the plugin Makefile.

The GStreamer example plugin (gst-dsexample) demonstrates the following:

 - Processing the entire frame, with downscaling / color conversion if required.

- Processing objects detected by the Primary Detector, specifically, cropping these objects from the frame and then processing the crops.

- In-place modification of the buffer frame contents using OpenCV
