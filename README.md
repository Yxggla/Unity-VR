# Unity-VR

This is a VR mini-game based on Unity and SteamVR, and it is also a personal project for my virtual reality course  
这个是基于Unity和SteamVR制作的VR小游戏，也是我虚拟现实课程的个人大作业

## 2.1 开发平台和VR硬件设备，VR软件部分，插件部分

- Unity3D引擎、Pico4、Steam VR、Pico 互联

## 2.2 VR交互设计和实现思路

### 2.2.1 InteractionSystem中交互方式简介

1. **Player**，采用了Steam VR自带的Player。来实现VR中的人物。
2. **Interact**，交互器。使用相关代码Interactable来实现点击抓获，松开放下。
3. **SteamVR Input**，输入系统。使用这个来添加动作、选择动作、绑定手柄。
4. 具体本游戏实现的交互分别为物体的抓起、放下、射击、蓄力射击，人物的移动，还有UI的血量条等。

![image](https://github.com/user-attachments/assets/03cc06f3-03fd-4d26-944e-4c752004bb43)

### 2.2.2 拟采用的action或action sets罗列和设计

采用SteamVR Input的Action来实现效果。

1. **GrabGrip**来实现物体的抓取，并且在手柄上进行了绑定为扳机按钮。
2. **InteractUI**来实现射击，我把这个键绑定在了右手柄的A键上。配合代码实现枪的射击。
3. 自定义创建了**MovePlayer**的Action，绑定在了手柄的轮盘上，配合代码实现了Player的移动。
4. 自定义创建了**xvliAction**的Action，绑定在了右手柄的B键上。配合代码实现枪的蓄力射击。

![image](https://github.com/user-attachments/assets/b57b6bf6-d3c7-4790-8bb1-fc26eedbcd51)

### 2.2.3 3D建模方面修改部分

没有修改。Player采用Steam VR的Player，敌人使用Unity资源商店里的敌人Prefabs，武器使用Unity资源商店里武器Prefabs，游戏道具也使用Unity资源商店里道具3D Prefabs。

![image](https://github.com/user-attachments/assets/dc042a02-accb-4d8b-b1ec-a4dd3021ad2b)

### 2.2.4 3D骨骼绑定动画方面修改部分

基本没有修改。对敌人的Prefabs，添加进行骨骼绑定和添加自带的控制器demo。

![image](https://github.com/user-attachments/assets/f735e84e-ff5b-4247-bce8-d35e9d59e2fa)

### 2.2.5 碰撞方面修改部分

使用Collider来实现碰撞体。例如给武器添加Box Collider，给子弹添加Sphere Collider，也给一些游戏场景交互的对象添加了碰撞体的触发器，使用代码实现UI界面的更新变化。

![image](https://github.com/user-attachments/assets/66181f12-2cd7-4af7-8403-acf20cea7ccc)

### 2.2.6 计分方面修改部分

使用UI面板的Slider实现了敌人血量栏的效果和子弹射入指定区域后的积分数。

![image](https://github.com/user-attachments/assets/50d0e294-51f0-480a-b4fa-78e3b1baf96a)

### 2.2.7 Camera方面修改部分

没有修改，直接使用了Steam VR给的Player。使用Player里的VRCamera。

### 2.2.8 地形、背景方面修改部分

细微修改，直接使用了Unity资源商店里的场景，然后对场景中的部分物体进行了位置上和大小上的更改。让其更适配VR游戏内容。

![image](https://github.com/user-attachments/assets/fdcc0917-7925-4497-a003-d35df5242368)

### 2.2.9 声音方面修改部分

在枪扣射击的时候会发出开枪的声音。

![image](https://github.com/user-attachments/assets/0f97ef2c-9d36-4f15-b5bd-a05f831cf232)

### 2.2.10 界面方面修改部分

游戏界面为Unity资源商店里的场景。在UI方面设计了5个面板，分别为前文介绍的人物血量，物体信息介绍，游戏介绍和两个积分面板。

![image](https://github.com/user-attachments/assets/80bf9b2a-a76a-4398-ab91-dbe8a446f3a2)

### 2.2.11 脚本方面修改部分

1. 人物移动的脚本。在实现用新建的动作绑定到手柄轮盘后，可以用此代码来移动人物。

![image](https://github.com/user-attachments/assets/090f2189-a903-4cae-adef-f8d68402b9c7)

2. 盾拿起后会在一个固定的位置刷新一个敌人。

![image](https://github.com/user-attachments/assets/aaf9dec8-cf83-4ed5-b400-d3f19bcb38f1)

3. 枪的开火和拿起放下代码。

![image](https://github.com/user-attachments/assets/563d9e9c-7608-47ea-864d-d36d52976ba1)

4. 敌人被打后扣血的代码。

![image](https://github.com/user-attachments/assets/0a590eb7-b460-48d8-8415-4c62e592b97f)

5. 普通的点一下GrabGrip拿起，再点一下就放下代码。

![image](https://github.com/user-attachments/assets/a6a10965-767e-4fb2-a992-5c3d3b66e6ff)

6. 蓄力射击代码，在前面基础的射击代码之中添加了布尔属性的isCharging，并且可以通过计算蓄力时间来更改射出的初速度，以实现子弹的重力的运动轨迹。

![image](https://github.com/user-attachments/assets/896aab8f-3819-4299-8e28-c63b39b081db)

### 2.2.13 其他方面

#### 子弹发射部分：

1. 做一个gameobject来定位子弹生成的位置，这个gameobject需要在手枪模型的图层下。要向Y轴旋转90度这样实现方向和枪口方向一致。

![image](https://github.com/user-attachments/assets/f83ec6f3-fb00-4fab-b653-ad9a9cb7a696)

2. 做一个子弹的Prefab，我使用了球体，然后用了Sphere Collider的碰撞体，并且设置标签为“Weapon”。因为只有标签为这个还可以让敌人扣血。另一个带重力的子弹就是添加了Rigibody里的重力。

![image](https://github.com/user-attachments/assets/37b3c3ca-0728-4baf-add6-9cb09ac8369d)

3. 使用代码来实现枪的射击

![image](https://github.com/user-attachments/assets/6a1411c3-dd81-4741-b290-6b5b6ff74dea)

## 第3章 整体实现及问题解决方法

### 3.1 整体系统效果实现

采用Unity+SteamVR+Pico4+Pico互联的形式来做出这个VR游戏。

1. 在游戏进入的时候，可以用手柄的滚轮盘来进行移动。
2. 桌上有很多的武器，抬头可以看到游戏的大概介绍。

![image](https://github.com/user-attachments/assets/bd1fd505-4edb-4efd-9acf-0f6a8b4f2b96)

3. 移动人物可以走向武器。走向左边的手枪，单机扳机按钮可以拿起，再次按一下会掉落。按左边手柄的A键，会进行无重力，模拟真枪射击。

![image](https://github.com/user-attachments/assets/a0ca9ad8-a950-441e-a41a-b74a419bc1ff)

4. 手枪可以瞄准前方的假人模型，如果子弹射击到了就会触发一次假人身上的碰撞组件的“触发器”，从而实现假人头上UI面板的血量条的减少。这里通过给子弹预制体添加Weapon的标签，然后通过代码给假人实现一个如果指定的Weapon标签进入碰撞体就会触发扣除头顶上UI面板的血量的事项。

![image](https://github.com/user-attachments/assets/34db99e6-b3d4-4b99-9aa6-0940fc013edd)

5. 这里设计血量条的时候，采用了上学期期末作业中的自己血量条的做法。我采用UI面板中的Slider组件，设置了最大最小值和是整数。通过触发器的形式来触发函数来进行调整具体的Value，来调整血量的显示。我也在代码中设置了如果血量为0，那么就会摧毁自己，即假人消失。
6. 既然游戏名叫虚幻武器场，那肯定需要无限的练习。因此我设计了一种与VR手柄交互和游戏需求功能为一体的方式，举起边上的盾就会在指定位置生成一个假人Prefab，来满足玩家练习虚幻武器的欲望。这里特地使用举起盾的SteamVR手柄对应函数，对GrabGrip拿起后添加一个函数，可以在指定位置生成一个假人。

![image](https://github.com/user-attachments/assets/98f44665-5273-4e0c-b4c9-4937d2e6d56c)

7. 左数第二个武器是剑，我们可以长按扳机键来举起剑。同样我设置了剑为Weapon的标签，这样我们就可以把剑碰到假人，来实现扣血的效果。

![image](https://github.com/user-attachments/assets/2bb5b1cd-a92b-49de-921b-9a6e6f7f4245)

8. 左数第三个是弓的箭，我们可以单机扳机来拿起箭。同样也有Weapon的标签。
9. 左数第四个是弓，我们需要用左手单机扳机来拿起弓。我们也可以左手举起弓和右手拿起箭来感受一下。
10. 左数第五个是一把需要蓄力的枪，枪里的子弹就像是弹珠一下会被弹射出。我们可以单机右手扳机来实现拿枪，然后用左边手柄的B键来实现蓄力射击。如果射出的子弹进入了指定的管道中，那么管道所对应的UI面板会显示获得的积分，这里共有两个管道和对应面板。在UI面板中我使用的是text的组件，利用管道里偷偷放的圆柱设置碰撞体的触发器来驱动对应函数来改变text里的内容。这里我给圆柱碰撞体添加了对应的代码，以实现UI面板内积分的效果。同理我给有枪射出来的子弹Prefab添加了Weapon的标签，并且添加了Rigidbody的重力效果，以实现有趣的重力效果。通过Weapon标签，我可以给这个碰撞体一个代码，来实现指定的标签会触发一定的函数，由此驱动UI的text变化。

![image](https://github.com/user-attachments/assets/d5f67378-d036-45fe-bb2b-77d196e46f6c)

### 3.2 遇到问题及其解决方法

- **问题1**：没有VR设备就算Unity没有报错也不能调试。
  - **解决方案**：Pico淘宝旗舰店购置一台Pico4，然后7天无理由退换。或者和我们班其他同学一样，租一台Pico4，一起调试。

- **问题2**：在没有VR的时候，对物体使用VR手的，一键举起，一键放下代码功能时。GameObject会被摧毁，就是东西没了，放下不了。
  - **解决方案**：使用VR进行调试的时候就好了。

- **问题3**：VR界面看到不游戏场景摄像机里的UI面板。在Unity里调试时以为没问题，但是上了真机发现UI面板不见了。
  - **解决方案**：将UI面板的渲染模式设置为“世界空间”，然后设置具体的位置。

- **问题4**：子弹发射的时候会往左边射击
  - **解决方案**：调整初始位置的那个子弹位置定位的空对象的y轴旋转90。

- **问题5**：设置好了手型但是在真机中握的时候又有较大差错。
  - **解决方案**：需要多次保存手型。

- **问题6**：VR真机里截好的图，无法导入到电脑中。
  - **解决方案**：下载个PICO的APP，然后可以获取截图。

#视频  
https://github.com/user-attachments/assets/7f4ae594-37e7-4caf-92b3-c6c2ab3f245d

