# CVFX-homework-6
Homework 6 for CVFX, team 7.

## Assign
1. 5% (Take videos by yourselves)
2. 10% (Make these visual effects with ORB-SLAM2)
3. 10% (Make these visual effects with any post-production software)
4. 10% (Compare above methods)
5. 10% (Make some special effects based on the pose information, such as rotating, zooming in or out)
6. 5% (Insert a 3D model to your video)
7. 10% (Bonus- Make visual effects with other SLAM methods.)

## Take videos by yourselves

The video is <a href="https://drive.google.com/file/d/1hVUXxp7q34hKQpOnVNforME0AhKJYDIE/view?usp=sharing">here</a>. 

## Make these visual effects with ORB-SLAM2

### Results

The video is <a href="https://youtu.be/TwPsq0ncPQc">here</a>. 

This is <a hred="https://youtu.be/tzAapfS7m94" >color version</a>

### 作法
ORB SLAM中利用相機視角與key points深度建構了一個3D的世界，frame.h中的cv::Mat mRcw、cv::Mat mtcw就是將3D世界坐標系轉2D相機畫面再轉到圖片座標需要的矩陣。

所以我們做的事就是固定一個3D世界座標，然後用公式轉到圖片座標。作法如下圖。
<img src="./img/transform.png" width="500px">


P是固定的世界座標[-0.1, 0.2, 0.8]，並沒有特殊意義，只是從map points的座標中發現這附近數值的點是可以在相機中出現較常時間的。

為了確認該點在3D世界中的位置，在pangolin的frame也把點畫上去並跟目前圖片畫面比較：  
右圖中青色的點就是目前"Hello"字樣所在的空間位置。可以看到兩者是差不多的。

|2D Picture Frame|3D World Frame|
|:--:|:--:|
|<img src="./img/2dpic.png" width="300px">|<img src="./img/3dworld.png" width="300px">|

此外，因為在做處理時，ORB SLAM會將圖轉成灰階，我們希望在顯示時能是彩色，所以在Tracking.cc裡面做了一些調整，保留原本的彩色frame給FrameDrawer畫。

### 小結
我們使用的是KITTI dataset設定的.yaml檔，但從相機軌跡上來看，其實他是有一些不準確的，我們實際上的移動情況應該如下圖：  
橘色箭頭是相機移動的軌跡，紫色箭頭是相機視角方向。

<img src="./img/path.png" width="400px">

所以在結果的影片中，字所在位置其實沒有非常準。如果希望相機軌跡能跟實際更相近、更準確的話，可能要自己做camera calibration，因為比較花時間所以這部分我們並沒有做。

## Make these visual effects with any post-production software

## Compare above methods

## Make some special effects based on the pose information, such as rotating, zooming in or out

## Insert a 3D model to your video
