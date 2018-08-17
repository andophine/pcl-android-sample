# pcl-android-sample
build instruction
1. compiled pcl for android libraries by following the instruction of https://github.com/bashbug/pcl-for-android (test build pass with android ndk version: 14, fail with 17)
or using superbuid from https://github.com/hirotakaster/pcl-superbuild.git.  
2. copy the compiled files/directories to app/libs include boost-android, flann-android, pcl-android and eigen.
done
3. NDK version on Android Studio must be 16(version 14 missing omp library).
4. PCL library link passed for arm target, but fail with x86 target during Android Studio build.
