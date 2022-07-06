#include <iostream>
#include <string.h>
using namespace std;
static int p = 0;

class Bus
{
  char busn[5], arrival[10], depart[10], from[10], to[10], seat[5][4][10];

public:
  void install();
  void allotment();
  void empty();
  void show();
  void position(int i);
}

bus[10];

void vline(char ch)
{
  for (int i=80;i>0;i--)
  cout<<ch;
}

void Bus::install()
{
  cout<<"\nEnter bus no: ";
  cin>>bus[p].busn;
  cout<<"\nArrival time: ";
  cin>>bus[p].arrival;
  cout<<"\nDeparture: ";
  cin>>bus[p].depart;
  cout<<"\nFrom: \t";
  cin>>bus[p].from;
  cout<<"\nTo: \t";
  cin>>bus[p].to;
  bus[p].empty();
  p++;
}

void Bus::allotment()
{
  int seat;
  char number[5];
  top:
  cout<<"Bus no: ";
  cin>>number;
  int n;
  for(n=0;n<=p;n++)
  {
    if(strcmp(bus[n].busn, number)==0)
    break;
  }
  while(n<=p)
  {
    cout<<"\nSeat Number: ";
    cin>>seat;
    if(seat>20)
    {
      cout<<"\nThere are only 20 seats available in this bus.";
    }
    else
    {
    if (strcmp(bus[n].seat[seat/4][(seat%4)-1], "Empty")==0)
      {
        cout<<"Enter passanger's name: ";
        cin>>bus[n].seat[seat/4][(seat%4)-1];
        break;
      }
    else
      cout<<"The seat no. is already reserved.\n";
      }
      }
    if(n>p)
    {
      cout<<"Enter correct bus no.\n";
      goto top;
    }
  }

void Bus::empty()
{
  for(int i=0; i<5;i++)
  {
    for(int j=0;j<4;j++)
    {
      strcpy(bus[p].seat[i][j], "Empty");
    }
  }
}

void Bus::show()
{
  int n;
  char number[5];
  cout<<"Enter bus no: ";
  cin>>number;
  for(n=0;n<=p;n++)
  {
    if(strcmp(bus[n].busn, number)==0)
    break;
  }
while(n<=p)
{
  
  cout<<"Bus no: "<<bus[n].busn<<endl;
  cout<<"Arrival time:\t\t"<<bus[n].arrival<<endl;
  cout<<"Departure time:\t\t"<<bus[n].depart<<endl;
  cout<<"From: "<<bus[n].from<<endl;
  cout<<"To: "<< bus[n].to<<endl;


 
  bus[0].position(n);
  int a=1;
  for (int i=0; i<5; i++)                                   // 
  {
    for(int j=0;j<4;j++)
    {
      a++;
      if(strcmp(bus[n].seat[i][j],"Empty")!=0)
      cout<<"\nThe seat no "<<(a-1)<<" is reserved for "<<bus[n].seat[i][j]<<".";
    }
  }
  break;
  }
  if(n>p)
    cout<<"Enter correct bus no: ";
}

void Bus::position(int l)
{
  int s=0;p=0;
  for (int i =0; i<5;i++)
  {
    cout<<"\n";
    for (int j = 0;j<4; j++)
    {
      s++;
      if(strcmp(bus[l].seat[i][j], "Empty")==0)
        {
          cout.width(5);
          cout.fill(' ');
          cout<<s<<".";
          cout.width(10);
          cout.fill(' ');
          cout<<bus[l].seat[i][j];
          p++;
        }
        else
        {
        cout.width(5);
        cout.fill(' ');
        cout<<s<<".";
        cout.width(10);
        cout.fill(' ');
        cout<<bus[l].seat[i][j];
        }
      }
    }
  cout<<"\n\nThere are "<<p<<" seats empty in Bus No: "<<bus[l].busn;
  }


int main()
{
system("cls");
int w;
while(1)
{
  cout<<"\n\n\t\t\t -----BUS RESERVATION SYSTEM-----\t\t\t"<<endl;
  cout<<"\t1.Install\n\t"
  <<"2.Reservation\n\t"
  <<"3.Show\n\t"
  <<"4.Exit";
  cout<<"\n\tEnter your choice:-> ";
  cin>>w;
  switch(w)    
  {
    case 1:  bus[p].install();
      break;
    case 2:  bus[p].allotment();
      break;
    case 3:  bus[0].show();
      break;
    case 4:  exit(0);
  }
}
return 0;
}
