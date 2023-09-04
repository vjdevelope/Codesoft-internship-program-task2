WordCounter;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.*;

	public class Task2 {
	    public static void main(String[] args) {
	        Scanner scanner = new Scanner(System.in);

	        System.out.println("Welcome to Word Counter!");

	        while (true) {
	            System.out.print("Enter '1' to input text or '2' to provide a file: ");
	            int choice = scanner.nextInt();
	            scanner.nextLine();

	            if (choice == 1) {
	                System.out.print("Enter the text: ");
	                String text = scanner.nextLine();
	                countWords(text);
	                break;
	            } else if (choice == 2) {
	                System.out.print("Enter the file path: ");
	                String filePath = scanner.nextLine();
	                String text = readFile(filePath);
	                if (text != null) {
	                    countWords(text);
	                    break;
	                }
	            } else {
	                System.out.println("Invalid choice. Please try again.");
	            }
	        }

	        scanner.close();
	    }

	    public static void countWords(String text) {
	        String[] words = text.split("[\\s.,;:!?()\\[\\]{}\"']+");
	        int totalCount = words.length;

	        Map<String, Integer> wordCountMap = new HashMap<>();
	        for (String word : words) {
	            word = word.toLowerCase();
	            if (!word.isEmpty()) {
	                wordCountMap.put(word, wordCountMap.getOrDefault(word, 0) + 1);
	            }
	        }

	        System.out.println("Total word count: " + totalCount);
	        System.out.println("Unique word count: " + wordCountMap.size());

	        // Uncomment the following code to display the frequency of each word
	        /*
	        System.out.println("\nWord Frequency:");
	        for (Map.Entry<String, Integer> entry : wordCountMap.entrySet()) {
	            System.out.println(entry.getKey() + ": " + entry.getValue());
	        }
	        */
	    }

	    public static String readFile(String filePath) {
	        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
	            StringBuilder stringBuilder = new StringBuilder();
	            String line;
	            while ((line = reader.readLine()) != null) {
	                stringBuilder.append(line).append(" ");
	            }
	            return stringBuilder.toString().trim();
	        } catch (IOException e) {
	            System.out.println("Error reading the file. Please check the file path and try again.");
	        }
	        return null;
	    }
	}
