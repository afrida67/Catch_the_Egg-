# Catch_the_Egg-
2D game in opengl


#include<windows.h>
#include <GL/glut.h>
#include <stdlib.h>
#include <math.h>
#include <stdio.h>
#define PI 3.1416
int a=0,b=0;
float p=-31.0;
//float p;
static GLfloat spin = 0.0;//initial degree for spinning
static float	tx	=  0.0;
static float	ty	=  0.0;
int w, h;
/*GLUT_BITMAP_8_BY_13
GLUT_BITMAP_9_BY_15
GLUT_BITMAP_TIMES_ROMAN_10
GLUT_BITMAP_TIMES_ROMAN_24
GLUT_BITMAP_HELVETICA_10
GLUT_BITMAP_HELVETICA_12
GLUT_BITMAP_HELVETICA_18*/
const int font=(int)GLUT_BITMAP_TIMES_ROMAN_24;
char s[30];
double t;
void bowl(){
    //float p=-31.0;
	if(p<=+15.0)
       p=p+0.007;
    else
        p=-31;
    glutPostRedisplay();
    glLineWidth(140);
    glBegin(GL_POLYGON); // It can be any type Gl_POINT,_LINE
    glColor3f(1.0f, 0.498f, 0.313f);
    glVertex2d(p+3.0,2.0);
    glVertex2d(p+0.0,2.0);
    glVertex2d(p+0.0,-2.0);
    glVertex2d(p+0.0,1.0);
    glEnd();

    glPushMatrix();
    //printf("%f , %f\n",tx , ty);
	glColor3f(1.0, 0.388, 0.278);

    glRectf(p-4.0,-2.2,p+0.0,2.0);

    glBegin(GL_POLYGON); // It can be any type Gl_POINT,_LINE
    glColor3f(1.0f, 0.498f, 0.313f);

    glVertex2d(p-4.0,2.0);
    glVertex2d(p-6.0,2.0);
    glVertex2d(p-8.0,2.0);
    glVertex2d(p-4.0,-2.0);

    glPopMatrix();

    glEnd();

}
void resize(int width, int height)
{
    const float ar = (float) width / (float) height;
    w = width;
    h = height;
    glViewport(0, 0, width, height);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    glFrustum(-ar, ar, -1.0, 1.0, 2.0, 100.0);
    //glMatrixMode(GL_MODELVIEW);
    glLoadIdentity() ;
}
void setOrthographicProjection() {
    glMatrixMode(GL_PROJECTION);
    glPushMatrix();
    glLoadIdentity();
    gluOrtho2D(0, w, 0, h);
    glScalef(1, -1, 1);
   glTranslatef(0, -h, 0);
    glMatrixMode(GL_MODELVIEW);
}
void resetPerspectiveProjection() {
    glMatrixMode(GL_PROJECTION);
    glPopMatrix();
    glMatrixMode(GL_MODELVIEW);
}
void renderBitmapString(float x, float y, void *font,const char *string){
    const char *c;
    glRasterPos2f(x, y);
    for (c=string; *c != '\0'; c++) {
        glutBitmapCharacter(font, *c);
    }
}
void circle(float x,float y)
{
	float angle;
    //glLineWidth(140);
    int i;
  //  glPolygonMode(GL_FRONT_AND_BACK, GL_LINE);
	glBegin(GL_POLYGON);

		for(i = 0; i < 100; i++)
		{
			angle = 2 * PI * i / 100;
			glVertex3f (cos(angle) * x-0, sin(angle) *y-30, 0);
		}

	glEnd();
	//glPolygonMode(GL_FRONT_AND_BACK, GL_FILL);
	//p=0;
}
void brokenegg(){

    //glClear(GL_COLOR_BUFFER_BIT);
	glPushMatrix();
	glColor3f(0.98,0.98, 0.823);

	glTranslatef(tx,ty,0);
	circle(3,3);
	glColor3f(1,0.843, 0.0);
	circle(1.3,1.3);

	glPopMatrix();
	glFlush();
}
void egg(float x,float y){
    float angle;
    if(p<=+15.0)
       p=p+0.007;
    else
        p=-31;
    glutPostRedisplay();
	glBegin(GL_POLYGON);

	if(a==0 || a==2){
		for(int i = 0; i <=100; i++)
		{
			angle = 2 * PI * i /100;
			glVertex2f (cos(angle)*x , sin(angle)*y-30);
		}
	}
	else if(a==1){
       for(int i = 0; i <=100; i++)
		{
			angle = 2 * PI * i /100;
			glVertex2f (p+cos(angle)*x , sin(angle)*y-30);
		}
	}
	glEnd();

}
void sky1(float x,float y){
    float angle;
	//glMatrixMode(GL_MODELVIEW);
	glBegin(GL_POLYGON);

		for(int i = 0; i <=100; i++)
		{
			angle = 2 * PI * i /100;
			glVertex2f (cos(angle)*x+4 , sin(angle)*y+19);
		}
	glEnd();

}
void sky2(float x,float y){
    float angle;
	//glMatrixMode(GL_MODELVIEW);
	glBegin(GL_POLYGON);

		for(int i = 0; i <=100; i++)
		{
			angle = 2 * PI * i /100;
			glVertex2f (cos(angle)*x , sin(angle)*y+20);
		}
	glEnd();

}
void sky3(float x,float y){
    float angle;
	//glMatrixMode(GL_MODELVIEW);
	glBegin(GL_POLYGON);

		for(int i = 0; i <=100; i++)
		{
			angle = 2 * PI * i /100;
			glVertex2f (cos(angle)*x-4 , sin(angle)*y+19);
		}
	glEnd();

}
void sky4(float x,float y){
    float angle;
	//glMatrixMode(GL_MODELVIEW);
	glBegin(GL_POLYGON);

		for(int i = 0; i <=100; i++)
		{
			angle = 2 * PI * i /100;
			glVertex2f (cos(angle)*x , sin(angle)*y+19);
		}
	glEnd();

}
void grass1(float x,float y){
    float angle;
	//glMatrixMode(GL_MODELVIEW);
	glBegin(GL_POLYGON);

		for(int i = 0; i <=100; i++)
		{
			angle =  PI * i /100;
			glVertex2f (cos(angle)*x-27 , sin(angle)*y-33);
		}
	glEnd();

}
void grass2(float x,float y){
    float angle;
	//glMatrixMode(GL_MODELVIEW);
	glBegin(GL_POLYGON);

		for(int i = 0; i <=100; i++)
		{
			angle =  PI * i /100;
			glVertex2f (cos(angle)*x-31 , sin(angle)*y-33);
		}
	glEnd();

}
void grass6(float x,float y){
    float angle;
	//glMatrixMode(GL_MODELVIEW);
	glBegin(GL_POLYGON);

		for(int i = 0; i <=100; i++)
		{
			angle =  PI * i /100;
			glVertex2f (cos(angle)*x-32 , sin(angle)*y-33);
		}
	glEnd();

}
void grass3(float x,float y){
    float angle;
	//glMatrixMode(GL_MODELVIEW);
	glBegin(GL_POLYGON);

		for(int i = 0; i <=100; i++)
		{
			angle =  PI * i /100;
			glVertex2f (cos(angle)*x-29 , sin(angle)*y-33);
		}
	glEnd();

}
void grass4(float x,float y){
    float angle;
	//glMatrixMode(GL_MODELVIEW);
	glBegin(GL_POLYGON);

		for(int i = 0; i <=100; i++)
		{
			angle =  PI * i /100;
			glVertex2f (cos(angle)*x-28 , sin(angle)*y-33);
		}
	glEnd();

}
void grass5(float x,float y){
    float angle;
	//glMatrixMode(GL_MODELVIEW);
	glBegin(GL_POLYGON);

		for(int i = 0; i <=100; i++)
		{
			angle =  PI * i /100;
			glVertex2f (cos(angle)*x-30 , sin(angle)*y-33);
		}
	glEnd();

}
void sun(float x,float y){
    float angle;
	//glMatrixMode(GL_MODELVIEW);
	glBegin(GL_POLYGON);

		for(int i = 0; i <=100; i++)
		{
			angle = 2 * PI * i /100;
			glVertex2f (cos(angle)*x+26 , sin(angle)*y+26);
		}
	glEnd();

}
void broke(){
    if (a==2){
        brokenegg();
    }
}

void border1(float radius_x, float radius_y)
{
	int i = 0;
	float angle = 0.0;
glLineWidth(12);
//glColor3f(1.0,1, 0.0);
	glBegin(GL_LINE_STRIP);

		for(i = 0; i < 100; i++)
		{
			angle = 2 * PI * i / 100;
			glVertex3f (cos(angle) * radius_x-26, sin(angle) * radius_y-18, 0);
		}

	glEnd();
}
void border2(float radius_x, float radius_y)
{
	int i = 0;
	float angle = 0.0;
glLineWidth(12);
//glColor3f(1.0,1, 0.0);
	glBegin(GL_LINE_STRIP);

		for(i = 0; i < 100; i++)
		{
			angle = 2 * PI * i / 100;
			glVertex3f (cos(angle) * radius_x-26, sin(angle) * radius_y-6, 0);
		}

	glEnd();
}
void circle3(float radius_x, float radius_y)
{
	int i = 0;
	float angle = 0.0;
glLineWidth(20);
//glColor3f(1.0,1, 0.0);
	glBegin(GL_POLYGON);

		for(i = 0; i < 100; i++)
		{
			angle = 2 * PI * i / 100;
			glVertex3f (cos(angle) * radius_x-26, sin(angle) * radius_y-18, 0);
		}

	glEnd();
}
void circle4(float radius_x, float radius_y)
{
	int i = 0;
	float angle = 0.0;

	glBegin(GL_POLYGON);

		for(i = 0; i < 100; i++)
		{
			angle = 2 * PI * i / 100;
			glVertex3f (cos(angle) * radius_x-26, sin(angle) * radius_y-6, 0);
		}

	glEnd();
}
void lip(float radius_x, float radius_y){
    int i = 0;
	float angle = 0.0;

	glBegin(GL_POLYGON);

		for(i = 0; i < 100; i++)
		{
			angle =  2*PI * i / 3;
			glVertex3f (cos(angle) * radius_x-26, sin(angle) * radius_y-9, 0);
		}

	glEnd();
}
void lipb(float radius_x, float radius_y){
    int i = 0;
	float angle = 0.0;
    glLineWidth(3);
	glBegin(GL_LINE_STRIP);

		for(i = 0; i < 100; i++)
		{
			angle =  2*PI * i / 3;
			glVertex3f (cos(angle) * radius_x-26, sin(angle) * radius_y-9, 0);
		}

	glEnd();
}
void eye1(float radius_x, float radius_y)
{
	int i = 0;
	float angle = 0.0;

	glBegin(GL_POLYGON);

		for(i = 0; i < 100; i++)
		{
			angle = 2 * PI * i / 100;
			glVertex3f (cos(angle) * radius_x-24.5, sin(angle) * radius_y-4, 0);
		}

	glEnd();
}
void eye2(float radius_x, float radius_y)
{
	int i = 0;
	float angle = 0.0;

	glBegin(GL_POLYGON);

		for(i = 0; i < 100; i++)
		{
			angle = 2 * PI * i / 100;
			glVertex3f (cos(angle) * radius_x-27, sin(angle) * radius_y-4, 0);
		}

	glEnd();
}
void eye22(float radius_x, float radius_y)
{
	int i = 0;
	float angle = 0.0;

	glBegin(GL_POLYGON);

		for(i = 0; i < 100; i++)
		{
			angle = 2 * PI * i / 100;
			glVertex3f (cos(angle) * radius_x-27, sin(angle) * radius_y-4, 0);
		}

	glEnd();
}
void border3(float radius_x, float radius_y)
{
	int i = 0;
	float angle = 0.0;
    glLineWidth(10);
//glColor3f(1.0,1, 0.0);
	glBegin(GL_LINE_STRIP);

		for(i = 0; i < 100; i++)
		{
			angle = 2 * PI * i / 100;
			glVertex3f (cos(angle) * radius_x-27, sin(angle) * radius_y-4, 0);
		}

	glEnd();
}
void border4(float radius_x, float radius_y)
{
	int i = 0;
	float angle = 0.0;
    glLineWidth(10);
//glColor3f(1.0,1, 0.0);
	glBegin(GL_LINE_STRIP);

		for(i = 0; i < 100; i++)
		{
			angle = 2 * PI * i / 100;
			glVertex3f (cos(angle) * radius_x-24.5, sin(angle) * radius_y-4, 0);
		}

	glEnd();
}
void eye11(float radius_x, float radius_y)
{
	int i = 0;
	float angle = 0.0;

	glBegin(GL_POLYGON);

		for(i = 0; i < 100; i++)
		{
			angle = 2 * PI * i / 100;
			glVertex3f (cos(angle) * radius_x-24.5, sin(angle) * radius_y-4, 0);
		}

	glEnd();
}
void fea(float radius_x, float radius_y)
{
	   int i = 0;
	float angle = 0.0;

	glBegin(GL_POLYGON);

		for(i = 0; i < 4; i++)
		{
			angle =  PI * i / 3;
			glVertex3f (cos(angle) * radius_x-25.7, sin(angle) * radius_y, 0);
		}

	glEnd();
}

void display(void)
{
    glClear(GL_COLOR_BUFFER_BIT);
    glBegin(GL_QUADS); // It can be any type Gl_POINT,_LINE

    glColor3f(0.59607f, 0.96f, 1.0f);

     glVertex2d(37.0,37.0);
    glVertex2d(-37.0,37.0);
    glVertex2d(-37.0,-37.0);
    glVertex2d(37.0,-37.0);

    glEnd();


   glBegin(GL_QUADS); // It can be any type Gl_POINT,_LINE
    glColor3f(0.0f, 0.5450f, 0.270f);
    //glColor3f(0.0f, 0.5450f, 0.0f);
    glVertex2d(37.0,4.0);
    glVertex2d(-37.0,4.0);
    glVertex2d(-37.0,-37.0);
    glVertex2d(37.0,-37.0);
    glEnd();

    glPushMatrix();

    //hen start
    glColor3f(1,0.843, 0.0);
	circle3(6,10);
	glColor3f(0,0.0, 0.0);
	border1(6.2,10.2);
	glColor3f(1,0.843, 0.0);


	circle4(4,7);
	glColor3f(0,0.0, 0.0);
	border2(4.1,7.1);
	glColor3f(0,0.0, 0.0);
	border3(.8,1.5);
	border4(.8,1.5);
	glColor3f(1,1.0, 1.0);
	eye1(.8,1.5);
	eye2(.8,1.5);
	glColor3f(0,0.0, 0.0);
	eye11(.3,.8);
	eye22(.3,.8);
	glColor3f(.933,0.0, 0.0);
    lip(1.2,2.3);
    glColor3f(0,0.0,0.0);
     lipb(1.2,2.3);

    glColor3f(.933,0.0, 0.0);
    fea(2,4);
    glRectf(-26.5,-28.0,-26.9,-31.0);
    glRectf(-25.5,-28.0,-25.9,-31.0); //hen end


	glColor3f(0.545, 0.278,0.149);

	glBegin(GL_TRIANGLES); // It can be any type Gl_POINT,_LINE
        glVertex2d(17,12);
        glVertex2d(16,8);
        glVertex2d(18,8);                //fench
    glEnd();
	glRectf(18.0,8.0,16.0,-7.0);

	glBegin(GL_TRIANGLES); // It can be any type Gl_POINT,_LINE
        glVertex2d(21,12);
        glVertex2d(20,8);
        glVertex2d(22,8);                //fench
    glEnd();
    glRectf(22.0,8.0,20.0,-7.0);


    glBegin(GL_TRIANGLES); // It can be any type Gl_POINT,_LINE
        glVertex2d(25,12);
        glVertex2d(24,8);
        glVertex2d(26,8);                //fench
    glEnd();
    glRectf(26.0,8.0,24.0,-7.0);

    glColor3f(0.0f, 0.0f, 0.0f);
        glBegin(GL_LINE_LOOP); // It can be any type Gl_POINT,_LINE
        glVertex2d(13.0, 0.55);
        glVertex2d(29.0, 0.55);

        glEnd();

        glBegin(GL_LINE_LOOP); // It can be any type Gl_POINT,_LINE
        glVertex2d(13.0, -2.55);
        glVertex2d(29.0,-2.55);

        glEnd();

        glBegin(GL_LINE_LOOP); // It can be any type Gl_POINT,_LINE
        glVertex2d(13.0, 5.555555);
        glVertex2d(29.0,5.55555);

        glEnd();

        glBegin(GL_LINE_LOOP); // It can be any type Gl_POINT,_LINE
        glVertex2d(13.0,2.5);
        glVertex2d(29.0,2.5);

        glEnd();

        glColor3f(0.545, 0.278,0.149);
      glRectf(29.0,0.5,13.0,-2.5);  //fench ar majhe 2nd ta
      glRectf(29.0,5.5,13.0,2.5); //fench ar majhe 1st ta

    glPopMatrix();
    glEnd();

	//printf("%f\n",p);

	bowl();
	glColor3f(0.941, 1.0,1.0);
	sky1(3,3);
	sky2(3,3);
	sky3(3,3);
	sky4(5,5);
    glColor3f(0.678f, 1.0f, 0.184f);

	grass1(0.3,3);
	grass2(0.3,3);
	grass3(0.3,3);
	grass4(0.3,3);
	grass5(0.3,3);
	grass6(0.3,3);
	glColor3f(1.0, 1.0,0.0);
	sun(2,4);
	glTranslatef(tx,ty,0);
    glColor3f(1.0, 0.854,0.7254);
	egg(1,3);

	glPopMatrix();
	glutSwapBuffers();
	glEnd();

	glColor3d(1.0, 0.0, 0.0);
    setOrthographicProjection();
    glPushMatrix();
    glLoadIdentity();
    renderBitmapString(150,120,(void *)font,"Catch The Egg");
    renderBitmapString(150,150, (void*)font, s);

    //renderBitmapString(30,24,(void *)font,"Esc - Quit");
   // glPushAttrib(GL_ALL_ATTRIB_BITS);
      if(a==1){
            //save=save+1;
        renderBitmapString(1000,120,(void *)font,"Score:");
        renderBitmapString(1070,120,(void *)font,"1");
       // break;
      }
   else if(a==2) {
        renderBitmapString(570,570,(void *)font,"You've broken the egg");
      }
    //glPopAttrib();
    glPopMatrix();
    resetPerspectiveProjection();
    glutSwapBuffers();
    glEnd();
    broke();
    glFlush();
    //p=0;

}
void update(int value){
    t = glutGet(GLUT_ELAPSED_TIME) / 1000.0;
    int time = (int)t;
    sprintf(s, "TIME : %2d Sec", time);
    glutTimerFunc(1000, update, 0);
    glutPostRedisplay();
}
void init(void)
{
	glClearColor (0.0, 0.0, 0.0, 0.0);
	//glOrtho(-31.0, 31.0, -31.0, 31.0, -31.0, 31.0);
	glOrtho(-37.0, 37.0, -37.0, 37.0, -37.0, 37.0);
}

void click(int button, int state, int x, int y){
//ty+=0;
   switch (button) {
      case GLUT_LEFT_BUTTON:

         if (state == GLUT_DOWN){
             if(ty<32 && p>=-2 && p<=2){
                  PlaySound("Croc_-_Level_Complete_.wav", NULL, SND_FILENAME| SND_ASYNC);
                ty +=32;
                a=a+1;
            egg(1,3);
            glPopMatrix();
            glFlush();
          }
          else if(ty<31){
            PlaySound("Fail_Horn_-_SOUND_EFFECT.wav", NULL, SND_FILENAME| SND_ASYNC);
            ty+=0;
            a=2;
            brokenegg();
          }

         }
          break;

      default:
         break;
   }

}
int main()
{
    PlaySound("Candy_Crush_Soda_Saga.wav", NULL, SND_FILENAME| SND_ASYNC);
	glutInitDisplayMode (GLUT_SINGLE | GLUT_RGB);
	glutInitWindowSize (800, 600);
	glutInitWindowPosition (200, 200);
	glutCreateWindow ("Egg Game1");
	init();
    glutDisplayFunc(display);
    glutMouseFunc(click);
    glutReshapeFunc(resize);
    glutTimerFunc(25, update, 0);

// glClear();

	glutMainLoop();
	return 0;   /* ANSI C requires main to return int. */
}

