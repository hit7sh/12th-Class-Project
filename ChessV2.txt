
/**
 * Chess game version 2
 * by Hitesh Kumar Saini 
 * 12th 'A'
 * #My first Graphical game
 */
import sun.audio.*;
import java.awt.event.*;
import java.io.*;
import javax.imageio.ImageIO;
import java.io.File;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import javax.swing.*;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.applet.Applet;
public class chessV2 extends Frame
{
    int xp,yp,q,x1,y1,v,b=1,rs,cs,kx,ky;
    String[]B[]=new String[9][9];boolean check;
    public int xx=0,xs[]=new int[30],ys[]=new int[30];
    
    public chessV2(){
        setTitle("Chess Game_");
        setSize(500,500);
        setVisible(true);
    }
    
    public boolean keyDown(Event e,int k)
    {
        if(k==67|k==67+32|k==(int)'x'|k==(int)'X')
        {
            int result = JOptionPane.showConfirmDialog(null,"U sure u wna close game?");
            switch (result) { 
      
                case JOptionPane.NO_OPTION:
                break;
                case JOptionPane.YES_OPTION:
            System.exit(0);break;
        }}
        if(k==(int)'r'|k==(int)'R')
        {int result = JOptionPane.showConfirmDialog(null,"U sure u wna restart?");
            switch (result) { 
      
                case JOptionPane.NO_OPTION:
                break;
                case JOptionPane.YES_OPTION:
                ini();repaint();b=1;rs=-1;break;
        }}
        return true;
    }
    
    public boolean mouseDown(Event e,int x,int y)
    {
        //y-=24-4+10;
        x+=6;
        y-=40;
        //x-=3;
        if(q++%2==0)
        {
            x1=x;
            y1=y;
            addspot(x-3,y+30);
            addmoves(y,x);
        }
        else
        {
            int i,f=0;
            for(i=0;i<30;i++)
            {
                if(xs[i]==-1)
                break;
                if(ys[i]==(int)(y+65)/80&&xs[i]==(int)(x/80))
                f=1;
            }
            if(f==1)
            {
            move(x,y);
            b++;
            }
        }
        return true;
    }
   
    /*function to check if chess piece is moveable to specified location*/
     boolean isMoveAble(String x,String y)
    {
        if(y==null)
        return true;
        char ch1=x.charAt(0),ch2=y.charAt(0);
        int i=0;
        if(ch1<=(char)75353&ch1>=(char)75348&ch2>(char)75353&ch2<=(char)75359)
        return true;
        else if(ch1>(char)75353&ch1<=(char)75359&ch2<=(char)75353&ch2>=(char)75348)
        return true;
        else
        return false;
    }
    
    /*function Overload for special cases*/
     boolean isMoveAble(String x,String y,int t)
    {
        if(y==null)
        return false;
        char ch1=x.charAt(0),ch2=y.charAt(0);
        int i=0;
        if(ch1<=(char)75353&ch1>=(char)75348&ch2>(char)75353&ch2<=(char)75359)
        return true;
        else if(ch1>(char)75353&ch1<=(char)75359&ch2<=(char)75353&ch2>=(char)75348)
        return true;
        else
        return false;
    }
    
    void addmoves(int x, int y)
    {
        ++xx;
        int a=0,b=0;
        x=((x+15)/80)+1;
        y=((y+65)/80);
        
        try
        {
        //for Knight
        if(B[x][y].charAt(0)==(char)75352|B[x][y].charAt(0)==(char)75358)
        {
            if(x+2<9&x+2>0&y+1>0&y+1<9)
            if(isMoveAble(B[x][y],B[x+2][y+1]))
                {ys[a++]=(x+2);xs[b++]=(y+1)-1;}
            if(x+2<9&x+2>0&y-1>0&y-1<9)
            if(isMoveAble(B[x][y],B[x+2][y-1]))    
                {ys[a++]=(x+2);xs[b++]=(y-1)-1;}
            if(x-2<9&x-2>0&y+1>0&y+1<9)
            if(isMoveAble(B[x][y],B[x-2][y+1]))
                {ys[a++]=(x-2);xs[b++]=(y+1)-1;}
            if(x-2<9&x-2>0&y-1>0&y-1<9)
            if(isMoveAble(B[x][y],B[x-2][y-1]))
                {ys[a++]=(x-2);xs[b++]=(y-1)-1;}
            if(x+1<9&x+1>0&y+2>0&y+2<9)
            if(isMoveAble(B[x][y],B[x+1][y+2]))
                {ys[a++]=(x+1);xs[b++]=(y+2)-1;}
            if(x-1<9&x-1>0&y+2>0&y+2<9)
            if(isMoveAble(B[x][y],B[x-1][y+2]))
                {ys[a++]=(x-1);xs[b++]=(y+2)-1;}
            if(x+1<9&x+1>0&y-2>0&y-2<9)
            if(isMoveAble(B[x][y],B[x+1][y-2]))
                {ys[a++]=(x+1);xs[b++]=(y-2)-1;}
            if(x-1<9&x-1>0&y-2>0&y-2<9)
            if(isMoveAble(B[x][y],B[x-1][y-2]))
                {ys[a++]=(x-1);xs[b++]=(y-2)-1; }
        }
        
        //for pawn(white)
        if(B[x][y].charAt(0)==(char)75353)
        {
            if(x>1&B[x-1][y]==null)
            {ys[a++]=(x-1);xs[b++]=(y)-1;}
            if(x==7&B[x-2][y]==null&B[x-1][y]==null)
            {ys[a++]=(x-2);xs[b++]=(y)-1;}
            if(x==2&y==8){ys[a++]=1;xs[b++]=6;}
            if(x==3&y==8){ys[a++]=2;xs[b++]=6;}
            if(y<8&y>1&x>1&x<8)
            if(isMoveAble(B[x][y],B[x-1][y-1],0))
            {ys[a++]=(x-1);xs[b++]=(y-1)-1;}
            if(isMoveAble(B[x][y],B[x-1][y+1],0))
            {ys[a++]=(x-1);xs[b++]=(y+1)-1;}
            if(y==1&x>1)if(B[x-1][y+1]!=null)
            if(isMoveAble(B[x][y],B[x-1][y+1],0))
            {ys[a++]=(x-1);xs[b++]=(y+1)-1;}
            if(y==8&x>1)if(B[x-1][y-1]!=null)
            if(isMoveAble(B[x][y],B[x-1][y-1],0))
            {ys[a++]=(x-1);xs[b++]=(y-1)-1;}
        }
        
        //for pawn(black)
        if(B[x][y].charAt(0)==(char)75359)
        {
            if(y==8)
            {if(isMoveAble(B[x][y],B[x+1][y]))
            {ys[a++]=x+1;xs[b++]=y-1;}
            if(isMoveAble(B[x][y],B[x+1][y-1],0))
            {ys[a++]=x+1;xs[b++]=y-1-1;}}
            if(x==7)
            if(B[x+1][y]==null)
            {ys[a++]=x+1;xs[b++]=y-1;}
            
            if(x<7&B[x+1][y]==null)
            {ys[a++]=(x+1);xs[b++]=(y)-1;}
            if(x==2&B[x+2][y]==null&B[x+1][y]==null)
            {ys[a++]=(x+2);xs[b++]=(y)-1;}
            if(y<8&y>1&x>1&x<8)
            if(isMoveAble(B[x][y],B[x+1][y-1],0))
            {ys[a++]=(x+1);xs[b++]=(y-1)-1;}
            if(isMoveAble(B[x][y],B[x+1][y+1],0))
            {ys[a++]=(x+1);xs[b++]=(y+1)-1;}
            if(y==1&x<7)if(B[x+1][y+1]!=null)
            if(isMoveAble(B[x][y],B[x+1][y+1],0))
            {ys[a++]=(x+1);xs[b++]=(y+1)-1;}
            if(y==8&x<7)if(B[x+1][y-1]!=null)
            if(isMoveAble(B[x][y],B[x+1][y-1],0))
            {ys[a++]=(x+1);xs[b++]=(y-1)-1;}
        }
        
        
        //for Rook & Queen
        if(B[x][y].charAt(0)==(char)75356|(B[x][y].charAt(0)==(char)75350)|
        B[x][y].charAt(0)==(char)75349|(B[x][y].charAt(0)==(char)75355))
        {
            int i=x-1,j=y-1,k=0;
            for(;i>0;i--)
            if(isMoveAble(B[x][y],B[i][y]))
            {
                ys[a++]=i;xs[b++]=y-1;
                k++;
                if(isMoveAble(B[x][y],B[i][y],1))
                break;
            }
            else 
            break;
            
            i=x+1;
            for(;i<9;i++)
            if(isMoveAble(B[x][y],B[i][y]))
            {
                ys[a++]=i;xs[b++]=y-1;
                k++;
                if(isMoveAble(B[x][y],B[i][y],1))
                break;
            }
            else 
            break;
            
            for(;j>0;j--)
            if(isMoveAble(B[x][y],B[x][j]))
            {
                ys[a++]=x;xs[b++]=j-1;
                k++;
                if(isMoveAble(B[x][y],B[x][j],1))
                break;
            }
            else
            break;
            
            j=y+1;
            for(;j<9;j++)
            if(isMoveAble(B[x][y],B[x][j]))
            {
                ys[a++]=x;xs[b++]=j-1;
                k++;
                if(isMoveAble(B[x][y],B[x][j],1))
                break;
            }
            else 
            break;
        }
        
        
        //for Bishop & Queen
        if(B[x][y].charAt(0)==(char)75351|(B[x][y].charAt(0)==(char)75357)|
        B[x][y].charAt(0)==(char)75349|(B[x][y].charAt(0)==(char)75355))
        {
            int i=0,j,k=0;
            if(x>1&y>1)
            {
            i=x-1;
            j=y-1;
            while(i>0&j>0)
            {
            if(isMoveAble(B[x][y],B[i][j]))
            {
                ys[a++]=i;xs[b++]=j-1;
                k++;
                if(isMoveAble(B[x][y],B[i][j],1))
                break;
            }
            else
            break;
            i--;
            j--;
            }
            }
            if(x>1&y<8)
            {
                i=x-1;
                j=y+1;
                while(i>0&j<=8)
                {
                    if(isMoveAble(B[x][y],B[i][j]))
                    {
                        ys[a++]=i;xs[b++]=j-1;
                        k++;
                        if(isMoveAble(B[x][y],B[i][j],1))
                        break;
                    }
                    else
                    break;
                    i--;
                    j++;
                }
            }
            if(x<8&y>1)
            {
            i=x+1;
            j=y-1;
            while(i<=8&j>0)
            {
            if(isMoveAble(B[x][y],B[i][j]))
            {
                ys[a++]=i;xs[b++]=j-1;
                k++;
                if(isMoveAble(B[x][y],B[i][j],1))
                break;
            }
            else
            break;
            i++;
            j--;
            }
            }
            if(x<8&y<8)
            {
                i=x+1;
                j=y+1;
            while(i<=8&j<=8)
            {
            if(isMoveAble(B[x][y],B[i][j]))
            {
                ys[a++]=i;xs[b++]=j-1;
                k++;
                if(isMoveAble(B[x][y],B[i][j],1))
                break;
            }
            else
            break;
            i++;
            j++;
            }
            }
        }
        
        //#King
        if(B[x][y].charAt(0)==(char)75348|(B[x][y].charAt(0)==(char)75354))
        {
            if(x==8&y==8){
            if(isMoveAble(B[8][8],B[8][7]))
            {ys[a++]=8;xs[b++]=7-1;}
            if(isMoveAble(B[8][8],B[7][7]))
            {ys[a++]=7;xs[b++]=7-1;}
            if(isMoveAble(B[8][8],B[7][8]))
            {ys[a++]=7;xs[b++]=8-1;}}
            
            if(x==8&y==5){
            if(B[x][2]==null&B[x][3]==null&B[x][4]==null&B[x][1].charAt(0)==(char)75356)
            {ys[a++]=8;xs[b++]=3-1;}
             if(B[x][6]==null&B[x][7]==null&B[x][8].charAt(0)==(char)75356)
            {ys[a++]=8;xs[b++]=7-1;}}
            if(x==1&y==5){
            if(B[x][2]==null&B[x][3]==null&B[x][4]==null&B[x][1].charAt(0)==(char)75350)
            {ys[a++]=1;xs[b++]=3-1;}
             if(B[x][6]==null&B[x][7]==null&B[x][1].charAt(0)==(char)75350)
            {ys[a++]=1;xs[b++]=7-1;}}
            if(x==8)
            {
                if(isMoveAble(B[x][y],B[x][y+1]))
                {ys[a++]=(x);xs[b++]=(y)+1-1;}
                if(isMoveAble(B[x][y],B[x-1][y]))
            {ys[a++]=x-1;xs[b++]=y-1;}
            if(isMoveAble(B[x][y],B[x-1][y+1]))
            {ys[a++]=x-1;xs[b++]=y+1-1;}}
            if(y==1)
            {
                if(isMoveAble(B[x][y],B[x+1][y]))
                {ys[a++]=x+1;xs[b++]=y-1;}
                if(isMoveAble(B[x][y],B[x+1][y+1]))
                {ys[a++]=x+1;xs[b++]=y+1-1;}
                if(isMoveAble(B[x][y],B[x][y+1]))
                {ys[a++]=x;xs[b++]=y+1-1;}
                if(isMoveAble(B[x][y],B[x-1][y]))
                {ys[a++]=x-1;xs[b++]=y-1;}
                if(isMoveAble(B[x][y],B[x-1][y+1]))
                {ys[a++]=x-1;xs[b++]=y+1-1;}
            }
            else if(y==8)
            {
                if(isMoveAble(B[x][y],B[x-1][y]))
                {ys[a++]=x-1;xs[b++]=y-1;}
                if(isMoveAble(B[x][y],B[x-1][y-1]))
                {ys[a++]=x-1;xs[b++]=y-1-1;}
                if(isMoveAble(B[x][y],B[x][y-1]))
                {ys[a++]=x;xs[b++]=y-1-1;}
                if(isMoveAble(B[x][y],B[x+1][y]))
                {ys[a++]=x+1;xs[b++]=y-1;}
                if(isMoveAble(B[x][y],B[x+1][y-1]))
                {ys[a++]=x+1;xs[b++]=y-1-1;}
            }
            else
            {
            if(x<8)
            if(isMoveAble(B[x][y],B[x][y+1]))
            {ys[a++]=x;xs[b++]=(y+1)-1;}
            
            if(x<8&y<8)
            {
            if(isMoveAble(B[x][y],B[x+1][y]))
            {ys[a++]=(x+1);xs[b++]=(y)-1;}
            
            if(isMoveAble(B[x][y],B[x+1][y+1]))
            {ys[a++]=(x+1);xs[b++]=(y+1)-1;}
            }
            
            if(x==1)if(isMoveAble(B[x][y],B[x][y-1]))
            {ys[a++]=(x);xs[b++]=(y)-1-1;}
            
            if(x>1)
            if(isMoveAble(B[x][y],B[x][y-1]))
            {ys[a++]=x;xs[b++]=(y-1)-1;}
            
            if(x>1&y>1)
            {
            if(isMoveAble(B[x][y],B[x-1][y]))
            {ys[a++]=(x-1);xs[b++]=(y)-1;}
            
            if(isMoveAble(B[x][y],B[x-1][y-1]))
            {ys[a++]=(x-1);xs[b++]=(y-1)-1;}
            }
            
            if(x<8&y>1)
            {
            if(isMoveAble(B[x][y],B[x+1][y]))
            {ys[a++]=(x+1);xs[b++]=(y)-1;}
            
            if(isMoveAble(B[x][y],B[x+1][y-1]))
            {ys[a++]=(x+1);xs[b++]=(y-1)-1;}
            }
            
            if(x>1&y<8)
            {
            if(isMoveAble(B[x][y],B[x][y-1]))
            {ys[a++]=x;xs[b++]=(y-1)-1;}
            
            if(isMoveAble(B[x][y],B[x-1][y+1]))
            {ys[a++]=(x-1);xs[b++]=(y+1)-1;}
            }
        }
        }
        }
        catch(Exception e)
        {
            //do nothing 
        }
        
        xs[a++]=-1;
        //for check(kings)
        for(int i=0;i<30;i++)
        {if(xs[i]==-1)break;
        if(B[ys[i]][xs[i]+1]!=null)
        if(B[ys[i]][xs[i]+1].charAt(0)==(char)(75348)||B[ys[i]][xs[i]+1].charAt(0)==(char)(75354))
        {check=true;kx=xs[i];ky=ys[i];}}
           
        repaint();
    }
    
    public void move(int x,int y)
    {
        try{
        int b=((x-15)/80)+1;
        int a=((y+65+16)/80);
        int m=((x1-15)/80)+1,n=(y1+65)/80;
        if(B[a][b]==null)
        {
          if(B[n][m]==(char)75348+""&(int)(n)==8&(int)(m)==5&B[8][1]==(char)75350+""&b==3)
            {B[8][3]=(char)75348+"";B[8][4]=(char)75350+"";B[8][1]=null;B[8][5]=null;cs=1;}else
            if(B[n][m]==(char)75348+""&(int)(n)==8&(int)(m)==5&B[8][8]==(char)75350+""&(b==7))
            {B[8][7]=(char)75348+"";B[8][6]=(char)75350+"";B[8][8]=null;B[8][5]=null;cs=1;}else
          if(B[n][m]==(char)75354+""&(int)(n)==1&(int)(m)==5&B[1][1]==(char)75356+""&b==3)
          {B[1][3]=(char)75354+"";B[1][4]=(char)75356+"";B[1][1]=null;B[1][5]=null;cs=1;}else
          if(B[n][m]==(char)75354+""&(int)(n)==1&(int)(m)==5&B[1][8]==(char)75356+""&b==7)
          {B[1][7]=(char)75354+"";B[1][6]=(char)75356+"";B[1][8]=null;B[1][5]=null;cs=1;}
            else if(a==1&B[(n)][m].charAt(0)==(char)75353)
            {pawnChoice(B,n,m,1);b++;
        addspot(x-3,y+30);}
        else if(a==8&B[(n)][m].charAt(0)==(char)75359)
        {pawnChoice(B,n,m,2);b++;
        addspot(x-3,y+30);}
          else{
        String t=B[a][b];
        B[a][b]=B[(n)][m];
        B[(n)][m]=t;
        }}
        else if((B[a][b].charAt(0)<=(char)75353&B[a][b].charAt(0)>=(char)75348&
        B[(n)][m].charAt(0)>(char)75353&
        B[(n)][m].charAt(0)<=(char)75359)|(B[a][b].charAt(0)>(char)75353&
        B[a][b].charAt(0)<=(char)75359&B[(n)][m].charAt(0)<=(char)75353&
        B[(n)][m].charAt(0)>=(char)75348))
        {
            String t=B[a][b];
            B[a][b]=B[(n)][m];
            B[(n)][m]=null;
        }}
        catch(Exception e){}
            for(int i=0;i<30;i++)
            {
                xs[i]=0;
                ys[i]=0;
            }
        addspot(x-3,y+30);
    }
    
    public void addspot(int x,int y)
    {
        xp=x;
        yp=y;
        repaint();
    }
    
    public void ini()
    {
        String b[]={(char)(75356)+"",(char)(75358)+"",(char)(75357)+"",
        (char)(75355)+"",(char)(75354)+"",(char)(75357)+"",(char)(75358)+"",(char)(75356)+""};
        for(int i=1;i<9;i++)
        B[1][i]=b[i-1]; 
        String[]w={(char)(75350)+"",(char)(75352)+"",(char)(75351)+"",(char)(75349)+"",
            (char)(75348)+"",(char)(75351)+"",(char)(75352)+"",(char)(75350)+""};
            for(int i=3;i<=6;i++)
            for(int j=1;j<=8;j++)
            B[i][j]=null;
        for(int i=1;i<9;i++)
        B[8][i]=w[i-1];
        int i=0,j=0;
        for(i=1;i<9;i++)
        {
            B[2][i]=(char)(75359)+"";
            B[7][i]=(char)(75353)+"";
        }
    }
    
    /*function to check for Black King*/
     boolean searchBlackKing(String[][]B)
    {
        int i,j=0,k=0;
        for(i=1;i<9;i++)
        for(j=1;j<9;j++)
        if(B[i][j]!=null)
        if(B[i][j].charAt(0)==(char)(75354))
        k=1;
        return k==1;
    }
    
    /*function to check for white King*/
     boolean searchWhiteKing(String[][]B)
    {
        int i,j=0,k=0;
        for(i=1;i<9;i++)
        for(j=1;j<9;j++)
        if(B[i][j]!=null)
        if(B[i][j].charAt(0)==(char)(75348))
        k=1;
        return k==1;
    }
    
    public void paint(Graphics g)
    {
        if(g instanceof Graphics2D){
            Graphics2D g2=(Graphics2D)g;
            g2.setRenderingHint(RenderingHints.KEY_TEXT_ANTIALIASING,RenderingHints.VALUE_TEXT_ANTIALIAS_ON);
        }
        try{
        int k=0,x=0,i=0,j=0;
        if(++v==1)
        ini();
        
        setSize(1366,768);
        g.setColor(Color.orange);
        for ( j = 31; j < 640; j += 80)
        {
        for ( i =8; i < 570; i+= 80)
        if(k++%2==0)
        {
        g.setColor(Color.black);
        g.draw3DRect(i,j,80,80,true);
        g.drawRect(i,j,81,81);
        }
        else
        {   
        g.setColor(Color.cyan.darker());
        g.fill3DRect(i,j,80,80,true);
        g.setColor(Color.black);
        g.draw3DRect(i,j,80,80,true);
        g.setColor(Color.cyan.darker());
        }
        k++;
        }
        g.setColor(Color.black);
        Font f = new Font("TimesRoman", Font.PLAIN,75);
        g.setFont(f);
        g.setColor(Color.black);
        k=65;
        
        for(i=1;i<9;i++)
        {
            x=8;
            for(j=1;j<9;j++)
            {
                if(B[i][j]!=null)
                g.drawString(B[i][j],x,k+31);
                x+=80;
            }
            k+=80;
        }

        if(xp!=0)
        {
            g.setColor(Color.red);
            g.fillOval(xp-30+8,yp,40,40);
        }
        int td=0;
        if(xx!=0)
        {
            
            for(i=0;i<30;i++)
            {
            xx=0;
            if(xs[i]==-1)break;
            g.setColor(Color.green);
            
            g.drawRect((80*xs[i])+8,(80*ys[i])-65+31+6-21,79,79);
            g.drawRect((80*xs[i])+8+1,(80*ys[i])-65+31+6-21+1,78+1,79);
            g.drawRect((80*xs[i])+8+2,(80*ys[i])-65+31+6-21+2,76+2,76+2);
            g.drawRect((80*xs[i])+8+3,(80*ys[i])-65+31+6-21+3,75+3,75+3);
            g.setColor(Color.orange);
            g.drawRect((80*xs[i])+8+4,(80*ys[i])-65+31+6-21+4,74,74);
            
            //g.draw3DRect((80*xs[i])-1+35+8,(80*ys[i])-65+31+8,25,25,true);
            } 
        }
        g.setColor(Color.red);
        g.setFont(new Font("TimesRoman", Font.PLAIN,60));
        if(rs==-1)
        {g.drawString("game restarted",655+8,350+31);rs=0;}
        g.setColor(Color.black);
        g.setFont(new Font("TimesRoman",Font.BOLD,25));
        g.draw3DRect(0,0+31,641+8,640,true);
        if(b%2==0)
        g.drawString("( BLACK'S TURN )",670+8,200+31);
        else
        g.drawString("( WHITE'S TURN )",670+8,200+31);
        if(cs==1)
        {g.setColor(Color.blue);g.drawString(">castling move<",700+8,500);cs=0;}
        if(check){g.setColor(Color.red);g.drawString(">=CHECK=<",700+8,500);
            g.fill3DRect((80*kx)-1+35+8,(80*ky)-65+31+8,25,25,true);check=false;}
        g.setColor(Color.black);
        g.drawString("<press 'c' or 'x' to close game>",665+8,254+31);
        g.drawString("<press 'r' to restart game>",665+8,294+31);
        g.setColor(Color.red);
        for(i=208;i<212;i++)
        g.drawLine(660+8,i+31,890+8,i+31);
        g.setColor(Color.black);
        if(!searchBlackKing(B))
        g.drawString("WHITE KINGDOM WON",50+8,250+31);
        if(!searchWhiteKing(B))
        g.drawString("BLACK KINGDOM WON!!!",50+8,250+31);
        
        g.setColor(Color.blue);
        g.drawString("CHESS GAME BY CLASS-12'A'",650+8,20+36);
        g.drawString("MARIA SCHOOL JASPUR",660+8,50+36);
        g.draw3DRect(649+8,0+34,369+8,57,true);BufferedImage img=null;
        try{img=ImageIO.read(new File("F:\\z.comp mov\\chess\\images\\signature.jpg"));}catch(Exception e){}
        g.drawImage(img,642+8+5,591,this);g.draw3DRect(641+8,591,165+8,135,true);}catch(Exception e){}
    }
     
    JFrame jf=new JFrame("promotion");
     JButton queen = new JButton("queen");
    JButton knight = new JButton("knight");
     JButton rook = new JButton("rook");
    JButton bishop=new JButton("bishop");
     JPanel pane = new JPanel();
    void pawnChoice(String B[][],int x,int y,int z) 
    {
        jf.setSize(400, 300);
        pane.add(queen);
        pane.add(knight);
        pane.add(rook);
        pane.add(bishop);
        jf.add(pane);
        queen.addActionListener(new ActionListener()
        {
            public void actionPerformed(ActionEvent e)
            {
                int tmp=0;
                switch(z)
                {case 1:tmp=-1;break;case 2:tmp=1;break; }
                B[x+tmp][y]=(char)((int)(B[x][y].charAt(0))-4)+"";
                B[x][y]=null;jf.setState(jf.ICONIFIED);
            }
        });
        knight.addActionListener(new ActionListener()
        {
            public void actionPerformed(ActionEvent e)
            {
                int tmp=0;
                switch(z)
                {case 1:tmp=-1;break;case 2:tmp=1;break; }
                B[x+tmp][y]=(char)((int)(B[x][y].charAt(0))-1)+"";B[x][y]=null;jf.setState(jf.ICONIFIED);
        }
     });
     rook.addActionListener(new ActionListener()
     {
     public void actionPerformed(ActionEvent e)
     {
                int tmp=0;
                switch(z)
                {case 1:tmp=-1;break;case 2:tmp=1;break; }
                    B[x+tmp][y]=(char)((int)(B[x][y].charAt(0))-3)+"";
                    B[x][y]=null;jf.setState(jf.ICONIFIED);
    }
    });
    bishop.addActionListener(new ActionListener()
    {
        public void actionPerformed(ActionEvent e)
     {
                int tmp=0;
                switch(z)
                {case 1:tmp=-1;break;case 2:tmp=1;break; }
                B[x+tmp][y]=(char)((int)(B[x][y].charAt(0))-2)+"";B[x][y]=null;jf.setState(jf.ICONIFIED);
    }
    });
    jf.setVisible(true);
    }
    
    public static void main(String args[])
    {
        new chessV2();
    }
}
