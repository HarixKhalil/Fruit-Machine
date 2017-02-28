# Fruit-Machine
import java.io.BufferedReader;
import java.io.FileReader;
import java.util.*;
public class Main {
	//I used static and initialised the variables outside the methods because I need them in other methods
	static String word="";
	static int errorcheck = 0;
	static int errorcheck2 = 0;
	static int userchoice1 = 0;
    public static void main(String[] args) throws Exception 
    {//final
	userInput(); // this is calling the method 
	
      Scanner input = new Scanner(System.in);
      finch f = new finch();
     // String answer = " ";     
      int loop = 0;
     String[] characters = {"A", "B", "C", "D", "E", "F", "G", "H", "I",
    		   "J", "K", "L",
                               "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X",
                               "Y", "Z",
                             
                               "1", "2", "3", "4", "5", "6", "7", "8", "9", "0","."};
       
      String[] signs = {".-", "-...", "-.-.", "-..", ".", "..-.", "--.", "....", "..",
    		  
                             ".---", "-.-", ".-..", "--", "-.", "---", ".--.", "--.-", ".-.",
                             
                             "...", "-", "..-", "...-", ".--", "-..-", "-.--", "--..",
                             
                              
                             
                             ".----", "..---", "...--", "....-", ".....", "-....", "--...", 
                             "---..", "----.", "-----",".-.-.-"};
      while(loop == 0 && errorcheck2==0)
      {
        if(userchoice1==1){
        System.out.print("Please enter two  English words seperated by space: ");
        word = input.nextLine();}
        if(userchoice1==2){
        	FileReader read = new FileReader("myfile.txt");
        	BufferedReader br = new BufferedReader(read);
        	word=br.readLine();
        }
           int blanks=0;
  			for (int i=0;i<word.length();i++)
  			{
  				if(word.charAt(i)==' ')
  					blanks++;
  			}
  			if(blanks>1)
  			{
  				System.out.println("You entered more than two words,Please try again");
  				errorcheck=1;//error check if equals to 1 finch will not work
  				word="";
  			
  			
  			}
  			else if (blanks==0)
  			{
  				
  				System.out.println("You entered less than two words,Please try again");
  				errorcheck=1;
  				word="";
  				
  			}
  			else{
  				errorcheck=0;
  			}
if (word.contains(","))
				{
				String[] arr=word.split(" ");
				String word1 = arr[0];
				String word2 = arr[1];
				if (word1.contains(","))
					{
						word1=word1.replaceAll(",", "");
						StringBuffer buffer = new StringBuffer(word1);
						buffer.reverse();
						word1=buffer.toString();
					}
				if (word2.contains(","))
				{
					word2=word2.replaceAll(",", "");
					StringBuffer buffer = new StringBuffer(word2);
					buffer.reverse();
					word2=buffer.toString();
				}
				word=word1+" "+word2;
					
				}
			
              for (int A=0; A<word.length(); A++)
                  {char cha = word.charAt(A);
                  if ((Character.isLowerCase(cha)))
                	  {
                    System.out.println("Invalid  - word Must have all Upper Case characters-Input again.");
                    errorcheck=1;
                    word= " ";
                  }
          }
         
              StringBuilder sb = new StringBuilder();
              int spacecheck=0;
              for(int d = 0; d < word.length(); d++ )
              { 
                  for(int s = 0; s < characters.length; s++) 
                  { // SUBSTRING IS REMOVE BACK WORD
                      if(word.substring(d, (d+1)).equals(characters[s])){// WHAT IS IN CHARACTERS
                        	sb.append(signs[s]);
                        	if(spacecheck<1 && word.charAt(d+1)==' '){  // IT is use to PUT SPACE ALSO TO SHow
                        		sb.append(' ');
                        		spacecheck++;
                        	}
                      }
                  } 
              }
              String s = sb.toString();
              System.out.println(s);
              if(errorcheck==0){
            	  f.ledfinch(s);
              }
              
 
          loop++;
          System.out.println("Do you wanna convert again some word into morse code  (Yes or No): ");
          String UserAnswer = input.next();
          input.nextLine();
          while(!(UserAnswer.equalsIgnoreCase("Yes") || UserAnswer.equalsIgnoreCase("No")))
             {
                System.out.print("wrong answer, please input only 'Yes' or 'No'.");
                UserAnswer = input.next();
                userchoice1=0;
                errorcheck=0;
            }
          if(UserAnswer.equalsIgnoreCase("Yes"))
           { 
              loop = 0;
              userInput();
           }
          else
              {
                System.out.println("now the working of my program is end . Thanks alot");
                input.close();
              }
      }}
	public static void userInput(){
		Scanner choiceofuser = new Scanner(System.in);
		System.out.println(" Morse Code conversion program of Dawood");	
		do{
			System.out.println("\n1.please enter words From Keyboard \n2.please enter words From a File which is created");
			userchoice1=choiceofuser.nextInt();
			if((userchoice1==1) || (userchoice1==2)){
		System.out.println("you use valid");
		errorcheck2=0;
			}
		else
		{System.out.println("you did not use valid option");
		errorcheck2=1;
		}
		}while(!(errorcheck2==0));
	}
}
