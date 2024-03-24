# Reorganize String

Given a string s, rearrange the characters of s so that any two adjacent characters are not the same.

Return any possible rearrangement of s or return "" if not possible.

 

Example 1:

Input: s = "aab"
Output: "aba"
Example 2:

Input: s = "aaab"
Output: ""
 

Constraints:

1 <= s.length <= 500
s consists of lowercase English letters.

``` js
/**
 * @param {string} s
 * @return {string}
 */
var reorganizeString = function(s) {
    
    let charCount = new Array(26).fill(0);

    let len = s.length;
    for (let i=0; i<len; i++){
        let j = s.charCodeAt(i) - 97;
        charCount[j]++;
    }
    let maxCharCount = 0;
    for(let i=0; i<26; i++){
        if(charCount[i]>charCount[maxCharCount]){
            maxCharCount = i;
        }
    }
    
    if(charCount[maxCharCount]> Math.floor((len+1)/2)){
        return "";
    }
    let idx =0;
    let result = new Array(len);
    while(charCount[maxCharCount]>0){
        result[idx] = String.fromCharCode(maxCharCount + 97);
        idx +=2;
        charCount[maxCharCount]--;
    }
    for(let i =0; i<26; i++){
        while(charCount[i]>0){
            if(idx>=len){
                idx = 1;
            }
            result[idx] = String.fromCharCode(i+97);
            idx +=2;
            charCount[i]--;
        }
    }
    return result.join("");
    // console.log(charCount);
};

```
