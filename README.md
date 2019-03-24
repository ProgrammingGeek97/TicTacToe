# TicTacToe
TicTacToe game
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace ticTacToe
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
            p1Count.Text = player1wincount.ToString(); //win count of player1
            p2Count.Text = player2wincount.ToString(); //win count of player2
        }
        bool Turn = true;
        int count = 0;
        string winner = "";
        int player1wincount = 0;
        int player2wincount = 0;
        private void btnClick(object sender, RoutedEventArgs e)
        {
            string o = player1Name.Text; //name of player1
            string x = player2Name.Text; //name of player2
            Button b = (Button)sender;
            if(Turn)
            {
                b.Content = "O";
                b.IsEnabled = false;
                lbTurn.Content = x + "'s Turn!";
            }
            else
            {
                b.Content = "X";
                b.IsEnabled = false;
                lbTurn.Content = o +"'s Turn!";
            }
            Turn = !Turn;
            count++;
            checkWinner();
        }
        void checkWinner()
        {
            bool winnerExists = false;
            //row wise check
            if ((!btn1.IsEnabled) && btn1.Content == btn2.Content && btn2.Content == btn3.Content)
                winnerExists = true;
            if ((!btn4.IsEnabled) && btn4.Content == btn5.Content && btn5.Content == btn6.Content)
                winnerExists = true;
            if ((!btn7.IsEnabled) && btn7.Content == btn8.Content && btn8.Content == btn9.Content)
                winnerExists = true;
            //column wise check
            if ((!btn1.IsEnabled) && btn1.Content == btn4.Content && btn4.Content == btn7.Content)
                winnerExists = true;
            if ((!btn2.IsEnabled) && btn2.Content == btn5.Content && btn5.Content == btn8.Content)
                winnerExists = true;
            if ((!btn3.IsEnabled) && btn3.Content == btn6.Content && btn6.Content == btn9.Content)
                winnerExists = true;
            //digonal check
            if ((!btn1.IsEnabled) && btn1.Content == btn5.Content && btn5.Content == btn9.Content)
                winnerExists = true;
            if ((!btn7.IsEnabled) && btn7.Content == btn5.Content && btn5.Content == btn3.Content)
                winnerExists = true;
            if(winnerExists)
            {
                if (Turn)
                {
                    winner = player2Name.Text;
                    player2wincount++;
                }
                else
                {
                    winner = player1Name.Text;
                    player1wincount++;
                }
                MessageBox.Show("Congratulations " + winner + "! You won.");
                p1Count.Text = player1wincount.ToString();
                p2Count.Text = player2wincount.ToString();
                disableButton();
            }
            if (count == 9 && winner!=player1Name.Text && winner!=player2Name.Text)
                MessageBox.Show("Good Effort! Game Draw.");
        }
        void disableButton()
        {
            btn1.IsEnabled = false;
            btn2.IsEnabled = false;
            btn3.IsEnabled = false;
            btn4.IsEnabled = false;
            btn5.IsEnabled = false;
            btn6.IsEnabled = false;
            btn7.IsEnabled = false;
            btn8.IsEnabled = false;
            btn9.IsEnabled = false;
        }

        private void initialGridLoad(object sender, RoutedEventArgs e)
        {
            lbTurn.Content = "";
        }

        private void restartGame(object sender, RoutedEventArgs e)
        {
            //clearing contents
            btn1.Content = "";
            btn2.Content = "";
            btn3.Content = "";
            btn4.Content = "";
            btn5.Content = "";
            btn6.Content = "";
            btn7.Content = "";
            btn8.Content = "";
            btn9.Content = "";
            winner = "";
            lbTurn.Content = player1Name.Text + "'s Turn!";
            count = 0;
            enableButton();
        }
        void enableButton()
        {
            btn1.IsEnabled = true;
            btn2.IsEnabled = true;
            btn3.IsEnabled = true;
            btn4.IsEnabled = true;
            btn5.IsEnabled = true;
            btn6.IsEnabled = true;
            btn7.IsEnabled = true;
            btn8.IsEnabled = true;
            btn9.IsEnabled = true;
        }
    }
}
