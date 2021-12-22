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

### 🔮 Model Construction

### 📝 Step 1️⃣: Point-Cloud Downsampling
At the first step, we preprocess Point-Cloud by downsampling. To achieve this, we have used voxel grids to create a uniformly downsampled Point-Cloud from an input Point-Cloud. First, points are bucketed into voxels. Then, each occupied voxel generates exactly one point by averaging all points inside. 

### 📝 Step 2️⃣: Point-Cloud Denoising
To denoise Point-Clouds, we have used the method statistical_outlier_removal and Radius oulier removal. The first function removes points that are further away from their neighbors compared to the average for the Point-Cloud, the second function removes points that have few neighbors in a given sphere around them.

### 📝 Step 3️⃣: Point-Cloud Redressing and Scaling 
We first rotate the Point-Cloud so that the plane in the PointCloud is XoY plane
Then we scale the Point-Cloud so that the height in the model would match the height in real world
In the end, we translate the Point-Cloud so that the plane equation could be Z=0

Please note that here we need to do an iteration so that we could get a more precise model
### 🗺️ Height Visualization


### 📝 Step 1️⃣: Model Construction
To find the plane with the largest support in the point cloud, we used the method [Segment_Plane](http://www.open3d.org/docs/release/python_api/open3d.geometry.PointCloud.html#open3d.geometry.PointCloud.segment_plane) from [Open3D](http://www.open3d.org/). The function returns the plane as (𝑎,𝑏,𝑐,𝑑) where for each point (𝑥,𝑦,𝑧) on the plane we have 𝑎𝑥+𝑏𝑦+𝑐𝑧+𝑑=0. The function further returns a list of indices of the inlier points. From [Open3D](http://www.open3d.org/) using the attribute Points, we get coordinate information of each points. 


After this, we calculate the relative height of the buildings based on the formula of point-to-plane distance. Once the plane equation is obtained, we could calculate the distances between each point and the plane and save them in a (n, 1) array. 

To visualise the height of the building, the first method is to change the colors of the points in the PointCloud model. For each point in the ‘PointCloud’, it has a ‘Colors' attribute. By calling this attribute, an (n, 3) array of value range [0, 1], containing RGB colors information of the points will be returned. Therefore, by normalising the ‘distances array’ values to the range of [0,1] and expanding the 'distances array' to three dimensions by replication, we get a (n, 3) ‘height array' in the form of (n, 3) 'colors array’.

### 📝 Step 2️⃣: Map Construction
In this step, we transform the PointCloud coordinates information into a DataFrame, and plot the z-coordinate on a X-Z plane 2D map.
## 🎉 Results

![This is an image](http://fdh.epfl.ch/images/4/47/Height_tab20c.png)


## 👤 Contributors
Yuhan Bi, Yuxiao Li, Sruti Bhattacharjee

