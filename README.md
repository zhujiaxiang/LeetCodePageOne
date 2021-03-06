# LeetCodeOne
### 461. Hamming Distance
The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers x and y, calculate the Hamming distance.


### Note:
0 ≤ x, y < 231.

### Example:


```
Input: x = 1, y = 4

Output: 2

Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
```
### 问题
求两个数的二进制表示中，不同位数的个数。
### 思路
1. 将两个数进行异或
2. 统计异或后的数字中1的个数
### C++

```
class Solution {
public:
    int hammingDistance(int x, int y) {
        int dist = 0; int n = x^y;  //异或
        while(n)
        {
            ++dist;
            n = n&(n-1);
        }
        return dist;
    }
};
```

### 476. Number Complement
Given a positive integer, output its complement number. The complement strategy is to flip the bits of its binary representation.

The above arrows point to positions where the corresponding bits are different.
#### Note:
The given integer is guaranteed to fit within the range of a 32-bit signed integer.
You could assume no leading zero bit in the integer’s binary representation.
#### Example 1:

```
Input: 5
Output: 2
Explanation: The binary representation of 5 is 101 (no leading zero bits), and its complement is 010. So you need to output 2
```

#### Example 2:

```
Input: 1
Output: 0
Explanation: The binary representation of 1 is 1 (no leading zero bits), and its complement is 0. So you need to output 0.
```
### 问题
取一个正整数的二进制表达的反
### 思路
1. 制作一个mask 将正整数的二进制位数对应的位数 置为0；
2. 将正整数取反 与 ~mask(00000000111)作与运算

### C++

```
class Solution {
public:
    int findComplement(int num) {
      unsigned mask = ~0;             //制作mask
        while (num & mask) mask <<= 1;//根据正整数的二进制位数 将mask对应的位数置为0；
        return ~mask & ~num;          //将正整数取反，与mask作与运算
    }
};
```

### 190. Reverse Bits
Reverse bits of a given 32 bits unsigned integer.

#### For example
given 
```
input 43261596 (represented in binary as 00000010100101000001111010011100)
```

```
, return 964176192 (represented in binary as 00111001011110000010100101000000).
```


#### Follow up:
If this function is called many times, how would you optimize it?

### 问题
反转比特
### 思路
1. 每次取最后一位加入result
2. 再将imput右移抛出已加入的数字

### C++

```
 uint32_t reverseBits(uint32_t input)
{
    uint32_t result = 0;
    const uint32_t BITS_OF_BYTES = 8 ;
    for (int i=0; i<sizeof(input)*BITS_OF_BYTES; i++) {
        result = (result << 1 )|(input & 1);            //result左移空出位置，将input最后一位加入
        input = input >> 1;                            //input右移
    }
    
    
    return result;
}
```

### 500. Keyboard Row

Given a List of words, return the words that can be typed using letters of alphabet on only one row's of American keyboard like the image below.
![image](https://leetcode.com/static/images/problemset/keyboard.png)
#### Example 1:

```
Input: ["Hello", "Alaska", "Dad", "Peace"]
Output: ["Alaska", "Dad"]
```
#### Note:
You may use one character in the keyboard more than once.

You may assume the input string will only contain letters of alphabet.
#### 问题
给你一列表的单词，返回那些只包含美式键盘一行的单词
#### 思路
查每个单词的第一个字母，将其设为某行，随后遍历每个字母，看是否都在那一行
#### C++

```
std::vector<std::string> findWords(std::vector<std::string> &words)
{

    std::unordered_set<char> set1 = {'q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p'};
    std::unordered_set<char> set2 = {'a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l'};
    std::unordered_set<char> set3 = {'z', 'x', 'c', 'v', 'b', 'n', 'm'};
    std::vector<std::unordered_set<char>> sets = {set1, set2, set3};

    std::vector<std::string> result;

    for (int i = 0; i < words.size(); i++) {
        int index = 0, flag = 0;
        if (set1.find(tolower(words[i][0])) != set1.end()) {
            index = 0;
        } else if (set2.find(tolower(words[i][0])) != set2.end()) {
            index = 1;
        } else {
            index = 2;
        }

        std::unordered_set<char> tempset = sets[index];

        for (char a : words[i]) {
            if (tempset.find(tolower(a)) == tempset.end()) {
                flag = 1;
                break;
            }

        }
        
        if (flag == 0) {
            result.push_back(words[i]);
        }
    }

    return result;
}

```
#### 收获
==using namespace std; or using std::xxxxx；==
### 412. Fizz Buzz
Write a program that outputs the string representation of numbers from 1 to n.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.
#### Example:
```
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```
#### 问题
给一个N 从1到n中的数 放入数组，如果是三的倍数输出Fizz，五的倍数输出Buzz，三五的倍数输出FizzBuzz
#### 思路
分支判断
#### C++

```
using namespace std;

vector<string> fizzBuzz(int n)
{
    vector<string> a;
    for (int i = 1; i <= n; i++) {
        if (i%15==0) {
            a.push_back("FizzBuzz");
        }else if (i%5==0){
            a.push_back("Buzz");
        }else if (i%3==0){
            a.push_back("Fizz");
        }else{
            a.push_back(to_string(i));
        }
    }
    return a;
}

```
#### 收获
==to_string()== int=>string
#### 别人写法

```
vector<string> fizzBuzz(int n) {
        vector<string> ret_vec(n);
        for(int i=1; i<=n; ++i)
        {
            if(i%3 == 0)
            {
                ret_vec[i-1] += string("Fizz");
            }
            if(i%5 == 0)
            {
                ret_vec[i-1] += string("Buzz");
            }
            if(ret_vec[i-1] == "")
            {
                ret_vec[i-1] += to_string(i);
            }
        }
        return ret_vec;
    } 
```
### 344. Reverse String
Write a function that takes a string as input and returns the string reversed.
#### Example:

```
Given s = "hello", return "olleh".
```
### C++

```
string reverseString(string s) {
    
    if(s==""){
        return "";
    } ;
    string result = "";
    int length = (int)s.length();
    
    if(length != 0)
    {
        for (int i = length; i>0; i--) {
            char temp = s[i-1];
            result+=temp;       }
    }

    
    return result;
}

```
#### 别人写法

```
 string reverseString(string s) {
        int i = 0, j = s.size() - 1;
        while(i < j){
            swap(s[i++], s[j--]); 
        }
        
        return s;
    }
```
#### 收获

```
swap函数
```
### 496. Next Greater Element I
You are given two arrays (without duplicates) nums1 and nums2 where nums1’s elements are subset of nums2. Find all the next greater numbers for nums1's elements in the corresponding places of nums2.

The Next Greater Number of a number x in nums1 is the first greater number to its right in nums2. If it does not exist, output -1 for this number.
#### Example 1:

```
Input: nums1 = [4,1,2], nums2 = [1,3,4,2].
Output: [-1,3,-1]
Explanation:
    For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.
    For number 1 in the first array, the next greater number for it in the second array is 3.
    For number 2 in the first array, there is no next greater number for it in the second array, so output -1.
```
#### Example 2:

```
Input: nums1 = [2,4], nums2 = [1,2,3,4].
Output: [3,-1]
Explanation:
    For number 2 in the first array, the next greater number for it in the second array is 3.
    For number 4 in the first array, there is no next greater number for it in the second array, so output -1.
```
#### Note:
All elements in nums1 and nums2 are unique.

The length of both nums1 and nums2 would not exceed 1000.
### C++

```
vector<int> nextGreaterElement(vector<int>& findNums, vector<int>& nums) {
    int n = findNums.size();
    int m = nums.size();
    vector<int> result(n);
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            if (findNums[i] == nums[j]) {

                for (int k=j; k<m; k++) {
                    if (nums[k]>findNums[i]) {
                        result[i]=nums[k];
                        break;
                    }
                    
                }
                if (!result[i]) {
                    result[i]=-1;
                }
                
                break;
            }else{
                result[i] = -1;
            }
        }
        
    }
    return result;
}
```
### 别人写法
通过建立一个键值对，预先保存nums中每个数的nextGreaterElement，随后对其进行查找。

```
class Solution {
public:
 vector<int> nextGreaterElement(vector<int>& findNums, vector<int>& nums) {
		unordered_map<int, int> mark;
		deque<int> next;
		for (auto i : nums){
			while (!next.empty() && i > next.back()){
				mark[next.back()] = i;
				next.pop_back();
			}
			next.push_back(i);
		}
		vector<int >res;
		for (auto i : findNums){
			if (mark.find(i) != mark.end()){
				res.push_back(mark[i]);
			}
			else{
				res.push_back(-1);
			}
		}
		return res;
	}
};

```
### 463. Island Perimeter
You are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water. Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells). The island doesn't have "lakes" (water inside that isn't connected to the water around the island). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.
#### Example:

```
[[0,1,0,0],
 [1,1,1,0],
 [0,1,0,0],
 [1,1,0,0]]

Answer: 16
Explanation: The perimeter is the 16 yellow stripes in the image below:

```
![image](https://leetcode.com/static/images/problemset/island.png)
#### 问题
0是海1是岛，求岛的边界
#### 思路
从非边缘行，列开始遍历，遍历到1，count++，检查其左上两个是否也为一，若为1记录为一个repeat，
#### C++

```
int islandPerimeter(vector<vector<int>>& grid) {
    int count = 0;
    int repeat = 0;
    for (int i=0; i<grid.size(); i++) {
        for (int j=0; j<grid[i].size(); j++) {
            if (grid[i][j] == 1) {
                count ++;
                if (j!=0 && grid[i][j-1] == 1) {
                    repeat ++;
                }
                if (i!=0 && grid[i-1][j] == 1) {
                    repeat ++;
                }
            }
        }
    }
    
    return count * 4 -repeat;
}

```

#### 收获
遍历二维vector的方法

```
for (int i=0; i<grid.size(); i++) 
{
        for (int j=0; j<grid[i].size(); j++) 
        {
        }
}
```
### 292. Nim Game
You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.

Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.

For example, if there are 4 stones in the heap, then you will never win the game: no matter 1, 2, or 3 stones you remove, the last stone will always be removed by your friend.
#### Hint:
If there are 5 stones in the heap, could you figure out a way to remove the stones such that you will always be the winner?
#### 问题
取石头 一个人能取1，2，3块石头，如果你是先手，判断是否能赢
#### 思路
是4的倍数必输
#### C++

```
bool canWinNim(int n) {
        return (n &0B11) != 0;
    }
```
#### 收获

```
(n % 4) != 0 
(n &0B11) != 0;
```
### 485. Max Consecutive Ones
Given a binary array, find the maximum number of consecutive 1s in this array.
#### Example 1:

```
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.
```
#### Note:
The input array will only contain 0 and 1.

The length of input array is a positive integer and will not exceed 10,000
#### 问题
求最长的连续1的数量
#### 思路
做一个mark数组标记0的位置，再进行处理
#### C++

```
 int findMaxConsecutiveOnes(vector<int>& nums) {
    vector<int> mark;
    int count = 0;
    mark.push_back(-1);
    for(int i=0;i<nums.size();i++){
        if (nums[i] == 0) {
            mark.push_back(i);
            count ++;
        }
    }
    if(count == 0){
        return (int)nums.size();
    }
    mark.push_back(nums.size());
    int max = 0;
    for (int j=1; j<mark.size(); j++) {
        if (mark[j]-mark[j-1] -1 >max) {
            max = mark[j]-mark[j-1]-1;
        }
    }
    return max;
        }
```

#### 别人写法

```
int findMaxConsecutiveOnes(vector<int>& nums) {
int max=0,cur=0;
for(int i=0;i<nums.size();i++)
{
if(nums[i]&1)
{
max=max>++cur?max:cur;
}
else cur=0;
}
return max;
}
```

#### 收获
别想太复杂
### 136. Single Number
Given an array of integers, every element appears twice except for one. Find that single one.

#### Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

#### 问题
求一个数组中的单个数字，要求线性时间复杂度，无额外空间
#### 思路
异或为0
#### C++

```
int singleNumber(vector<int>& nums) {
            for(int i=1;i<nums.size();i++)
    {
        nums[0]=nums[0]^nums[i];
    }
    return nums[0];
    }
```

#### 收获
多关注位运算，异或，与，非，反

### 448. Find All Numbers Disappeared in an Array
Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.
#### Example:

```
Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
```
#### 问题
寻找数组中消失的数字
#### 思路
把数字放到该放的地方，然后找出消失的数字
#### C++

```
vector<int> findDisappearedNumbers(vector<int>& nums) {
    int len = (int)nums.size();
    for (int i=0; i<len; i++) {
        int m = abs(nums[i])-1;
        nums[m]= nums[m]>0?-nums[m]:nums[m];
    }
    vector<int> res;
    for (int i=0; i<len; i++) {
        if(nums[i] > 0) res.push_back(i+1);
    }
    return res;
}
```
### 520. Detect Capital
Given a word, you need to judge whether the usage of capitals in it is right or not.

We define the usage of capitals in a word to be right when one of the following cases holds:

All letters in this word are capitals, like "USA".
All letters in this word are not capitals, like "leetcode".
Only the first letter in this word is capital if it has more than one letter, like "Google".
Otherwise, we define that this word doesn't use capitals in a right way.

#### Example 1:

```
Input: "USA"
Output: True
```

#### Example 2:

```
Input: "FlaG"
Output: False
```

#### Note: 
The input will be a non-empty word consisting of uppercase and lowercase latin letters.
#### 问题
看string是否符合标准大写规则
#### 思路
分支判断
#### C++

```
bool detectCapitalUse(string word) {
    char c = word[0];
    if (!isupper(c)) {
        for (auto a:word) {
            if (isupper(a)) {
                return false;
            }
        }
    }else{
        if (isupper(word[1])) {
            for (auto a:word) {
                if (islower(a)) {
                    return false;
                }
            }

        }else{
            for(int i = 2;i<word.length();i++){
                if (isupper(word[i])) {
                    return false;
                }
            }
        }
    }
    return true;
}
```
#### 别人写法

```
 public boolean detectCapitalUse(String word) {
        int cnt = 0;
        for(char c: word.toCharArray()) if('Z' - c >= 0) cnt++;
        return ((cnt==0 || cnt==word.length()) || (cnt==1 && 'Z' - word.charAt(0)>=0));
    }
```
#### 收获
通过ASC码判断，大写字母的ASC码比小写字母小。
### 104. Maximum Depth of Binary Tree
#### 问题
求树的最大深度
#### 思路
深度优先||广度优先
#### C++

```
深度优先
int maxDepth(TreeNode* root) {
    return root == NULL ? 0 :max(maxDepth(root->left), maxDepth(root->right))+1;
}
广度优先
int maxDepth(TreeNode *root)
{
    if(root == NULL)
        return 0;
    
    int res = 0;
    queue<TreeNode *> q;
    q.push(root);
    while(!q.empty())
    {
        ++ res;
        for(int i = 0, n = q.size(); i < n; ++ i)
        {
            TreeNode *p = q.front();
            q.pop();
            
            if(p -> left != NULL)
                q.push(p -> left);
            if(p -> right != NULL)
                q.push(p -> right);
        }
    }
    
    return res;
}
```
### 389. Find the Difference
#### 问题
寻找两个字符串不同的字符
#### 思路
位运算 异或能找出单个不同的字符
#### C++

```
char findTheDifference(string s, string t) {

    char res = '\0';
    for (char a:s) {
        res = res^a;
    }
    
    for (char b:t) {
        res = res^b;
    }
    cout<<res;
    
    return res;
}
```

#### 收获
异或找不同
### 371. Sum of Two Integers
Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

#### Example:
Given a = 1 and b = 2, return 3.

#### 问题
在不使用+ -的情况下 实现加法
#### 思路
通过异或来实现0+1或1+0，通过与并左移实现进位
#### C++

```
int getSum(int a, int b) {
    int sum = a;
    while (b!=0) {
        sum = a^b;
        b = (a&b)<<1;
        a = sum;
    }
    return sum;
}
```

#### 收获
可以通过异或来实现0+1或1+0，通过与+左移实现进位
### 226. Invert Binary Tree

```
Invert a binary tree.

     4
   /   \
  2     7
 / \   / \
1   3 6   9
to
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```
#### 问题
翻转二叉树
#### 思路
递归，非递归（广度优先）
#### C++

```
递归
TreeNode* invertTree(TreeNode* root) {
              if(root == NULL)
    {
        return NULL;
    }
    
    if (root) {
        TreeNode *temp = root->left;
        root->left = root->right;
        root->right = temp;
        
        if(root->left !=NULL){
            invertTree(root->left);
        }
        if (root->right !=NULL) {
            invertTree(root->right);
        }
    }
    
    return root;
    }
非递归
TreeNode *invertTree(TreeNode *root)
{
    stack<TreeNode *> stack;
    stack.push(root);
    while (!stack.empty()) {
        TreeNode *p = stack.top();
        stack.pop();
        if (p) {
            stack.push(root->left);
            stack.push(root->right);
            swap(root->left, root->right);
        }
    }
    return root;
}

```
#### 收获
swap函数
### 258. Add Digits
Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

#### For example:

Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.

#### Follow up:
Could you do it without any loop/recursion in O(1) runtime?
#### 问题
38-》3+8=11》1+1》2  一个数，各位数相加，直至只剩一位数
#### 思路
[数根](https://www.zhihu.com/question/30972581)
#### C++

```
    int addDigits(int num) {
        return 1+(num-1)%9;
    }
```

#### 收获
12345 % 9 = (1 + 2 + 3 + 4 +5 ) % 9 
### 492. Construct the Rectangle
For a web developer, it is very important to know how to design a web page's size. So, given a specific rectangular web page’s area, your job by now is to design a rectangular web page, whose length L and width W satisfy the following requirements:


```
1. The area of the rectangular web page you designed must equal to the given target area.

2. The width W should not be larger than the length L, which means L >= W.

3. The difference between length L and width W should be as small as possible.
You need to output the length L and the width W of the web page you designed in sequence.
```

#### Example:

```
Input: 4
Output: [2, 2]
Explanation: The target area is 4, and all the possible ways to construct it are [1,4], [2,2], [4,1]. 
But according to requirement 2, [1,4] is illegal; according to requirement 3,  [4,1] is not optimal compared to [2,2]. So the length L is 2, and the width W is 2.
```

#### Note:
The given area won't exceed 10,000,000 and is a positive integer
The web page's width and length you designed must be positive integers
#### 问题
给定一个正方形面积，求出符合要求的一组长款
#### 收获
时间复杂度，的优化
#### C++

```
写法1：99ms
vector<int> constructRectangle(int area) {
    
    int l = sqrt(area);
    for(int i = l;i<=area;i++)
    {
        if (area%i==0) {
            l=i;
            break;
        }
    }
    int w = area/l;
    
    if(w>l){
        swap(w,l);
    }
    vector<int> result = {l,w};
    
    return result;
}
更新写法2：3ms
vector<int> constructRectangle(int area) {
    
    int w ;
    for(int i = 1;i*i<=area;i++)
    {
        if (area%i==0) {
            w=i;

        }
    }

    vector<int> result = {area/w,w};
    
    return result;
}
```
#### 收获
不用系统函数，想办法替代
### 283. Move Zeroes
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

#### Note:
You must do this in-place without making a copy of the array.
Minimize the total number of operations.
#### 问题
将数组中的0移动到数组末尾
#### 思路
遇到非0就覆盖原数组，最后再将0添上
#### C++

```
void moveZeroes(vector<int>& nums) {
    int j = 0;
    for (int i=0; i<nums.size(); i++) {
        if (nums[i]!=0) {
            nums[j++]=nums[i];
        }
    }
    
    for (; j<nums.size(); j++) {
        nums[j] = 0;
    }
}
```
### 506. Relative Ranks
Given scores of N athletes, find their relative ranks and the people with the top three highest scores, who will be awarded medals: "Gold Medal", "Silver Medal" and "Bronze Medal".

#### Example 1:

```
Input: [5, 4, 3, 2, 1]
Output: ["Gold Medal", "Silver Medal", "Bronze Medal", "4", "5"]
Explanation: The first three athletes got the top three highest scores, so they got "Gold Medal", "Silver Medal" and "Bronze Medal". 
For the left two athletes, you just need to output their relative ranks according to their scores.
```

#### Note:
N is a positive integer and won't exceed 10,000.
All the scores of athletes are guaranteed to be unique.
#### 问题
根据数组中的得，输出其对应的排名    
#### 思路
利用C++ map的递增特性，进行输出
#### C++

```
vector<string> findRelativeRanks(vector<int>& nums) {

    map<int,int> mp;
    
    for (int i=0; i<nums.size(); i++) {
        mp[nums[i]]=i;
    }
    
    vector<string> res(nums.size(),"");
    int cnt = 0;
    for (map<int,int>::reverse_iterator it = mp.rbegin(); it!=mp.rend(); it++,cnt++) {
        if (cnt== 0) {
            res[it->second] = "Gold Medal";
        }else if (cnt==1){
            res[it->second] = "Silver Medal";
        }else if (cnt==2){
            res[it->second] = "Bronze Medal";
        }else{
            res[it->second] = to_string(cnt+1);
        }
    }
    
    return res;
}
```
#### 收获
C++ map是递增的，it—>first是key it->second是value，倒序遍历迭代器的方法

```
for(map<int,int>::reverse_iterator it=mp.rbegin();it!+mp.rend();it++)
```
### 530. Minimum Absolute Difference in BST
Given a binary search tree with non-negative values, find the minimum absolute difference between values of any two nodes.

#### Example:


```
Input:

   1
    \
     3
    /
   2

Output:
1
```


#### Explanation:
The minimum absolute difference is 1, which is the difference between 2 and 1 (or between 2 and 3).
Note: There are at least two nodes in this BST.
#### 问题
求二叉搜索树中，求两个结点绝对值相差最小的值
#### 思路
中序遍历出的二叉搜索树是有序递增的，在这个有序的队列中求最小值
#### C++

```
 public:void inorderTraverse(TreeNode* root, int& val, int& min_dif) {
    if (root->left != NULL) inorderTraverse(root->left, val, min_dif);
    if (val >= 0) min_dif = min(min_dif, root->val - val);
    val = root->val;
    if (root->right != NULL) inorderTraverse(root->right, val, min_dif);
}
public:int getMinimumDifference(TreeNode* root) {
    auto min_dif = INT_MAX, val = -1;
    inorderTraverse(root, val, min_dif);
    return min_dif;
}
```

#### 收获
中序遍历二叉搜索树是有序的

### 167. Two Sum II - Input array is sorted
Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution and you may not use the same element twice.

#### Input:
numbers={2, 7, 11, 15}, target=9
#### Output:
index1=1, index2=2
#### 问题
给一个数组，给一个目标，找出相加为目标数的两个数在数组中的位置
#### 描述
一左一右两个指针， while
#### C++

```
 vector<int> twoSum(vector<int>& numbers, int target) {
    
    int r = (int)numbers.size() - 1;
    
    int l = 0;
    
    while (l<r) {
        if (numbers[l] + numbers[r] == target) {
          vector<int> res{l+1,r+1};
            return res;
        }else if(numbers[l] + numbers[r] > target){
            r--;
        }else if(numbers[l] + numbers[r] < target){
            l++;
        }
    }
    
    vector<int> fail;
    return fail;
}
```
### 521. Longest Uncommon Subsequence I
Given a group of two strings, you need to find the longest uncommon subsequence of this group of two strings. The longest uncommon subsequence is defined as the longest subsequence of one of these strings and this subsequence should not be any subsequence of the other strings.

A subsequence is a sequence that can be derived from one sequence by deleting some characters without changing the order of the remaining elements. Trivially, any string is a subsequence of itself and an empty string is a subsequence of any string.

The input will be two strings, and the output needs to be the length of the longest uncommon subsequence. If the longest uncommon subsequence doesn't exist, return -1.

#### Example 1:

```
Input: "aba", "cdc"
Output: 3
Explanation: The longest uncommon subsequence is "aba" (or "cdc"), 
because "aba" is a subsequence of "aba", 
but not a subsequence of any other strings in the group of two strings.
```

#### Note:

Both strings' lengths will not exceed 100.
Only letters from a ~ z will appear in input strings.
#### 问题
两个字符串中最长的字符串是否是第二个字符串的子串，如果是则返回-1，否做返回其长度
#### C++

```
int findLUSlength(string a, string b) {
    
    if (a.size() == b.size()) {
        if (a==b) {
            return -1;
        }else{
            return (int)a.size();
        }
    }else{
        return (int)max(a.size(), b.size());
    }
}
```
### 455. Assign Cookies
Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie. Each child i has a greed factor gi, which is the minimum size of a cookie that the child will be content with; and each cookie j has a size sj. If sj >= gi, we can assign the cookie j to the child i, and the child i will be content. Your goal is to maximize the number of your content children and output the maximum number.

#### Note:
You may assume the greed factor is always positive. 
You cannot assign more than one cookie to one child.

#### Example 1:

```
Input: [1,2,3], [1,1]

Output: 1

Explanation: You have 3 children and 2 cookies. The greed factors of 3 children are 1, 2, 3. 
And even though you have 2 cookies, since their size is both 1, you could only make the child whose greed factor is 1 content.
You need to output 1.
```

#### Example 2:

```
Input: [1,2], [1,2,3]

Output: 2


Explanation: You have 2 children and 3 cookies. The greed factors of 2 children are 1, 2. 
You have 3 cookies and their sizes are big enough to gratify all of the children, 
You need to output 2.
```
#### 问题
给小孩分曲奇，两个数组
第一个是小孩的需求数组【1，2，3】，代表有3个小孩，分别要1，2，3大小的曲奇
第二个是自己拥有的曲奇数组【1，2】代表有2个曲奇，大小分别为1，2
#### 思路 
贪心算法，先对两个数组进行递增排序，随后开始比较，作一个关于饼干数组的循环，如果遇到合适的小孩，则分配给他，然后对下一个下小孩进行分析

#### C++

```
int findContentChildren(vector<int>& g, vector<int>& s) {
    sort(g.begin(),g.end());
    sort(s.begin(), s.end());
    
    int i=0,j=0;
    
    for (; i < g.size()&& j < s.size(); j++) {
        if (g[i]<=s[j]) {
            i++;
        }
    }
    
    return i;
};
```

#### 收获
贪心算法，sort函数

### 453. Minimum Moves to Equal Array Elements
Given a non-empty integer array of size n, find the minimum number of moves required to make all array elements equal, where a move is incrementing n - 1 elements by 1.

#### Example:


```
Input:
[1,2,3]

Output:
3
```


#### Explanation:
Only three moves are needed (remember each move increments two elements):


```
[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```

#### 问题
给一组n个数，每次只能进行n-1个数的+1操作，问将他们都变为相同的数字最少需要几步。
#### 思路
（min+k）*n = sum+k*(n-1)
k = sum - min*n

#### C++

```
int minMoves(vector<int>& nums) {
    
    if (nums.size()<=1) {
        return 0;
    }else{
        int sum=0,minimum=INT_MAX;
        for (int i=0; i<nums.size(); i++) {
            sum += nums[i];
            minimum = min(minimum,nums[i]);
        }
        int res = sum-(int)(minimum*nums.size());
        return res;
    }
}
```

#### 别人写法

```
int minMoves(vector<int>& nums) {
    return accumulate(begin(nums), end(nums), 0L) - nums.size() * *min_element(begin(nums), end(nums));
}
```

#### 收获
列出等式，找规律 

```
#include <numeric>
int sum = accumulate(begin(nums), end(nums), 0);
min_element(begin(nums), end(nums));

```
### 383. Ransom Note
Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.

Each letter in the magazine string can only be used once in your ransom note.

#### Note:
You may assume that both strings contain only lowercase letters.

canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true

#### 问题
给两个数组，如果能用第二个数组中的元素构成第一个数组，则返回true
#### 思路
对数组2的每一个字母进行计数+1，计数完后再对数组1对应进行计数-1，如果有数计数<0，则返回false，否则则返回true
#### C++

```
bool canConstruct(string ransomNote, string magazine) {
    vector<int> vec(26,0);
    
    for (int i=0; i<magazine.size(); i++) {
        ++vec[magazine[i]-'a'];
    }
    
    for (int j=0; j<ransomNote.size(); j++) {
        if (--vec[ransomNote[j]-'a']<0) {
            return false;
        }
    }
    
    return true;
}
```

#### 收获
一种比较的思路

### 349. Intersection of Two Arrays    
Given two arrays, write a function to compute their intersection.

#### Example:
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].

#### Note:
Each element in the result must be unique.
The result can be in any order.
Subscribe to see which companies asked this question.
#### 问题
给2个数组，找出共同的元素
#### 思路
比较，去除重复元素 使用unique
#### C++

```
vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
    if(nums1.size()<=0||nums2.size()<=0)
    {
        return vector<int>{};
    }
    vector<int> res;
    sort(nums1.begin(),nums1.end());
    sort(nums2.begin(),nums2.end());
    int i=0,j=0;
    for (; i<nums1.size()&&j<nums2.size(); j++) {
        if (nums1[i]==nums2[j]) {
            res.push_back(nums1[i]);
            i++;
        }else if (nums1[i]<nums2[j]){
            i++;
            j--;
        }
    }
    vector<int>::iterator new_end;
    new_end=unique(res.begin(),res.end());
    res.erase(new_end, res.end());
    return res;
}
```

#### 收获

```
去除重复元素

new_end=unique(res.begin(),res.end());
res.erase(new_end, res.end());
```

### 404. Sum of Left Leaves   
Find the sum of all left leaves in a given binary tree.

#### Example:

```
    3
   / \
  9  20
    /  \
   15   7
```

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
#### 问题
统计一棵树的左叶子和
#### 思路
递归
#### C++

```
int sumOfLeftLeaves(TreeNode* root) {
    
    if(!root){
        return 0;
    }

    
    if (root->left && !root->left->left && !root->left->right) {
        return root->left->val + sumOfLeftLeaves(root->right);
    }
    
    return sumOfLeftLeaves(root->left) + sumOfLeftLeaves(root->right);
}
```

#### 收获
从最小的一部分观察，制定递归策略

### 122. Best Time to Buy and Sell Stock II   
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
#### 问题
给一个数组，数组i代表天数，a[i-1]代表当天股票价值，问怎么样才能获取最大值？
#### 思路
累加差值，如果遇到下跌的天数就跳过
#### C++

```
int maxProfit(vector<int> &prices)
{
    if (prices.size() == 0) {
        return 0;
    }
    int maximum = 0;

    for (int i = 0; i < prices.size()-1; i++) {
       
        if (prices[i] < prices[i+1]) {
            maximum = maximum + prices[i+1]-prices[i];
        }
    }

    return maximum;
}
```
#### 别人的写法

```
int maxProfit(vector<int> &prices) {
    int ret = 0;
    for (size_t p = 1; p < prices.size(); ++p) 
      ret += max(prices[p] - prices[p - 1], 0);    
    return ret;
}   
```
#### 收获

```
if (prices[i] < prices[i+1]) 
{
     maximum = maximum + prices[i+1]-prices[i];
}
        
 ret += max(prices[p] - prices[p - 1], 0);
```
### 387. First Unique Character in a String
Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

#### Examples:
```
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```
#### 问题
求string中第一个不重复的字符的下标
#### 思路
使用map将string按字符一个个存入map，并count
#### C++

```
int firstUniqChar(string s) {
    unordered_map<char, int> map;
    
    for(auto c:s)
    {
        map[c]++;
    }
    
    for (int i = 0; i< s.size(); i++) {
        if(map[s[i]] - 1 ==0)
        {
            return i;
        }
        
    }
    return -1;
}
```
#### 收获
多用键值对，通过

```
for (int i = 0; i< s.size(); i++) {
        if(map[s[i]] - 1 ==0)
        {
            return i;
        }
        
    }
```
能实现按顺序查找第一个不重复的字符。

### 122. Best Time to Buy and Sell Stock II
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
#### 问题
给定一个数组 下标为天数，各个元素为当天股票价格，球可获利的最大值
#### 思路
累加
#### C++

```
int maxProfit(vector<int> &prices) {
    int ret = 0;
    for (size_t p = 1; p < prices.size(); ++p) 
      ret += max(prices[p] - prices[p - 1], 0);    
    return ret;
}
```

### 171. Excel Sheet Column Number

Given a column title as appear in an Excel sheet, return its corresponding column number.

#### For example:


```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28
```

#### 问题
类似于Excel的列标题，求其代表的数字
#### 思路
按位数分析累加
#### C++

```
int titleToNumber(string s) {
    
    int res = 0;
    
    for (int i = 0; i < s.size(); res = res*26 + s[i] - 'A' + 1 , i++ ) ;
    
    return res;
}
```


### 237. Delete Node in a Linked Lis
Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Supposed the linked list is 1 -> 2 -> 3 -> 4 and you are given the third node with value 3, the linked list should become 1 -> 2 -> 4 after calling your function.
#### 问题
删除节点
#### 思路
用被删除结点之后的结点替换被删除结点
#### C++

```
    void deleteNode(ListNode* node) {
        *node = *node -> next;
    }
```

### 100. Same Tree
Given two binary trees, write a function to check if they are equal or not.

Two binary trees are considered equal if they are structurally identical and the nodes have the same value.
#### 问题
判断两棵树是否相等
#### 思路
递归判断
#### C++

```
bool isSameTree(TreeNode* p, TreeNode* q) {
    
    if (p == NULL || q == NULL) {
        return p==q;
    }
    
    return (p->val == q->val && isSameTree(p->left, q->left) && isSameTree(p->right, q->right));
}
```


### 169. Majority Element
Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array
#### 问题
求一个数组中，出现次数超过一半的字符
#### 思路
排序后，出现次数超过一半的字符肯定在中间
#### C++

```
public:
int majorityElement(vector<int>& nums) {
    
    unordered_map<int, int> cnt;
    
    for (int i = 0; i < nums.size(); i++) {
        cnt[nums[i]]++;
    }
    
    for (int i=0; i<nums.size(); i++) {
        if(cnt[nums[i]] > nums.size()/2){
            return nums[i];
        }
    }
    return 0;
}
```
#### 别人的写法

```
    int majorityElement(vector<int>& nums) {
        nth_element(nums.begin(), nums.begin() + nums.size() / 2, nums.end());
        return nums[nums.size() / 2];
    } 
```

### 242. Valid Anagram
Given two strings s and t, write a function to determine if t is an anagram of s.

#### For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

#### Note:
You may assume the string contains only lowercase alphabets.

#### Follow up:
What if the inputs contain unicode characters? How would you adapt your solution to such case?
#### 问题
两个数组，问他们是否重新组合后是否为同一个单词
#### 思路
对第二个数组中的字母一一计数，随后再对第一个数组中的字母一一扣除，如果为负，则false
#### C++

```
bool isAnagram(string s, string t) {
    vector<int> count(26,0);
    
       if (s.size() != t.size()) {
        return false;
    }
    
    for (int i=0; i<s.size(); i++) {
        ++count[s[i]-'a'];
    }
    
    for (int j=0; j<t.size(); j++) {
        if (--count[t[j]-'a']<0) {
            return false;
        }
    }
    
    return true;
    
}
```
### 504. Base 7
Given an integer, return its base 7 string representation.


```
Example 1:
Input: 100
Output: "202"
Example 2:
Input: -7
Output: "-10"
Note: The input will be in range of [-1e7, 1e7].
```

#### 问题
给一个数，转化为7进制数
#### 思路
递除取余
#### C++

```
string convertToBase7(int num) {
    int i = 0;
    int n = num;
    string res = "";

    num = abs(num);
    do {
        res.insert(i,to_string(num%7));
        num = num/7;
    } while (num != 0);
    
    
    
    return (n >=0?"":"-") + res;
}
```
### 409. Longest Palindrome
Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

#### Note:
Assume the length of given string will not exceed 1,010.

#### Example:


```
Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
```

#### 问题
求能组成的最长回文子串的长度
#### 思路
统计所有偶数长度的字符并相加，统计所有奇数长度的字符并减一相加，只保留一个奇数不减一
#### C++

```
int longestPalindrome(string s) {
    vector<int> m(256,0);
    int cnt = 0;
    for (auto i : s) {
        m[i-'\0']++;
    }
    for (auto j : m) {
        cnt += j % 2 ? (cnt % 2 ? j-1 : j) :  j;
    }
    return cnt;
}
```


### 217. Contains Duplicate
Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.
#### 问题
给一个数字数组，如果有重复的则返回true
#### 思路
统计，遇到超过1的返回
#### C++

```
bool containsDuplicate(vector<int>& nums) {
    unordered_map<int, int> map;
    
    if (nums.size()==0) {
        return false;
    }
    
    for (int i: nums) {
        if(++map[i]>1){
            return true;
        }
    }
    
    return false;
}
```

### 13. Roman to Integer
Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.
#### 问题
转化罗马数字
#### 思路
做一个字典，分小紧随大，大紧随小 两种罗马字符减加情况
#### C++

```
public:
    int romanToInt(string s)
{
    unordered_map<char, int> map{{'I', 1},
                                 {'V', 5},
                                 {'X', 10},
                                 {'L', 50},
                                 {'C', 100},
                                 {'D', 500},
                                 {'M', 1000}};
    
    int res = 0;
    
    for (int i = 0; i < s.size(); i++) {
        if (map[s[i]]<map[s[i+1]]) {
            res -= map[s[i]];
        }else{
            res += map[s[i]];
        }
    }
    return res;
    
}
```

### 401. Binary Watch
A binary watch has 4 LEDs on the top which represent the hours (0-11), and the 6 LEDs on the bottom represent the minutes (0-59).

Each LED represents a zero or one, with the least significant bit on the right.

![image](https://upload.wikimedia.org/wikipedia/commons/8/8b/Binary_clock_samui_moon.jpg)
For example, the above binary watch reads "3:25".

Given a non-negative integer n which represents the number of LEDs that are currently on, return all possible times the watch could represent.

Example:


```
Input: n = 1
Return: ["1:00", "2:00", "4:00", "8:00", "0:01", "0:02", "0:04", "0:08", "0:16", "0:32"]
Note:
The order of output does not matter.
The hour must not contain a leading zero, for example "01:00" is not valid, it should be "1:00".
The minute must be consist of two digits and may contain a leading zero, for example "10:2" is not valid, it should be "10:02".
```

#### 问题
二进制手表，当亮点个数为n时，给出所有时间组合
#### 思路
二进制表示各时间，符合count则添加进返回vector
#### C++

```
vector<string> readBinaryWatch(int num) {
    vector<string> res;
    for(int h = 0; h < 12;h++)
        for(int m = 0; m < 60;m++){
            if (bitset<10>(h<<6|m).count() == num) {
                res.emplace_back(to_string(h) + (m<10?":0":":")  + to_string(m));
            }
        }
    return res;
}
```

#### 收获
bitset<10>

emplace_back 比 push_back 更高效
### 206. Reverse Linked List
#### 问题 
翻转链表
#### 思路
设立一个pre指针，一个next指针，进行翻转
#### C++

```
ListNode* reverseList(ListNode* head) {
    

    ListNode *a = NULL;
    

    
    while(head){
        ListNode *tmp = head->next;
        head->next = a;
        a=head;
        head=tmp;
       
    }
    
    return a;
}
```

###
#### 问题
#### 思路
#### C++
#### 收获
