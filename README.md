# dsa-using-java

## Q: Majority Element
Given an array ‘A’ of ‘N’ integers, find the majority element of the array. A majority element in an array ‘A’ of size ‘N’ is an element that appears more than floor(N / 2) times.

Note: The floor function returns the largest possible integer value which is equal to the value or smaller than that. It is guaranteed that there is always a majority element in the array ‘A’.

Example:

<pre><code>Input: ‘N’ = 9 ‘A’ = [2, 2, 1, 3, 1, 1, 3, 1, 1]

Output: 1

Explanation: The frequency of ‘1’ is 5, which is greater than floor(N / 2), 
hence ‘1’ is the majority element.
</code></pre>

https://www.codingninjas.com/studio/problems/majority-element_6783241

```java
import java.util.Map;
import java.util.HashMap;

public class Solution {
    public static int majorityElement(int []v) {
        // Write your code here
        int f = (int) Math.floor(v.length/2);

        HashMap<Integer, Integer> map = new HashMap();

        for(int i = 0; i < v.length; i++) {
            if(map.containsKey(v[i])){
                int count = map.get(v[i]);
                map.put(v[i], count + 1);
            } else {
                map.put(v[i], 1);
            }
        }

        //System.out.println(f);

        int ans = Integer.MIN_VALUE;

        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            int key = entry.getKey();
            int value = entry.getValue();
            // System.out.println("Key=" + key + ", Value=" + value);
             if(value > f && ans < key ) {
                ans = key;
            } 
        }

        return ans;
    }
}
```

Another approach is to use Moore's Voting algorithm

```java
public class Solution {
    public static int majorityElement(int []v) {
        // Write your code here

        int ans = v[0];
        int f = 1;
        
        for(int i = 1; i < v.length; i++) {
            if(v[i] == ans) {
                f += 1;
            } else {
                f -= 1;
            }

            if(f == 0) {
                ans = v[i];
                f = 1;
            }
        }

        return ans;
    }
}
```

## Q: Sort 0s,1s and 2s.

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

 

Example 1:

Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
Example 2:

Input: nums = [2,0,1]
Output: [0,1,2]

```java
class Solution {
    public void sortColors(int[] nums) {
        int low = 0;
        int mid = 0;
        int high = nums.length - 1;

        while(mid <= high) {
            if(nums[mid] == 0) {
                int temp = nums[mid];
                nums[mid] = nums[low];
                nums[low] = temp;

                low++;
                mid++;
            } else if(nums[mid] ==1) {
                mid++;
            } else if(nums[mid] == 2) {
                int temp = nums[mid];
                nums[mid] = nums[high];
                nums[high] = temp;
                high--;
            }
        }
    }
}
```