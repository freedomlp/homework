# 智能蛇实验报告
&emsp;&emsp;在上周的贪吃蛇游戏中，蛇走动的方向依靠玩家在缓冲区中**输入**的方向wasd来决定。而在本周的智能蛇游戏中，玩家无需进行任何操作，蛇会通过**算法**计算出怎样走会**最快**吃到食物。

## 核心问题
1. Q:如何判断怎样走最快？

&emsp;&emsp;A:计算出蛇头向四个方向移动后的横纵坐标，再与食物的横纵坐标对应相减并取绝对值再加和，得到移动后与食物间的距离，最小距离对应的方向即为需要走的方向。

2. Q:如何避免蛇走回头路以及撞到自己？

&emsp;&emsp;A:先判断蛇头移动后的位置，若为身体或墙壁，则将9999赋给这样走所计算出的与食物间距离。

## 伪代码
````
       Hx,Hy: 头的位置
    // Fx,Fy：食物的位置
	function whereGoNext(Hx,Hy,Fx,Fy) {
	// 用数组movable[3]={“a”,”d”,”w”,”s”} 记录可走的方向
	// 用数组distance[3]={0,0,0,0} 记录离食物的距离
	// 分别计算蛇头周边四个位置到食物的距离。H头的位置，F食物位置
	//     例如：假设输入”a” 则distance[0] = |Fx – (Hx-1)| + |Fy – Hy|
	//           如果 Hx-1，Hy 位置不是Blank，则 distance[0] = 9999
	// 选择distance中存最小距离的下标p，注意最小距离不能是9999
	// 返回 movable[p]
	}
````

## C语言实现
````
char whereGoNext(int Hx,int Hy,int foodposition[],char array[][12])	{
	char movable[]={"wasd"};
	int distance[4];
	int temp;
	int min = 12;
	distance[0] = abs(Hx - foodposition[1]) + abs(Hy - 1 - foodposition[0]);
	if(array[Hy - 1][Hx] == 'X')
		distance[0] = 9999;
	distance[1] = abs(Hx - 1 - foodposition[1]) + abs(Hy - foodposition[0]);
	if(array[Hy][Hx - 1] == 'X')
		distance[1] = 9999;
	distance[2] = abs(Hx - foodposition[1]) + abs(Hy + 1 - foodposition[0]);
	if(array[Hy + 1][Hx] == 'X')
		distance[2] = 9999;
	distance[3] = abs(Hx + 1 - foodposition[1]) + abs(Hy - foodposition[0]);
	if(array[Hy][Hx + 1] == 'X')
		distance[3] = 9999;
	for(int i = 0;i < 4;++i)	{
		min = (distance[i] < min ? distance[i] : min);
	} 
	for(int i = 0;i < 4;++i)	{
		if(distance[i] == min)	{
			printf("%c",movable[i]);
			return movable[i];
		}
	}
}