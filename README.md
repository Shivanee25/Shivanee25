
import java.util.Scanner;

public class avilable 
{
	
	int slot2[]=new int[5];
	int slot[]= {2,3,2,3,2};
	String str2[]={"b","cb","c","b",""};//new String[5];
	String str3[]= {"xxxx","vvvvzzzz","ssss","cccc",""};
	
	public void test1(int no,int k) 
	{
		int i;
		char ch1[]=str3[no-1].toCharArray();
		if(k==0) 
		{
			for(i=0;i<4;i++)
			ch1[i]=' ';
		}
		
		if(k==1) 
		{
			for(i=4;i<8;i++)
			ch1[i]=' ';
		}
		
		if(k==2) 
		{
			for(i=8;i<12;i++)
			ch1[i]=' ';
		}
		String s1=new String(ch1);
		str3[no-1]=s1.replaceAll("    ", "");
	}
	
	public void test(int no,String num) 
	{
		String num1="";
		int k=-1;
		num1=str2[no-1];
		char ch[]=num1.toCharArray();
		char ch1[]=num.toCharArray();
		for(int i=0;i<ch.length;i++) 
		{
			if(ch[i]==ch1[0])
				k=i;
		}
		str2[no-1]=num1.replaceAll(num,"");
		if(k>=0)
			test1(no,k);
	}

	
	public void delete1(int v,int no)
	{
		String num="";
		int flag=0;		
		
		if(v==1) 
		{
			num="s";
			test(no,num);
		}
		
		else if(v==2)
		{
			num="c";
			test(no,num);
		}
	
		else if(v==3)
		{
			num="b";
			test(no,num);
		}
		
		else if(v==4)
			run2(slot2,str2);
		
		else
		{
			System.out.println("invalid");
		}
		
	}
	
	public void update1(int v,int no) 
	{
		String num="";
		int flag=0;
		Scanner sc=new Scanner(System.in);
		if(v==1 && slot2[no-1]==3) 
		{
			num="s";
			str2[no-1]=num;
		}
		else if(v==2 && slot2[no-1]>=2)
		{
			num="c";
			str2[no-1]=str2[no-1]+num;
		}
	
		else if(v==3 && slot2[no-1]>=1)
		{
			num="b";
			str2[no-1]=str2[no-1]+num;
		}
		else if(v==4)
			run2(slot2,str2);
		
		else
		{
			System.out.println("no space");
			flag=1;
		}
		
		if(flag == 0) 
		{
			System.out.println("########## Enter the vehicle number ##########");
			String vn=sc.next();
			str3[no-1]=str3[no-1]+vn.substring(0, 4);
		}
//		slot2[no-1]=slot2[no-1]-num;
	}
	
	int[] convert1(String str1[]) 
	{
		int slot1[]=new int[5];
		for(int i=0;i<5;i++) 
		{
			if((str1[i].length())==1) 
			{
				if(str1[i].equalsIgnoreCase("b"))
					slot1[i]=1;

				if(str1[i].equalsIgnoreCase("c"))
					slot1[i]=2;

				if(str1[i].equalsIgnoreCase("s"))
					slot1[i]=3;

			}
			
			if((str1[i].length())==2) 
			{
				if(str1[i].equalsIgnoreCase("cb") || str1[i].equalsIgnoreCase("bc"))
					slot1[i]=3;
			}
			
			if((str1[i].length())==2) 
			{
				if(str1[i].equalsIgnoreCase("bb"))
					slot1[i]=2;
			}
			
			if((str1[i].length())==2) 
			{
				if(str1[i].equalsIgnoreCase("cc"))
					slot1[i]=3;
			}
			
			if((str1[i].length())==3) 
			{
				if(str1[i].equalsIgnoreCase("bbb"))
					slot1[i]=3;
			}
			
			if((str1[i].length())==0) 
			{
					slot1[i]=0;
			}
		}
		return slot1;
	}
	
	public void run1() 
	{
	//	String str1[]= {"b","cb","c","b",""};
		int slot1[]=convert1(str2);
		int sum=0;
		for(int i=0;i<5;i++) 
		{
			sum=slot[i]-slot1[i];
			slot2[i]=sum;
			
			//System.out.println("Available slot in slot no."+(i+1)+" is : "+slot2[i]);
		}
		run2(slot2,str2);
	}
	
	public void run2(int arr[],String str[]) 
	{
		String vc="",vc1="",vc2="",vc3="";
		System.out.println("########## Status ###########");
		for(int i=0;i<5;i++) 
		{
			if(slot[i]==2) 
				vc2="Car";
			else
				vc2="SUV";
			if(str2[i].length()==1) 
			{
				if(str2[i].equalsIgnoreCase("b")) 
				{
					vc="Bike";
				}
				
				if(str2[i].equalsIgnoreCase("c")) 
				{
					vc="Car";
				}
				
				if(str2[i].equalsIgnoreCase("s")) 
				{
					vc="SUV";
				}
			}
			
			if(str2[i].length()==2) 
			{
				if(str2[i].equalsIgnoreCase("bc")) 
				{
					vc="Bike";
					vc1="Car";
				}
				
				if(str2[i].equalsIgnoreCase("cb")) 
				{
					vc="Car";
					vc1="Bike";
				}
				
				if(str2[i].equalsIgnoreCase("bb")) 
				{
					vc="Bike";
					vc1="Bike";
				}
				
				if(str2[i].equalsIgnoreCase("cc")) 
				{
					vc="Car";
					vc1="Car";
				}
				
			}
			
			if(str2[i].length()==3) 
			{
				if(str2[i].equalsIgnoreCase("bbb")) 
				{
					vc="Bike";
					vc1="Bike";
					vc3="Bike";
				}
			}
			
			if(arr[i]==3)
			{
				System.out.println("Slot-"+(i+1)+" "+vc2+" Parking : Available for 1 Suv or 3 bike or 1 car and 1 bike");
				System.out.println("Empty");
			}
			
			if(arr[i]==2)
			{
				System.out.println("Slot-"+(i+1)+" "+vc2+" Parking : Available for 2 bike or 1 car");
				if(str2[i]=="")
					System.out.println("empty");
			}
			
			if(arr[i]==1)
			{
				System.out.println("Slot-"+(i+1)+" "+vc2+" Parking : Available for 1 bike");
			}
			
			if(arr[i]==0)
			{
				System.out.println("Slot-"+(i+1)+" "+vc2+" Parking : No Space");
			}
			
			if(str3[i].length()==4) 
			{
				System.out.print("Vehicle number is: \n");
				System.out.println(vc+" "+str3[i]);
			}
			
			if(str3[i].length()==8) 
			{
				System.out.print("Vehicle number is: \n");
				System.out.println(vc+" "+str3[i].subSequence(0,4));
				System.out.println(vc1+" "+str3[i].subSequence(4,8));
			}
			
			if(str3[i].length()==12)
			{
				System.out.print("Vehicle number is: \n");
				System.out.println(vc+" "+str3[i].subSequence(0,4));
				System.out.println(vc1+" "+str3[i].subSequence(4,8));
				System.out.println(vc1+" "+str3[i].subSequence(8,12));
			}
			System.out.println("");
			
		}
		run3();
	}
	
	public void run3() 
	{
		Scanner sc=new Scanner(System.in);
		System.out.println("########## Insert the Action ##############\n1.Park the Car\n2.Remove the Car");
		int l=sc.nextInt();
		System.out.println("########## Insert the Slot no ##############");
		int no=sc.nextInt();
		System.out.println("########## Select the Vehicle #############\n1.SUV\n2.Car\n3.Bike\n4.Exit");
		int v=sc.nextInt();
		if(l==1)
			update1(v, no);
		else
			delete1(v, no);
		
		if(v<4)
			run1();
	}
	
	public static void main(String args[]) 
	{
		System.out.println("Shivanee");
		avilable a=new avilable();
		a.run1();
	}
}
