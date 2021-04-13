
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

using System;


namespace ConsoleApp51
{
	public class PlayerData
	{


		public static int steps { get; private set; }


		public static int totalPlayers;

		public string playerName;




		public PlayerData(string name)
		{

			playerName = name;
			totalPlayers++;
			
		}


		public static int WhoesTurn()
		{

			return (steps % totalPlayers) + 1;
		}


		public string GetPlayerName()
		{

			return playerName;
		}

		public static void displaydata()
        {
			Console.WriteLine("Total players are : " + totalPlayers);

        }


	}

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
		public void Board()
		{
			Console.Clear();
			char[,] board = new char[9, 10];
			double rows = 6;
			double columns = 7;
			Console.WriteLine("Now playing player: {0}", PlayerData.WhoesTurn());

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

			string choice;
			string playerName;
			List<PlayerData> players = new List<PlayerData>();
			do
			{
				Console.WriteLine("Please enter a player name: ");
				playerName = Console.ReadLine();
				PlayerData newPlayer = new PlayerData(playerName);
				players.Add(newPlayer);
				Console.WriteLine("Another player? :Y/N ");
				choice = Console.ReadLine();
			} while (choice == "y" || choice == "Y");


			Console.Clear();

			Display board = new Display();
			board.Board();


			int answer;
			do
			{

			
				Console.WriteLine("Do you want to Continue   \n Yes : 1  No  :  0");
				string answers = Console.ReadLine();
				 answer = Convert.ToInt32(answers);
				again a = new again(answer);

				a.starter();
			} while (answer == 1);




			Console.ReadLine();
		}
	}
}

