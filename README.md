# 🏭 Venice-2020 Detection of building heights
Please clone this repository using ```git clone --xxxxxxxxxxxxxxx``` to properly initalize

This repository is a pipeline to detect heights of different buildings in Venice from Google Earth View and drone videos from YouTube.
This pipeline is implemented during course Foundation of Digital Humanities (DH-405) given in fall 2021 at EPFL.
For details please go through our [wiki page](http://fdh.epfl.ch/index.php/Venice2020_Building_Heights_Detection).
Please find the details on how to run the pipeline below:

# ⏳ Background Motivation
Over the last 100 years, the city of Venice has lost about 9 inches because of its geography and Global warming. As a part of  [Venice Time Machine](https://en.wikipedia.org/wiki/Venice_Time_Machine), this project proposes a pipeline to detect building heights of Venice from 2020 Google EThe pipeline allows us to stay on track with the current height information of each building in Venice which can be used as historical data in the future. 
Earth data. 

![This is an image](http://fdh.epfl.ch/images/3/38/Venice_whole.png)

## 📋 Pipeline

Our initial plan was to download drone videos of Venice on the YouTube platform, used FFmpeg to extract images from the video one frame per second, and generate dense point cloud models based on the images that we obtained. However, the videos we could get from drone videos are very limited. Hence in order to access building data all over the Venice, we decided to use Google Earth images. Following  photogrammetry route from Google Earth images of whole Venice were collected in order to generate point cloud models.

## 🔮 Model Construction

### 📝 Step 1️⃣: Point-Cloud Downsampling
At the first step, we preprocess Point-Cloud by downsampling. To achieve this, we have used voxel grids to create a uniformly downsampled Point-Cloud from an input Point-Cloud. First, points are bucketed into voxels. Then, each occupied voxel generates exactly one point by averaging all points inside. 

### 📝 Step 2️⃣: Point-Cloud Denoising
To denoise Point-Clouds, we have used the method statistical_outlier_removal, which removes points that are further away from their neighbors compared to the average for the Point-Cloud.

### 📝 Step 3️⃣: Point-Cloud Redressing and Scaling 
We first rotate the Point-Cloud so that the plane in the PointCloud is XoY plane
Then we scale the Point-Cloud so that the height in the model would match the height in real world
In the end, we translate the Point-Cloud so that the plane equation could be Z=0

Please note that here we need to do an iteration so that we could get a more precise model

## 🗺️ Height Visualization

### 📝 Method 1️⃣: Height Model Construction

In this method, we visualize the height of a point by normalising its height information and save it into its 'Colors' attribute. The higher a point is, the lighter its color will be, and vice versa.

### 📝 Method 2️⃣: Height Map Construction
In this section, we transform the PointCloud coordinates information into a DataFrame, and plot the z-coordinate on a XoY plane 2D map.
## 🎉 Results

![This is an image](http://fdh.epfl.ch/images/4/47/Height_tab20c.png)

## 👤 Contributors
Yuhan Bi, Yuxiao Li, Sruti Bhattacharjee
