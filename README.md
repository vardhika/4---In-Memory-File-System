4---In-Memory-File-System
=========================
package com.code.test;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.nio.channels.FileChannel;

public class Test1 {
	static File fileIs = new File(Constants.file_path);
	static File destFile = new File(Constants.dest_file_path);
	static File folder = new File(Constants.folderPath);

	/**
	 * @param args
	 * @throws Exception 
	 */
	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub

		//1.Creating folder
		createFolder();

		//Creating a file in folder
		CreateSrcfile();
		//search for a file 
	
	}	 	
	private static void CreateSrcfile() throws Exception {
		// TODO Auto-generated method stub

		if(!fileIs.exists()){
			try {
				fileIs.createNewFile();
				System.out.println("File created sucessfully");
				WriteContentToFile(fileIs);
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}

		} else
			if((fileIs.exists())){
				fileIs.delete();
				//System.out.println("file deleted");
				fileIs.createNewFile();
				System.out.println("Case 2::"+"File created sucessfully");
				WriteContentToFile(fileIs);
			}



	}
	private static void createFolder() {
		// TODO Auto-generated method stub


		if(!folder.exists()){
			folder.mkdir();
			System.out.println("Case 1::"+"Folder creation sucessful");
		}else
		
				if((folder.exists())){
					folder.delete();
					//System.out.println("folder deleted");
					try {
						folder.createNewFile();
					} catch (IOException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}
					System.out.println("Case 1::"+"folder created sucessfully");
					
				}


	}
	//Writing to File
	private static void WriteContentToFile(File folder) throws Exception {
		// TODO Auto-generated method stub

		BufferedWriter output = new BufferedWriter(new FileWriter(folder));
		output.write("Testing code");
		output.close();
        
		copyFile(fileIs,destFile);

	}


	public static void copyFile(File sourceFile, File destFile) throws IOException { 

		if(!destFile.exists()) {    	

			destFile.createNewFile();
			System.out.println("File2 Created ");
		}
		else
			System.out.println("Case 4::"+"Copying file");

		FileChannel source = null;
		FileChannel destination = null;

		try {
			source = new FileInputStream(sourceFile).getChannel();
			destination = new FileOutputStream(destFile).getChannel();
			destination.transferFrom(source, 0, source.size());
		}
		finally {
			if(source != null) {
				source.close();
			}
			if(destination != null) {
				destination.close();
			}
		}


		//Reading content of file2
		readFromfile(destFile);
		// to get Content of folder
		contentfromfolder(Constants.folderPath);
	}

	private static String contentfromfolder(String folderpath) {
		// TODO Auto-generated method stub

		File folder = new File(folderpath);
		File[] listOfFiles = folder.listFiles();

		for (int i = 0; i < listOfFiles.length; i++) {
			if (listOfFiles[i].isFile()) {
				System.out.println("File " + listOfFiles[i].getName());
			} else if (listOfFiles[i].isDirectory()) {
				System.out.println("Directory " + listOfFiles[i].getName());
			}
		}
		
		String ret = null;
		
		for (File file : listOfFiles)
		{
		  if (!file.isDirectory())
		  {
		    ret = file.getPath();
		    System.out.println("Path for searching files is "+ret);
		    break;
		  }
		}

		return ret;

	}



	static void readFromfile(File destFile2) throws IOException{

		try(BufferedReader br = new BufferedReader(new FileReader(destFile2))) {
			StringBuilder sb = new StringBuilder();
			String line = br.readLine();

			while (line != null) {
				sb.append(line);
				sb.append(System.lineSeparator());
				line = br.readLine();
			}
			String contentfrmfile2 = sb.toString();
			System.out.println(""+contentfrmfile2);
		}

package com.code.test;

import java.io.File;

public class Constants {
	
	public static final String folderPath = "c://Folder";
	public static final String file_path = Constants.folderPath+File.separator+"File1.txt";
	public static final String src_file_path = Constants.folderPath+File.separator+"Src_file.txt";
	public static final String dest_file_path = Constants.folderPath+File.separator+"File2.txt";
	
	
	
	
	
	

}



	}

}






