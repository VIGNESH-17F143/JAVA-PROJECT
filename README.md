package vignesh_project;
import java.io.BufferedReader;
import java.io.File;  
import java.io.FileWriter;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.Scanner;
import java.util.*;
public class sam{

private static BufferedReader br;

public static void main(String[] args) throws ArrayIndexOutOfBoundsException, IOException{
long start = System.nanoTime();
TreeSet<String> al=new TreeSet<String>();
List<String> list=new ArrayList<>();
String line = "";  
String splitBy = ",";
int word_replace=0;
Hashtable<String, String> hashTable = new Hashtable<String, String>();
Hashtable<String, Integer> hash = new Hashtable<String, Integer>();
try {
     File myObj1 = new File("find_words.txt");
     Scanner myReader1 = new Scanner(myObj1);
     while (myReader1.hasNextLine()) {
       String data = myReader1.nextLine();
       al.add(data);
       hash.put(data, 0);
     }
     myReader1.close();
     br = new BufferedReader(new FileReader("french_dictionary.csv"));  
while ((line = br.readLine()) != null)    
{  
String[] employee = line.split(splitBy);    
hashTable.put(employee[0], employee[1]);

}
File myObj3 = new File("t8.shakespeare.txt");
     Scanner myReader3 = new Scanner(myObj3);
     while (myReader3.hasNext()) {
       String data = myReader3.next();
        String temp=data.replaceAll("[',.]*", "");
       if(al.contains(temp)){
        data=data.replaceFirst(temp,hashTable.get(temp));
        hash.put(temp,hash.get(temp)+1);
        word_replace+=1;
        list.add(data);
       
       }
     }
    myReader3.close();
    FileWriter myWriter = new FileWriter("filename.txt");
    for(String x:list){
    myWriter.write(x+" ");
    }
     myWriter.close();
   
   }
catch (FileNotFoundException e) {
     System.out.println("An error occurred.");

   }

long beforeUsedMem=Runtime.getRuntime().totalMemory()-Runtime.getRuntime().freeMemory();
   
long end = System.nanoTime();
System.out.println("Unique list of words that was replaced with French words from the dictionary");
System.out.println(al.toString());
System.out.println("Number of times a word was replace");
System.out.println(word_replace);
System.out.println("Frequency of each word replaced");
System.out.println(hash);
System.out.println("Time taken to process");
System.out.println("Time taken(s): " + (end - start)/1.0e9);
System.out.println("Memory taken to process");
System.out.println(beforeUsedMem+" In bytes");


}

}
