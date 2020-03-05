import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.function.*;
import java.util.regex.*;
import java.util.stream.*;
import static java.util.stream.Collectors.joining;
import static java.util.stream.Collectors.toList;

class Result {

    /*
     * Complete the 'diagonalDifference' function below.
     *
     * The function is expected to return an INTEGER.
     * The function accepts 2D_INTEGER_ARRAY arr as parameter.
     */

    public static int diagonalDifference(List<List<Integer>> arr) 
    {
    // Write your code here
    //for top to bottom
    //for bottom to top
    int sum1 = 0;
    int sum2 = 0;
    //total  sum
    int ts = 0;
    //for loop for outer list
    for (int i = 0; i < arr.size() ; i++)
    {
        // for inner list
        for( int j = 0; j < arr.get(i).size() ; j++)
        {
            //i and j are same 00 11 22 33 
            if ( i == j)
            {
                //sum from left to right
                sum1 = arr.get(i).get(j) + sum1;
            }
            //i = get(i).size()-1
            if( i == (arr.get(i).size()-j))
            {
                //sum from right to left
                sum2 = arr.get(i).get(j) + sum2;
            }

            //modules in java y abs() method
            ts = Math.abs(sum1) - Math.abs(sum2);

        }
    }

    //return to calling function
            return ts;
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int n = Integer.parseInt(bufferedReader.readLine().trim());

        List<List<Integer>> arr = new ArrayList<>();

        IntStream.range(0, n).forEach(i -> {
            try {
                arr.add(
                    Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
                        .map(Integer::parseInt)
                        .collect(toList())
                );
            } catch (IOException ex) {
                throw new RuntimeException(ex);
            }
        });

        int result = Result.diagonalDifference(arr);

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}
