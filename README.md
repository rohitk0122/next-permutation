# next-permutation
import java.util.Arrays;

public class Solution {
    public void nextPermutation(int[] nums) {
        int pivotIndex = nums.length - 2;

        // Find the first element from the right that is smaller than its right neighbor
        while (pivotIndex >= 0 && nums[pivotIndex] >= nums[pivotIndex + 1]) {
            pivotIndex--;
        }

        // If no such element exists, the array is in descending order, so reverse it
        if (pivotIndex == -1) {
            reverse(nums, 0, nums.length - 1);
            return;
        }

        // Find the first element from the right that is greater than the pivot
        int successorIndex = nums.length - 1;
        while (nums[successorIndex] <= nums[pivotIndex]) {
            successorIndex--;
        }

        // Swap pivot and successor
        int temp = nums[pivotIndex];
        nums[pivotIndex] = nums[successorIndex];
        nums[successorIndex] = temp;

        // Reverse the portion of the array to the right of the pivot
        reverse(nums, pivotIndex + 1, nums.length - 1);
    }

    private void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }

    public static void main(String[] args) {
        Solution solution = new Solution();

        int[] arr1 = {1, 2, 3};
        solution.nextPermutation(arr1);
        System.out.println(Arrays.toString(arr1)); // Output: [1, 3, 2]

        int[] arr2 = {2, 3, 1};
        solution.nextPermutation(arr2);
        System.out.println(Arrays.toString(arr2)); // Output: [3, 1, 2]

        int[] arr3 = {3, 2, 1};
        solution.nextPermutation(arr3);
        System.out.println(Arrays.toString(arr3)); // Output: [1, 2, 3]
    }
}
