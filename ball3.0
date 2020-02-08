#undef UNICODE
#undef _UNICODE
#include<iostream>
#include<easyx.h>//这个游戏制作需要这个图形库，原vs2010中没有，需要另外下载配置
#include<windows.h>
#include<conio.h>
#include<string>
#include<cstdlib>
#include<ctime>
#include<fstream>
using namespace std;

#define ROW 48
#define COL 64
#define NUM 64//敌人数量

enum game{SPACE,WALL,BALL,DOOR,ENEMY};
unsigned long t1,t2,tm;
unsigned long t3,t4,t;
int map[ROW][COL];
COORD ball;
COORD enemy[NUM];

int dot=1;
char dir='D';
char dir2='S';
char Time[10];//用于计时
void Save(int time);

void start();
void intro();
void record();
void chose();
void Drawmap();
void init();
void move();
void move2(int n);
void changedir();

int main()
{
	ST:initgraph(640,480);
	start();
	outtextxy(180,100,"->");
	chose();
	if(dot==1)
	{
	init();
	t=GetTickCount();
	while(1)
	{
		tm=GetTickCount();//用来计时算分的
		t2=GetTickCount();
		t4=GetTickCount();
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
		if(t4-t3>150)
		{
			for(int i=0;i<NUM;i++)
			{
				move2(i);
			}
			t3=t4;
		}
	}
	getchar();
	closegraph();
	}
	if(dot==2)
		return 0;
	if(dot==3)
	{
		initgraph(640,480);
		intro();
		getch();
		dot=1;
		goto ST;
	}
	if(dot==4)
	{
		initgraph(640,480);
		record();
		getch();
		dot=1;
		goto ST;
	}
}

void init()
{
	srand(time(NULL));
	setbkcolor(WHITE);
	memset(map,SPACE,sizeof(map));//接近100行用来设置地图
	for(int i=0;i<ROW;i++)
	{
		map[i][0]=map[i][COL-1]=WALL;
	}
	for(int i=1;i<ROW/3;i++)
	{
		map[i][COL/2+4]=WALL;
	}
	for(int i=ROW-9;i<ROW-1;i++)
	{
		map[i][COL-8]=WALL;
	}
	for(int i=ROW-3;i<ROW-1;i++)
	{
		map[i][COL-5]=WALL;
	}
	for(int i=ROW-1;i>ROW-10;i--)
	{
		map[i][COL/3-12]=WALL;
	}
	for(int i=ROW-13;i>ROW/2-16;i--)
	{
		map[i][COL/4+6]=WALL;
	}
	for(int i=ROW-15;i>ROW/2;i--)
	{
		map[i][COL/2+7]=WALL;
	}
	for(int i=ROW-13;i>ROW/2+3;i--)
	{
		map[i][COL/2+14]=WALL;
	}
	for(int i=ROW-15;i>ROW/2;i--)
	{
		map[i][COL/2+21]=WALL;
	}
	for(int i=5;i<ROW/2-6;i++)
	{
		map[i][COL/4-4]=WALL;
	}


	for(int j=1;j<COL-1;j++)
	{
		map[0][j]=map[ROW-1][j]=WALL;
	}
	for(int i=COL/2;i<COL-1;i++)
	{
		map[ROW/2][i]=WALL;
	}
	for(int i=COL/2;i>0;i--)
	{
		map[4][i]=WALL;
	}
	for(int i=COL/4+6;i<COL/2+4;i++)
	{
		map[ROW/2-5][i]=WALL;
	}
	for(int i=COL/4+6;i<COL/2+4;i++)
	{
		map[ROW/2+5][i]=WALL;
	}
	for(int i=COL/4+6;i<COL/2+4;i++)
	{
		map[ROW/2+5][i]=WALL;
	}
	for(int i=COL/4+6;i>COL/4-12;i--)
	{
		map[ROW/2+2][i]=WALL;
	}
	for(int i=COL-5;i<COL-1;i++)
	{
		map[ROW-6][i]=WALL;
	}
	for(int i=COL/3-10;i<COL-1;i++)
	{
		map[ROW-12][i]=WALL;
	}
	for(int i=1;i<COL/3-14;i++)
	{
		map[ROW-12][i]=WALL;
	}


	for(int i=COL-2;i>COL-4;i--)
	{
		map[ROW-12][i]=SPACE;
	}

	map[ROW/2-5][COL/2-5]=ENEMY;
	enemy[0].X=ROW/2-5;
	enemy[0].Y=COL/2-5;
	for(int i=1;i<NUM;i++)
	{
		int ey=rand()%(ROW-2)+1;
		int ex=rand()%(COL-2)+1;
		map[ey][ex]=ENEMY;
		enemy[i].X=ROW/2-5;
		enemy[i].Y=COL/2-5;
	}
	map[1][1]=BALL;
	ball.X=1;
	ball.Y=1;

	map[ROW-2][COL-3]=DOOR;
	map[ROW-3][COL-3]=DOOR;
}

void start()//初始界面
{
	setbkcolor(WHITE);
	cleardevice();
	setbkmode(TRANSPARENT);
	settextcolor(BLUE);
	outtextxy(200,100,"1.开始游戏");
	outtextxy(200,150,"2.退出游戏");
	outtextxy(200,200,"3.游戏介绍");
	outtextxy(200,250,"4.历史记录");
	outtextxy(200, 300,"** 数字键 1,2,3 & W,S选择，Enter 键进入游戏");
	outtextxy(200, 340,"** 字母键 W,S,A,D 方向键 上下左右 控制方向");
	outtextxy(200, 380,"** 初玩者建议先看介绍");

}

void intro()//游戏介绍
{
	setbkcolor(YELLOW);
	cleardevice();
	setbkmode(TRANSPARENT);
	settextcolor(RGB(233,2,123));
	outtextxy(10,10,"有一个可怜的球陷入困境，你要帮它逃出困境");
	outtextxy(10,40,"绿色的门是出口，达到即是胜利");
	outtextxy(10,70,"蓝色的是怪物,会吃掉球,碰到会失败");
	outtextxy(10,100,"由于怪物随机出现，可能存在刚进入游戏便死掉的可能，不要惊慌，再次游戏即可");
	outtextxy(280,140,"->");
	outtextxy(300,140,"退出");
}

void record()
{
	setbkcolor(RGB(255,233,255));
	cleardevice();
	setbkmode(TRANSPARENT);
	settextcolor(RGB(233,23,233));
	ifstream fp("分数记录.txt",ios::in);
	char f[1000];
	for(int i=0;fp>>noskipws>>f[i];i++)
	{
	}
	if(!fp)
	{
		outtextxy(10,10,"不能读取记录，可能原因");
		outtextxy(10,40,"1.您不小心删除或移动了相关文件。");
		outtextxy(10,70,"2.您还未开始游戏，故没有记录。");
		outtextxy(10,100,"3.请检查电脑相关配置，可能杀毒软件禁止了该游戏正常的读取与建立文件。");
		outtextxy(280,140,"->");
		outtextxy(300,140,"退出");
	}
	else
	{
		outtextxy(10,10,f);
	}
	fp.close();
}

void chose()
{
	while(1)
	{
		char a=getch();
		if(a=='1'||a=='2'||a=='3'||a=='4'||a==(char)13)
		{
			switch(a)
			{
				case '1':
					start();
					outtextxy(180,100,"->");
					dot=1;
					break;
				case '2':
					start();
					outtextxy(180,150,"->");
					dot=2;
					break;
				case '3':
					start();
					outtextxy(180,200,"->");
					dot=3;
					break;
				case '4':
					start();
					outtextxy(180,250,"->");
					dot=4;
					break;
				case 13:
					return;
					break;
				default:break;
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
						outtextxy(180,150,"->");
						dot=2;
						break;
					case 13:
						return;
						break;
					default:break;
				}
			}
			else if(dot==2)
			{
				switch(a)
				{
					case 'w':
					case 'W':
						start();
						outtextxy(180,100,"->");
						dot=1;
						break;
					case 's':
					case 'S':
						start();
						outtextxy(180,200,"->");
						dot=3;
						break;
					case 13:
						return;
						break;
					default:break;
				}
			}
			else if(dot==3)
			{
				switch(a)
				{
					case 'w':
					case 'W':
						start();
						outtextxy(180,150,"->");
						dot=2;
						break;
					case 's':
					case 'S':
						start();
						outtextxy(180,250,"->");
						dot=4;
						break;
					case 13:
						return;
						break;
					default:break;
				}
			}
			else if(dot==4)
			{
				switch(a)
				{
					case 'w':
					case 'W':
						start();
						outtextxy(180,200,"->");
						dot=3;
						break;
					case 13:
						return;
						break;
					default:break;
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
	outtextxy(15,15,"Time:");
	sprintf(Time,"%.2fs",(float)(tm-t)/1000);
	outtextxy(55,15,Time);
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
				fillrectangle(x*10,y*10,x*10+10,y*10+10);
				break;
			case BALL:
				setlinecolor(RGB(0,245,233));
				setfillcolor(RED);
				circle(x*10+5,y*10+5,5);
				fillcircle(x*10+5,y*10+5,5);
				break;
			case DOOR:
				setlinecolor(RGB(10,45,233));
				setfillcolor(GREEN);
				fillrectangle(x*10,y*10,x*10+10,y*10+10);
				break;
			case ENEMY:
				setlinecolor(RGB(10,45,23));
				setfillcolor(BLUE);
				POINT pp[]={{x*10,y*10+5},{x*10+5,y*10},{x*10+10,y*10+5},{x*10+5,y*10+10}};
				clearpolygon(pp,4);
				fillpolygon(pp,4);
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

void Save(int t)
{
	fstream fp1("分数记录.txt",ios::app||ios::out);
	if(!fp1)
	{
		cerr<<"Error!"<<endl;
		return;
	}
	fp1<<"本次成绩:"<<t<<"s"<<endl;
	fp1.close();
	return;
}

void move()
{
	COORD next;
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
	case DOOR:
		map[ball.X][ball.Y]=SPACE;
		ball=next;
		map[ball.X][ball.Y]=BALL;
		char sss[32];
		sprintf(sss,"Time:%s",Time);
		Drawmap();
		MessageBoxA(NULL, "You win the game!!!\nYou can try again", sss, MB_OK);
		Save(tm-t);
		exit(0);
	case ENEMY:
		MessageBoxA(NULL, "You lose the game!\nPlease try again", "SORRY", MB_OK);
		exit(0);
	default:break;
	}
}

void move2(int n)
{
	COORD next;
	if((t4-t)%1500>1350)
	{
	int i;
	i=rand()%4+1;
	switch(i)
	{
	case 1:
		dir2='A';break;
	case 2:
		dir2='S';break;
	case 3:
		dir2='W';break;
	case 4:
		dir2='D';break;
	default:break;
	}
	}
	switch(dir2)
	{
	case 'A':
		next.X=enemy[n].X;
		next.Y=enemy[n].Y-1;
		break;
	case 'W':
		next.X = enemy[n].X - 1;
		next.Y = enemy[n].Y;
		break;
	case 'D':
		next.X = enemy[n].X;
		next.Y = enemy[n].Y + 1;
		break;
	case 'S':
		next.X = enemy[n].X + 1;
		next.Y = enemy[n].Y;
		break;
	default:
		break;
	}
	switch(map[next.X][next.Y])
	{
	case SPACE:
		map[enemy[n].X][enemy[n].Y]=SPACE;
		enemy[n]=next;
		map[enemy[n].X][enemy[n].Y]=ENEMY;
		break;
	case WALL:
	case DOOR:
	case ENEMY:
		switch(dir2)
		{
		case 'A':
			dir2='D';break;
		case 'W':
			dir2='S';break;
		case 'S':
			dir2='W';break;
		case 'D':
			dir2='A';break;
		default:break;
		}
		break;
	case BALL:
		MessageBoxA(NULL, "You lose the game!\nPlease try again", "SORRY", MB_YESNO);
		exit(0);
	default:break;
	}
}
