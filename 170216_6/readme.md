### Owner
- KH

### Question Title
- [6. ZigZag Conversion](https://leetcode.com/problems/zigzag-conversion/)

### Question Description
> The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
```
P   A   H   N
A P L S I I G
Y   I   R
```
> And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string text, int nRows);
```
convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".


zigzag meaning:

```
/*n=numRows
Δ=2n-2    1                           2n-1                         4n-3
Δ=        2                     2n-2  2n                    4n-4   4n-2
Δ=        3               2n-3        2n+1              4n-5       .
Δ=        .           .               .               .            .
Δ=        .       n+2                 .           3n               .
Δ=        n-1 n+1                     3n-3    3n-1                 5n-5
Δ=2n-2    n                           3n-2                         5n-4
*/
```

### Question Type
- [x] String

# [Solution] 

- Solution 1: use array[numRows] to store each row's string then concatenate every string into one string.

- Solution 2: build math equation for numbers between each column.

### Thoughts


### Complexity

Solution 1 - easier to understand

- Time: O(word length)
- Space: O(1 array + numRows * StringBuilder)

Solution 2 - faster

- Time: O(word length)
- Space: O(1)

### Source Code
```java
//Solution 1
public String convert(String s, int numRows) {
    if(numRows<=1)return s;
    StringBuilder[] sb=new StringBuilder[numRows];
    for(int i=0;i<sb.length;i++){
        sb[i]=new StringBuilder();   //init every sb element **important step!!!!
    }
    int incre=1;
    int index=0;
    for(int i=0;i<s.length();i++){
        sb[index].append(s.charAt(i));
        if(index==0){incre=1;}
        else if(index==numRows-1){incre=-1;}
        index+=incre;
    }

    for(int i=1;i<sb.length;i++){
        sb[0].append(sb[i]);
    }
    return sb[0].toString();
}

//Solution 2
public String convert(String s, int numRows) {
    if(numRows==1) return s;
    int x = 2 * (numRows-1); // distance between pipes |/|/|...
    int len = s.length();
    char[] c = new char[len]; // faster than stringbuilder?
    int k =0;
    for(int i=0; i < numRows; i++)
    {
        for(int j=i;j<len;j=j+x)
        {
            c[k++] = s.charAt(j);
            if(i>0 && i<numRows-1 && j+x-2*i < len)
            {
                   c[k++] = s.charAt(j+x-2*i); // extra character between pipes
            }
        }
    }
    return new String(c);
}
```
