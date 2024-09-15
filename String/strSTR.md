## [28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/)
Given two strings `needle` and `haystack`, return the `index` of the first occurrence of `needle` in `haystack`, or `-1` if needle is not part of haystack.

Example 1:
```
Input: haystack = "sadbutsad", needle = "sad"
Output: 0
```
Explanation: "sad" occurs at index 0 and 6.

The first occurrence is at index 0, so we return 0.

Example 2:
```
Input: haystack = "leetcode", needle = "leeto"
Output: -1
```
Explanation: "leeto" did not occur in "leetcode", so we return -1.

**Solution:**
<details>
  <summary>Brute Force</summary>
  
  **Approach:**
  traverse all the possible starting points of haystack (from 0 to haystack.length() - needle.length()) and see if the following characters in haystack match those of needle.
  
```cpp
class Solution {
public:
    int strStr(string haystack, string needle) {
        int n = haystack.size(), m = needle.size();// leetcode    leeto
        for (int i = 0; i <= n - m; i++) {
            int j = 0;
            for (; j < m; j++) {
                if (haystack[i + j] != needle[j]) break;
            }
            if (j == m) return i;
        }
    return -1;
    }
};
```
Time Complexity:  O(M * (N - M + 1))

Space Complexity : O(1)
</details>

<details>
  <summary>KMP</summary>
  
  **Approach:**
- uses degenerating property (pattern having the same sub-patterns appearing more than once in the pattern)
- lps[i] = the longest proper prefix of pat[0..i] which is also a suffix of pat[0..i].
```
For the pattern “AAAA”, lps[] is [0, 1, 2, 3]
For the pattern “ABCDE”, lps[] is [0, 0, 0, 0, 0]
For the pattern “AABAACAABAA”, lps[] is [0, 1, 0, 1, 2, 0, 1, 2, 3, 4, 5]
For the pattern “AAACAAAAAC”, lps[] is [0, 1, 2, 0, 1, 2, 3, 3, 3, 4] 
For the pattern “AAABAAA”, lps[] is [0, 1, 2, 0, 1, 2, 3]
```
Illustration of preprocessing (or construction of lps[]):
```
 pat[] = “AAACAAAA”
=> len = 0, i = 0: 
- lps[0] is always 0, we move to i = 1
lps[] = |0| | | | | | | |

=> len = 0, i = 1:
- Since pat[len] and pat[i] match, do len++, 
- store it in lps[i] and do i++.
- Set len = 1, lps[1] = 1, i = 2
lps[] = |0|1| | | | | | |

=> len = 1, i  = 2:
- Since pat[len] and pat[i] match, do len++, 
- store it in lps[i] and do i++.
- Set len = 2, lps[2] = 2, i = 3
lps[] = |0|1|2| | | | | |

=> len = 2, i = 3:
- Since pat[len] and pat[i] do not match, and len > 0, 
- Set len = lps[len-1] = lps[1] = 1
lps[] = |0|1|2| | | | | |

=> len = 1, i = 3:
- Since pat[len] and pat[i] do not match and len > 0, 
- len = lps[len-1] = lps[0] = 0
lps[] = |0|1|2| | | | | |

=> len = 0, i = 3:
- Since pat[len] and pat[i] do not match and len = 0, 
- Set lps[3] = 0 and i = 4
lps[] = |0|1|2|0| | | | |

=> len = 0, i = 4:
- Since pat[len] and pat[i] match, do len++, 
- Store it in lps[i] and do i++. 
- Set len = 1, lps[4] = 1, i = 5
lps[] = |0|1|2|0|1| | | |

=> len = 1, i = 5:
- Since pat[len] and pat[i] match, do len++, 
- Store it in lps[i] and do i++.
- Set len = 2, lps[5] = 2, i = 6
lps[] = |0|1|2|0|1|2| | |

=> len = 2, i = 6:
- Since pat[len] and pat[i] match, do len++, 
- Store it in lps[i] and do i++.
- len = 3, lps[6] = 3, i = 7
lps[] = |0|1|2|0|1|2|3| |

=> len = 3, i = 7:
- Since pat[len] and pat[i] do not match and len > 0,
- Set len = lps[len-1] = lps[2] = 2
lps[] = |0|1|2|0|1|2|3| |

=> len = 2, i = 7:
- Since pat[len] and pat[i] match, do len++, 
- Store it in lps[i] and do i++.
- len = 3, lps[7] = 3, i = 8
lps[] = |0|1|2|0|1|2|3|3|
```
- The idea is to not match a character that we know will anyway match.
- We start the comparison of pat[j] with j = 0 with characters of the current window of text.
- We keep matching characters txt[i] and pat[j] and keep incrementing i and j while pat[j] and txt[i] keep matching.
- When we see a mismatch:
  - We know that characters pat[0..j-1] match with txt[i-j…i-1] (Note that j starts with 0 and increments it only when there is a match).
  - We also know (from the above definition) that lps[j-1] is the count of characters of pat[0…j-1] that are both proper prefix and suffix.
  - From the above two points, we can conclude that we do not need to match these lps[j-1] characters with txt[i-j…i-1] because we know that these characters will anyway match.
```cpp
class Solution {
public:
    void lpsArray(string& needle, int m, vector<int>& lps) {
        // Length of the previous longest prefix suffix
        int len = 0;
        // lps[0] is always 0
        lps[0] = 0;
        // loop calculates lps[i] for i = 1 to m-1
        int i = 1;
        while (i < m) {
            if (needle[i] == needle[len]) {
                len++;
                lps[i] = len;
                i++;
            } else // (needle[i] != needle[len])
            {
                if (len != 0) {
                    len = lps[len - 1];
                } else // if (len == 0)
                {
                    lps[i] = 0;
                    i++;
                }
            }
        }
    }
    int strStr(string haystack, string needle) {
        int m = needle.length(), n = haystack.length();

        // Create lps[] that will hold the longest prefix suffix
        vector<int> lps(m);

        vector<int> result;

        // Preprocess the needletern (calculate lps[] array)
        lpsArray(needle, m, lps);

        int i = 0; // index for haystack
        int j = 0; // index for needle
        while (i < n) {
            if (needle[j] == haystack[i]) {
                j++;
                i++;
            }

            if (j == m) {

                return i - j;
            }

            // mismatch after j matches
            else if (i < n && needle[j] != haystack[i]) {
                // Do not match lps[0..lps[j-1]] characters, they will match
                // anyway
                if (j != 0) {
                    j = lps[j - 1];
                } else {
                    i++;
                }
            }
        }
        return -1;
    }
};
```
Time Complexity:  O(N + M)

Space Complexity : O(M)
</details>

