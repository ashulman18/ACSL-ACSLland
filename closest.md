# ACSLland
December 2014 ACSL Project

//Andrea Shulman
//Navigating ACSLland
//December 2014

import java.util.ArrayList;
public class ACSLland
{
   private int [] miles;
   private String[] cities;
   private String pos1, pos2;
   private int time1, time2; //will be recorded in military time
   private boolean am1,am2;
   private int speed1, speed2;
   public ACSLland(String str)
   {
      //----------initializing variables from given String----------
      int[]commas=new int [7]; //array with indexes of commas
      int count=0;
      for(int i=0; i<str.length();i++)
      {
         if((str.substring(i,i+1)).equals(","))
         {
            commas[count]=i;
            count++;
         }
      }
      pos1=str.substring(0,commas[0]);
      pos2=str.substring(commas[0]+1,commas[1]);
      time1=Integer.parseInt(str.substring(commas[1]+1,commas[2]));
      if((str.substring(commas[2]+1,commas[3])).equals("AM")&&time1!=12)
         am1=true;
      else
         am1=false;
      time2=Integer.parseInt(str.substring(commas[3]+1,commas[4]));
      if((str.substring(commas[4]+1,commas[5])).equals("AM")||time2==12)
         am2=true;
      else
         am2=false;
      speed1=Integer.parseInt(str.substring(commas[5]+1,commas[6]));
      speed2=Integer.parseInt(str.substring(commas[6]+1));

      if(!am1)
         time1=(time1+12)%24;
      if(!am2)
         time2=(time2+12)%24;
      //--------------set up cities and distances----------
      cities= new String[] {"A","B","C","D","E","F","G","H","J","K"};
      miles=new int[] {0,450,590,715,1080,1330,1490,1870,2105,2425};
   }
   
   public int howFar()//calculates distance between cities
   {
      int spot1=-1;
      int spot2=-1; 
      for(int i=0;i<cities.length;i++)
      {
         if(pos1.equals(cities[i]))
            spot1=i;
         if(pos2.equals(cities[i]))
            spot2=i;
      }
      if((miles[spot1]-miles[spot2])>(miles[spot2]-miles[spot1]))
         return miles[spot1]-miles[spot2];
      return miles[spot2]-miles[spot1];
   }

   public void meetingTime()
   {
      int rate=speed1+speed2;
      int trav=0;
      int use=0;
      if(time1>time2)
      {
         if(time1-time2>12)
         {
            trav=((Math.abs(time1-time2-24))*(speed1));
            use=Math.abs(time1-time2-24);
         }
         else
         {
            trav=(time1-time2)*(speed2);
            use=time1-time2;
         }
      }
      else if(time1<time2)
      {
         if(time2-time1>12)
         {
            trav=((Math.abs(time2-time1-24))*(speed2));
            use=Math.abs(time2-time1-24);
         }
         else
         {
            trav=(time2-time1)*(speed1);
            use=time2-time1;
         }   
      }
      int hour=((howFar()-trav)/rate)+use;
      System.out.println(hour);
      String mins=""+((((((double)howFar()-trav)/rate)+use)-hour)*60);
      double hold=Double.parseDouble(mins);
      if(hold>=10)
      {
         if(Integer.parseInt(mins.substring(3,4))>=5)
            mins=""+(Integer.parseInt(mins.substring(0,2))+1);
         else
            mins=mins.substring(0,2);
      }
      else
      {
         if(Integer.parseInt(mins.substring(2,3))>=5)
            mins="0"+(Integer.parseInt(mins.substring(0,1))+1);
         else
            mins="0"+mins.substring(0,1);
      }
      System.out.println(""+hour+":"+mins);  
   }
   
   public static void main(String[]args)
   {
      /*ACSLland land=new ACSLland("A,C,1,PM,2,PM,50,60");
      land.meetingTime();
      ACSLland land2=new ACSLland("A,D,9,AM,1,PM,50,60");
      land2.meetingTime();
      ACSLland land3=new ACSLland("B,E,5,PM,3,PM,50,60");
      land3.meetingTime();
      ACSLland land4=new ACSLland("C,F,11,PM,2,AM,50,60");
      land4.meetingTime();
      ACSLland land5=new ACSLland("E,K,10,AM,12,PM,65,55");
      land5.meetingTime();*/
      
      //ACSLland land1=new ACSLland("G,K,12,AM,10,PM,55,65");
      //land1.meetingTime();
      //ACSLland land2=new ACSLland("B,F,1,PM,10,AM,60,70");
      //land2.meetingTime();
      //ACSLland land3=new ACSLland("J,K,12,PM,11,AM,70,55");
      //land3.meetingTime();
      /*ACSLland land4=new ACSLland("A,F,9,AM,9,AM,50,60");
      land4.meetingTime();
      ACSLland land5=new ACSLland("A,C,9,AM,7,AM,50,60");
      land5.meetingTime();*/
   }
}
