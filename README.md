# hello-world
/*
This program checks if the date entered by a user is a valid date and prints it in
the following format.
Input: 12/15/2016
Output: Thursday, 15th December 2016
*/
package dayMonthYear;
import java.util.Scanner;

public class DayMonths {
	public static final int DAYS_IN_WEEK = 7;
	public static final int JANUARY=1;
	public static final int FEBRUARY= 2;
    
	public static void main(String[] args) {
		int day =-1;
		int month =-1;
		int year =-1;
		boolean valid=true;
		Scanner input = new Scanner(System.in);
		input.useDelimiter("/|\n|\r\n|\\s+");
		if(input.hasNextInt())
		{
			day = input.nextInt();
			if(input.hasNextInt())
			{
				month = input.nextInt();
				if(input.hasNextInt())
				{
					year= input.nextInt();
					
				}
				else valid = false;
			}
			else valid = false;
		}
		else valid = false;
		
		input.close();
		if(isValidDate(year,month,day) && valid)
		{
			System.out.print(dayOfTheWeek(day,month,year) + ", " + day + numberEnding(day) + " " + monthName(month) + " " + year);
		}
		else System.out.print("Not a valid date");
	}

	public static boolean isValidDate(int year, int month, int day)
	{
		boolean isValid = false;
		if(day>0 && day<=daysInMonth(month,year) && month>0 && month<=12)
		{
			isValid = true;
		}
		return isValid;
	}
	public static int daysInMonth(int month, int year)
	{
		int days=0;
		switch(month)
		{
		case 2: if(isLeapYear(year))
				days = 29;
				else days = 28;
				break;
		case 1: days = 31;	
		case 3: days = 31;
		case 5: 
		case 7:
		case 8:
		case 10:
		case 12: days = 31;
			     break;
		case 4: 
		case 6: 
		case 9:
		case 11: days = 30;
				 break;
				
		}
		return days;
	}
	public static boolean isLeapYear(int year)
	{
		boolean leapYear = false;
		if((year%400==0) ||((year%4==0)&& (year%100!=0)))
		{
			leapYear= true;
		}
		return leapYear;
	}
	public static String numberEnding(int day)
    {
    	String endFormat="";
    	int lastDigit=-1;
    	
    	if(day>=10&& day<=19)
    	{
    		endFormat="th";
    	}
    	
    	else 
    	{
    		lastDigit = day%10;
    		
    		if(lastDigit==3)
    		{
    			endFormat="rd";
    		}
    		else if(lastDigit==2)
    		{
    			endFormat="nd";
    		}
    		else if(lastDigit==1)
    		{
    			endFormat="st";
    		}
    		else endFormat="th";
    	}
    	return endFormat;
    }
	
    public static String monthName(int month)
    {
    	String[] monthName = {"January","February", "March","April","May","June","July","August",		
    						"September","October","November","December"};
    	return monthName[month-1];
    }
    
    public static String dayOfTheWeek(int day, int month, int year)
    {
    	String[] dayName={"Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"};
    	int dayOfWeek=0;
    	int y=0;
    	if(month == JANUARY || month== FEBRUARY)
    	{
    		year=year-1;
    	}
    	if(year<10)
    	{
    		y = year;
    	}
    	else y=year%100;
    	
    	/*int copyYear= year;
    	/*while(copyYear/100!=0)
    	{
    		copyYear=copyYear/10;
    	}
    	int c=copyYear;*/
    	
    	int c=year/100;    // at first I thought we are supposed to get the first two digits of the year no matter how many
    					   // digits the year had, but after testing some more, it seems that c should be simply year/100
    	                  // in order to get the expected result. Although there are no online calendars to check for
    	                  // year<1000 or year>9999
    	
    	dayOfWeek =  day +(int)( Math.floor(2.6 * (double)(((month + 9) % 12) + 1) - 0.2) 
    					+ y + Math.floor(y/4) + Math.floor(c/4) - 2*c) ;
    	
 
    
    	while(dayOfWeek<0)
    	{
    		dayOfWeek= dayOfWeek + DAYS_IN_WEEK;
    		
    	}
    	dayOfWeek = dayOfWeek % DAYS_IN_WEEK;
   	    
    	return dayName[dayOfWeek];
    	
    }
   
}
