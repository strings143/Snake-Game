# Snake-Game 
採用Pygame結合OpenCV，透過偵測物體的方式，來達到跟隨物體玩貪吃蛇的遊戲。
# 預覽畫面
* 按下空白鍵開始遊戲。
* 右邊綠色框是偵測到的物體，左右上下移動來控制蛇。
* 碰到自己或邊界就死亡，在玩一次按空白鍵，結束按Q鍵。
![](https://i.imgur.com/CqQgeXz.png)
![](https://i.imgur.com/yOagxMB.png)
# 建置
**偵測物體參數，如需更換物體，請改Code這部分的參數。**
```
 lower=np.array([22,127,98])
 upper=np.array([38,210,255])
 mask=cv2.inRange(hsv,lower,upper)
```
**更改參數的 Test Code** : 
```
import cv2
import numpy as np
def callme(i):
    pass
cap =cv2.VideoCapture(0)
cv2.namedWindow('myBar')
cv2.resizeWindow('myBar',600,300)
cv2.createTrackbar('H-min','myBar',0,179,callme)
cv2.createTrackbar('H-MAX','myBar',179,179,callme)
cv2.createTrackbar('S-min','myBar',0,255,callme)
cv2.createTrackbar('S-MAX','myBar',255,255,callme)
cv2.createTrackbar('V-min','myBar',0,255,callme)
cv2.createTrackbar('V-MAX','myBar',255,255,callme)
while True:
    ret,frame=cap.read()
    if ret:
        frame=cv2.resize(frame,(0,0),fx=0.8,fy=0.8)
        hsvImg=cv2.cvtColor(frame,cv2.COLOR_BGR2HSV)
        H_min = cv2.getTrackbarPos('H-min', 'myBar')
        H_MAX = cv2.getTrackbarPos('H-MAX', 'myBar')
        S_min = cv2.getTrackbarPos('S-min', 'myBar')
        S_MAX = cv2.getTrackbarPos('S-MAX', 'myBar')
        V_min = cv2.getTrackbarPos('V-min', 'myBar')
        V_MAX = cv2.getTrackbarPos('V-MAX', 'myBar')
        lower = np.array([H_min, S_min, V_min])
        upper = np.array([H_MAX, S_MAX, V_MAX])
        irImg = cv2.inRange(hsvImg, lower, upper)
        bwAndImg=cv2.bitwise_and(frame,frame,mask=irImg)
        cv2.imshow('ori',frame)
        cv2.imshow('hsv', hsvImg)
        cv2.imshow('mask', irImg)
        cv2.imshow('bwand', bwAndImg)
        cv2.waitKey(1)
cap.release()
cv2.destroyAllWindows()
```
# 流程圖
![](https://i.imgur.com/ofSHCkh.png)
# 參考
**參考了作者的製作的貪吃蛇遊戲，再自己結合OpenCV偵測物體來控制蛇的上下左右移動。**
> [https://medium.com/@shit6333/%E4%BD%BF%E7%94%A8pygame-%E6%92%B0%E5%AF%AB%E8%B2%AA%E5%90%83%E8%9B%87%E9%81%8A%E6%88%B2-c6cada8478c8](https://)
