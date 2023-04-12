public static String longestPalindromicSubstring(String s) {
    int n = s.length();
    boolean[][] dp = new boolean[n][n];
    String ans = "";
    
    // Every string with length 1 is a palindrome
    for (int i = 0; i < n; i++) {
        dp[i][i] = true; // Marking single character strings as palindromes
        ans = s.substring(i, i+1); // Store the current character in ans
    }
    
    // Check for palindromes of length 2
    for (int i = 0; i < n-1; i++) {
        if (s.charAt(i) == s.charAt(i+1)) { // Checking if consecutive characters are same
            dp[i][i+1] = true; // Marking the 2 character substring as palindrome
            ans = s.substring(i, i+2); // Store the current 2 character substring in ans
        }
    }
    
    // Check for palindromes of length >= 3
    for (int len = 3; len <= n; len++) { // Iterating over all possible substring lengths
        for (int i = 0; i < n-len+1; i++) { // Iterating over all possible starting indices
            int j = i+len-1; // Calculating the ending index of the current substring
            if (s.charAt(i) == s.charAt(j) && dp[i+1][j-1]) { // Checking if the ends are same and the substring inside is a palindrome
                dp[i][j] = true; // Marking the current substring as palindrome
                ans = s.substring(i, j+1); // Store the current substring in ans
            }
        }
    }
    
    return ans; // Return the longest palindromic substring
}
