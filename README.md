using System;


namespace ConsoleApp51
{
	public class players
	{
		public string Name { get; set; }
		public string logo { get; set; }

	}
	public  class Display
    {
		public void board()
        {
			char[,] board = new char[9, 10];
			double rows = 6;
			double columns = 7;

			for (int i = 1; i <= rows; i++)
			{
				Console.Write("        || ");
				for (int j = 1; j <= columns; j++)
				{
					if (board[i, j] != 'O' && board[i, j] != 'X')
						board[i, j] = '*';

					Console.Write(board[i, j]);

				}

				Console.WriteLine(" ||");
			}

		}

    }
	class Program
	{
		static void Main(string[] args)
		{
			players Fplayer = new players();
			players Splayer = new players();

			Console.WriteLine("Starting the game...");
			Console.WriteLine("Enter first player name");
			Fplayer.Name = Console.ReadLine();
			Console.WriteLine("******************************");
			Console.WriteLine("Enter first player name");
			Splayer.Name = Console.ReadLine();
			Fplayer.logo = "X";
			Splayer.logo = "O";
			
			Console.WriteLine("***********************");
			Console.WriteLine("First Player :" + Fplayer.Name);
			Console.WriteLine("Second Player :" + Splayer.Name);
			Console.WriteLine("***********************\n\n");

			Display board = new Display();
			board.board();

			Console.ReadLine();
		}
	}
}
