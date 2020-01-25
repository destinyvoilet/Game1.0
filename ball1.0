#undef UNICODE
#undef _UNICODE
#include<stdio.h>
#include<easyx.h>
#include<windows.h>
#include<conio.h>
#include<string.h>
#include<time.h>

#define ROW 48
#define COL 64

enum game{SPACE,WALL,BALL};
unsigned long t1,t2;
int map[ROW][COL];
COORD ball;

int dot=1;
char dir='D';
void start();
void chose();
void Drawmap();
void init();
void move();
void changedir();
int main()
{
	initgraph(640,480);
	start();
	outtextxy(260,150,"->");
	chose();
	if(dot==1)
	{
	init();
	while(1)
	{
		t2=GetTickCount();
		Drawmap();
		if(kbhit())
		{
			changedir();
			move();
			t2=GetTickCount();
			t1=t2;
		}
		if(t2-t1>25)
		{
			move();
			t1=t2;
		}
	}
	getchar();
	closegraph();
	}
	if(dot==2)
		return 0;
}
void init()
{
	srand(time(NULL));
	setbkcolor(WHITE);
	memset(map,SPACE,sizeof(map));
	for(int i=0;i<ROW;i++)
	{
		map[i][0]=map[i][COL-1]=WALL;
	}
	for(int j=1;j<COL-1;j++)
	{
		map[0][j]=map[ROW-3][j]=WALL;
	}
	map[3][5]=BALL;
	ball.X=3;
	ball.Y=5;
}
void start()
{
	setbkcolor(WHITE);
	cleardevice();
	setbkmode(TRANSPARENT);
	settextcolor(BLUE);
	outtextxy(280,150,"1.开始游戏");
	outtextxy(280,200,"2.退出游戏");
	outtextxy(200, 250,"数字键 1,2选择，Enter键进入游戏");
	outtextxy(200, 300,"字母键 W,S,A,D 方向键 上下左右 控制方向");

}
void chose()
{
	while(1)
	{
		char a=getch();
		if(a=='1'||a=='2'||a=='\n')
		{
			switch(getch())
			{
				case '1':
					start();
					outtextxy(260,150,"->");
					dot=1;
					break;
				case '2':
					start();
					outtextxy(260,200,"->");
					dot=2;
					break;
				case '\n':
				case 13:
					return;
					break;
			}
		}
		else
		{
			if(dot==1)
			{
				switch(a)
				{
					case 's':
					case 'S':
						start();
						outtextxy(260,200,"->");
						dot=2;
						break;
					case '\n':
					case 13:
						return;
						break;
				}
			}
			if(dot==2)
			{
				switch(a)
				{
					case 'w':
					case 'W':
						start();
						outtextxy(260,150,"->");
						dot=1;
						break;
					case '\n':
					case 13:
						return;
						break;
				}
			}

		}
	}
}
void Drawmap()
{
	BeginBatchDraw();
	setbkcolor(WHITE);
	settextcolor(RGB(238,0,0));
	cleardevice();
	for(int y=0;y<ROW;y++)
	{
		for(int x=0;x<COL;x++)
		{
			switch(map[y][x])
			{
			case SPACE:
				break;
			case WALL:
				setlinecolor(BLACK);
				setfillcolor(RGB(238,233,233));
				fillrectangle(x*10,y*10+20,x*10+10,y*10+30);
				break;
			case BALL:
				setlinecolor(RGB(0,245,233));
				setfillcolor(RED);
				circle(x*10+5,y*10+25,5);
				fillcircle(x*10+5,y*10+25,5);
				break;
			}
		}
	}
	EndBatchDraw();
}
void changedir()
{
	switch(getch())
	{
	case 'A':
	case 'a':
	case 75:
		dir='A';break;
	case 'S':
	case 's':
	case 80:
		dir='S';break;
	case 'W':
	case 'w':
	case 72:
		dir='W';break;
	case 'D':
	case 'd':
	case '77':
		dir='D';break;
	case 32:
		getch();break;
	default:break;
	}
}
void move()
{
	COORD next;
	int i;
	switch(dir)
	{
	case 'A':
		next.X=ball.X;
		next.Y=ball.Y-1;
		break;
	case 'W':
		next.X = ball.X - 1;
		next.Y = ball.Y;
		break;
	case 'D':
		next.X = ball.X;
		next.Y = ball.Y + 1;
		break;
	case 'S':
		next.X = ball.X + 1;
		next.Y = ball.Y;
		break;
	default:
		break;
	}
	switch(map[next.X][next.Y])
	{
	case SPACE:
		map[ball.X][ball.Y]=SPACE;
		ball=next;
		map[ball.X][ball.Y]=BALL;
		break;
	case WALL:
		switch(dir)
		{
		case 'A':
			dir='D';break;
		case 'W':
			dir='S';break;
		case 'S':
			dir='W';break;
		case 'D':
			dir='A';break;
		default:break;
		}
		break;
	default:break;
	}
}



