Z[i] represents the length of the longest substring that is prefix of s and prefix of suffix of s starting from i.
```java
public static int[] z_function_efficient(String s) {
    int n = s.length();
    int z[] = new int[n];
    for(int i = 1, l = 0, r = 0 ; i < n ; i++) {
        if(i <= r) {
            z[i] = Math.min(r-i+1, z[i-l]);
        }
        while(i+z[i]<n && s.charAt(z[i]) == s.charAt(i+z[i])){
            z[i]++;
        }
        if(i+z[i]-1 > r) {
            l=i;
            r=i+z[i]-1;
        }
    }
    return z;
}
```


Pattern matching using z function

let s = (t + "?" + p)
z = z_function(s);

we will ensure that '?' is not a character in p and t.

if(z[i] == length(p)) pattern matched

runtime = o(length(p)) + o(length(t))


