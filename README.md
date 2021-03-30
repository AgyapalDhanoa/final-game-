# final-game

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp51
{
    public class players
    {
        public string Name;
        public string logo;

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
            Console.WriteLine(Fplayer.Name + Splayer.Name);
            Console.WriteLine(Fplayer.logo + Splayer.logo);

            Console.ReadLine();
        }
    }
}
