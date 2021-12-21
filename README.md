# 🏭 Venice-2020 Detection of building heights
Please clone this repository using ```git clone --xxxxxxxxxxxxxxx``` to properly initalize

This repository is a pipeline to detect heights of different buildings in Venice from Google Earth View and drone videos from Youtube.
This pipeline is implemented during course  Foundation of Digital Humanities (DH-405) given in fall 2021 at EPFL.
For details please go through our [wiki page](http://fdh.epfl.ch/index.php/Venice2020_Building_Heights_Detection).
Please find the details on how to run the pipeline below:

# ⏳ Background Motivation
Over the last 100 years, the city of Venice has lost about 9 inches because of its geography and Global warming. As a part of  [Venice Time Machine](https://en.wikipedia.org/wiki/Venice_Time_Machine), this project proposes a pipeline to detect building heights of Venice from 2020 Google EThe pipeline allows us to stay on track with the current height information of each building in Venice which can be used as historical data in the future. 
Earth data. 

![This is an image](http://fdh.epfl.ch/images/3/38/Venice_whole.png)


## 📋 Pipeline

Our initial plan was to download drone videos of Venice on the Youtube platform, used FFmpeg to extract images from the video one frame per second, and generate dense point cloud models based on the images that we acquired. However, the videos we could get from drone videos are very limited. Hence in order to access building data all over the Venice, we decided to use Google Earth images. Following  photogrammetry route from Google Earth images of whole Venice were collected in order to generate point cloud models.

### 🔮 Model Construction

### 📝 Step 1️⃣: Point-cloud Downsampling


### 📝 Step 2️⃣: Point-cloud Denoise


### 📝 Step 3️⃣: Point-cloud Redressing and Scaling 

### 🗺️ Height Visualization


### 📝 Step 1️⃣: Model Construction
To find the plane with the largest support in the point cloud, we used the method [Segment_Plane](http://www.open3d.org/docs/release/python_api/open3d.geometry.PointCloud.html#open3d.geometry.PointCloud.segment_plane) from [Open3D](http://www.open3d.org/). The function returns the plane as (𝑎,𝑏,𝑐,𝑑) where for each point (𝑥,𝑦,𝑧) on the plane we have 𝑎𝑥+𝑏𝑦+𝑐𝑧+𝑑=0. The function further returns a list of indices of the inlier points.


### 📝 Step 2️⃣: Map Construction

## 🎉 Results



## 👤 Contributors
Yuhan Bi, Yuxiao Li, Sruti Bhattacharjee

