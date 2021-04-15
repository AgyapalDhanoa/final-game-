
using System;

namespace ConsoleApp51
{

    public class playerInfo
    {
        public String Name { get; set; }
        public char Logo { get; set; }

    };

    public class again : Display
    {
        public int Nowagain { get; set; }

        public again()
        {

        }

        public again(int again)
        {
            Nowagain = again;
        }

        public void starter()
        {
            if (Nowagain == 1)
            {
                Display newer = new Display();
                newer.Board();

            }
            else
            {
                Console.WriteLine("Game End");
            }
        }


    }

    public class Display :playerInfo
    {
        
        public double rows = 6;
        public double columns = 7;
        char[,] Boards { get; set; }
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
                if (board[vertical, chosen] != 'X' && 
                    board[vertical, chosen] != 'O')
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




    public class Entry 
    {

      public static  int entrychoice;
        public Entry()
        {

        }

        public static int enterdata(char[,] board, playerInfo current)
        {
           

            Console.WriteLine(current.Name + " is playing now  \n\n");

            do
            {
                Console.WriteLine("Enter in the limit of 1 to 7: ");
                entrychoice = Convert.ToInt32(Console.ReadLine());
            } while (entrychoice <=0 || entrychoice >= 6);


            return entrychoice;
        }
    }







    public class Condtions
    {




        public static int conditions(char[,] board, playerInfo current)
        {
            char pattern;
            int win;

            pattern = current.Logo;
            win = 0;

            for (int i = 7; i >= 0; --i)
            {

                for (int j = 8; j >= 0; --j)
                {

                    if (board[i, j] == pattern &&
                        board[i - 1, j - 1] == pattern &&
                        board[i - 2, j - 2] == pattern && 
                        board[i - 3, j - 3] == pattern)
                    {
                        win++;
                    }
                    else if (board[i, j] == pattern
                        && 
                        board[i - 1, j] == pattern
                        &&

                  board[i - 2, j] == pattern 
                  &&
                  board[i - 3, j] == pattern)
                    {
                        win++;
                    }

                    else if (board[i, j] == pattern &&
                        board[i, j - 1] == pattern &&
                         board[i, j - 2] == pattern &&
                         board[i, j - 3] == pattern)
                    {
                        win++;
                    }

              

                    else if (board[i, j] == pattern &&
                        board[i - 1, j + 1] == pattern &&
                        board[i - 2, j + 2] == pattern && 
                        board[i - 3, j + 3] == pattern)
                    {
                        win++;
                    }

                    else if (board[i, j] == pattern && 
                        board[i, j + 1] == pattern &&
                             board[i, j + 2] == pattern &&
                             board[i, j + 3] == pattern)
                    {
                         win++;
                    }
                }

            }
            return win;
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

                Console.Write("|| \n");
            }

        } 
    }
    class Program
    {


        static void Main(string[] args)
        {
            playerInfo FPlayer = new playerInfo();
            playerInfo SPlayer = new playerInfo();


            


            Console.WriteLine("Enter player 1 name: ");
            FPlayer.Name = Console.ReadLine();
            FPlayer.Logo = 'X';
            Console.WriteLine("Enter player 2 name: ");
            SPlayer.Name = Console.ReadLine();
            SPlayer.Logo = 'O';

            int choose, win = 0, reset = 0;
            char[,] board = new char[9, 10];
            WholeBoardDisplay.DisplayBoard(board);

            do
            {
                choose = Entry.enterdata(board, FPlayer);
                Winning.winner(board, FPlayer, choose);
                WholeBoardDisplay.DisplayBoard(board);
                win = Condtions.conditions(board, FPlayer);

                choose = Entry.enterdata(board, SPlayer);
                Winning.winner(board, SPlayer, choose);
                WholeBoardDisplay.DisplayBoard(board);
                win = Condtions.conditions(board, SPlayer);
                if (win == 1)
                {
                    Console.WriteLine("Player 1 wins");
                }
                if (win == 2)
                {
                    Console.WriteLine("Player 2 wins");


                }


            } while (reset == 1);

        }
    }
}
