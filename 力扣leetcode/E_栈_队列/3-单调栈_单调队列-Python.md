#### �������С�����ջ

������·���ȷ������⣬�Ƿ�Ҫʹ�õ���ջ���������У���֪�����ݵı仯���̣��������д���й��ɵģ����������д��������ʮ��������

```python
1. ��ǰ��󣬱���ÿһ��Ԫ�� (��Ԫ��һ�������ջ/����)
	for r in range(size):
2. whileѭ��, ���ֵ�����
	2.1. while ѭ������ and ��Ŀ����
    		��[]���Ƴ������㵥���Ե�ջ��/��β����:pop(-1)
	2.2. ���� ����[] �󣬿�����Ҫ(������ + ��������)
3. ...
4. Ԫ�ؽ��� ����[]
	4.1. ������ ����[] �󣬿�����Ҫ(���½�� + ��������)
```



---



#### [��ָ Offer 59 - I. �������ڵ����ֵ](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

:small_airplane: ��������

```python
class Solution(object):
    def maxSlidingWindow(self, nums, k):
        size = len(nums)
        ans = []
        queue = []  # �������� (�ɴ�С), ����ˡ��±꡿
        for r in range(size):  # ѭ������
            # 1. ���ֶ��еĵ�����
            while queue and nums[r] > nums[queue[-1]]: # [5,3,2], ����4, Ҫ����ɾ��[2,3]
                queue.pop(-1)
            # 2. ɾ������ͷ��
            if queue and r-queue[0]+1 > k:  # ɾ��5
                queue.pop(0)
            # 3. Ԫ�������
            queue.append(r)
            # 4. ����������
            if r+1 >= k:
                ans.append(nums[queue[0]])  # ��ǰ���ڵ����ֵ: nums[queue[0]]
        return ans
```



#### [LeetCode ������59 - II. ���е����ֵ](https://segmentfault.com/a/1190000021962984):slightly_smiling_face:

Ҫ�󣺻�ȡ���е����ֵ��ʱ�临�Ӷ�ΪO(1)



---



------

:smile_cat:�������Ŀ���� `����ջ`

#### [739. ÿ���¶�](https://leetcode-cn.com/problems/daily-temperatures/):slightly_smiling_face:

```python
�����ÿ�������б���������һ���б���Ӧλ�õ����Ϊ��Ҫ��۲⵽���ߵ����£�������Ҫ�ȴ��������������������֮�󶼲������ߣ����ڸ�λ���� 0 �����档
���磬
	����һ���б� temperatures = [73, 74, 75, 71, 69, 72, 76, 73]
	������Ӧ���� [1, 1, 4, 2, 1, 1, 0, 0]��
```

ջ�д�ŵ�Ԫ�أ����±꣬����nums[i]

```python
class Solution(object):
    def dailyTemperatures(self, T):
        ans = [0] * len(T)  # ������[0, 0, 0, ... ...]
        stack = []  # ����ջ, ��š��±꡿
        for i in range(len(T)):
            while stack and T[stack[-1]] < T[i]:  # ջ���¶� < ��ǰ�¶�
                ans[stack[-1]] = i - stack[-1]    # ����ջʱ��, ����ջ��(�±�λ��)�Ľ��ֵ
                stack.pop()
            stack.append(i)
        return ans
```



#### [402. �Ƶ�Kλ����](https://leetcode-cn.com/problems/remove-k-digits/)

����һ�����ַ�����ʾ�ķǸ����� *num*���Ƴ�������е� *k* λ���֣�ʹ��ʣ�µ�������С��

```
����: num = "1432219", k = 3
���: "1219"
����: �Ƴ����������� 4, 3, �� 2 �γ�һ���µ���С������ 1219	��
```

ջ�д�ŵ�Ԫ���� num[i]�������±�

```python
class Solution(object):
    def removeKdigits(self, num, k):
        stack = []
        for e in num:
            while stack and stack[-1] > e and k:  # ����ջ (�෴)
                stack.pop()
                k -= 1
            stack.append(e)  # ʼ�ն�����ǰԪ�ؼ���ջ
        ret = stack[:-k] if(k > 0) else stack
        return "".join(ret).lstrip('0') or '0'  # ���stack��ʣ�µ�Ԫ�أ������������ǽ��
```



#### [496. ��һ������Ԫ�� I](https://leetcode-cn.com/problems/next-greater-element-i/)

�������� `û���ظ�Ԫ��` ������ nums1 �� nums2 ������nums1 �� nums2 ���Ӽ����ҵ� nums1 ��ÿ��Ԫ���� nums2 �е���һ��������ֵ��

nums1 ������ x ����һ������Ԫ����ָ x �� nums2 �ж�Ӧλ�õ��ұߵĵ�һ���� x ���Ԫ�ء���������ڣ���Ӧλ����� -1 ��

```
����: nums1 = [4,1,2], nums2 = [1,3,4,2].
���: [-1,3,-1]
����:
    ����num1�е�����4�����޷��ڵڶ����������ҵ���һ����������֣������� -1��
    ����num1�е�����1���ڶ�������������1�ұߵ���һ���ϴ������� 3��
    ����num1�е�����2���ڶ���������û����һ����������֣������� -1��
```



```python
class Solution(object):
    def nextGreaterElement(self, nums1, nums2):
        stack = []
        hash = {}
        for e in nums2:
            while stack != [] and stack[-1] < e:  # ����ջ
                hash[stack[-1]] = e  # ��<Ԫ��,��һ����Ԫ�ش��ֵ>���浽��ϣ��
                stack.pop()
            stack.append(e)
        ret = []
        for e in nums1: # ����ÿ��Ԫ�أ��ӹ�ϣ���������Ӧ�ĵ�һ���ϴ�ֵ
            if e in hash.keys():
                ret.append(hash[e])
            else:
                ret.append(-1)
        return ret
```



#### [503. ��һ������Ԫ�� II](https://leetcode-cn.com/problems/next-greater-element-ii/)

����һ��ѭ�����飨���һ��Ԫ�ص���һ��Ԫ��������ĵ�һ��Ԫ�أ������ÿ��Ԫ�ص���һ������Ԫ�ء����� x ����һ�������Ԫ���ǰ��������˳���������֮��ĵ�һ�������������������ζ����Ӧ��ѭ��������������һ�������������������ڣ������ -1��

```shell
����: [1,2,1]
���: [2,-1,2]
����: ��һ�� 1 ����һ����������� 2��
���� 2 �Ҳ�����һ����������� 
�ڶ��� 1 ����һ����������Ҫѭ�����������Ҳ�� 2��
```



```python
class Solution(object):
    def nextGreaterElements(self, nums):
        db_nums = nums * 2  # ����������ƴ��
        size = len(nums)    # ԭ���鳤��
        ret = [-1] * size   # ��ʼ�����[-1, -1, -1, ... ...]
        stack = []  # ջ (ջ�д�����±�)
        for i in range(size * 2):
            while stack != [] and db_nums[stack[-1]] < db_nums[i]:
                ret[stack[-1]] = db_nums[i]  # ��ջǮ��������
                stack.pop()
            if i < size: # ����ڵ㲻��ջ
                stack.append(i)
        return ret
```

