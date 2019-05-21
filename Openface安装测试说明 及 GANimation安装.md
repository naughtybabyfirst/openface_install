# Openface安装测试说明 及 GANimation安装



## 1.     Ubuntu Env Installation

If you already have any of the following dependencies you can skip those steps

### 1.1 Get newest GCC, done using:

```bash
sudo apt-get update

sudo apt-get install build-essential
```



### 1.2 Cmake:

```bash
sudo apt-get install cmake
```



### 1.3 Get OpenBLAS

```bash
sudo apt-get install libopenblas-dev
```



#### 1.4 Download and compile OpenCV 3.4.0

##### 	1.4.1 Install OpenCV dependencies:

```bash
sudo apt-get install git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
```

```bash
sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev
```

##### 	1.4.2 Download OpenCV 3.4.0 from <https://github.com/opencv/opencv/archive/3.4.0.zip>

 		wget https://github.com/opencv/opencv/archive/3.4.0.zip

##### 	1.4.3 Unzip it and create a build folder:

```bash
 sudo unzip 3.4.0.zip

 cd opencv-3.4.0

 mkdir build

 cd build
```



##### 	1.4.4 Build it using:

```bash
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D BUILD_TIFF=ON -D WITH_TBB=ON -D BUILD_SHARED_LIBS=OFF ..

make -j2

sudo make install
```



#### 1.5 Get Boost:

```bash
sudo apt-get install libboost-all-dev
```

会因依赖库而不能安装，因此使用下载源文件进行安装

download boost <https://dl.bintray.com/boostorg/release/1.69.0/source/>

```bash
tar -xzvf boost_1_67_0.tar.gz

sudo ./bootstrap.sh

sudo ./b2 install
```



#### 1.6 Download and compile dlib:

```bash
wget <http://dlib.net/files/dlib-19.13.tar.bz2>

tar xf dlib-19.13.tar.bz2

cd dlib-19.13

mkdir build

cd build

cmake ..

cmake --build . --config Release

sudo make install

sudo ldconfig

cd ../..
```




## 2. Model Download:

 

<https://onedrive.live.com/download?cid=2E2ADA578BFF6E6E&resid=2E2ADA578BFF6E6E%2153072&authkey=AKqoZtcN0PSIZH4>

 

<https://onedrive.live.com/download?cid=2E2ADA578BFF6E6E&resid=2E2ADA578BFF6E6E%2153079&authkey=ANpDR1n3ckL_0gs>

 

<https://onedrive.live.com/download?cid=2E2ADA578BFF6E6E&resid=2E2ADA578BFF6E6E%2153074&authkey=AGi-e30AfRc_zvs>

 

<https://onedrive.live.com/download?cid=2E2ADA578BFF6E6E&resid=2E2ADA578BFF6E6E%2153070&authkey=AD6KjtYipphwBPc>

 

·        [scale 0.25](https://onedrive.live.com/download?cid=2E2ADA578BFF6E6E&resid=2E2ADA578BFF6E6E%2153072&authkey=AKqoZtcN0PSIZH4)

·        [scale 0.35](https://onedrive.live.com/download?cid=2E2ADA578BFF6E6E&resid=2E2ADA578BFF6E6E%2153079&authkey=ANpDR1n3ckL_0gs)

·        [scale 0.50](https://onedrive.live.com/download?cid=2E2ADA578BFF6E6E&resid=2E2ADA578BFF6E6E%2153074&authkey=AGi-e30AfRc_zvs)

·        [scale 1.00](https://onedrive.live.com/download?cid=2E2ADA578BFF6E6E&resid=2E2ADA578BFF6E6E%2153070&authkey=AD6KjtYipphwBPc)

 

**在执行完第3步OpenFace installation*后，Openface编译后**，

**再把四个.dat文件放到OpenFace\build\bin\model\patch_experts目录下**

 

## 3. Actual OpenFace installation

### 3.1 Get OpenFace

```bash
git clone https://github.com/TadasBaltrusaitis/OpenFace.git
```



### 3.2 Create an out-of-source build directory to store the compiled artifacts:

```bash
cd OpenFace mkdir build cd build
```



### 3.3 Compile the code using:

```bash
cmake -D CMAKE_BUILD_TYPE=RELEASE CMAKE_CXX_FLAGS="-std=c++11" -D CMAKE_EXE_LINKER_FLAGS="-std=c++11" ..

make
```



### 3.4 Test it with (测试示例)

o   for videos:

```bash
./bin/FaceLandmarkVid -f "../samples/changeLighting.wmv" -f "../samples/2015-10-15-15-14.avi"
```

o   for images:

```bash
./bin/FaceLandmarkImg -fdir "../samples/" -wild
```

o   for multiple faces in videos:

```bash
./bin/FaceLandmarkVidMulti -f ../samples/multi_face.avi
```

o   for feature extraction (facial landmarks, head pose, AUs, gaze and HOG and similarity aligned faces):

```bash
./bin/FeatureExtraction -verbose -f "../samples/default.wmv"
```

 

## 4. Command line arguments（执行命令参数）

### FaceLandmarkImg（图片）

**Single image analysis(单张图片分析)**

`-f` <filename> the image file being input, can have multiple `-f` flags

`-out_dir` <directory> name of the output directory, where processed features will be places (i.e. CSV file for landmarks, gaze, and aus, HOG feature file, image with detected landmarks and a meta file)

`-root `<dir> the root directory so `-f` can be specified relative to it

`-inroot <dir>` the input root directory so `-f` can be specified relative to it

**Batch image analysis**

`-fdir <directory>` - runs landmark detection on all images (.jpg, .jpeg, .png, and .bmp) in a directory

`-bboxdir` optional directory that contains .txt files (image_name.txt) with bounding box (`min_x min_y max_x max_y`), it will use those for initialisation instead of an internal face detector

`-out_dir <directory>` name of the output directory, where processed features will be places (i.e. CSV file for landmarks, gaze, and aus, HOG feature file, image with detected landmarks and a meta file)

For more details on output format see [here](https://github.com/TadasBaltrusaitis/OpenFace/wiki/Output-Format#facelandmarkimg)

### FeatureExtraction and FaceLandmarkVidMulti（多个视频）

**Input parameters**

```bash
-f <filename>` the video file being input, can specify multiple `-f
```

`-fdir <directory>` run the feature extraction on every image (.jpg, .jpeg, .png, and .bmp) in a directory (the output will be stored in individual files for the whole directory)

`-device <device id>` the device id of a webcam to perform feature extraction from a live feed

`-cam_width` the input webcam witch resolution (default 640), only valid if device is set

`-cam_height` the input webcam height resolution (default 480), only valid if device is set

`-root <dir>` the root for input

`-inroot <dir>` the root for input

`-au_static` if this flag is specified the AU prediction will be performed as if on static images rather than videos, see [here](https://github.com/TadasBaltrusaitis/OpenFace/wiki/Action-Units#static-vs-dynamic) for a more detailed explanation, this is the default behavior for FaceLandmarkVidMulti

**Parameters for output (for more details on output format see** [**here**](https://github.com/TadasBaltrusaitis/OpenFace/wiki/Output-Format#featureextraction)**)**

`-out_dir <dir>` the root directory relevant to which the output files are created

`-of <filename>` the filename of the output (if not specified will use original filename, the name of the directory in case of `-fdir` and webcam + timestamp in case of a webcam)

`-oc <FOURCC_CODE>` the codec of the output video file (list of FOURCC codes can be found here - <https://www.fourcc.org/codecs.php>)

**Additional parameters for output (applicable for both FaceLandmarkImg and FeatureExtraction)**

`-verbose` visualise the processing steps live: tracked face with gaze, action units, similarity aligned face, and HOG features (not visualized by default), this flag turns all of them on, below flags allow for more fine-grained control. Visualizing these outputs will reduce processing speeds, potentially by a significant amount.

`-vis-track` visualise the tracked face

`-vis-hog` visualise the HOG features

`-vis-align` visualise similarity aligned faces

`-vis-aus` visualise Action Units

`-simscale <float>` scale of the face for similarity alignment (default 0.7)

`-simsize <int>` width and height of image in pixels when similarity aligned (default 112)

`-format_aligned <format>` output image format for aligned faces (e.g. png or jpg), any format supported by OpenCV

```bash
-format_vis_image <format>` output image format for visualized images (e.g. png or jpg), any format supported by OpenCV. Only applicable to `FaceLandmarkImg
```

`-nomask` forces the aligned face output images to not be masked out

`-g` output images should be grayscale (for saving space)

By default the executable will output all features (tracked videos, HOG files, similarity aligned images and a .csv file with landmarks, action units and gaze). You might not always want to extract all the output features, you can specify the desired output using the following flags:

`-2Dfp` output 2D landmarks in pixels

`-3Dfp` output 3D landmarks in milimeters

`-pdmparams` output rigid and non-rigid shape parameters

`-pose` output head pose (location and rotation)

`-aus` output the Facial Action Units

`-gaze` output gaze and related features (2D and 3D locations of eye landmarks)

`-hogalign` output extracted HOG feaure file

`-simalign` output similarity aligned images of the tracked faces

`-nobadaligned` if outputting similarity aligned images, do not output from frames where detection failed or is unreliable (thus saving some disk space)

`-tracked` output video with detected landmarks

### FaceLandmarkVid（视频）

**Parameters for input**

`-f <filename>` the video file being input, can specify multiple files by having multiple `-f` flags

`-device <device_num>` the webcam from which to read images (default 0)

`-cam_width` the input webcam witch resolution (default 640)

`-cam_height` the input webcam height resolution (default 480)

`-inroot <directory>` the root of input so `-f` can be specified relative to it

 

 

## 5. GANimation

### 5.1 添加ganimation依赖库

 

Openface安装完后，

执行

```bash
pip install numpy matplotlib tqdm dlib face_recognition opencv-contrib-python
```

 

### 5.2 生成aus_openface.pkl文件

```
python data/prepare_au_annotations.py -ia ./imgs_csv/ -op ./data/
```

输入项：``-ia ./imgs_csv/ ``为``Openface``生成的``csv``文件

输出项：`-op ./data/`



### 5.3 训练：

```bash
python train.py --data_dir path/to/dataset/ --name experient_1 --batch_size 25
```

`--data_dir path/to/dataset/ `     输入头像的文件夹

`--name experient_1`            	checkpoint下的文件名

`--batch_size 25`                	batch_size 大小

如果显存溢出，可将batch_size设置小一些

 

如果出现训练出错，要将checkpoint下的对应experient文件夹删除掉，再重新训练

### 5.4 预测：

```bash
python test.py --name experient_1 --input_path ./data/imgs --output_dir ./data/output
```

`--name experient_1`                 使用上次训练保存下来的文件名

`--input_path ./data/imgs`             输入文件名

`--output_dir ./data/output`            输出文件名