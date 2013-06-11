using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
using Microsoft.Phone.Controls;
using System.Windows.Threading;
namespace 贪吃蛇最终版
{
    public partial class MainPage : PhoneApplicationPage
    {
        // Constructor
        static DispatcherTimer timer = new DispatcherTimer();
        public MainPage()
        {
            
            InitializeComponent();
            timer.Interval = TimeSpan.FromSeconds(1);
            media.Play();
            timer.Start();
            if ((Application.Current as App).ifchoosed == false)
            {
                (Application.Current as App).difficulty = 11;
            }
            timer.Tick += new EventHandler(delegate(object s, EventArgs z)
            {
                if (media.Position.TotalSeconds >= 103)
                {
                    media.Stop();
                    media.Play();
                }
            });
        }
        /*private void button1_Click(object sender, RoutedEventArgs e)
        {
           // media2.Play();
            NavigationService.Navigate(new Uri("/Page1.xaml", UriKind.Relative));
            
        }*/

        private void button2_Click(object sender, RoutedEventArgs e)
        {
            //media2.Play();
            NavigationService.Navigate(new Uri("/Page2.xaml",UriKind.Relative) );
            
        }

        private void button1_Click_1(object sender, RoutedEventArgs e)
        {
            NavigationService.Navigate(new Uri("/Page1.xaml", UriKind.Relative));
        }

        private void button2_Click_1(object sender, RoutedEventArgs e)
        {
            NavigationService.Navigate(new Uri("/Page2.xaml", UriKind.Relative));
            
        }

        
    }
}





using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
using Microsoft.Phone.Controls;
using System.Windows.Threading;

namespace 贪吃蛇最终版
{
    public partial class Page1 : PhoneApplicationPage
    {
        private   DispatcherTimer timer1 = new DispatcherTimer();
        private   DispatcherTimer timer2 = new DispatcherTimer();
        private   DispatcherTimer timer3 = new DispatcherTimer();
        private  DispatcherTimer timer4 = new DispatcherTimer();
        //private   DispatcherTimer timermusic = new DispatcherTimer();
        private  DispatcherTimer timersu = new DispatcherTimer();
        private DispatcherTimer timerbone = new DispatcherTimer();
        //private DispatcherTimer timerimage = new DispatcherTimer();
        public Random a = new Random(), b = new Random();
        public double x;
        public double y;
        public int count,judgesu;
        public bool hide;
        public bool judge1(Rectangle rectangle1, Rectangle rectangle2)
        {
            if ((Canvas.GetTop(rectangle1) == Canvas.GetTop(rectangle2) + 30) && (Canvas.GetLeft(rectangle1) == Canvas.GetLeft(rectangle2)))
                return true;
            return false;
        }
        public bool judge2(Rectangle rectangle1, Rectangle rectangle2)
        {
            if ((Canvas.GetTop(rectangle1) == Canvas.GetTop(rectangle2)) && (Canvas.GetLeft(rectangle1) == Canvas.GetLeft(rectangle2) + 30))
                return true;
            return false;
        }
        public bool judge3(Rectangle rectangle1, Rectangle rectangle2)
        {
            if ((Canvas.GetTop(rectangle1) == Canvas.GetTop(rectangle2)) && (Canvas.GetLeft(rectangle1) == Canvas.GetLeft(rectangle2) - 30))
                return true;
            return false;
        }
        public bool judge4(Rectangle rectangle1, Rectangle rectangle2)
        {
            if ((Canvas.GetTop(rectangle1) == Canvas.GetTop(rectangle2) - 30) && (Canvas.GetLeft(rectangle1) == Canvas.GetLeft(rectangle2)))
                return true;
            return false;
        }
        public bool judge5( List<Rectangle> snake)
        {
            int l = snake.Count - 1, i;
            if (Canvas.GetTop(snake[0]) < 0 || Canvas.GetTop(snake[0]) > 450 || Canvas.GetLeft(snake[0]) < 0 || Canvas.GetLeft(snake[0]) > 480)
                return false;
            else
            {
                    for (i = l; i > 0; i--)
                    {
                        if ((Canvas.GetTop(snake[0]) == Canvas.GetTop(snake[i])) && (Canvas.GetLeft(snake[0]) == Canvas.GetLeft(snake[i])))
                        {
                            return false;
                        }
                    }
                    if (hide == true)
                    {
                        for (i = l; i >= 0; i--)
                        {
                            if (Canvas.GetTop(snake[i]) == Canvas.GetTop(rectangle3) && Canvas.GetLeft(snake[i]) == Canvas.GetLeft(rectangle3))
                                return false;
                            if (Canvas.GetTop(snake[i]) == Canvas.GetTop(rectangle4) && Canvas.GetLeft(snake[i]) == Canvas.GetLeft(rectangle4))
                                return false;
                            if (Canvas.GetTop(snake[i]) == Canvas.GetTop(rectangle5) && Canvas.GetLeft(snake[i]) == Canvas.GetLeft(rectangle5))
                                return false;
                        }
                    }
            }
            return true;
        }
        public bool judge6(List<Rectangle>snake,double x,double y)
        {
            int l = snake.Count - 1,i;
            for (i = 0; i <= l; i++)
            {
                if ((Canvas.GetLeft(snake[i]) == x) &&(Canvas.GetTop(snake[i]) == y))
                    return false;
            }
            return true;
        }

        public  List<Rectangle> snake = new List<Rectangle>();
        public Page1()
        {
            InitializeComponent();
            //double ima1, ima2;
            button1.IsEnabled = true ;
            button2.IsEnabled = true ;
            button3.IsEnabled = true ;
            button4.IsEnabled = true ;
            count = 0; hide = false;
            int second = 0,tisu=0; bool sutype = false;
            /*Canvas.SetTop(rectangle1 , 120);
            Canvas.SetLeft(rectangle1 , 120);*/
            /*snake[0].Width = 30;
            snake[0].Height = 30;
            snake[0].Fill = new SolidColorBrush(Colors.White);*/
            /*Canvas.SetLeft(rectangle1 , 120);
            Canvas.SetTop(rectangle1 , 120);*/
            Canvas.SetLeft(rectangle1, 120);
            Canvas.SetTop(rectangle1, 120);
            snake.Add(rectangle1);
            //canvas1.Children.Add(snake[0]);
            do
            {
                x = a.Next(17);
                y = b.Next(16);
            } while (judge6(snake, x * 30, y * 30) == false);
            Canvas.SetLeft(rectangle2, x * 30);
            Canvas.SetTop(rectangle2, y * 30);
            int di;
            di = (Application.Current as App).difficulty;
            (Application.Current as App).timetype = true ;
            timersu.Interval = TimeSpan.FromSeconds(1);
            switch (di )
            {
                case 11:
                    {
                        timer1.Interval = TimeSpan.FromSeconds(0.3);
                        timer2.Interval = TimeSpan.FromSeconds(0.3);
                        timer3.Interval = TimeSpan.FromSeconds(0.3);
                        timer4.Interval = TimeSpan.FromSeconds(0.3);
                       // timerimage.Interval = TimeSpan.FromSeconds(0.3);
                        media.Source = new Uri("Resources/06 THEME OF ADORU 1993.mp3", UriKind.Relative);
                        
                         tisu = 60; judgesu = 10;
                        MessageBox.Show("在这一关，你需要在一分钟内吃掉十个豆子，加油吧！");
                    }break;
                case 12:
                    {
                        timer1.Interval = TimeSpan.FromSeconds(0.2);
                        timer2.Interval = TimeSpan.FromSeconds(0.2);
                        timer3.Interval = TimeSpan.FromSeconds(0.2);
                        timer4.Interval = TimeSpan.FromSeconds(0.2);
                       // timerimage.Interval = TimeSpan.FromSeconds(0.3);
                        tisu = 90; judgesu = 20;
                        media.Source = new Uri("Resources/Falcom Sound Team jdk - エスピナへ捧ぐ祈り.mp3", UriKind.Relative);
                        MessageBox.Show("在这一关，你需要在一分半钟内吃掉二十个豆子，加油吧！");
                        
                    } break;
                case 13:
                    {
                        timer1.Interval = TimeSpan.FromSeconds(0.1);
                        timer2.Interval = TimeSpan.FromSeconds(0.1);
                        timer3.Interval = TimeSpan.FromSeconds(0.1);
                        timer4.Interval = TimeSpan.FromSeconds(0.1);
                       // timerimage.Interval = TimeSpan.FromSeconds(0.3);
                        tisu = 90; judgesu = 25;
                        media.Source = new Uri("Resources/08 SCARLET TEMPEST.mp3", UriKind.Relative);
                        MessageBox.Show("在这一关，你需要在一分半钟内吃掉二十五个豆子，加油吧！");
                        
                    } break;
                case 14:
                    {
                        timer1.Interval = TimeSpan.FromSeconds(0.1);
                        //timerimage.Interval = TimeSpan.FromSeconds(0.3);
                        timer2.Interval = TimeSpan.FromSeconds(0.1);
                        timer3.Interval = TimeSpan.FromSeconds(0.1);
                        timer4.Interval = TimeSpan.FromSeconds(0.1);
                        timerbone.Interval = TimeSpan.FromSeconds(4);
                        tisu = 120; judgesu = 25; hide = true;
                        media.Source = new Uri("Resources/阿女神.mp3", UriKind.Relative);
                        rectangle3.Visibility = Visibility.Visible;
                        rectangle4.Visibility = Visibility.Visible;
                        rectangle5.Visibility = Visibility.Visible;
                        MessageBox.Show("不错嘛，你居然能闯到这一关，你还是需要在两分钟内吃掉二十五个豆子，但要小心我布置的棋子哦！哈哈哈……");
                        do
                        {
                            x = a.Next(17);
                            y = b.Next(16);
                        } while (judge6(snake, x * 30, y * 30) == false||((Canvas .GetLeft (rectangle2 )==x*30)&&(Canvas .GetTop (rectangle2 )==y*30)));
                        Canvas.SetLeft(rectangle3, x * 30);
                        Canvas.SetTop(rectangle3, y * 30);
                        do
                        {
                            x = a.Next(17);
                            y = b.Next(16);
                        } while (judge6(snake, x * 30, y * 30) == false || ((Canvas.GetLeft(rectangle2) == x * 30) && (Canvas.GetTop(rectangle2) == y * 30)) || ((Canvas.GetLeft(rectangle3) == x * 30) && (Canvas.GetTop(rectangle3) == y * 30)));
                        Canvas.SetLeft(rectangle4, x * 30);
                        Canvas.SetTop(rectangle4, y * 30);
                       
                        timerbone.Start();
                    }break;
        }
            media.Play();
           // timerimage.Start();
           /* timermusic.Interval = System.TimeSpan.FromSeconds(1);
            timermusic.Start();
           timermusic.Tick += new EventHandler(delegate(object s, EventArgs z)
            {
                if (media.Position.TotalSeconds >=ti )
                {
                    media.Stop();
                    media.Play();

                }

            });*/
          /*  timerimage.Tick += new EventHandler(delegate(object s, EventArgs z)
            {
                ima1 = Canvas.GetLeft(image1);
                ima2 = Canvas.GetLeft(image2);
                Canvas.SetLeft(image1,ima1-20);
                Canvas.SetLeft(image2, ima2 - 20);
                if (ima1-20== -510)
                {
                    Canvas.SetLeft(image1, 510);
                }
                if (ima2-20 == -510)
                {
                    Canvas.SetLeft(image2, 510);
                }
            });*/
            timerbone.Tick += new EventHandler(delegate(object s, EventArgs z)
            {
                do
                {
                    x = a.Next(17);
                    y = b.Next(16);
                } while (judge6(snake, x * 30, y * 30) == false || ((Canvas.GetLeft(rectangle2) == x * 30) && (Canvas.GetTop(rectangle2) == y * 30)));
                Canvas.SetLeft(rectangle3, x * 30);
                Canvas.SetTop(rectangle3, y * 30);
                do
                {
                    x = a.Next(17);
                    y = b.Next(16);
                } while (judge6(snake, x * 30, y * 30) == false || ((Canvas.GetLeft(rectangle2) == x * 30) && (Canvas.GetTop(rectangle2) == y * 30)) || ((Canvas.GetLeft(rectangle3) == x * 30) && (Canvas.GetTop(rectangle3) == y * 30)));
                Canvas.SetLeft(rectangle4, x * 30);
                Canvas.SetTop(rectangle4, y * 30);
            });
           timersu.Tick += new EventHandler(delegate(object s, EventArgs z)
           {
               second++;
               if (second < 10)
                   textBlock3.Text = "0:0" + second.ToString();
               else if (second < 60)
                   textBlock3.Text = "0:" + second.ToString();
               else if (second < 70)
                   textBlock3.Text = "1:0" + (second - 60).ToString();
               else if (second < 120)
                   textBlock3.Text = "1:" + (second - 60).ToString();
               else
                   textBlock3.Text = "2:00";
               if (second >= tisu )
               {
                   button1.IsEnabled = false;
                   button2.IsEnabled = false;
                   button3.IsEnabled = false;
                   button4.IsEnabled = false;
                   timer1.Stop();
                   timer2.Stop();
                   timer3.Stop();
                   timer4.Stop();
                   timersu.Stop();
                   //timerimage.Stop();
                   rectangle3.Visibility = Visibility.Collapsed;
                   rectangle4.Visibility = Visibility.Collapsed;
                   rectangle5.Visibility = Visibility.Collapsed;
                   if (timerbone.IsEnabled == true)
                       timerbone.Stop();
                   snake.RemoveRange(0, snake.Count - 1);
                   if (count < judgesu)
                       MessageBox.Show("厄啊，楼主失败了！！！");
                   else
                   {
                       if (judgesu == 10)
                           (Application.Current as App).s1 = true;
                       else if (judgesu == 20)
                           (Application.Current as App).s2 = true;
                       else
                           (Application.Current as App).s3 = true;
                       MessageBox.Show("恭喜，楼主赢了！！！");
                   }
                   NavigationService.Navigate(new Uri("/MainPage.xaml", UriKind.Relative));
               }

           });
           timer1.Tick += new EventHandler(delegate(object s, EventArgs z)//上
           {
               if (sutype == false)
               {
                   timersu.Start();
                   sutype = true;
               }
               if ((Application.Current as App).timetype == true)
               {
                   Canvas.SetLeft(snake[0], 120);
                   Canvas.SetTop(snake[0], 120);
                   (Application.Current as App).timetype = false;
               }
               int l = snake.Count - 1;
               double x1, y1;
               if (judge1(snake[0], rectangle2))
               {
                   double g, h;
                   x1 = Canvas.GetTop(snake[0]);
                   y1 = Canvas.GetLeft(snake[0]);
                   g = Canvas.GetLeft(snake[l]);
                   h = Canvas.GetTop(snake[l]);
                   snake.Add(new Rectangle());
                   //media2.Stop();
                   Canvas.SetLeft(snake[0], Canvas.GetLeft(rectangle2));
                   Canvas.SetTop(snake[0], Canvas.GetTop(rectangle2));
                   for (int i = l; i > 0; i--)
                   {
                       if (i == 1)
                       {
                           Canvas.SetTop(snake[i], x1);
                           Canvas.SetLeft(snake[i], y1);
                       }
                       else
                       {
                           Canvas.SetTop(snake[i], Canvas.GetTop(snake[i - 1]));
                           Canvas.SetLeft(snake[i], Canvas.GetLeft(snake[i - 1]));
                       }
                   }
                   snake[l + 1].Width = 30;
                   snake[l + 1].Height = 30;
                  // snake[l + 1].Fill = new SolidColorBrush(Colors.White);
                   snake[l + 1].Fill = new SolidColorBrush();
                   snake[l + 1].Fill = rectangle6.Fill;
                   Canvas.SetLeft(snake[l + 1], g);
                   Canvas.SetTop(snake[l + 1], h);
                   canvas1.Children.Add(snake[l + 1]);
                   do
                   {
                       x = a.Next(17);
                       y = b.Next(16);
                   } while (judge6(snake, x * 30, y * 30) == false);
                   Canvas.SetLeft(rectangle2, x * 30);
                   Canvas.SetTop(rectangle2, y * 30);
                   count ++;
               }
               else
               {
                   x1 = Canvas.GetTop(snake[0]);
                   y1 = Canvas.GetLeft(snake[0]);
                   Canvas.SetTop(snake[0], Canvas.GetTop(snake[0]) - 30);
                   for (int i = l; i > 0; i--)
                   {
                       if (i == 1)
                       {
                           Canvas.SetTop(snake[i], x1);
                           Canvas.SetLeft(snake[i], y1);
                       }
                       else
                       {
                           Canvas.SetTop(snake[i], Canvas.GetTop(snake[i - 1]));
                           Canvas.SetLeft(snake[i], Canvas.GetLeft(snake[i - 1]));
                       }
                   }
                   if (judge5(snake) == false)
                   {
                       button1.IsEnabled = false;
                       button2.IsEnabled = false;
                       button3.IsEnabled = false;
                       button4.IsEnabled = false;
                       timer1.Stop();
                       timer2.Stop();
                       timer4.Stop();
                       timer3.Stop();
                       timersu.Stop();
                       //timerimage.Stop();
                       rectangle3.Visibility = Visibility.Collapsed;
                       rectangle4.Visibility = Visibility.Collapsed;
                       rectangle5.Visibility = Visibility.Collapsed;
                       if (timerbone.IsEnabled == true)
                           timerbone.Stop();
                       snake.RemoveRange(0, snake.Count - 1);
                       //snake.RemoveAt(0);
                       MessageBox.Show("厄啊，楼主失败了！！！");
                       NavigationService.Navigate(new Uri("/MainPage.xaml", UriKind.Relative));
                   }
               }
               textBlock4.Text = count.ToString();
           });
           timer2.Tick += new EventHandler(delegate(object s, EventArgs z)//左
           {
               if (sutype == false)
               {
                   timersu.Start();
                   sutype = true;
               }
               if ((Application.Current as App).timetype == true)
               {
                   Canvas.SetLeft(snake[0], 120);
                   Canvas.SetTop(snake[0], 120);
                   (Application.Current as App).timetype = false;
               }
               int l = snake.Count - 1; double x1, y1;
               if (judge2(snake[0], rectangle2))
               {
                   double g, h;
                   g = Canvas.GetLeft(snake[l]);
                   h = Canvas.GetTop(snake[l]);
                   x1 = Canvas.GetTop(snake[0]);
                   y1 = Canvas.GetLeft(snake[0]);
                   snake.Add(new Rectangle());
                 //  media2.Stop();
                   Canvas.SetLeft(snake[0], Canvas.GetLeft(rectangle2));
                   Canvas.SetTop(snake[0], Canvas.GetTop(rectangle2));
                   for (int i = l; i > 0; i--)
                   {
                       if (i == 1)
                       {
                           Canvas.SetTop(snake[i], x1);
                           Canvas.SetLeft(snake[i], y1);
                       }
                       else
                       {
                           Canvas.SetTop(snake[i], Canvas.GetTop(snake[i - 1]));
                           Canvas.SetLeft(snake[i], Canvas.GetLeft(snake[i - 1]));
                       }
                   }
                   snake[l + 1].Width = 30;
                   snake[l + 1].Height = 30;
                   //snake[l + 1].Fill = new SolidColorBrush(Colors.White);
                   snake[l + 1].Fill = new SolidColorBrush();
                   snake[l + 1].Fill = rectangle6.Fill;
                   Canvas.SetLeft(snake[l + 1], g);
                   Canvas.SetTop(snake[l + 1], h);
                   canvas1.Children.Add(snake[l + 1]);
                   do
                   {
                       x = a.Next(17);
                       y = b.Next(16);
                   } while (judge6(snake, x * 30, y * 30) == false);
                   Canvas.SetLeft(rectangle2, x * 30);
                   Canvas.SetTop(rectangle2, y * 30);
                   count++;
               }
               else
               {
                   x1 = Canvas.GetTop(snake[0]);
                   y1 = Canvas.GetLeft(snake[0]);
                  Canvas.SetLeft(snake[0], Canvas.GetLeft(snake[0]) - 30);
                   for (int i = l; i > 0; i--)
                   {
                       if (i == 1)
                       {
                           Canvas.SetTop(snake[i], x1);
                           Canvas.SetLeft(snake[i], y1);
                       }
                       else
                       {
                           Canvas.SetTop(snake[i], Canvas.GetTop(snake[i - 1]));
                           Canvas.SetLeft(snake[i], Canvas.GetLeft(snake[i - 1]));
                       }
                   }
                   if (judge5(snake) == false)
                   {
                       button1.IsEnabled = false;
                       button2.IsEnabled = false;
                       button3.IsEnabled = false;
                       button4.IsEnabled = false;
                       timer1.Stop();
                       timer2.Stop();
                       timer4.Stop();
                       timer3.Stop();
                       timersu.Stop();
                       //timerimage.Stop();
                       rectangle3.Visibility = Visibility.Collapsed;
                       rectangle4.Visibility = Visibility.Collapsed;
                       rectangle5.Visibility = Visibility.Collapsed;
                       if (timerbone.IsEnabled == true)
                           timerbone.Stop();
                       snake.RemoveRange(0, snake.Count - 1);
                       // snake.RemoveAt(0);
                       MessageBox.Show("厄啊，楼主失败了！！！");
                       NavigationService.Navigate(new Uri("/MainPage.xaml", UriKind.Relative));

                   }
               }
               textBlock4.Text = count.ToString();
           });
            timer3.Tick += new EventHandler(delegate(object s, EventArgs z)//右
           {
               if (sutype == false)
               {
                   timersu.Start();
                   sutype = true;
               }
               if ((Application.Current as App).timetype == true)
               {
                   Canvas.SetLeft(snake[0], 120);
                   Canvas.SetTop(snake[0], 120);
                   (Application.Current as App).timetype = false;
               }
               int l = snake.Count - 1;
               double x1, y1;
               if (judge3(snake[0], rectangle2))
               {
                   double g, h;
                   g = Canvas.GetLeft(snake[l]);
                   h = Canvas.GetTop(snake[l]);
                   snake.Add(new Rectangle());
                  // media2.Stop();
                   x1 = Canvas.GetTop(snake[0]);
                   y1 = Canvas.GetLeft(snake[0]);
                   Canvas.SetLeft(snake[0], Canvas.GetLeft(rectangle2));
                   Canvas.SetTop(snake[0], Canvas.GetTop(rectangle2));
                   for (int i = l; i > 0; i--)
                   {
                       if (i == 1)
                       {
                           Canvas.SetTop(snake[i], x1);
                           Canvas.SetLeft(snake[i], y1);
                       }
                       else
                       {
                           Canvas.SetTop(snake[i], Canvas.GetTop(snake[i - 1]));
                           Canvas.SetLeft(snake[i], Canvas.GetLeft(snake[i - 1]));
                       }
                   }
                   snake[l + 1].Width = 30;
                   snake[l + 1].Height = 30;
                   //snake[l + 1].Fill = new SolidColorBrush(Colors.White);
                   snake[l + 1].Fill = new SolidColorBrush();
                   snake[l + 1].Fill = rectangle6.Fill;
                   Canvas.SetLeft(snake[l + 1], g);
                   Canvas.SetTop(snake[l + 1], h);
                   canvas1.Children.Add(snake[l + 1]);
                   do
                   {
                       x = a.Next(17);
                       y = b.Next(16);
                   } while (judge6(snake, x * 30, y * 30) == false);
                   Canvas.SetLeft(rectangle2, x * 30);
                   Canvas.SetTop(rectangle2, y * 30);
                   count++;
               }

               else
               {
                   x1 = Canvas.GetTop(snake[0]);
                   y1 = Canvas.GetLeft(snake[0]);
                   Canvas.SetLeft(snake[0], Canvas.GetLeft(snake[0]) + 30);
                   for (int i = l; i > 0; i--)
                   {
                       if (i == 1)
                       {
                           Canvas.SetTop(snake[i], x1);
                           Canvas.SetLeft(snake[i], y1);
                       }
                       else
                       {
                           Canvas.SetTop(snake[i], Canvas.GetTop(snake[i - 1]));
                           Canvas.SetLeft(snake[i], Canvas.GetLeft(snake[i - 1]));
                       }
                   }
                   if (judge5(snake) == false)
                   {
                       button1.IsEnabled = false;
                       button2.IsEnabled = false;
                       button3.IsEnabled = false;
                       button4.IsEnabled = false;
                       timer1.Stop();
                       timer2.Stop();
                       timer4.Stop();
                       timer3.Stop();
                       timersu.Stop();
                       //timerimage.Stop();
                       rectangle3.Visibility = Visibility.Collapsed;
                       rectangle4.Visibility = Visibility.Collapsed;
                       rectangle5.Visibility = Visibility.Collapsed;
                       if (timerbone.IsEnabled == true)
                           timerbone.Stop();
                       snake.RemoveRange(0, snake.Count - 1);
                       //snake.RemoveAt(0);
                       MessageBox.Show("厄啊，楼主失败了！！！");
                       NavigationService.Navigate(new Uri("/MainPage.xaml", UriKind.Relative));
                   }
               }
               textBlock4.Text = count.ToString();
           });
           timer4.Tick += new EventHandler(delegate(object s, EventArgs z)//下
           {
               if (sutype == false)
               {
                   timersu.Start();
                   sutype = true;
               }
               if ((Application.Current as App).timetype == true)
               {
                   Canvas.SetLeft(snake[0], 120);
                   Canvas.SetTop(snake[0], 120);
                   (Application.Current as App).timetype = false;
               }
               int l = snake.Count - 1;
               double x1, y1;
               if (judge4(snake[0], rectangle2))
               {
                   double g, h;
                   x1 = Canvas.GetTop(snake[0]);
                   y1 = Canvas.GetLeft(snake[0]);
                   g = Canvas.GetLeft(snake[l]);
                   h = Canvas.GetTop(snake[l]);
                   snake.Add(new Rectangle());
                   //media2.Stop();
                   Canvas.SetLeft(snake[0], Canvas.GetLeft(rectangle2));
                   Canvas.SetTop(snake[0], Canvas.GetTop(rectangle2));
                   for (int i = l; i > 0; i--)
                   {
                       if (i == 1)
                       {
                           Canvas.SetTop(snake[i], x1);
                           Canvas.SetLeft(snake[i], y1);
                       }
                       else
                       {
                           Canvas.SetTop(snake[i], Canvas.GetTop(snake[i - 1]));
                           Canvas.SetLeft(snake[i], Canvas.GetLeft(snake[i - 1]));
                       }
                   }
                   snake[l + 1].Width = 30;
                   snake[l + 1].Height = 30;
                   //snake[l + 1].Fill = new SolidColorBrush(Colors.White);
                   snake[l + 1].Fill = new SolidColorBrush();
                   snake[l + 1].Fill = rectangle6.Fill;
                   Canvas.SetLeft(snake[l + 1], g);
                   Canvas.SetTop(snake[l + 1], h);
                   canvas1.Children.Add(snake[l + 1]);
                   do
                   {
                       x = a.Next(17);
                       y = b.Next(16);
                   } while (judge6(snake, x * 30, y * 30) == false);
                   Canvas.SetLeft(rectangle2, x * 30);
                   Canvas.SetTop(rectangle2, y * 30);
                   count++;
               }
               else
               {
                   x1 = Canvas.GetTop(snake[0]);
                   y1 = Canvas.GetLeft(snake[0]);
                   Canvas.SetTop(snake[0], Canvas.GetTop(snake[0]) + 30);
                   for (int i = l; i > 0; i--)
                   {
                       if (i == 1)
                       {
                           Canvas.SetTop(snake[i], x1);
                           Canvas.SetLeft(snake[i], y1);
                       }
                       else
                       {
                           Canvas.SetTop(snake[i], Canvas.GetTop(snake[i - 1]));
                           Canvas.SetLeft(snake[i], Canvas.GetLeft(snake[i - 1]));
                       }
                   }
                   if (judge5(snake) == false)
                   {
                       button1.IsEnabled = false;
                       button2.IsEnabled = false;
                       button3.IsEnabled = false;
                       button4.IsEnabled = false;
                       timer1.Stop();
                       timer2.Stop();
                       timer4.Stop();
                       timer3.Stop();
                       timersu.Stop();
                      // timerimage.Stop();
                       rectangle3.Visibility = Visibility.Collapsed;
                       rectangle4.Visibility = Visibility.Collapsed;
                       rectangle5.Visibility = Visibility.Collapsed;
                       if (timerbone.IsEnabled == true)
                           timerbone.Stop();
                       snake.RemoveRange(0, snake.Count - 1);
                       //  snake.RemoveAt(0);
                       MessageBox.Show("厄啊，楼主失败了！！！");
                       NavigationService.Navigate(new Uri("/MainPage.xaml", UriKind.Relative));
                   }

               }
               textBlock4.Text = count.ToString ();

           });
        }
     
        private void button3_Click(object sender, RoutedEventArgs e)
        {
            if (timer2.IsEnabled != true)
            {
                timer2.Stop();
                timer1.Stop();
                timer4.Stop();
                timer3.Start();
            }
        }

        private void button2_Click(object sender, RoutedEventArgs e)
        {
            if (timer3.IsEnabled != true)
            {
                timer3.Stop();
                timer1.Stop();
                timer4.Stop();
                timer2.Start();
            }
        }

        private void button1_Click(object sender, RoutedEventArgs e)
        {
            if (timer4.IsEnabled != true)
            {
                timer4.Stop();
                timer2.Stop();
                timer3.Stop();
                timer1.Start();
            }
        }

        private void button4_Click(object sender, RoutedEventArgs e)
        {
            if (timer1.IsEnabled != true)
            {
                timer1.Stop();
                timer2.Stop();
                timer3.Stop();
                timer4.Start();
            } 
        }

        private void button5_Click(object sender, RoutedEventArgs e)
        {
            button1.IsEnabled = false;
            button2.IsEnabled = false;
            button3.IsEnabled = false;
            button4.IsEnabled = false;
            timer1.Stop();
            timer2.Stop();
            timer3.Stop();
            timer4.Stop();
            timersu.Stop();
            //timerimage.Stop();
            rectangle3.Visibility = Visibility.Collapsed;
            rectangle4.Visibility = Visibility.Collapsed;
            rectangle5.Visibility = Visibility.Collapsed;
            if (timerbone.IsEnabled == true)
                timerbone.Stop();
            //int i;
           // for (i = 0; i <= snake.Count - 1; i++)
                //canvas1.Children.Remove(snake[i]);
            snake.RemoveRange(0, snake.Count - 1);
          //  snake.RemoveAt(0);
            NavigationService.Navigate(new Uri("/MainPage.xaml", UriKind.Relative));
        }

    }
}




using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
using Microsoft.Phone.Controls;
using System.Windows.Threading;
namespace 贪吃蛇最终版
{
    public partial class Page2 : PhoneApplicationPage
    {
        static DispatcherTimer timer = new DispatcherTimer();
        public Page2()
        {
            InitializeComponent();
            (Application.Current as App).ifchoosed = true;
            media.Play();
            timer.Interval = System.TimeSpan.FromSeconds(1);
            timer.Tick += new EventHandler(delegate(object s, EventArgs z)
            {
                if (media.Position.TotalSeconds >= 124)
                {
                    media.Stop();
                    media.Play();
                }

            });
            if ((Application.Current as App).s1 == true && (Application.Current as App).s2 == true && (Application.Current as App).s3 == true)
                radioButton4.Visibility = Visibility.Visible;
        }

        private void button1_Click(object sender, RoutedEventArgs e)
        {
            //media2.Stop(); 
            NavigationService.Navigate(new Uri("/MainPage.xaml", UriKind.Relative));
           // media2.Play();
        }

        private void radioButton1_Checked(object sender, RoutedEventArgs e)
        {
            (Application.Current as App).difficulty = 11;
            //media3.Play();

        }

        private void radioButton2_Checked(object sender, RoutedEventArgs e)
        {
            //media3.Stop();
            (Application.Current as App).difficulty = 12;
           // media3.Play();
        }

        private void radioButton3_Checked(object sender, RoutedEventArgs e)
        {
           //media3.Stop();
            (Application.Current as App).difficulty = 13;
            //media3.Play();
        }

        private void radioButton4_Checked(object sender, RoutedEventArgs e)
        {
           // media3.Stop();
            (Application.Current as App).difficulty = 14;
            //media3.Play();
        }

      

    }
}
