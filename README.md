# Binary-Search-4

## Problem1 Intersection of Two Arrays II

```Java
// Time Complexity : O(m+n)
// Space Complexity : O(m), m -> elements of smaller array as we are adding those elements in the hashmap
// Did this code successfully run on Leetcode : yes
// Any problem you faced while coding this : no

class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        //null
        if(nums1 == null || nums2 == null)
            return new int[0];

        //hashmap approach
        //making sure nums2 is smaller everytime
        if(nums1.length < nums2.length){
            return intersect(nums2, nums1);
        }

        HashMap<Integer, Integer> map = new HashMap<>();
        int m = nums1.length;
        int n = nums2.length;

        //putting elements of nums2 in hashmap with total number of occurence of each elemenrt
        for(int num : nums2){
            map.put(num, map.getOrDefault(num,0) +1);
        }

        List<Integer> li = new ArrayList<>();
        for(int num : nums1){
            if(map.containsKey(num)){
                li.add(num);
                map.put(num, map.get(num)-1);
                map.remove(num,0);
            }
        }

        int[] result = new int[li.size()];
        for(int i=0;i<result.length;i++){
            result[i] = li.get(i);
        }

        return result;
    }
}
```

## Problem2 Median of Two Sorted Arrays

```Java
// Time Complexity : O(log n)
// Space Complexity : O(1)
// Did this code successfully run on Leetcode : yes
// Any problem you faced while coding this : no

class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        if (nums1.length == 0 && nums2.length == 0) {
            return 0.0;
        }
        int n1 = nums1.length;
        int n2 = nums2.length;

        if (n1 > n2) {
            return findMedianSortedArrays(nums2, nums1);
        }

        int low = 0;
        int high = n1;

        while (low <= high) {
            int partX = low + (high - low) / 2;
            int partY = (n1 + n2) / 2 - partX;

            double l1 = partX == 0 ? Integer.MIN_VALUE : nums1[partX - 1];
            double r1 = partX == n1 ? Integer.MAX_VALUE : nums1[partX];
            double l2 = partY == 0 ? Integer.MIN_VALUE : nums2[partY - 1];
            double r2 = partX == n2 ? Integer.MAX_VALUE : nums2[partY];

            if (l2 <= r1 && l1 <= r2) {
                //correct partition
                if ((n1 + n2) % 2 == 0) { //check odd or even
                    return (Math.max(l1, l2) + Math.min(r1, r2)) / 2;
                } else {
                    return Math.min(r1, r2);
                }
            }
            //if not correct partition
            else if (l1 > r2) {
                high = partX - 1;
            } else {
                low = partX + 1;
            }
        }
        return 8.99;
    }
}
```


