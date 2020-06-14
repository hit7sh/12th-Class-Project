/**
 * Chess multiplayer Game :-)
 * By Hitesh
 * 12th 'A'
 */

import java.util.Scanner;
class chessV1
{
    /*function to print chess board*/
     void printC(String[][]c)
    {
        System.out.println("\n\n\n\n\n\n");
        int i,j=0;
        System.out.println("___________________________________________________________________");
        for(i=0;i<9;i++)
        {
            for(j=0;j<9;j++)
            if(c[i][j]==null)
            System.out.print("\t");
            else
            System.out.print(c[i][j]+"\t");
            System.out.println("\n\n");
        }
        System.out.println("___________________________________________________________________");
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
    
    
    
    /*function to check for available moves*/
     void avb(String[][]z ,int x ,int y)
    {
        int c=0;
        System.out.println("Available Moves ::");
        
        //for Knight
        if(z[x][y].charAt(0)==(char)75352|z[x][y].charAt(0)==(char)75358)
        {
            if(x+2<9&x+2>0&y+1>0&y+1<9)if(isMoveAble(z[x][y],z[x+2][y+1]))
                System.out.print("("+(x+2)+","+(y+1)+"), ");
            if(x+2<9&x+2>0&y-1>0&y-1<9)if(isMoveAble(z[x][y],z[x+2][y-1]))    
                System.out.print("("+(x+2)+","+(y-1)+"), ");
            if(x-2<9&x-2>0&y+1>0&y+1<9)if(isMoveAble(z[x][y],z[x-2][y+1]))
                System.out.print("("+(x-2)+","+(y+1)+"), ");
            if(x-2<9&x-2>0&y-1>0&y-1<9)if(isMoveAble(z[x][y],z[x-2][y-1]))
                System.out.print("("+(x-2)+","+(y-1)+"), ");
            if(x+1<9&x+1>0&y+2>0&y+2<9)if(isMoveAble(z[x][y],z[x+1][y+2]))
                System.out.print("("+(x+1)+","+(y+2)+"), ");
            if(x-1<9&x-1>0&y+2>0&y+2<9)if(isMoveAble(z[x][y],z[x-1][y+2]))
                System.out.print("("+(x-1)+","+(y+2)+"), ");
            if(x+1<9&x+1>0&y-2>0&y-2<9)if(isMoveAble(z[x][y],z[x+1][y-2]))
                System.out.print("("+(x+1)+","+(y-2)+"), ");
            if(x-1<9&x-1>0&y-2>0&y-2<9)if(isMoveAble(z[x][y],z[x-1][y-2]))
                System.out.print("("+(x-1)+","+(y-2)+"), "); 
        }
        
        //for pawn(white)
        if(z[x][y].charAt(0)==(char)75353)
        {
            System.out.print("Available moves: ");
            if(x>1&z[x-1][y]==null)
            System.out.print("("+(x-1)+","+(y)+"), ");
            if(x==7&z[x-2][y]==null)
            System.out.print("("+(x-2)+","+(y)+"), ");
            if(y<8&y>1&x>1&x<8)
            if(isMoveAble(z[x][y],z[x-1][y-1],0))
            System.out.print("("+(x-1)+","+(y-1)+"), ");
            if(isMoveAble(z[x][y],z[x-1][y+1],0))
            System.out.print("("+(x-1)+","+(y+1)+"), ");
            if(y==1&x>1)if(z[x-1][y+1]!=null)
            if(isMoveAble(z[x][y],z[x-1][y+1],0))
            System.out.print("("+(x-1)+","+(y+1)+"), ");
            if(y==8&x>1)if(z[x-1][y-1]!=null)
            if(isMoveAble(z[x][y],z[x-1][y-1],0))
            System.out.print("("+(x-1)+","+(y-1)+"), ");
        }
        
        //for pawn(black)
        if(z[x][y].charAt(0)==(char)75359)
        {
            System.out.print("Available moves: ");
            if(x<7&z[x+1][y]==null)
            System.out.print("("+(x+1)+","+(y)+"), ");
            if(x==2&z[x+2][y]==null)
            System.out.print("("+(x+2)+","+(y)+"), ");
            if(y<8&y>1&x>1&x<8)
            if(isMoveAble(z[x][y],z[x+1][y-1],0))
            System.out.print("("+(x+1)+","+(y-1)+"), ");
            if(isMoveAble(z[x][y],z[x+1][y+1],0))
            System.out.print("("+(x+1)+","+(y+1)+"), ");
            if(y==1&x<7)if(z[x+1][y+1]!=null)
            if(isMoveAble(z[x][y],z[x+1][y+1],0))
            System.out.print("("+(x+1)+","+(y+1)+"), ");
            if(y==8&x<7)if(z[x+1][y-1]!=null)
            if(isMoveAble(z[x][y],z[x+1][y-1],0))
            System.out.print("("+(x+1)+","+(y-1)+"), ");
        }
        
        //for Rook & Queen
        if(z[x][y].charAt(0)==(char)75356|(z[x][y].charAt(0)==(char)75350)|z[x][y].charAt(0)==(char)75349|(z[x][y].charAt(0)==(char)75355))
        {
            int i=x-1,j=y-1,k=0;
            for(;i>0;i--)
            if(isMoveAble(z[x][y],z[i][y]))
            {
                System.out.print("("+i+","+y+"), ");
                k++;
                if(isMoveAble(z[x][y],z[i][y],1))
                break;
            }
            else 
            break;
            
            i=x+1;
            for(;i<9;i++)
            if(isMoveAble(z[x][y],z[i][y]))
            {
                System.out.print("("+i+","+y+"), ");
                k++;
                if(isMoveAble(z[x][y],z[i][y],1))
                break;
            }
            else 
            break;
            
            for(;j>0;j--)
            if(isMoveAble(z[x][y],z[x][j]))
            {
                System.out.print("("+x+","+j+"), ");
                k++;
                if(isMoveAble(z[x][y],z[x][j],1))
                break;
            }
            else
            break;
            
            j=y+1;
            for(;j<9;j++)
            if(isMoveAble(z[x][y],z[x][j]))
            {
                System.out.print("("+x+","+j+"), ");
                k++;
                if(isMoveAble(z[x][y],z[x][j]))
                break;
            }
            else 
            break;
            
            if(k==0)
            System.out.println("\nNo Moves possible!");
        }
        
        //for Bishop & Queen
        if(z[x][y].charAt(0)==(char)75351|(z[x][y].charAt(0)==(char)75357)|z[x][y].charAt(0)==(char)75349|(z[x][y].charAt(0)==(char)75355))
        {
            int i=0,j,k=0;
            if(x>1&y>1)
            {
            i=x-1;
            j=y-1;
            while(i>0&j>0)
            {
            if(isMoveAble(z[x][y],z[i][j]))
            {
                System.out.print("("+i+","+j+"), ");
                k++;
                if(isMoveAble(z[x][y],z[i][j],1))
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
                    if(isMoveAble(z[x][y],z[i][j]))
                    {
                        System.out.print("("+i+","+j+"), ");
                        k++;
                        if(isMoveAble(z[x][y],z[i][j],1))
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
            if(isMoveAble(z[x][y],z[i][j]))
            {
                System.out.print("("+i+","+j+"), ");
                k++;
                if(isMoveAble(z[x][y],z[i][j],1))
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
            if(isMoveAble(z[x][y],z[i][j]))
            {
                System.out.print("("+i+","+j+"), ");
                k++;
                if(isMoveAble(z[x][y],z[i][j],1))
                break;
            }
            else
            break;
            i++;
            j++;
            }
            }
        }
        
        //King
        if(z[x][y].charAt(0)==(char)75348|(z[x][y].charAt(0)==(char)75354))
        {
            if(x<8)
            if(isMoveAble(z[x][y],z[x][y+1]))
            System.out.print("("+x+","+(y+1)+")");
            
            if(x<8&y<8)
            {
            if(isMoveAble(z[x][y],z[x+1][y]))
            System.out.print("("+(x+1)+","+(y)+")");
            
            if(isMoveAble(z[x][y],z[x+1][y+1]))
            System.out.print("("+(x+1)+","+(y+1)+")");
            }
            
            if(x>1)
            if(isMoveAble(z[x][y],z[x][y-1]))
            System.out.print("("+x+","+(y-1)+")");
            
            if(x>1&y>1)
            {
            if(isMoveAble(z[x][y],z[x-1][y]))
            System.out.print("("+(x-1)+","+(y)+")");
            
            if(isMoveAble(z[x][y],z[x-1][y-1]))
            System.out.print("("+(x-1)+","+(y-1)+")");
            }
            
            if(x<8&y>1)
            {
            if(isMoveAble(z[x][y],z[x+1][y]))
            System.out.print("("+(x+1)+","+(y)+")");
            
            if(isMoveAble(z[x][y],z[x+1][y-1]))
            System.out.print("("+(x+1)+","+(y-1)+")");
            }
            
            if(x>1&y<8)
            {
            if(isMoveAble(z[x][y],z[x][y-1]))
            System.out.print("("+x+","+(y-1)+")");
            
            if(isMoveAble(z[x][y],z[x-1][y+1]))
            System.out.print("("+(x-1)+","+(y+1)+")");
            }
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
    
    static  void pawnChoice(String[][]B,int x,int y)
    {
        Scanner in=new Scanner(System.in);
        System.out.println("What do you choose:");
        System.out.println("1. Queen");
        System.out.println("2. Knight");
        System.out.println("3. Rook");
        System.out.println("4. Bishop");
        int n=in.nextInt(),c=0;
        switch(n)
        {
            case 1:
            c=4;
            break;
            case 2:
            c=1;
            break;
            case 3:
            c=3;
            break;
            case 4:
            c=2;
        }
        B[x][y]=(char)((int)(B[x][y].charAt(0)-c))+"";
    }
    
    /*function to play*/
    void play()
    {
        System.out.println("Hey There! Welcome to Chess");
        System.out.println("It's recommended to play with the num pad ");
        Scanner in=new Scanner(System.in);
        String[]B[]=new String[9][9];
        String b[]={(char)(75356)+"",(char)(75358)+"",(char)(75357)+"",(char)(75354)+"",(char)(75355)+"",(char)(75357)+"",(char)(75358)+"",(char)(75356)+""};
        for(int i=1;i<9;i++)
        B[1][i]=b[i-1]; 
        String[]w={(char)(75350)+"",(char)(75352)+"",(char)(75351)+"",(char)(75348)+"",(char)(75349)+"",(char)(75351)+"",(char)(75352)+"",(char)(75350)+""};
        for(int i=1;i<9;i++)
        B[8][i]=w[i-1];
        int i=0,j=0;
        for(i=1;i<9;i++)
        {
            B[2][i]=(char)(75359)+"";
            B[7][i]=(char)(75353)+"";
        }
        
        for(i=0;i<9;i++)
        B[i][0]=i+"";
        for(i=1;i<9;i++)
        B[0][i]=i+"";
        printC(B);
        int x,y,x1,y1;
        i=1;
        String t="";
        while(true)
        {
            
            if(!(searchBlackKing(B)))
            {
            System.out.println("Congratulations! White Kingdom won!!");
            break;
            }
            if(!(searchWhiteKing(B)))
            {
            System.out.println("Conguratulations! Black Kingdom won!!");
            break;
            }
            
        if(i%2==0)
        System.out.println("White's turn::");
        else 
        System.out.println("Black's turn::");
        
        System.out.println("enter coordinates to move: (x,y) , \n (0) to exit.");
        x=in.nextInt();
        if(x==0)
        break;
        y=in.nextInt();
        
        int e=0;
        if(B[x][y]==null)
        System.out.println("Invalid Location !");
        else
        {
            if(e++!=0)
            System.out.println("\n\n\n\n");
            i++;
            avb(B,x,y);
            t=B[x][y];
            System.out.println("Where to move? (x,y)");
            x1=in.nextInt();
            y1=in.nextInt();
            if(x1==1&B[x][y].charAt(0)==(char)(75353))
            pawnChoice(B,x,y);
            else if(x1==8&B[x][y].charAt(0)==(char)(75359))
            pawnChoice(B,x,y);
            if(isMoveAble(B[x][y],B[x1][y1]))
            {
            B[x1][y1]=B[x][y];
            B[x][y]=null;
            }
            printC(B);
        }
        }
        System.out.println("Game Terminates!");
    }
    
    /*main function*/
    public static void main(String args[])
    {
        chessV1 game=new chessV1();
        game.play();
    }
}
