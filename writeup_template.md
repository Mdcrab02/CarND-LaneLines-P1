# Finding Lane Lines on the Road

## Introduction

This is the first project for the Self-Driving Car nanodegree on Udacity.

---

## Purpose

The goals / steps of this project are the following:

* Make a pipeline that finds lane lines on the road for both pictures and videos
* Adjust the pipeline to draw long single lines for each side of the lane
* Reflect on my work in this written report

---

## Reflection

My pipeline consisted of 7 steps:

1. The images are converted into their grayscale equivalents.
2. The Gaussian transform is performed on each image so the gradients can be seen.
3. The Canny edge detection algorithm is used to detect the edges in the image.  I followed one of the recommended threshold rules (1:3)
4. A region similar to a trapezoid is mapped on the image by hard-coding vertices of the shape.
5. All edges found outside the aforementioned shape are masked.
6. The Hough transform is performed on the unmasked edges in order to identify the lane lines.
7. The image with the Hough lines is then overlayed atop the original image.

The first pass of this process involved only drawing lines in segments where lane lines were found.  This means that a solid line was drawn as a solid line, and a segment was drawn as a segment.

### Modifying draw_lines()

In order to draw the lane line as a single line on both sides based on the actual lane lines and segments, the draw_lines() function had to be modified.  I modified it based on the idea that the lines in Image Space are represented with found points, and their associated lines in Hough Space will intersect.  I also had to include:

* A small buffer of 10 to account for the front of the car in the video
* Only taking the gradient from two points if that gradient is less than infinity

---

## Potential Shortcomings

While I made some changes and improvements to draw_lines(), there are still some strange things happening to the processing of the videos:

* Sometimes lane lines move erratically when light levels at a distance change rapidly.
* Lane lines in the challenge video have serious difficultly being computed presumably due to the tree line and changes/faults in the road.


## Possible Improvements

Some possible improvements could be some adjustments to the region of interest (the shape containing unmasked lines).  I wonder if this in combination to some minor changes in the Canny thresholds and parameters for the Gaussian transform could eliminate erratic line behavior.  I also suspect that some slow performance issues might be remedied by changing the nested conditional logic in draw_lines() to something more efficient.
