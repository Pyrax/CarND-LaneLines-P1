# **Finding Lane Lines on the Road** 

## Writeup 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[pipeline2]: docs_media/pipeline_2_gaussian_blur_grayscale.jpg "Blurred grayscale image"
[pipeline3]: docs_media/pipeline_3_canny_edges.jpg "Image with canny edges"
[pipeline6]: docs_media/pipeline_6_final_result.jpg "Result with lanes and region of interest"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. First, I converted the images to grayscale and then applied a gaussian blur afterwards 
to smoothen it.

![Blurred grayscale image][pipeline2]

Thereafter, edges in the grayscale image were detected through the canny edge algorithm which outputs a binary image. 

![Image with canny edges][pipeline3]

Next, the view of the binary image was restricted to an area by blacking out all pixels which are not in a previously 
defined region of interest. The region has been defined through hard-coded values which were obtained by examining the 
picture's properties.

Then, I calculated the lines through hough transformation and sorted them into the left or right lane by their slopes. 
Furthermore, I fitted the lines associated with each lane to a polynomial of degree 1 to recieve a single straight line
on each side.

As final step, the drawn lines were added to the input image with a mask. For demonstration purposes I included the 
final result combined with the region of interest in this paper:

![Result with lanes and region of interest][pipeline6]

An example of an image passing every step of the pipeline as well as a video with steps of the pipeline can be found 
in the directory [/docs_media](/docs_media).


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming of the pipeline could be lines which run parallel to the current lane lines as they occur at 
intersections, traffic lights and crosswalks. These are likely to be detected by the current pipeline and would falsify 
the result.

Another issue might be bad vision generally caused by environmental influences. Especially fog and snow but also dark 
lighting could make the pipeline fail.

Similarly to bad vision, further problems can be distortion as seen with raindrops, shadows on the road and reflections
where the challenge video already shows examples for the latter two issues.

Also the parameters of the algorithms (e.g. canny edge and hough transform) were fitted using given examples which
means they might perform completely different on images taken from another camera with varying contrast for example.

Lastly, a general shortcoming is the approach of hard-coding the shape of the region of interest because in real-world
applications it might be impractical to have one static region defined beforehand.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be dynamic adjustment of the region of interest based on the actual position of the lanes.

Another improvement would be to add a color mask for yellow and white lines.
