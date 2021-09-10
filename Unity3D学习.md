

# Unity3D快捷键

## 变换工具

移动场景 Q，鼠标右键

移动物体 W，鼠标左键

旋转物体 E

缩放物体 R

顶点吸附：选择物体后按住V，拖拽物体到定点保持对齐，松开V

旋转：

![image-20210717173542110](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210717173542110.png)



global表示全局，旋转时坐标不动

![image-20210717173623105](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210717173623105.png)

local表示局部，旋转时坐标一起旋转

## 创建物体

不同组件合并整体，将子容器拖拽到父容器合并整体，操作父容器子容器一起动，操作子容器父容器不动，用空容器作为父容器层

Hierarchy栏右键->3D Object->cube：一个正方体

Hierarchy栏右键->3D Object->plane：一个平板（单面，只有一面能看到，需要两面拼接形成墙体）

Hierarchy栏右键->3D Object->capsule：一个胶囊

Hierarchy栏右键->3D Object->cylinder：一个圆柱体

Hierarchy栏右键->create empty ：创建空物体（任何容器自带transform组件）

1.![image-20210717175225577](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210717175225577.png)

选择添加mesh filter组件

2.![image-20210717175400505](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210717175400505.png)

选择任意形状网格（但是看不见没有渲染，mesh filter负责获取网格信息）

3.![image-20210717175551155](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210717175551155.png)

再次添加mesh renderer负责渲染网格为初始颜色，其中materials表示设置材质，在element->中可以选择颜色

## 创建材质Material

材质本质是shader的实例，

Shader着色器：一段嵌入到渲染管线中的程序，可以控制GPU运算图像效果算法，

Shader可以换，不同设置取决于shader中的属性有什么，初始为标准（standard）

![image-20210717191335045](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210717191335045.png)



project->create->material在资源中新建材质

![image-20210717185438820](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210717185438820.png)

1.Albedo选择颜色，前面可以选择贴图

2.材质做好后，需要在子容器的mesh renderer组件中选择或者拖拽到子容器上，材质是给到mesh renderer组件，父容器也可以增加mesh renderer组件用于存放材质

3.rendering mode（渲染模式）：

·opaque：不透明的

·cutout：透明通道去掉，显示不透明部分

·transparent：透明的（玻璃），需要在Albedo中设置颜色，调节A通道

·fade：淡入淡出，调节A通道，可以变透明完全看不见

4.metallic设置金属度

## 坐标

X：红色（左右），Y：绿色（上下），Z：蓝色（前后）

世界坐标：整个场景的固定坐标，不随物体改变而改变

本地坐标：物体自身坐标，随旋转而改变

场景：一组关联游戏对象的集合，展现关卡中的所有物体，Ctrl+S保存当前场景，后缀为unity，Ctrl+N新建场景

游戏对象：一种容器，挂载组件

组件：功能模块，一个类的实例，

· Transform变换组件：决定物体大小、位置、旋转；

· mesh filter网格过滤器（决定形状）：用于从资源中获取网格信息

· mesh renderer网格渲染器（决定外观）：从网格过滤器中获得几何形状，再根据变换组件定义的位置进行渲染；

· 网格过滤器和网格渲染器联合使用，将模型显示到屏幕上

## 摄像机

附加了摄像机Camera组件的游戏对象；多个摄像机时将其他Audio Listener取消，只留一个主摄像机

1）添加层：

![image-20210718200255515](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210718200255515.png)

Layer->add Layer，集合物体可以放在同一层内，集合中某一物体也可以单独设置为一层

2）添加后在物体的layer中选中新加入的层，

3）在摄像机组件中取消不想看到的物体层

![image-20210718202429431](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210718202429431.png)



组件：

一、transform ：变换组件 

二、Camera ：向玩家捕获和显示世界

### ·clear flags：选择空白部分如何处理（solid color表示纯色填充）

### 		· skybox

​		围绕整个场景的包装器，用于模拟天空的材质

​			1）6sided 表示自定义六个面的图片作为天空盒，上下左右前后（project->create->material->skybox->6sided）使用方法一：添加skybox组件；使用方法二：window->Lighting->Environment Lighting->skybox中选择自定义天空盒,可作为反射源将天空色彩反射到场景物体中）

​			2）procedural为默认天空盒，系统自带太阳属性

### · culling mask选择遮罩（摄像机可以看到所选层，没选该层则相机看不见，看不见的层不渲染）

### · projection 投射关系（1.perspective 3D近大远小 2.orthographic 2D没有远近之分）

### · field of view（放大镜，60默认）

### · clipping planes（选择视锥的最大视角和最小视角，在视角内才渲染）

### ·viewpoit rect（W：game视窗的宽，H：game视窗的高，X：game视窗的x轴，Y：game视窗的y轴）

### ·depth（深度值，主屏幕深度值小于子屏幕深度值，深度值大的盖住深度值小的）

3.Flare Layer 耀斑层：激活可显示光源耀斑 （用的少）

4.GUI Layer：激活可渲染二维GUI元素 （用的少）

5.Audio LIstener音频监听器：接收场景输入的音频源并播放（多个摄像机时只允许保持一个音频）

# InstantOC

![image-20210719180426237](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210719180426237.png)



## 一、渲染管线

![image-20210719175039966](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210719175039966.png)

Draw Call：![image-20210719175240224](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210719175240224.png)CPU：

计算待渲染物体的顶点数据，调用Draw Call，最后数据交给

### GPU。

### GPU：

1.顶点处理：接收模型顶点数据（CPU传来）；坐标系转换

2.图元装配：组装面，连接相邻顶点绘制为三角形

3.光栅化：计算三角面上的像素，并为着色阶段提供合理的插值

4.像素处理：对每个像素区域进行着色，写入缓存

5.缓存：一个存储像素数据的内存块，最重要的缓存是帧缓存和深度缓存。

​	1）帧缓存：存储每个像素的色彩，即渲染后的图像，帧缓存在显卡中，显卡不断读取并输出到屏幕。

​	2）深度缓存：存储像素的深度信息，即物体到摄像机的距离（光栅化时已经计算好了），若新的深度值比现有深度值更近，像素颜色才会被写入帧缓存中，并替换深度缓存。

## 二、即时遮挡剔除 Instant Occlusion Culling

1.遮挡剔除：当物体被送进渲染流水线之前，将摄像机视角内看不到的物体进行剔除，减少每帧渲染数据量，提高性能。（场景密集时使用）

​	1）将IOCcam拖到摄像机上。

​	2）将参与遮挡剔除的物体放在层和tag中，然后在插件中选择参与遮挡替代的层和tag。（原理是让摄像机随机发射射线若打中则看得见，打不中则取消物体的渲染组件）

​	3）给物体增加碰撞组件（box Collider)

## 三、多细节层次 LOD

LOD技术指根据物体模型的节点在显示环境中所处的位置和重要度，决定物体渲染的资源分配，降低非重要物体的面数和细节度，提高渲染效率。

# 光照系统

## 一、全局光照 GI

能够计算直接光、间接光、环境光以及反射光的光照系统；通过GI算法可以使渲染出来的光照效果更为真实。

Light->point：点光源，圆球型光源（同一场景可以加多个光源，均匀分布）

Light->spot：手电筒光源

​	1）range范围：调节光从物体中心发射的范围，适用于点光源和手电筒

​	2）spot Angle 聚光灯角度：灯光的聚光角度，适用于聚光灯

​	3）color颜色：光线的颜色

​	4）Intensity强度：光线明亮程度

​	5）Culling Mask 选择遮蔽层：选择要照射的层layer

## 阴影

灯光中可以选择有无阴影

![image-20210720164438054](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210720164438054.png)

当某个物体不想要阴影时，在物体的mesh renderer组件中取消（mesh renderer->cast shadows->off）

## 二、环境光照

Environment Lighting控制，Intensity Multiplier调节反射关照强度，source光照来源（一般为天空盒）。

![image-20210720165204811](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210720165204811.png)

## 三、反射光照

Environment Lighting->Reflection控制，Intensity Multiplier调节反射关照强度。

![image-20210720165614683](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210720165614683.png)

## 四、间接光照

物体表面在接收光照后反射出来的光，通过Light组件中Indirect Multiplier控制强度

![image-20210720170714173](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210720170714173.png)

需要将静止物体设为static，需要计算静态物体的光照效果

![image-20210720170315314](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210720170315314.png)

## 五、实时光照（Realtime GI）

在开发时进行预计算，将游戏对象设为static静态

## 六、烘焙光照（烘焙GI）

场景中包含大量物体时，实时光照和阴影对游戏性能有很大影响。使用烘焙技术，可以将光线效果预渲染成贴图再作用到物体上模拟光照，从而提高性能，例如手游等。

![image-20210720171813275](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210720171813275.png)

选择baked为烘焙光照。Mixed为混合模式。

## 七、光源侦测（Light Probes）

由于烘焙光只能作用于static物体上，导致运动物体无法接收光照，增加光源侦测，使光存储在侦测小球中，小球为运动物体投射光源。

![image-20210720174528828](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210720174528828.png)

# 声音

3D声音：有空间感，近大远小

2D声音：背景音乐

## 一、Audio Listener组件

和摄像机在一起

## 二、Audio Source

![image-20210720175754085](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210720175754085.png)

loop：循环播放

3D音乐设置：

Volume Rolloff（音乐衰减方式，一般选Linear Rolloff线性）

![image-20210720175950213](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210720175950213.png)

# C#基础

## 一、输入输出

```c#
Console.Title = "第一个程序";//设置程序title，title为Console中属性
Console.WriteLine("你好，世界");//从控制台接收

Console.ReadLine();//使程序停止在这一行

//从键盘输入需要用readline函数读入键盘的值，输出需要用writeline函数+readline函数
//键入
Console.WriteLine("请输入你的名字：");
string name = Console.ReadLine();//读入键盘输入放在name里
//输出
Console.WriteLine("我的名字是："+name);
Console.ReadLine();//将WriteLine函数构造好的语句输出

//占位符{位置的编号}
string str = string.Format("枪的名称为：{0}，容量为：{1}",gunname,gunrongliang);
//标准数字字符串格式化
Console.WriteLine("金额：{0:c}",10);//金额：￥10.00
Console.WriteLine("金额：{0:d2}",5);//金额：05，两位占位
Console.WriteLine("金额：{0:f1}",5.26);//金额：5.3，指定精度，四舍五入
Console.WriteLine("金额：{0:p}",0.526);//金额：52.60%，默认保留两位
Console.WriteLine("金额：{0:p0}",0.526);//金额：53%，百分号，四舍五入
```

1）Console是一个类，WriteLine和ReadLine是方法。

2）全部对齐：全选后 Ctrl+K+F

3）全部注释：Ctrl+K+C

4）取消注释：Ctrl+K+U

## 二、变量

1）变量类型 变量名称;

2）转义符：改变字符原始含义用\

```c#
Console.WriteLine("我爱\"Unity!\"");//我爱"Unity!"
char c1 = '\0';//空字符
//	\r\n换行，\t空格
Console.WriteLine("你好，\r\n我是\txxx.");
//你好，
//我是	xxx.
```

```c#
//.NET编译过程
/*源代码（.cs的文本文件）————>CLS编译————>CIL通用中间语言（.exe文件）————CLR编译————>机器码01
						目的：跨语言						 目的：优化 跨平台
*/
```

3）算术运算符：+，-，*，/，%。

4）快捷运算符：+=，-=，*=，/=，%=。

5）二元运算符：自增、自减。i++（先取值再加一）；++i（先加一再取值）；i--（先取值再减一）；--i（先减一再取值）；&&；||。

```c#
int n1 = 1,n2 = 2;

bool res1 = n1 > n2 && n1++ >1;//&&运算 一假则假 前面有假则不看后面
Console.WriteLine(n1);//1

bool res2 = n1 < n2 && n2++ <1;//||运算 一真则真 前面有真则不看后面
Console.WriteLine(n2);//2
```

6）三元运算符：数据类型 变量名 = 条件 ？满足条件结果：不满足条件结果。

7）优先级：先乘除后加减，小括号最高

## 三、数据类型转换

```c#
//1.Parse转换：string转其他类型
//待转数据必须像目标类型
string strNumber = "18";
int num01 = int.Parse(strNumber);//将string转为int型,18
float num01 = float.Parse(strNumber);//将string转为float型,18.0
//2.任意类型转换为string类型
int number = 18；
string str = number.ToString();
//3.隐式类型转换
byte n1 = 100;
int n2 = n1;
//4.显式转换
int n3 = 100;//因为int占4字节，byte只占1字节，转换需要舍去精度
byte n4 = (byte)n3;//1字节8位
```

## 四、随机数

```c#
Random random = new Random();//创建随机数工具
int num = random.Next(1,101);//产生随机数，左闭右开
```

## 五、常用方法

访问修饰符：public（公开）private（隐私）

可选修饰符：static（静态）

[访问修饰符] [可选修饰符] 返回类型 方法名称（参数列表）{

​	//方法体

​	return 结果

}

main方法中使用函数名调用函数。

```c#
private static void Fun1(参数列表){
    //方法体
    return	;
}

//C#中根据年月日得到是周几的函数
DateTime dt = new DateTime(inputyear, month, day);
return (int)dt.DayOfWeek;//需要强转为int型比较

Array.IndexOf(数组名，待查元素);//返回元素在数组内第一个下标，不存在返回-1

//排序
Array.Sort(ticket, 0, 6);//从0开始排6个
Array.Sort(数组名, 起始, 长度);

//foreach加强for循环
foreach(int it in arr){
    Console.WriteLine(it);
}

```

## 六、2048游戏实现

```c#
using System;

namespace Day04
{
    class Program
    {
        private static int[,] arr_2048 = new int[4, 4];
        private static Random random = new Random();
        private static void Create_2()
        {
            while (true)
            {
                int h = random.Next(0, 4);
                int l = random.Next(0, 4);
                if (arr_2048[h, l] == 0)
                {
                    arr_2048[h, l] = 2;
                    break;
                }
            }
            
        }
        private static void print_2048()
        {
            for(int i = 0; i < 4; i++)
            {
                for(int j = 0; j < 4; j++)
                {
                    Console.Write(arr_2048[i, j]+"\t");
                }
                Console.WriteLine();
            }
        }
        private static void w_move()
        {
            //有数字的上移
            for (int i = 0; i < 4; i++)
            {
                int k = 0;
                for (int j = 0; j < 4; j++)
                {
                    if (arr_2048[j, i] != 0)
                    {
                        arr_2048[k++, i] = arr_2048[j, i];
                    }
                }
                for (; k < 4; k++)
                {
                    arr_2048[k, i] = 0;
                }
            }
            for (int i = 0; i < 4; i++)//列
            {
                for(int j = 1; j < 4; j++)//行
                {
                    if(arr_2048[j - 1, i]!=0&& arr_2048[j - 1, i]== arr_2048[j, i]){//相同相加
                        arr_2048[j - 1, i] += arr_2048[j, i];//加到前一个上
                        arr_2048[j, i] = 0;//后一个设为0

                    }
                }
            }
            //有数字的上移
            for(int i = 0; i < 4; i++)
            {
                int k = 0;
                for (int j = 0; j < 4; j++)
                {
                    if (arr_2048[j, i] != 0)
                    {
                        arr_2048[k++, i] = arr_2048[j, i];
                    }
                }
                for (; k < 4; k++)
                {
                    arr_2048[k, i] = 0;
                }
            }
        }
        private static void a_move()
        {
            //有数字的左移
            for(int i = 0; i < 4; i++)
            {
                int k = 0;
                for(int j = 0; j < 4; j++)
                {
                    if (arr_2048[i, j] != 0)
                    {
                        arr_2048[i, k++] = arr_2048[i, j];
                    }
                }
                for (; k < 4; k++)
                {
                    arr_2048[i, k] = 0;
                }
            }
            //合并
            for (int i = 0; i < 4; i++)
            {
                for (int j = 1; j < 4; j++)
                {
                    if (arr_2048[i, j] != 0 && arr_2048[i, j] == arr_2048[i, j - 1])
                    {
                        arr_2048[i, j - 1] += arr_2048[i, j];
                        arr_2048[i, j] = 0;
                    }
                }
            }
            //有数字的左移
            for (int i = 0; i < 4; i++)
            {
                int k = 0;
                for (int j = 0; j < 4; j++)
                {
                    if (arr_2048[i, j] != 0)
                    {
                        arr_2048[i, k++] = arr_2048[i, j];
                    }
                }
                for (; k < 4; k++)
                {
                    arr_2048[i, k] = 0;
                }
            }
        }
        private static void s_move()
        {
            //有数字的下移
            for (int i = 3; i >= 0; i--)
            {
                int k = 3;
                for (int j = 3; j >= 0; j--)
                {
                    if (arr_2048[j, i] != 0)
                    {
                        arr_2048[k--, i] = arr_2048[j, i];
                    }
                }
                for (; k >= 0; k--)
                {
                    arr_2048[k, i] = 0;
                }
            }
            for (int i = 3; i >= 0; i--)//列
            {
                for (int j = 2; j >= 0; j--)//行
                {
                    if (arr_2048[j + 1, i] != 0 && arr_2048[j + 1, i] == arr_2048[j, i])
                    {//相同相加
                        arr_2048[j + 1, i] += arr_2048[j, i];//加到前一个上
                        arr_2048[j, i] = 0;//后一个设为0

                    }
                }
            }
            //有数字的下移
            for (int i = 3; i >= 0; i--)
            {
                int k = 3;
                for (int j = 3; j >= 0; j--)
                {
                    if (arr_2048[j, i] != 0)
                    {
                        arr_2048[k--, i] = arr_2048[j, i];
                    }
                }
                for (; k >= 0; k--)
                {
                    arr_2048[k, i] = 0;
                }
            }
        }
        private static void d_move()
        {
            //有数字的右移
            for (int i = 3; i >= 0; i--)
            {
                int k = 3;
                for (int j = 3; j >= 0; j--)
                {
                    if (arr_2048[i, j] != 0)
                    {
                        arr_2048[i, k--] = arr_2048[i, j];
                    }
                }
                for (; k >= 0; k--)
                {
                    arr_2048[i, k] = 0;
                }
            }
            //合并
            for (int i = 3; i >= 0; i--)
            {
                for (int j = 2; j >= 0; j--)
                {
                    if (arr_2048[i, j] != 0 && arr_2048[i, j] == arr_2048[i, j + 1])
                    {
                        arr_2048[i, j + 1] += arr_2048[i, j];
                        arr_2048[i, j] = 0;
                    }
                }
            }
            //有数字的右移
            for (int i = 3; i >= 0; i--)
            {
                int k = 3;
                for (int j = 3; j >= 0; j--)
                {
                    if (arr_2048[i, j] != 0)
                    {
                        arr_2048[i, k--] = arr_2048[i, j];
                    }
                }
                for (; k >= 0; k--)
                {
                    arr_2048[i, k] = 0;
                }
            }
        }
        private static void move__2048(string flag)
        {
            if (flag == "w")
            {
                w_move();
                Create_2();
            }
            else if (flag == "a")
            {
                a_move();
                Create_2();
            }
            else if (flag == "s")
            {
                s_move();
                Create_2();
            }
            else if (flag == "d")
            {
                d_move();
                Create_2();
            }
        }
        private static bool Panwin()
        {
            int zeros = 0;
            foreach(int it in arr_2048)
            {
                if (it == 2048)
                {
                    Console.WriteLine("恭喜您，胜利了！");
                    return true;
                }
                if (it == 0) zeros++;
            }
            if (zeros == 0)
            {
                Console.WriteLine("很遗憾，您填满了整个屏幕，失败！");
                return true;
            }
            return false;
        }
        static void Main(string[] args)
        {
            Create_2();//创建2048的二维数组
            Console.WriteLine("————————游戏开始————————");
            print_2048();//展示数组
            Console.WriteLine("请输入方向wasd，输入#号键退出...");
            string step = Console.ReadLine();
            while (step != "#")
            {
                if(step=="w"|| step == "a" || step == "s" || step == "d")
                {
                    move__2048(step);
                    print_2048();
                    if (Panwin()) break;
                    Console.WriteLine("请输入方向wasd，输入#号键退出...");
                    step = Console.ReadLine();
                }
                else
                {
                    Console.WriteLine("请输入正确的方向键wasd，输入#号键退出...");
                    step = Console.ReadLine();
                }
            }
        }
    }
}

```

## 七、数组、交错数组和参数数组

```c#
//申请数组
int[] day = new int[] { 0, 31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };
//二维数组
int[,] arr=null;
arr = new int[5,3];
arr[0,1]=2;//第一行第二列存为2
arr.GetLength(0);//获取行数

//交错数组
int[][] array02;//null
//创建具有4个元素的交错数组
array02 = new int[4][];//交错数组元素数量为每个申请一维数组size的和
//创建一维数组 赋值给 交错数组的第一个元素
array02[0] = new int [3];
array02[1] = new int [5];
array02[2] = new int [4];
array02[3] = new int [1];
//在交错数组的第一个元素的第一个元素
array02[0][0] = 1;



//参数数组
//params 参数数组
//对于方法内部而言：就是普通数组
//对于调用者而言：可以传递数组 传递一组数据类型相同的变量集合 可以不传参数
//简化调用者调用方法的代码
private static int Add(params int[] arr)
{
	//方法体
}
static void Main(string[] args){
	int res1 = Add(new int[] { 1, 2, 3, 4, 5, 6 });//若没加params则必须传入一个数组
	int res2 = Add(1, 2, 3, 4, 5, 6);//若加入params关键字，可以直接传入相同数据类型的集合
	int res3 = Add();//使用params关键字可以传空值
}
```

## 八、数据类型

### 1、值类型：存值	

​	1）结构：数值类型、bool、char

​	2）枚举

### 2、引用类型：存地址

​	1）借口

​	2）类：string、array、委托

### 3、内存与分配

程序运行需要在内存中申请空间，CLR将申请的内存空间从逻辑上划分

栈区：

> 空间小（1MB），读取快
>
> 用于存储正在执行的方法，分配的空间叫栈帧。栈帧存储方法的参数以及变量，执行完毕后清除。

堆区：

> 空间大，读取慢
>
> 用于存储引用类型数据
>
> 堆中只能新建、清楚不能修改

### 4、值类型与引用类型

值类型：声明在栈中，数据存在栈中。

引用类型：声明在栈中，数据存在堆里，栈中存数据引用地址。

```c#
//int在栈中，数据在栈中
int a = 1;
int b = a;
a = 2;
Console.WriteLine(b);//b==1;

//int[]声明在栈中，数据在堆，栈中存地址
int[] arr1 = new int[] { 1 };
int[] arr2 = arr1;//arr2中存的arr1的地址
arr1[0] = 2;//堆中数据改变
Console.WriteLine(arr2[0]);//arr2[0]==2

//string是引用类型，声明在栈中，数据在堆里，栈中存地址
string s1 = "男";//堆中存“男”，栈中开辟空间存堆中数据地址
string s2 = s1;//s2指向s1的地址
s1 = "女";//s1指向堆中新的空间
Console.WriteLine(s2);//男

//引用类型，声明都在栈
object o1 = 1;
object o2 = o1;
o1 = 2;
Console.WriteLine(o2);//1

//方法传入引用可以改原本元素值
```

### 5、值参数与引用参数

> 值参数：按值传递 -- 传递实参变量存储的内容
>
> 作用：传递信息
>
> 引用参数：按引用传递 -- 传递实参变量自身的内存地址
>
> 作用：改变数据
>
> 输出参数：按引用传递 -- 传递实参变量自身的内存地址
>
> 作用：返回结果

```c#
private static void Fun1(int a,int[] arr){
    //方法体
}
private static void Fun2(ref int a){
    //方法体
    //方法内部修改引用参数，实质上修改了实参变量
}
private static void Fun2(out int a){
    //方法体
    a = 2;
}
static void Main(string[] args){
    int a = 1;
    Fun1(a,arr);
    int a2 = 1;
    Fun2(ref a2);//按引用传值需要写上ref
    int a3;//用于接收方法结果
    Fun2(out a3);//按引用传值需要写上out
}
//ref和out区别：
//1.输出参数必须在函数内部赋值（out出去前必须有值）
//2.ref在传入前必须赋值，输出参数传递前可以不赋值（ref传入前必须有值）
//多返回值时，使用out输出参数返回多个结果
```

### 6、垃圾回收器

GC是CLR中一种针对托管堆自动回收释放内存的服务。

从栈中的引用开始跟踪，从而判断哪些内存是正在使用的，若GC无法跟踪到某一块堆内存，那么就认为该内存不再使用，即为可回收。

少产生垃圾，指定时间回收垃圾。

引用类型在堆中申请空间会产生垃圾。

### 7、拆装箱

形参object类型，实参传递值类型，则装箱

可以通过重载、泛型避免

```c#
static void Main(string[] args){
    //装箱操作：值类型隐式转换为object类型或由此值类型实现的任何借口类型的过程
    int a = 1;//值类型
    //比较消耗性能
    object o = a;//引用类型，声明在栈中，需要先去堆中开辟空间o存地址
    //在堆内存中开辟三块空间（存数据、同步块索引、类型对象指针）
    
    //拆箱操作：从object类型到值类型或从借口类型到实现该接口的值类型的显式转换
    int b = (int)o;
    //比较消耗性能
    //1.检查o的堆中空间数据类型是否相同
    //2.将数据赋值到b
    
    //装箱比拆箱消耗性能
    
    //不同类型拼接会发生拆装箱
    num+"";//会发生
    num.ToString();//不会发生
}
```

### 8、字符串

字符串池：字符串具有不可变性，更改字符串内容等于在堆中开辟了新空间放入新值，栈中s1存的地址改为新地址，原先堆中旧内容丢弃。

```c#
String strNum = "";
for(int i = 0;i < 10;i++){
    //每次拼接产生新的对象 替换引用（原有内容变为垃圾）
    strNum = strNum + i.ToString();
}

//频繁对字符串操作使用可变字符串（增 删 改）
//可变字符串：可以在原有空间修改内容
StringBuilder builder = new StringBuilder(10);//一次性开辟可容纳10个字符大小的空间，避免产生垃圾
for(int i = 0;i < 10;i++){
    builder.Append(i);//一次开很大的空间，拼接在同一块空间进行
}
//builder是可变大小，超出原定大小再次开辟更大空间，拷贝数据
return builder.ToString();
builder.Insert(0,"abc");//直接在idx位插入
builder.Replace();
builder.Remove();
```



![image-20210723184231901](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210723184231901.png)

### 9、枚举

枚举类是值类型

选择多个枚举值使用运算符|（按位或运算）：当两个对应的二进制位中有一个为1，结果位为1

0000000000 	|	 0000000001	==>0000000001

条件：

1.任意多个枚举值做 | 运算 的结果不能与其他枚举值相同

2.定义枚举时，使用[Flags]修饰

```c#
[Flags]
enum PersonStyle{
    tall = 1;		//0000000000
	rich = 2;		//0000000001
	handsome = 4;	//0000000010
	white = 8;		//0000000100
	beauty = 16;	//0000001000
	//值为2的n次方
}
```

判断标志枚举 是否包含指定枚举值

&（按位与运算）：两个对应的二进制位中都为1，结果位为1。

0000000011	&	0000000001	==>	0000000001

```c#
//数据类型转换
//int	==>	Enum
枚举类名称 style01 = (枚举类名称)2;
//Enum	==>	int
int num = (int)(枚举类名称.枚举元素);

//string	==>	Enum
//"beauty"
枚举类名称 style02 = (枚举类名称)Enum.Parse(typeof(枚举类名称),"beauty");//Enum.Parse为所有枚举类提供基类，传入枚举类型和字符串
//Enum	==>	string
string str = 枚举类名称.枚举类元素.ToString();
```

### 10、类和对象

1）面向对象：

> 一种开发思想

2）类：

> 是一个抽象概念，即为生活中的“类别”。

```c#
//类结构
访问级别 class 类名{
    字段：存储数据
    属性：保护手段
    构造函数：提供创建对象的方式，初始化类的数据成员
    方法：向类外提供某种功能
}
```

3）对象：

> 是类的具体实例，及归属于某类的“个体”。

4）成员变量：

> 1.具有默认值	2.存在堆里	3.可以与局部变量重名	4.成员变量的值类型和引用类型声明都在堆中	5.值存储在堆中引用存储地址在堆中

```c#
//创建类
访问级别 class 类名{
    类成员
}
//每个类在独立的c#源文件中
//创建了新的类意味在当前项目中产生了一种新的数据类型（引用）
```

```c#
class Wife{
    //数据成员
    private string name;
    private string sex;
    private int age;
    //方法成员
    public void SetName(string name){
        //this 这个对象（引用）
        this.name = name;//this.name里存name的地址
    }
    public string GetName(){
        return nams;
    }
    public void SetName(int age){
        //this 这个对象（值）
        this.age = age;//this.age里存age的值
    }
}
static void Main(){
    //声明Wife类型的引用
    Wife wife01;
    //指向Wife类型的对象（实例化Wife类型对象）
    wife01 = new Wife();//在堆上开辟数据成员总和的空间
    
    wife01.SetName("xxx");
    wife01.SetAge(18);
    
    Wife wife02 = wife01;//wife02存的wife01的地址
    wife02.SetName("yyy");//输出wife01的name变为yyy
}
```

5）访问修饰符：

> 默认private	public	

```c#
//属性：保护字段 本质是两个方法
//Wife类中成员
private string name;
public string Name{
    //读取保护
    get{return name;}
    //写入保护 value关键字表示要设置的数据
    set{this.name = value;}
}
private int age;
public int Age{
    //读取保护
    get{return age;}
    //写入保护 value关键字表示要设置的数据
    set{
        if(value > 30)	throw new Exception("erro");
        else	this.age = value;
    }
}
//使用
Wife wife03 = new Wife();
wife03.Name = "aaa";//本质调用set
Console.WriteLine(wife03.Name);//调用get方法
```

6）构造函数：

> 提供了创建对象的方式，常常用于初始化类的数据成员，自带默认无参构造函数，若自定义构造函数则默认构造取消，需要写无参和有参两种。

```c#
//Wife类
//构造函数名与类名相同，没有返回值，若不希望在类的外部创造对象就将构造函数私有化
public Wife(){
    //无参构造函数
}
public Wife(string name,int age)this(name){//调用一个名字的构造函数
    //有参构造函数
    this.name = name;//构造函数如果为字段赋值，属性中的代码块不会执行
    //this.age = age;//绕过属性的判断
    this.Age = age;//使用Age属性set方法
}
//在构造函数中调用其他构造函数
public Wife(string name):this(){
    this.name = name;
}
//使用
Wife wife04 = new Wife("bbb",19);//调用有参构造函数
Wife wife05 = new Wife();//调用无参构造函数
Wife wife06 = new Wife("ccc");//调用有参构造，在有参构造中调用无参构造


//.Net3.0后自动生成属性
public string Password{get;set;}//自动属性 包含一个字段 两个方法
private int size;
public int count{//属性 只读
    get{return size;}
}

//C# 泛型集合   List<数据类型>
List<User> list02 = new List<User>;
list02.Add(u1);
list02.Insert();//插入
list02.RemoveAt();//根据索引删
list02.Remove();//根据元素删

//字典集合 
Dictionary<string,User> dic = new Dictionary<string,User>;
dic.Add("xxx",new User("xxx","1234"));
User user = dic["xxx"];//直接取值，如同map
```

### 11、继承、static和结构体

```c#
protected //受保护的访问，子类可以使用
private //隐私成员，子类无法使用
    
//子类 可以使用父类

//父类型的引用 指向 子类对象，只能使用父类成员
Person person02 = new Student();
Student stu02 = (Student)person02;//将父类显式转换为子类
//异常，兄弟间无法转换
Teacher teacher02 = (Teacher)person02;//person02父类指向的student类对象，无法转换为Teacher类，可以显式转换为student类
//使用as，如果转换失败不会抛出异常
Teacher teacher02 = person02 as Teacher;//实际 teacher02为空，无法将person02转为Teacher类
```

```c#
//static关键字
//static修饰成员变量，静态变量属于类单独存储，在加载类时初始化，实例变量属于对象在创建是初始化
Student stu01；//类被加载
stu01 = new Student();//创建对象，初始化实例变量

//静态成员
//Student类
public static int cnt;//仅存储一份，其余共享
//使用
Console.WriteLine(Student.cnt);//静态变量使用类名调用

//静态构造函数作用：初始化类的静态数据成员
//执行时机：类加载时调用一次
//Student类静态构造方法，不允许使用访问修饰符
static Student(){
    
}

//静态方法
//静态代码块，只能访问静态成员
public static void Fun1(){
    访问实例成员//无法访问，静态成员创建时间早，调用实例方法时，实例方法还没创建
}
public void Fun2(){
    访问实例成员//可以直接访问，使用stu03.Fun2();每次调用自动传入一个引用即为this指针
}

//静态类：不能实例化，只能包含静态成员，不能被继承
//但是实例类中的静态方法、属性可以被继承
//利：共享数据做成静态，节约空间，使用方便（类名.属性）
//弊：静态方法只能访问静态成员，共享数据被多个对象访问会出现并发
//1.所有对象需要共享
//2.在没有对象前就要访问的成员
//3.工具类适合做静态类
```

```c#
//结构体：属于值类型，用于封装小型相关变量
//结构体属于值类型，声明和数据都在栈中；类属于引用类型，声明在栈中，数据在堆中。
//结构体自带无参数构造函数，不能自行写出
//有参构造函数中必须先为字段赋值，需要调用无参构造函数
public Direction(int rIndex,int cIndex):this()
{
	//构造函数中必须先为字段赋值，需要调用无参构造函数
	RIndex = rIndex;//:this()有参构造函数 先调用无参构造函数，为自动属性的字段赋值
	CIndex = cIndex;
}
//其余语法与类相同

//const常量，无法更改
```

# 脚本

> .cs文件，脚本是附加在游戏物体上用于定义游戏对象行为的指令代码

## 一、常用API

```c++
1）语法
using 命名空间;
public class 类名:MonoBehaviour{//普通c#类不需要挂载物体时可以不继承
    void 方法名(){
        Debug.Log("调试显示信息");
        print("本质就是Debug.Log方法");
    }
}
//1.文件名与类名必须一致
//2.写好的脚本必须附加到物体上才执行
//3.附加到游戏物体的脚本类必须从MonoBehavior类继承

2）编译过程
源代码——>（CLS）——>中间语言——>（Mono Runtime，转换作用）——>机器码（可以在不同平台运行）
```

类名和文件名一致

![image-20210730165843154](C:\Users\Jiao1\AppData\Roaming\Typora\typora-user-images\image-20210730165843154.png)

把脚本挂载在游戏物体上，实质上创建了一个对象，若需要调用其他组件，可以使用对象找到组件引用地址进而调用其中的属性。

### 1、MonoDevelop

> unity3D自带编译器

可以从unity3D中修改默认编译器，Edit——>Preferences——>External Tools——>External Script——>Editor

### 2、脚本的生命周期

> 1）Awake()：初始化，最先调用
>
> 2）Start()：初始化，比Awake慢
>
> 3）FixedUpdate()：用于对象做物理操作，默认0.02s调用
>
> 4）Update()：游戏逻辑，渲染时调用

```c#
public class Lifecycle : MonoBehaviour 
{
    //C#类：1.字段	2.属性	3.构造函数	4.方法

    //脚本：1.字段（属性在编译器中不能显示）	2.方法
  
    //脚本：.cs的文本文件   类文件
    //  附加到游戏物体上，定义游戏对象行为代码

    [SerializeField]//序列化字段，在编辑器中显示私有变量
    private int a;
    //public int b = 100;//公开属性可以在unity中更改
    [HideInInspector]//在编译器中隐藏字段
    public int b;
    [Range(0,100)]//设置更改范围
    public int c;
    //属性：在编译器中不显示，脚本通常不写
    /*public int A
    {
        get { return this.a; }
        set { this.a = value; }
    }*/

    /*public Lifecycle()//不能在脚本中写构造函数
    {
        //不能在子线程调用主线程成员
        b = (int)Time.time;
        Debug.Log("构造函数");//会调用两次
    }*/

    //**********************************初始阶段**********************************
    //unity单线程执行，Awake比Start先执行
    //先执行所有物体的Awake
    //执行时机：创建游戏对象时
    //作用：初始化对象，放在哪个都行
    //Awake在游戏物体创建立即执行，Start在游戏物体创建脚本启用后才执行
    //onEnable方法：每当脚本启用时调用
    private void Awake()//可以判断当满足某种条件执行此脚本 this.enable=true;（启用）
    {
        Debug.Log("Awake----" + Time.time + "----" + this.name);
    }
    private void Start()
    {
        Debug.Log("Start----" + Time.time + "----" + this.name);
    }

    //**********************************物理阶段**********************************
    //执行时机：脚本启用后，固定时间被调用，默认频率0.02s
    //用处：用于游戏对象做物理操作，不会受到渲染影响
    private void FixedUpdate()
    {
        //渲染时间不固定（每帧渲染量不同、机器性能不同）
        //Debug.Log(Time.time);
    }

    private void OnMouseDown()
    {
        Debug.Log("OnMouseDown");
    }

    //**********************************游戏逻辑**********************************
    //执行时机：渲染帧执行，执行间隔不固定
    //用处：处理游戏逻辑
    //LateUpdate：延迟更新，在Update被调用后执行，适用于跟随逻辑（游戏对象移动代码放在Update，视角跟随放在LateUpdate）
    private void Update()
    {
    }
}
```

#### 1、输入事件

1）OnMouseEnter 鼠标移入：鼠标移入当前Collider时调用。

2）OnMouseOver 鼠标经过：鼠标经过当前Collider时调用。

3）OnMouseExit 鼠标离开：鼠标离开当前Collider时调用。

4）OnMouseDown 鼠标按下：鼠标按下当前Collider时调用。

5）OnMouseUp 鼠标抬起：鼠标在当前Collider抬起时调用。

#### 2、场景渲染

1）OnBecameVisible 当可见：当Mesh Renderer 在任何相机上可见时调用。

2）OnBecameInvisible 当不可见：当Mesh Renderer 在任何相机上都不可见时调用。

#### 3、结束阶段

1）OnDisable 当不可用：对象变为不可用或游戏对象非激活时调用。

2）OnDestroy 当销毁：当脚本销毁或游戏对象被销毁时调用。

3）OnApplicationQuit 当程序结束：应用程序退出时被调用。

### 3、调试

1）控制台调试：Debug.Log(变量)、print(变量)

2）定义共有变量，运行后在编译器查看
