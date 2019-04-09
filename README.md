# py_camera
python调用摄像头  
参考资料：  
https://www.jianshu.com/p/2b79012c0228

## 1.安装opencv  
```
pip install opencv-python
```
## 2.打开摄像头  
```
import cv2

# 创建VideoCapture对象，如果有两个摄像头则可以选择参数为0，1
capture = cv2.VideoCapture(0)

while True:

    # 获取一帧
    # ret是一个布尔值，表示当前这一帧是否正常获取
    # frame表示截取到一帧的图片
    ret, frame = capture.read()

    # 将这帧转换为灰度图
    # gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    # 显示窗口
    cv2.imshow('frame', frame)

    # 按下q键退出
    if cv2.waitKey(1) == ord('q'):
        break
```
## 3.获取摄像头属性  
使用cap.get(propId)获取摄像头的属性，propId可以是0-18的数字，也可以是参数名。  
```
0:CV_CAP_PROP_POS_MSEC: Current position of the video file in milliseconds.
1:CV_CAP_PROP_POS_FRAMES: 0-based index of the frame to be decoded/captured next.
2:CV_CAP_PROP_POS_AVI_RATIO: Relative position of the video file: 0 - start of the film, 1 - end of the film.
3:CV_CAP_PROP_FRAME_WIDTH: Width of the frames in the video stream.
4:CV_CAP_PROP_FRAME_HEIGHT: Height of the frames in the video stream.
5:CV_CAP_PROP_FPS: Frame rate.
6:CV_CAP_PROP_FOURCC: 4-character code of codec.
7:CV_CAP_PROP_FRAME_COUNT: Number of frames in the video file.
8:CV_CAP_PROP_FORMAT: Format of the Mat objects returned by retrieve() .
9:CV_CAP_PROP_MODE: Backend-specific value indicating the current capture mode.
10:CV_CAP_PROP_BRIGHTNESS: Brightness of the image (only for cameras).
11:CV_CAP_PROP_CONTRAST: Contrast of the image (only for cameras).
12:CV_CAP_PROP_SATURATION: Saturation of the image (only for cameras).
13:CV_CAP_PROP_HUE: Hue of the image (only for cameras).
14:CV_CAP_PROP_GAIN: Gain of the image (only for cameras).
15:CV_CAP_PROP_EXPOSURE: Exposure (only for cameras).
16:CV_CAP_PROP_CONVERT_RGB: Boolean flags indicating whether images should be converted to RGB.
17:CV_CAP_PROP_WHITE_BALANCE: Currently unsupported
18:CV_CAP_PROP_RECTIFICATION: Rectification flag for stereo cameras (note: only supported by DC1394 v 2.x backend cur- rently)
```
```
# 通过cap.get(propId)获取摄像头的width和height值
width, height = capture.get(3), capture.get(4)
print(width, height)
```
使用cap.set(propId,value)来修改属性值  
```
# 以原分辨率的一倍来捕获
capture.set(cv2.CAP_PROP_FRAME_WIDTH, width * 2)
capture.set(cv2.CAP_PROP_FRAME_HEIGHT, height * 2)
```
