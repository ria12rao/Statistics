# Statistics
import java.util.Arrays;
import java.util.Scanner;



public class Statistics {
	public static void main(String[] args) {
		Scanner input = new Scanner(System.in);

		System.out.println("Welcome to Statistics!\n" + "This program will calculate the average, median, \n" +
				"mode, and most of any number of (double) values!\n");

		System.out.println("How many values will you be entering?");
		int length = input.nextInt(); 
		double[] numbers = new double[length]; 

		double values = 0; 
		for (int i = 0; i < length; i++) { 
			System.out.println("Please enter value #" + (i + 1) + ":"); 
			values = input.nextInt(); 
			numbers[i] = values; 

		}
		System.out.println("Values chosen");
		System.out.println(Arrays.toString(numbers));
		System.out.println("Average: " + average(numbers));
		System.out.println("Median: " + median(numbers));
		System.out.println("Most: " + Arrays.toString(most(numbers)));
		System.out.println("Mode: " + Arrays.toString(mode(numbers)));

	}



	public static double average(double[] values)
	{
		double sum = 0;					
		for (double value : values) {  
			sum += value;			  
		}
		return sum / values.length;	
								   
	}

	public static double median(double[] values)
	{
		Arrays.sort(values); 
		double median; 

		int length = values.length; 
		int middleNum1 = length / 2 - 1; 
		int middleNum2 = length / 2;

		if (values.length % 2 == 1) 
			median = ((double)values[(int) ((values.length / 2) + .5)]); 
		else
			median = ((double)values[(middleNum1)] + values[middleNum2]) / 2;

		return median;
	}

	public static double[] mode(double[] values)
	{
		int[] counts = new int[values.length];
		for (int i = 0; i < values.length; i++) { 
			counts[i] = ArrayHelper.count(values, values[i]);
		}

		int maxCount = 0; //this finds the max count value
		for (int count : counts) {
			if (count > maxCount) {
				maxCount = count;
			}
		}

		int numberOfModes = 0;
		for (int count : counts) {
			if (count == maxCount) {
				numberOfModes++;
			}
		}

		numberOfModes /= maxCount;
		double[] mode = new double[numberOfModes];
		int index = 0;

		for (int i = 0; i < counts.length; i++) {
			if (counts[i] == maxCount) {
				if (index < numberOfModes && !ArrayHelper.contains(mode, values[i])) {
					mode[index] = values[i];
					index++;
				}
			}
		}

		return mode;
	}

	private static boolean contains(double[] mode, double value) {
		return false;
	}

	public static double[] most(double[] values) {
		double average = average(values); 
										 
		int countNum = 0; 

		for(double value : values) { 
			if (value > average) {  
				countNum++;        
			}
		}
		double[] most = new double[countNum]; 
										     
		int index = 0; 

		for(double value : values) {
			if (value > average) {
				most[index] = value; 
				index++;			
			}
		}
		return most;

	}

	public static double[] sort(double[] values)
	{
		double[] temp = values.clone();
		Arrays.sort(temp);
		return temp;

	}

	}


