# Minimum-String-Length-After-Removing-Substrings

You are given a string s consisting only of uppercase English letters.

You can apply some operations to this string where, in one operation, you can remove any occurrence of one of the substrings "AB" or "CD" from s.

Return the minimum possible length of the resulting string that you can obtain.

Note that the string concatenates after removing the substring and could produce new "AB" or "CD" substrings.

 

Example 1:

Input: s = "ABFCACDB"
Output: 2
Explanation: We can do the following operations:
- Remove the substring "ABFCACDB", so s = "FCACDB".
- Remove the substring "FCACDB", so s = "FCAB".
- Remove the substring "FCAB", so s = "FC".
So the resulting length of the string is 2.
It can be shown that it is the minimum length that we can obtain.
Example 2:

Input: s = "ACBBD"
Output: 5
Explanation: We cannot do any operations on the string so the length remains the same.
 

Constraints:

1 <= s.length <= 100
s consists only of uppercase English letters.

# SOLUTION

Intuition
We aim to either remove characters that match specific patterns or retain them if no match is found.

This process is efficiently handled using a stack, where we pop characters when a pattern is detected and append them when no pattern is formed.

Approach
Reading the string from left to right, we evaluate each character, deciding whether to add it to the stack or remove a prior character.

if: If the stack isn’t empty, we compare the current character with the one at the top of the stack.
else if: If they form a pattern like "AB" or "CD," we pop the stack and skip pushing the current character, effectively removing both.
else: If no pattern is formed, we simply push the current character onto the stack.
At the end of this process, the characters left in the stack represent the shortest possible version of the string after all removable patterns have been eliminated.

Complexity
Time complexity: O(N)

Space complexity: O(N)

# JAVA CODE

class Solution {

    public int minLength(String s) {
    
        Stack<Character> stack = new Stack<>();
        

        for (int i = 0; i < s.length(); i++) {
        
            char cur_char = s.charAt(i);

            if (stack.isEmpty()) {
            
                stack.push(cur_char);
                
                continue;
                
            }
      
            if (cur_char == 'B' && stack.peek() == 'A') {
            
                stack.pop();
            }
            
            else if (cur_char == 'D' && stack.peek() == 'C') {
            
                stack.pop();
                
            }
            
            else {
            
                stack.push(cur_char);
            }
            
        }

        return stack.size();
    }
}
