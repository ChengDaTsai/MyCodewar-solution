Description:

ROT13 is a simple letter substitution cipher that replaces a letter with the letter 13 letters after it in the alphabet. ROT13 is an example of the Caesar cipher.
Create a function that takes a string and returns the string ciphered with Rot13. If there are numbers or special characters included in the string, they should be returned as they are. Only letters from the latin/english alphabet should be shifted, like in the original Rot13 "implementation".
我的解法:
```
#include <string> 
using namespace std; 
string rot13(string msg) 
{ 
  int l = msg.length(); 
  for(int i = 0 ; i<l ; i++ ){ 
    if('a' <= msg[i] && msg[i] <= 'z'){ //小寫 
      if(msg[i] >= 'n') 
        msg[i] = char(msg[i] - 13); 
      else 
        msg[i] = char(msg[i] + 13); 
    }  
    else if('A' <= msg[i] && msg[i] <= 'Z'){ //大寫 
      if(msg[i] >= 'N') 
        msg[i] = char(msg[i] - 13); 
      else 
        msg[i] = char(msg[i] + 13); 
    } 
    
  } 
  return msg; 
}
```
最佳解:
```
std::string rot13(std::string msg) 
{ 
  for(char& c : msg) 
    c = isupper(c) ? 'A' + (c - 'A' + 13) % 26 :  
        islower(c) ? 'a' + (c - 'a' + 13) % 26 :  
        c; 
  return msg; 
}
```

---
Description:

Some numbers have funny properties. For example:
89 --> 8¹ + 9² = 89 * 1
695 --> 6² + 9³ + 5⁴= 1390 = 695 * 2
46288 --> 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51
Given a positive integer n written as abcd... (a, b, c, d... being digits) and a positive integer p

- we want to find a positive integer k, if it exists, such as the sum of the digits of n taken to the successive powers of p is equal to k * n.
In other words:
Is there an integer k such as : (a ^ p + b ^ (p+1) + c ^(p+2) + d ^ (p+3) + ...) = n * k
If it is the case we will return k, if not return -1.
Note: n and p will always be given as strictly positive integers.
mine:
```
#include<math.h> 
#include<string> 
using namespace std; 
class DigPow 
{ 
public: 
  static int digPow(int n, int p){ 
    string sn = to_string(n); 
    int sum = 0,count = 0; 
    for(char& c : sn){ 
      sum += pow(int(c-'0'),p+count); 
      count ++ ; 
    } 
    return (sum % n ? -1 : sum / n); 
  } 
   
};
```
best
```
#include <cmath> 
using namespace std; 
class DigPow 
{ 
public: 
  static int digPow(int n, int p){ 
   long long sum=0; 
   for(char digit : to_string(n)){ 
     sum+=pow(digit-'0',p++); 
   } 
   return (sum/n)*n==sum ? sum/n : -1; 
  } 
};
```

---
C++中將string按照空格分割的方法(vector應用)
```
#include<iostream>
#include<string>
#include<sstream>
#include<vector>
using namespace std;

int main(){
    //用于存放分割后的字符串 
    vector<string> res;
    //待分割的字符串，含有很多空格 
    string word="   Hello, I want   to learn C++!   ";
    //暂存从word中读取的字符串 
    string result;
    //将字符串读到input中 
    stringstream input(word);
    //依次输出到result中，并存入res中 
    while(input>>result)
        res.push_back(result);
    //输出res 
    for(int i=0;i<res.size();i++){
        cout<<res[i]<<endl;
    }
    return 0;
}
```
