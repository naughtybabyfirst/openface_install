[Read More Step] https://github.com/naughtybabyfirst/openface_install/blob/master/Openface%E5%AE%89%E8%A3%85%E6%B5%8B%E8%AF%95%E8%AF%B4%E6%98%8E%20%E5%8F%8A%20GANimation%E5%AE%89%E8%A3%85.md 


1. install gcc

2. install cmake

      sudo apt-get install cmake

3. install openBLAS

      sudo apt-get install libopenblas-dev

4. install opencv

      4.1 sudo apt-get install git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev

 sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev
 
      4.2 download https://github.com/opencv/opencv/archive/3.4.0.zip
  
      4.3 sudo unzip 3.4.0.zip; cd opencv-3.4.0; mkdir build; cd build
  
      4.4 cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D BUILD_TIFF=ON -D WITH_TBB=ON -D BUILD_SHARED_LIBS=OFF ..
  
      4.5 make -j2
  
      4.6 sudo make install

5. install boost

      5.1 download boost https://dl.bintray.com/boostorg/release/1.69.0/source/
  
      5.2 tar -xzvf boost_1_67_0.tar.gz
  
      5.3 sudo ./bootstrap.sh
  
      5.4 sudo ./b2 install
  
6. install dlib

      6.1 download dlib http://dlib.net/compile.html
  
      6.2 tar xf dlib-19.17.tar.bz2
  
      6.3 cd dlib-19.17
  
      6.4 mkdir build; cd build ;cmake ..; cmake --build . --config Release; sudo make install; sudo ldconfig; cd ../..;
  
  
  
