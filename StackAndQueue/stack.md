<details>
  <summary>Implement Stack using Queues</summary>

  [Link](https://leetcode.com/problems/implement-stack-using-queues/)
  
-----

   **Optimal:**

  - use two queues,
  - for adding, add elements to the q2
      - while q1 is not epmpty, keep copying the elements to q2 and poppping from q1
      - swap q1 and q2
  - for popping:
      -  store int at top,
      -  pop from q1 then return stored value
  - for top = q1.front()
  - for empty() = q1.empty()
 ```cpp
 class MyStack {
public:
    queue<int>q1;
    queue<int>q2;
    MyStack() {
        
    }
    
    void push(int x) {
        q2.push(x);
        while(!q1.empty()){
            q2.push(q1.front());
            q1.pop();
        }
        swap(q1,q2);
    }
    
    int pop() {
        int ans = top();
        q1.pop();
        return ans;
    }
    
    int top() {
        return q1.front();
    }
    
    bool empty() {
        return q1.empty();
    }
};
```
    
</details>  


<details>
  <summary>Implement Queue using Stacks</summary>

  [Link](\https://leetcode.com/problems/implement-queue-using-stacks/)
  
-----

   **Optimal:**

  - use two stacks,in and out
  - for adding, add elements to `in`
  - for popping:
      - call `peek()`  
      -  store val at top of `out`,
      -  pop from `out` then return stored value
  - for `peek()`:
      - if `out` is empty
          - while `in` is not empty
          - push top of `in` to `out`
          - pop `in`
      - return `out.top()`
  - for empty() return true if both stacks are empty.
 ```cpp
 class MyQueue {
public:
    stack<int>in,out;
    
    MyQueue() {
        
    }
    
    void push(int x) {
        in.push(x);
    }
    
    int pop() {
        peek();
        int val = out.top();
        out.pop();
        return val;
    }
    
    int peek() {
        if(out.empty()){
            while(!in.empty()){
                out.push(in.top());
                in.pop();
            }
        }
        return out.top();
    }
    
    bool empty() {
        return in.empty() && out.empty();
    }
};
```
    
</details>  


<details>
  <summary>Next Greater Element I</summary>

  [Link](https://leetcode.com/problems/next-greater-element-i/)
  
-----

   **Optimal:**

  - use a stack and a hashmap, iterate through each int in nums2 from start to end.
  - for each element see top of stack, if empty then add -1 to that int in mpp
  - if top < nums2[i] then keep poping till top < nums2[i]
  - then add that int to map <nums2[i], it> and to stack
  - now that we have next greater element for elements in nums2, we go through all elements in nums1 and take out the next greater element for each through map and push it in array and return the ans.
 ```java
       class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Stack<Integer> st = new Stack<>();
        Map<Integer, Integer> mpp = new HashMap<>();
        int[] ans = new int[nums1.length];
        for(int i=nums2.length-1;i>=0;i--){
            while(!st.isEmpty() && st.peek()<= nums2[i]){
                st.pop();
            }
            if(st.isEmpty()){
                mpp.put(nums2[i],-1);
            }
            else mpp.put(nums2[i], st.peek());
            st.push(nums2[i]);
        }
        int i=0;
        for(int it: nums1){
            ans[i] = mpp.get(it);
            i++;
        }
        return ans;
    }
}
```
  </details>  
  
