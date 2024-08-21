Longest Consecutive subsequence in Java
Here, in this page we will discuss the program to find the longest consecutive subsequence in C++ . We are Given with an array of integers, we need to find the length of the longest sub-sequence such that elements in the sub-sequence are consecutive integers, the consecutive numbers can be in any order.

Longest Consecutive subsequence
Method Discussed :
Method 1 : Brute Force
Method 2 : Using Hash-map
Method 3 : Using Priority Queue.
Method 1 (Brute force Approach) :
First sort the given input array.
Remove the multiple occurrences of elements, run a loop and keep a count and max (both initially zero).
Run a loop from 0 to N and if the current element is not equal to the previous (element+1) then set the count to 1 else increase the count.
Update max with a maximum of count and max.
Time and Space Complexity
Time - complexity : O(n log n) Space - complexity : O(1)
Java Program to Find longest consecutive subsequence
Run
import java.io.*;
import java.util.*;
public
class Main {
    static int findLongestConseqSubseq(int arr[], int n)
    {
 
        // Sort the array
        Arrays.sort(arr);
 
        int ans = 0, count = 0;
       
        ArrayList v = new ArrayList();
        v.add(10);
       
        // Insert repeated elements
        // only once in the vector
        for (int i = 1; i < n; i++)
        {
            if (arr[i] != arr[i - 1])
                v.add(arr[i]);
        }
    
 
        // Find the maximum length
        // by traversing the array
        for (int i = 0; i < v.size(); i++)
        {
 
            // Check if the current element is
            // equal to previous element +1
            if (i > 0 && v.get(i) == v.get(i - 1))
                count++;
            else
                count = 1;
 
            // Update the maximum
            ans = Math.max(ans, count);
        }
        return ans;
    }
 
    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 9, 3, 10, 4, 20, 2 };
        int n = arr.length;
 
        System.out.println(
            "Length of the Longest "
            + "contiguous subsequence is "
            + findLongestConseqSubseq(arr, n));
    }
}
Output :
Length of the Longest contiguous subsequence is 3						
Related Pages
Given an array which consists of only 0, 1 and 2

Move all the negative elements to one side of the array

Find the Union and Intersection of the two sorted arrays

Find Largest sum contiguous Subarray

Minimize the maximum difference between heights 

Method 2 :
First we will create a hash-map.
Now, iterate over the array for every i-th element check if this element is the starting point of a subsequence. To check this, simply look for arr[i] – 1 in the hash, if not found, then this is the first element a subsequence.
If this element is the first element, then count the number of elements in the consecutive starting with this element. Iterate from arr[i] + 1 till the last element that can be found.
If the count is more than the previous longest subsequence found, then update this.
Time and Space Complexity
Time - complexity : O(n) Space - complexity : O(n)
Run
import java.io.*;
import java.util.*;
class Main {
    // consecutive subsequence
    static int findLongestConseqSubseq(int arr[], int n)
    {

        HashSet S = new HashSet();
        int ans = 0;


        // Hash all the array elements
        for (int i = 0; i < n; ++i)
            S.add(arr[i]);

        // check each possible sequence from the start
        // then update optimal length
        for (int i = 0; i < n; ++i)
        {
            // if current element is the starting
            // element of a sequence
            if (!S.contains(arr[i] - 1))
            {
                // Then check for next elements
                // in the sequence
                int j = arr[i];
                while (S.contains(j))
                    j++;

                // update  optimal length if this
                // length is more
                if (ans < j - arr[i])
                    ans = j - arr[i];
            }
        }
        return ans;
    }


    // Driver Code
    public static void main(String args[])

    {

        int arr[] = { 1, 9, 3, 10, 4, 20, 2 };
        int n = arr.length;
        System.out.println(
            "Length of the Longest consecutive subsequence is "
            + findLongestConseqSubseq(arr, n));
    }
}
Output :
Length of the Longest consecutive subsequence is 4
Method 3 :
In this method we will use priority queue.

Create a Priority Queue to store the element
Store the first element in a variable.
Remove it from the Priority Queue.
Check the difference between this removed first element and the new peek element
If the difference is equal to 1 increase count by 1 and repeats step 2 and step 3
If the difference is greater than 1 set counter to 1 and repeat step 2 and step 3
if the difference is equal to 0 repeat step 2 and 3
if counter greater than the previous maximum then store counter to maximum
Continue step 4 to 7 until we reach the end of the Priority Queue
Return the maximum value
 

Time and Space Complexity
Time - complexity : O(n logn) Space - complexity : O(n)
Run
import java.io.*;
import java.util.PriorityQueue;
class Main {
    static int findLongestConseqSubseq(int arr[], int N)
    {


        PriorityQueue<Integer> pq
            = new PriorityQueue();
        for (int i = 0; i < N; i++)
        {
            // adding element from
            // array to PriorityQueue
            pq.add(arr[i]);
        }
         
        // Storing the first element
        // of the Priority Queue
        // This first element is also
        // the smallest element
        int prev = pq.poll();
         
        // Taking a counter variable with value 1
        int c = 1;
         
        // Storing value of max as 1
        // as there will always be
        // one element
        int max = 1;


        for (int i = 1; i < N; i++)
        {
            // check if current peek
            // element minus previous
            // element is greater then
            // 1 This is done because
            // if it's greater than 1
            // then the sequence
            // doesn't start or is broken here
            if (pq.peek() - prev > 1)
            {
                // Store the value of counter to 1
                // As new sequence may begin
                c = 1;
                 
                // Update the previous position with the
                // current peek And remove it
                prev = pq.poll();
            }
             
            // Check if the previous
            //  element and peek are same
            else if (pq.peek() - prev == 0)
            {
                // Update the previous position with the
                // current peek And remove it
                prev = pq.poll();
            }
            // if the difference
            // between previous element and peek is 1
            else
            {
                // Update the counter
                // These are consecutive elements
                c++;
                  
                // Update the previous position
                //  with the current peek And remove it
                prev = pq.poll();
            }


            // Check if current longest
            // subsequence is the greatest
            if (max < c)
            {
                // Store the current subsequence count as
                // max
                max = c;
            }
        


    }
            return max;

    
}

     
    // Driver Code
    public static void main(String args[])
        throws IOException
    {
        int arr[] = { 1, 9, 3, 10, 4, 20, 2 };
        int n = arr.length;
        System.out.println(
            "Length of the Longest consecutive subsequence is "
            + findLongestConseqSubseq(arr, n));
    }
    
}
Output :
Length of the Longest consecutive subsequence is 4
