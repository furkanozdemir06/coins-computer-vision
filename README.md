# 🪙 Coin Detection and Counting with OpenCV

A classical computer vision pipeline that detects and counts coins in an image using OpenCV. No deep learning or training data is required: the workflow relies on image preprocessing, edge detection, and contour analysis, which makes it transparent and computationally light.

## Overview

Automated coin detection is useful for smart vending systems, currency counters, retail automation, and visual inventory management. This project walks through a complete detection workflow, from loading an image to drawing the detected coins and reporting how many there are.

## Highlights

- End-to-end OpenCV pipeline: grayscale, Gaussian blur, Canny edges, contour detection, and area filtering
- Automatic coin counting (8 coins detected in the sample image)
- Visual outputs at each stage: edges, contours, enclosing circles, and bounding boxes with contour areas
- Lightweight and fully explainable, with no model training

## Pipeline

1. **Image loading:** reads all `coin*.png` images into a pandas Series with `cv2.imread`.
2. **Preprocessing:** converts the image to grayscale and applies a Gaussian blur (11x11 kernel) to suppress noise.
3. **Edge detection:** applies the Canny edge detector with thresholds 30 and 150.
4. **Contour detection:** finds external contours with `cv2.findContours` (`RETR_EXTERNAL`).
5. **Noise filtering:** keeps only contours with an area above 150 pixels, removing small artifacts.
6. **Counting and visualization:**
   - Counts the remaining contours as coins.
   - Draws the minimum enclosing circle of each coin.
   - Draws bounding boxes labeled with each contour's pixel area.

## Results

The sample image (317 x 612 pixels) contains 8 coins, the front and back of four coins. The pipeline detects **8 coins**, matching the true count.

One detail worth noting: on the reverse of the smallest coin, the detected contour follows an inner engraving rather than the coin's outer edge. The count is still correct, but this shows a limitation of edge-based detection on coins with detailed designs.

## Tech Stack

- Python
- OpenCV
- NumPy
- pandas
- matplotlib
