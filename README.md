# Image Stitching using ORB Feature Matching and Homography

Stitches two overlapping images into a single panoramic view using ORB keypoint detection, feature matching, and homography-based perspective warping, with before/after visualization of the alignment process.

## Overview

This script takes two images with overlapping fields of view (e.g., left and right halves of a scene) and combines them into a single seamless panorama. It uses classical computer vision techniques — ORB feature detection, brute-force matching, and homography estimation via RANSAC — to align and warp the images before merging them.

## How It Works

1. **Load Images** — Reads the left and right images and displays them side by side for visual reference.
2. **Grayscale Conversion** — Converts both images to grayscale for feature detection.
3. **ORB Feature Detection** — Detects up to 3000 keypoints and computes descriptors for each image using ORB (Oriented FAST and Rotated BRIEF).
4. **Feature Matching** — Matches descriptors between the two images using a Brute-Force Matcher with Hamming distance, applying Lowe's ratio test (0.75) to filter out weak matches.
5. **Homography Estimation** — Computes a homography matrix from the matched keypoints using RANSAC to reject outliers.
6. **Perspective Warping & Canvas Calculation** — Transforms the corners of the second image to determine the final canvas size needed to fit both images.
7. **Image Warping & Placement** — Warps the second image into the first image's coordinate space and places the first image directly onto the resulting canvas.
8. **Visualization** — Displays the final stitched panorama.

## Requirements

```bash
pip install opencv-python numpy matplotlib
```

## Usage

```python
from stitch import stitch_images

result = stitch_images("left.jpg", "right.jpg")
```

The function displays the input images, performs the stitching, and returns the final panorama as a NumPy array (which can be saved using `cv2.imwrite`).

## Notes

- Works best when the two input images have sufficient overlap and distinguishable features.
- Performance may degrade with low-texture images (e.g., blank walls, sky) due to insufficient keypoints for matching.
- RANSAC threshold (currently `5.0`) can be tuned for stricter or looser inlier filtering depending on image quality.


```
