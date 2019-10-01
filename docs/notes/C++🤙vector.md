---
tags: [Notebooks/QT_C++]
title: "C++\U0001F919vector"
created: '2019-09-28T16:16:04.570Z'
modified: '2019-09-29T04:35:42.864Z'
---

# C++:call_me_hand:vector

<details>
<summary>vector查找元素</summary>
<markdwon>

```cpp
std::vector<int> arr = {5,4,3,2,1};
int ele = 1;
std::vector<int>::iterator result = std::find(arr.begin(), arr.end(), ele);

if (result != arr.end())
{
    for (std::vector<int>::iterator it = arr.begin(); it != result; it++)
    {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    for (std::vector<int>::iterator it = result+1; it != arr.end(); it++)
    {
        std::cout << *it << " ";
    }
    std::cout  << std::endl;
}
```
</markdown>
</details>


<details>
<summary>sub</summary>
<markdown>
```cpp
vector<T>::const_iterator first = myVec.begin() + 100000;
vector<T>::const_iterator last = myVec.begin() + 101000;
vector<T> newVec(first, last);
```

</markdown>
</details>

<details>
<summary>front</summary>
<markdown>
l
</markdown>
</details>
