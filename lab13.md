# 贪吃蛇代码
````
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#define SNAKE_MAX_LENGTH 20
int len = 5;

int snakeMove(int x[],int y[],char array[][12])	{		//得到输入的方向键后，对蛇每个部位的坐标进行变化 
	char direction;
	scanf("%c",&direction);
	if(direction == 'w')	{
		if(array[y[len - 1] - 1][x[len - 1]] == 'X' || array[y[len - 1] - 1][x[len - 1]] == '*')	{	//头即将到达的地方为墙壁和自己时，死亡 
			return 0;
		}
		else if(array[y[len - 1] - 1][x[len - 1]] == '$'){		//头即将到达的地方为食物时，蛇增加一个坐标，且食物变成头，以前的头变为身体 
			array[y[len - 1] - 1][x[len - 1]] = 'H';
			array[y[len - 1]][x[len - 1]] = 'X';
			x[len] = x[len - 1];
			y[len] = y[len - 1] - 1;
			++len;
			return 2;
		}
		else if(y[len - 2] >= y[len - 1])	{					// 若为普通前进，蛇坐标更新，以前的蛇尾消失，再结合head_change 
			array[y[0]][x[0]] = ' ';
			for(int i = 0;i < len - 1;++i)	{
				x[i] = x[i + 1];
			}
			int i;
			for(i = 0;i < len - 1;++i)	{
				y[i] = y[i + 1];
			}
			y[i] = y[i] - 1;
			return 1;
		}
		else if(y[len - 2] < y[len - 1])	{  					//若走回头路，则为无效操作 
			return 1;
		}	
	}
		
	if(direction == 'a')	{
		if(array[y[len - 1]][x[len - 1] - 1] == 'X' || array[y[len - 1]][x[len - 1] - 1] == '*')	{
			return 0;
		}
		else if(array[y[len - 1]][x[len - 1] - 1] == '$')	{
			array[y[len - 1]][x[len - 1] - 1] = 'H';
			array[y[len - 1]][x[len - 1]] = 'X';
			x[len] = x[len - 1] - 1;
			y[len] = y[len - 1];
			++len;
			return 2;
		}
		else if(x[len - 2] >= x[len - 1])	{
			array[y[0]][x[0]] = ' ';
			int i;
			for(i = 0;i < len - 1;++i)	{
				x[i] = x[i + 1];
			}
			x[i] = x[i] - 1;
			for(int i = 0;i < len - 1;++i)	{
				y[i] = y[i + 1];
			}
			return 1;
		}
		else if(x[len - 2] < x[len - 1])	{
			return 1;
		}
	}
	
	if(direction == 's')	{
		if(array[y[len - 1] + 1][x[len - 1]] == 'X' || array[y[len - 1] + 1][x[len - 1]] == '*')	{
			return 0;
		}
		else if(array[y[len - 1] + 1][x[len - 1]] == '$')	{
			array[y[len - 1] + 1][x[len - 1]] = 'H';
			array[y[len - 1]][x[len - 1]] = 'X';
			x[len] = x[len - 1];
			y[len] = y[len - 1] + 1;
			++len;
			return 2;
		}
		else if(y[len - 2] <= y[len - 1])	{
			array[y[0]][x[0]] = ' ';
			for(int i = 0;i < len - 1;++i)	{
				x[i] = x[i + 1];
			}
			int i;
			for(i = 0;i < len - 1;++i)	{
				y[i] = y[i + 1];
			}
			y[i] = y[i] + 1;
			return 1;
		}
		else if(y[len - 2] > y[len - 1])	{
			return 1;
		}
	}
	
	if(direction == 'd')	{
		if(array[y[len - 1]][x[len - 1] + 1] == 'X' || array[y[len - 1]][x[len - 1] + 1] == '*')	{
			return 0;
		}
		else if(array[y[len - 1]][x[len - 1] + 1] == '$')	{
			array[y[len - 1]][x[len - 1] + 1] = 'H';
			array[y[len - 1]][x[len - 1]] = 'X';
			x[len] = x[len - 1] + 1;
			y[len] = y[len - 1];
			++len;
			return 2;
		}
		else if(x[len - 2] <= x[len - 1])	{
			array[y[0]][x[0]] = ' ';
			int i;
			for(i = 0;i < len - 1;++i)	{
				x[i] = x[i + 1];
			}
			x[i] = x[i] + 1;
			for(int i = 0;i < len - 1;++i)	{
				y[i] = y[i + 1];
			}
			return 1;
		}
		else if(x[len - 2] > x[len - 1])	{
			return 1;
		}
	}
}

void head_change(int x[],int y[],char array[][12])	{				//则产生新头，以前的头变为身子 
	array[y[len - 2]][x[len - 2]] = 'X';
	array[y[len - 1]][x[len - 1]] = 'H';
}

void put_money(char array[][12])	{								//随机生成食物 
	int random1 = rand() % 10 + 1;
	int random2 = rand() % 10 + 1;
	if(array[random1][random2] = ' ')
		array[random1][random2] = '$';
	else
		put_money(array);
}

void output(char array[][12])	{									//打印出变换后的图 
	for(int i = 0;i < 12;++i)	{
		printf("%s\n",array[i]);
	}
}

void gameover()	{													//死亡时打出此图 
	char defeat[12][12] =
		{"***********",
		 "*         *",
		 "*         *",
		 "*         *",
		 "*  GAME   *",
		 "*  OVER   *",
		 "*         *",
		 "*         *",
		 "*         *",
		 "*         *",
		 "*         *",
		 "***********"};
	output(defeat);
}

int main()	{
	int snakeX[SNAKE_MAX_LENGTH] = {1,2,3,4,5};
	int snakeY[SNAKE_MAX_LENGTH] = {1,1,1,1,1};
	char map[12][12] = 
		{"***********",
		 "*XXXXH    *",
		 "*         *",
		 "*         *",
		 "*         *",
		 "*         *",
		 "*         *",
		 "*         *",
		 "*         *",
		 "*         *",
		 "*         *",
		 "***********"};
	put_money(map);
	output(map);
	while(1)	{
		int judge = snakeMove(snakeX,snakeY,map);
		if(judge == 1) {
			head_change(snakeX,snakeY,map);
			system("cls");												//清屏函数 
			output(map);
		}
		else if(judge == 2)	{
			put_money(map);
			system("cls");
			output(map);
		}
		else if(judge == 0)	{
			system("cls");
			gameover();
			break;
		}
	}
}
````