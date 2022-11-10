package Url;

import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;

import org.json.simple.JSONArray;
import org.json.simple.JSONObject;
import org.json.simple.parser.JSONParser;
import org.json.simple.parser.ParseException;

public class WriteUrl {

	public static void main(String[] args) throws IOException, ParseException {
	    
		int count = 0;

		Scanner myObj = new Scanner(System.in);  // Create a Scanner object

		    boolean TRUE = true;
			while (TRUE) {
			    System.out.println("ENTER COMMAND:");
			    String urlname = myObj.nextLine();		    	
		   
		    switch (urlname) {
		    case "storeurl":
		        String storeurl = myObj.nextLine();
		        storeUrl(storeurl);
		      break;
		    case "get":
		    	   String counturl = myObj.nextLine();
			    	
			 		  JSONParser jsonP1 = new JSONParser();  
					  FileReader reader1 = new FileReader("urls.json");
					   //Read JSON File
					   Object obj1 = jsonP1.parse(reader1);
					   JSONArray urlList1 = (JSONArray) obj1;
				

					   urlList1.forEach(url2 -> {
						try {
							countGet((JSONObject)url2);
						} catch (IOException e) {
							// TODO Auto-generated catch block
							e.printStackTrace();
						}
					});

		      break;
		    case "count":
		    	   String countur2 = myObj.nextLine();
		    	
			 		  JSONParser jsonP2 = new JSONParser();  
					  FileReader reader2 = new FileReader("urls.json");
					   //Read JSON File
					   Object obj2 = jsonP2.parse(reader2);
					   JSONArray urlList2 = (JSONArray) obj2;
				

					   urlList2.forEach(url3 -> counts((JSONObject)url3));

		      break;
		    case "list":
		 		  JSONParser jsonP3 = new JSONParser();  
				  FileReader reader3 = new FileReader("urls.json");
				   Object obj = jsonP3.parse(reader3);
				   JSONArray urlList3 = (JSONArray) obj;
				   urlList3.forEach(url4 -> urlList((JSONObject)url4));
		      break;
		    case "exit":
		        System.out.println("EXITED");
		        System.exit(0);

		      break;

		  }

		   
		    }
				
		

	}

	 private static void storeUrl(String storeurl) throws IOException, ParseException {
	        JSONParser jsonParser1 = new JSONParser();
            Object obj = jsonParser1.parse(new FileReader("urls.json"));
            JSONArray jsonArray1 = (JSONArray)obj;


			JSONObject url= new JSONObject();
			url.put("id",1);
			url.put("url",storeurl);
			url.put("count", '0');
			
			JSONObject urlObj1=new JSONObject();
			urlObj1.put("key", url);	
			
            jsonArray1.add(urlObj1);

			
			FileWriter file=new FileWriter("urls.json",false);
			file.write(jsonArray1.toJSONString());
			file.flush();
           //file.close();

	 }
	 
	 
	 private static void countGet(JSONObject url2) throws IOException {
		  JSONObject urlObj2 = (JSONObject) url2.get("key");
		  String urlname = (String) urlObj2.get("url");
		  int id = Integer.parseInt(urlObj2.get("id").toString());
		  int count = Integer.parseInt(urlObj2.get("count").toString());
		
		  if(count!=0) {  
		  JSONObject url1= new JSONObject();
		  count++;
			url1.put("id",id);
			url1.put("url",urlname);
			url1.put("count", count);
			  JSONObject empObj1 = (JSONObject) url2.get("key");
			  
			  System.out.println("counted by 1: " + urlname);
			
		  
			 JSONObject urlObj=new JSONObject();
			urlObj.put("key", url1);	
		  	
			JSONArray urlList= new JSONArray();
			urlList.add(urlObj);
		  
			FileWriter file=new FileWriter("urls.json");
			file.write(urlList.toJSONString());
			file.flush();	
		  }
	
	 }
	 
	 public static void counts(JSONObject url3){
		  JSONObject urlObj3= (JSONObject) url3.get("key");

		    int count = Integer.parseInt(urlObj3.get("count").toString());

			  System.out.println("Count: " + count);
	
	 }
	 private static void urlList(JSONObject url4) {
		  JSONObject urlObj4 = (JSONObject) url4.get("key");
		  String url = (String) urlObj4.get("url");
		  int id = Integer.parseInt(urlObj4.get("id").toString());
		  int count = Integer.parseInt(urlObj4.get("count").toString());
		  System.out.println("Url: " + url);
		  System.out.println("id: " + id);
		  System.out.println("Count: " + count);
	 }
	
}
