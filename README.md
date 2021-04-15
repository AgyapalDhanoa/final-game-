
using System;

namespace consoleApp51
{

    public class playerInfo
    {
        public String Name { get; set; }
        public char Logo { get; set; }

    };

    public class again : Display
    {
        public int nowagain { get; set; }

        public again()
        {

        }

        public again(int again)
        {
            nowagain = again;
        }

        public void starter()
        {
            if (nowagain == 1)
            {
                Display board = new Display();
                board.Board();

            }
            else
            {
                Console.WriteLine("Game End");
            }
        }


    }

    public class Display
    {
        
        public double rows = 6;
        public double columns = 7;
        char[,] Boards;
        public Display()
        {
            
        }
        public Display(char [,] board)
        {
            Boards = board;
        }
        public void Board()
        {
            Console.Clear();


            for (int i = 1; i <= rows; i++)
            {
                Console.Write("        || ");
                for (int j = 1; j <= columns; j++)
                {
                 Console.Write(Boards[i, j]);
                }
                Console.WriteLine(" ||");
            }
        }
    }
    public class Winning 
    {
        public static int vertical { get; set; } = 6;
        public Winning()
        {
        }
        public static void winner(char[,] board, playerInfo current, int chosen)
        {
            int  turn =0;
    

            do
            {
                if (board[vertical, chosen] != 'X' && board[vertical, chosen] != 'O')
                {
                    board[vertical, chosen] = current.Logo;
                    turn = 1;
                }
                else
                {
                    --vertical;
                }
            } while (turn != 1);
        }

    }
    public class Entry :playerInfo
    {

      public static  int entrychoice;
        public Entry()
        { 
        }
        public static int put(char[,] board, playerInfo current)
        {
           

            Console.WriteLine(current.Name + " is playing now  \n\n");
            do
            {
                Console.WriteLine("Enter in the limit of 1 to 7: ");
                entrychoice = Convert.ToInt32(Console.ReadLine());
            } while (entrychoice < 1 || entrychoice > 7);
            return entrychoice;
        }
    }
    public class WholeBoardDisplay
    {

        public static void DisplayBoard(char[,] board)
        {
            int rows = 6, columns = 7;
            Console.Clear();
            for (int i = 1; i <= rows; i++)
            {
                Console.Write("   ||");
                for (int j = 1; j <= columns; j++)
                {
                    if (board[i, j] != 'X' && board[i, j] != 'O')
                        board[i, j] = '*';

                    Console.Write(board[i, j]);

                }

                Console.Write("| \n");
            }

        }
        
    }


    class Program
    {


        static void Main(string[] args)
        {
            playerInfo FPlayer = new playerInfo();
            playerInfo SPlayer = new playerInfo();
            char[,] gameboard = new char[9, 10];
            Console.WriteLine("First player name: ");
            FPlayer.Name = Console.ReadLine();
            FPlayer.Logo = 'X';
            Console.WriteLine("Second player name : ");
            SPlayer.Name = Console.ReadLine();
            SPlayer.Logo = 'O';

            
            WholeBoardDisplay.DisplayBoard(gameboard);
            int Entered, win = 0, reset = 0;
            do
            {
                Entered = Entry.put(gameboard, FPlayer);
                Winning.winner(gameboard, FPlayer, Entered);
                WholeBoardDisplay.DisplayBoard(gameboard);
                Entered = Entry.put(gameboard, SPlayer);
                Winning.winner(gameboard, SPlayer, Entered);
                WholeBoardDisplay.DisplayBoard(gameboard);

                if (win == 1)
                {
                    Console.WriteLine("Player 1 wins");
    
                }
                if(win == 2)
                {
                    Console.WriteLine("player 2 wins");
                }

               
            } while (reset == 1);

        }

  
    }
}
