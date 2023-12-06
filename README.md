# 直播聊天室人机交互界面工具包设计指南 (Beta)
Design Guide of Live Stream Chat UIkit(Beta)

## 0.总的设计原则
### 0.1.功能与行为上确保通用、普遍、一般
### 0.2.风格上易于自定义
### 0.3.在业务形态上尽量不替用户做决定

## 1.全局样式（Style）

### 1.1.UIkit色彩规范
#### 1.1.1.颜色配置说明：
##### 1.1.1.1.颜色类（Color Class）
一般颜色类分为八类：
主题色（Theme Color）：Primary、 Secondary、Error三类；
渐变主题色（Primary Gradient）一类（含8种）；
透明色（Alpha Color）：On Light、On Dark两类；
中性色（Neutral Colors）：Neutral、Neutral Special两类；

##### 1.1.1.2.颜色模式（Hsla Model）
颜色模式为比较直观的hsla模式:
整个模型是一个圆柱体，圆柱体底面周长划分为360°，对应不同的色相（Hue）;
圆柱体的半径为饱和度（Saturation），圆心为0（最灰），半径值为100（最艳）；
圆柱体的高为亮度（Lightness），起始点为0（纯黑色），中心点是50(标准色,)，结束点为100(纯白色)。

##### 1.1.1.3.模型概览：
![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk1113.png)

#### 1.1.2.三种主题色（Theme Color）的色彩规范：

##### 1.1.2.1.关于用户可配项（Hue value）：
用户可设定颜色类的可配项Hue(0-360)为任意数值，修改后每类颜色的色相会发生变化，以贴合用户场景所需要的主题颜色。
Hue值(0-360)与色相的对应关系大致如以下图示所例：

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk11211.png)

用户可依据自身产品的品牌色指定色相数值（Hue），从而确认主题色Primary（主要用于UI组件中关键操作与重要文本展示，如推荐的action、高亮显示的文本等），以及用于积极提示的Secondary，和表示警示提示的Error。

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk11212.png)

##### 1.1.2.2.关于饱和度（Saturation value）:
饱和度(Saturation)不开放给用户设置，三种主题色Primary、 Secondary、Error默认饱和度为100%，Neutral默认为8%，Neutral Special默认为36% 

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk1122.png)

##### 1.1.2.3.关于亮度级别（Lightness level）:
亮度(Lightness)百分比用户不可随意设置，每个颜色类提供：0(0%) / 1(10%) / 2(20%) / 3(30%) / 4(40%) / 5(50%) / 6(60%) / 7(70%) / 8(80%) / 9(90%) / 95(95%) / 98(98%) / 100(100%)十三个级别供用户可选；

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk1123.png)

##### 1.1.2.4.举个例子吧：
如指定主题色Primary色相（Hue）为203，成功色Secondary色相（Hue）为155，警示色Error色相（Hue）为350，则会生成如下39种主题色可供用户在指定UI件块（View）颜色时使用：

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk1124.png)

其中，主题色Primary的L5为亮色模式下的基色（Key Color），L6为暗色模式下的基色（Key Color）。所有的颜色体系都是依照基色生成。

#### 1.1.3.关于渐变主题色(Primary Gradient)的规范：

渐变主题色是由Primary色派生出的渐变色，为线性渐变(Linar Gradient)，渐变方向依图示坐标系分为8类： 

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk113.png)

##### 1.1.3.1.关于渐变色的起始色(Start Color)：
渐变色中Start Color规则和Primary类的色值保持一致;

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk1131.png)

##### 1.1.3.2.关于渐变色的结束色(End Color)：
End Color用户可配置色相（Hue），亮度以0(20%) / 1(30%) / 2(40%) / 3(50%) / 4(60%) / 5(70%) / 6(75%) / 7(80%) / 8(85%) / 9(90%) / 95(95%) / 98(98%) / 100(100%)（对应Primary的13级亮度梯度值）为固定梯度值

以下以Hue：233为例，按照End Color颜色公式依旧得到13级颜色： 

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk11321.png)

起始色和结束色结合，得到相应的渐变结果 

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk11322.png)

##### 1.1.3.3.关于渐变主题色可配项(End Color Hue Value)：
用户仅可配置渐变色中End Color的色相（Hue）以达成与用户业务场景符合的渐变颜色效果；

##### 1.1.3.4.举个例子吧:
用户设置End Color Hue = 233，选择渐变方向为“↓”，则可得到如下效果： 

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk11341.png)

如使用渐变主题色，那么它将替代掉所有应用于背景色的Primary色 

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk11342.png)

但一般不替代UI件块的前景色，因为没有什么意义，且有干扰文字阅读的可能性

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk11343.png)

#### 1.1.4.关于透明色(Alpha)的规范：

##### 1.1.4.1.透明色（Alpha Color）:
在本案内带有透明度的组件仅有弹幕消息背景色、礼物消息背景色、模态背景色、轻提示背景色四种，应用范围有限，所以单独定义两个特殊的颜色类用于以上四种组件：Alpha onlight(hsl0, 0%, 0%) 和 Alpha ondark(hsl0, 0%, 100%)，Alpha值被指定为 0(0.0) / 1(0.1) / 2(0.2) / 3(0.3) / 4(0.4) / 5(0.5) / 6(0.6) / 7(0.7) / 8(0.8) / 9(0.9) / 95(0.95) / 98(0.98) / 100(1.0) 十三个梯度值，共26种颜色用例，以调整组件的背景色透明度。 

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk1141.png)

Alpha onlight 和 Alpha ondark 均为默认值，无任何可配置项。

1.1.5.关于中性色（Neutral Colors）：

1.1.5.1.中性色（Neutral）
中性色(Neutral)仅有一个可配项：色相（Hue），饱和度(Saturation)固定值为8，亮度级别（Lightness level）也和主题色相同，分为0(0%) / 1(10%) / 2(20%) / 3(30%) / 4(40%) / 5(50%) / 6(60%) / 7(70%) / 8(80%) / 9(90%) / 95(95%) / 98(98%) / 100(100%)十三个级别供用户可选；

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk1151.png)

Neutral和Primary的默认Hue值(色相)相同，也建议用户设置和主题色相同的Hue值已达成主题颜色和无彩色系的配套。但这仅仅是建议； 

1.1.5.2.举个例子吧：
如指定主题色Primary色相（Hue）为203，饱和度(Saturation)固定值为100%，中性色（Neutral）则也指定色相（Hue）为203，饱和度(Saturation)固定值为8%，则得到以下色列可供用户选择使用： 

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk11521.png)

其中，L98为亮色模式下背景色的主色，L1为亮色模式下前景色的主色；L1为暗色模式下背景色的主色，L98为暗色模式下前景色的主色。
 
![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk11522.png)

1.1.6.关于特殊中性色（Neutral Special）：
特殊中性色Neutral Special主要用于级别低于Primary和Secondary的强调信息，如当前页面状态、消息发送者的昵称等。
Neutral Special和Primary的默认Hue值(色相)类似，为近似色，也建议用户设置和主题色近似的Hue值已达成主题色和无彩色系的配套。但这仅仅是建议；

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk116a.png)

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk116b.png)

#### 1.1.6.1.举个例子吧：
如指定主题色Primary色相（Hue）为203，特殊中性色（Neutral）通过相似色原理（正负30度内）指定色相（Hue）为220，饱和度(Saturation)固定值为36%，则得到以下色列可供用户选择使用： 

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk1161.png)

## 1.2.主题

本期主题分为2种，每种分明亮（Light mode）和黑暗（Dark）两类。
### 1.2.1.圆润主题
组件一般采用较大的圆角，柔和轻盈

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk121.png)

### 1.2.2.硬朗主题
组件一般避免比较大的圆，硬朗实在
![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk1122.png)

以上两种主题可通过应用渐变主题色（Primary Gradient）得到两外两种渐变色主题。
至于业务相关的主题，如“社交”、“游戏”、“教育”、“商务”等主题分类，因违反本案的最基本设计原则“在业务形态上尽量不替用户做决定”，所以不在本期考虑范围内。

## 1.3.图标（Icon）

### 1.3.1.图标模板（Template）
图标参照Material Icon Font的模板 ，以24为基本栅格，须在安全区域(20x20的中心区域)内绘制，基本描边控制为1.5栅格。

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk1131.png)

### 1.3.2图标命名（Name）
为防止将图标语意固定，icon命名需要尽力避免定义操作行为，而是以“看见什么就是什么“进行命名，方便相同图标在不同操作行为下的复用。
如

![image text](https://github.com/StevieJiang/Chatroom-UIkit-Design-Guide/blob/main/Doc%20Image/cruk132.png)
