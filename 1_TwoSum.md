# 1. Two Sum

[Question Link](https://leetcode.com/problems/two-sum)

## 1. Problem Understanding
- **Problem Statement:**
  - Summarize the problem in your own words.
    > We are given two inputs those are `nums` which is a list of integers 
    and `target` which is an integer value, There are two elements that
    sum equal to `target`. Hence, we need to know which are 
    these element's indices.

  - Identify the key inputs and outputs.
    > We are given a list of integers and an integer 
    that the `nums` and the `target` respectively as inputs.

    > We should return a list of integers whose length should be 2 as output. 
    The result list's ordering does not matter.

- **Constraints:**
  - Note size, range, or special constraints.
    > 2 ≤ nums.len ≤ 10⁴, -10⁹ ≤ nums[i] ≤ 10⁹, -10⁹ ≤ target ≤ 10⁹ 

    > We can't use same element twice. That is, if we are given input, 
    for example `nums=[4, 2, 3]` and `target=6`, then we can't use the `3` twice.

    > Only one valid answer exists. That is, there ain't possible to have
    multiple elements whose sum is equivalent to `target`.

    > There are no invalid inputs and outputs. 
    The inputs and solution are always guaranteed.
     
- **Goal:**
  - Define the expected result or behaviour.
    > For the input `nums=[2, 7, 11, 15]`, `target=9`, the output is
    `[0, 1]`. Because `nums[0]+nums[1] == 9`, we return `[0, 1]`.
    
    > For the input `nums=[3, 2, 4]`, `target=6`, the output is
    `[1, 2]`. Because `nums[1]+nums[2] == 6`, we return `[1, 2]`.

---

## 2. Observations and Exploration
- **Patterns and Properties:**
  - What patterns or relationships do you notice?
    > In this case, question is very straightforward. Therefore, I didn't notice any patterns. 

- **Edge Cases:**
  - Consider scenarios like empty inputs, smallest/largest values, repeated values, etc.
    > Question ensures some boundaries that won't happen. Hence, there are no 
    extreme scenarios.

- **Assumptions:**
  - List any assumptions based on constraints.
    > Write here

---

## 3. Detailed Plan
- **Potential Methods:**
  - List possible algorithms or techniques (e.g., brute force, divide and conquer, greedy, etc.).
    > There are couple of algorithms in order to reach answer. Those are:
    `brute-force` and `hashmap`.

- **Trade-offs:**
  - Analyze time complexity, space complexity, and simplicity of each approach.
    > For brute-force, in the worst-case scenario, we iterate over the lists and
    look the value pairs for each of element. In the light of the knowledge, the time complexity will
    become `O(n²)`. Since, we take an element and iterate the each elements and perform the calculation over and over again 
    until reach to end of the list. As for implementation, we will just write nested loops and there is
    no further space occupation. Therefore, the space complexity will be `O(1)`.

    > For hashmap, in the worst-case scenario, our result could be at the end of the list. 
    In the light of the knowledge, the time complexity will become `O(n)`. 
    Since, we will iterate until reach to end of the list. As for implementation, there is no
    ambigious implementation. We just need extra `hashmap` structure and the structure can effect to
    space complexity. Therefore, the complexity will be `O(n)` if the all elements are unique and our answer
    is at the end of the list.

- **Chosen Approach:**
  - Which approach will you use? Why?
    > I will use both approach in order to show comparison of two solution.
    Further, I will implement the algorithm with use functional programming paradigm.

- **Step-by-Step Solution:**
  - Write pseudocode or a high-level breakdown.
    1. Brute-Force
    ```
    loop i=0; A.len-1
        loop j=i+1; A.len
            return [i, j] when A[i] + A[j] = t
            otherwise continue
    ```

    2. Hashmap
    ```
    define hmap<value: int, index: int>
    loop i=0; A.len
        scan hmap for (t - A[i]) if match
            case some(x) => return [i, x]
            case _       => add (A[i], i) into hmap
    ```

---

## 4. Implementation
- **Code:**
    1. Brute-Force
        ```scala
        def twoSum(nums: Array[Int], target: Int): Array[Int] = {
            var i = 0
            var j = 0

            while (i < nums.size - 1) {
                j = i+1
                while (j < nums.size) {
                    if (nums(i) + nums(j) == target) {
                        return Array(i, j)
                    } else {
                        j += 1
                    }
                }

                i += 1
            }

            Array.empty[Int]
        }
        ```

    2. Hashmap
        ```scala
        def twoSum(nums: Array[Int], target: Int): Array[Int] = {
            val hmap = scala.collection.mutable.Map.empty[Int, Int]
            var i = 0
            while (i < nums.size) {
                hmap.get(target - nums(i)) match {
                    case Some(ii) => return Array(ii, i)
                    case _        => hmap += (nums(i) -> i)
                }

                i += 1
            }

            Array.empty[Int]
        }

        // (with recursion)
        def twoSum(nums: Array[Int], target: Int): Array[Int] = {
            import scala.collection.mutable.Map

            @scala.annotation.tailrec
            def loop(i: Int, hmap: Map[Int, Int]): Array[Int] = {
                if (i >= nums.size) Array.empty[Int]
                else {
                    hmap.get(target - nums(i)) match {
                        case Some(ii) => return Array(ii, i)
                        case _ => loop(i+1, hmap += (nums(i) -> i))
                    }
                }
            }

            loop(0, Map.empty[Int, Int])
        }
        ```
- **Comments:**
  - Add meaningful comments to explain critical parts of the code.
    > Both implementations are purely functional. I used a variable but
    it doesn't violate the functional programming paradigm. I can
    use recursion instead of while-loop in order to do not use
    variables. Eventually, they will compile same byte code so it doesn't
    matter.

- **Error Handling:**
  - Include checks for edge cases or invalid inputs if necessary.
    > Write here

---
