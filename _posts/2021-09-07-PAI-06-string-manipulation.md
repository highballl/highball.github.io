---
title: "파이썬 알고리즘 인터뷰 06 문자열 조작"
layout: posts
permalink: categories/:categories/:title
categories:
  - Algorithm
tags:
  - Algorithm
  - Python
  - LEETCODE
#date: 2021-09-08T00:15:00
toc: true
---

`last update: 2021.09.08.WED` 


# 06-문자열 조작 | string manipulation

## 01 유효한 팰린드롬

### LEET CODE 125. Valid Palindrome

- 내 풀이(210906 MON) - `deque`

    [https://github.com/highballl/PythonAlgorithmInterview/blob/main/06_string_manipulation/01_valid_palindrome.py](https://github.com/highballl/PythonAlgorithmInterview/blob/main/06_string_manipulation/01_valid_palindrome.py)

    - code

        ```python
        from collections import deque
        import sys
        sentence = sys.stdin.readline().strip().lower()

        special_char = "\"\'[!@#$%^&*:()\,]"
        new_sentence = deque([])
        for word in sentence:
            new_word = word.lower()
            for char in new_word:
                if char in special_char or char == ' ':
                    pass
                else:
                    new_sentence.append(char)

        def is_valid(sentence):
            while new_sentence:
                left = new_sentence.popleft()
                if new_sentence:
                    right = new_sentence.pop()
                    if left == right:
                        pass
                    else:
                        return "false"
                        
            return "true"

            
        print(is_valid(new_sentence))
        ```

    ⇒ 해설 `3) 슬라이싱`으로 개선 가능

### 해설

- 1) 리스트

- 2) deque

- 3) slicing

- 100jun, gold1, 1053번 - 팰린드롬 공장


## 02  문자열 뒤집기

### LEET CODE 344. Reverse String

[https://leetcode.com/problems/reverse-string/](https://leetcode.com/problems/reverse-string/)

- 내 풀이(210906 MON) - `reverse()`
    - Leetcode ver

        Not yet

    - 로컬 확인용 코드

        [https://github.com/highballl/PythonAlgorithmInterview/blob/main/06_string_manipulation/02_reverse_str.py](https://github.com/highballl/PythonAlgorithmInterview/blob/main/06_string_manipulation/02_reverse_str.py)

        - code

            ```python
            input_list = ["h","e","l","l","o"]
            input_list.reverse()
            print(input_list)

            input_str = "hello"
            print(input_str[::-1])
            ```

### 해설

- 01 | 투 포인터를 이용한 스왑

- 02 | 파이썬다운 방식

  

## 03 로그파일 재정렬

### LEET CODE 937. Reorder Log Files

[https://leetcode.com/problems/reorder-data-in-log-files/](https://leetcode.com/problems/reorder-data-in-log-files/)

- 내 풀이(210907 TUE) - `lambda`
    - Leetcode ver

        [https://github.com/highballl/LEETCODE/blob/main/937_reorder_log_files.py](https://github.com/highballl/LEETCODE/blob/main/937_reorder_log_files.py)

        - code

            ```python
            Success
            Details 
            Runtime: 36 ms, faster than 74.40% of Python3 online submissions for Reorder Data in Log Files.
            Memory Usage: 14.5 MB, less than 37.68% of Python3 online submissions for Reorder Data in Log Files.

            Runtime: 40 ms, faster than 46.89% of Python3 online submissions for Reorder Data in Log Files.
            Memory Usage: 14.4 MB, less than 66.29% of Python3 online submissions for Reorder Data in Log Files.

            class Solution:
                def reorderLogFiles(self, logs: List[str]) -> List[str]:
                    digit = []
                    letter = []
                    count = 0
                    for log in logs:
                        for string in log:
                            if string == " ":
                                idx = log.index(string)
                                break
                        identifier = log[:idx]
                        rest = log[idx:]
                        rest_check = ''.join(rest.split())
               
                        if rest_check.isdigit():
                            digit.append(identifier+rest)
                        else:
                            letter.append([identifier, rest])
                            count += 1

                    sorted_letter = sorted(letter, key=lambda x: (x[1], x[0]))
                    letter = [sorted_letter[i][0]+sorted_letter[i][1] for i in range(count)]

                    return [*letter, *digit]
            ```

    - 로컬 확인용 코드

        [https://github.com/highballl/PythonAlgorithmInterview/blob/main/06_string_manipulation/03_reorder_data_in_log_files.py](https://github.com/highballl/PythonAlgorithmInterview/blob/main/06_string_manipulation/03_reorder_data_in_log_files.py)

### 해설

- 람다와 + 연산자를 이용


## 04 가장 흔한 단어

### LEET CODE 819. Most Common Word

[https://leetcode.com/problems/most-common-word/](https://leetcode.com/problems/most-common-word/)

- 내 풀이(210907 TUE) - `Counter` `regex` `re.sub('[^\w]', ' ', paragraph)`
    - Leetcode ver

        [https://github.com/highballl/LEETCODE/blob/main/819_most_common_word.py](https://github.com/highballl/LEETCODE/blob/main/819_most_common_word.py)

        - code

            ```python
            Runtime: 32 ms, faster than 88.30% of Python3 online submissions for Most Common Word.
            Memory Usage: 14.4 MB, less than 20.65% of Python3 online submissions for Most Common Word.

            from collections import Counter
            import re

            class Solution:
                def mostCommonWord(self, paragraph: str, banned: List[str]) -> str:
                    
                    result = []
                    words = [word for word in re.sub('[^\w]', ' ', paragraph).lower().split()]
                    for word in words:
                        if word not in banned:
                            result.append(word)

                    counter_word = Counter(result)
                    return counter_word.most_common(1)[0][0]
            ```

    - 로컬 확인용 코드

        [https://github.com/highballl/PythonAlgorithmInterview/blob/main/06_string_manipulation/04_most_common_word.py](https://github.com/highballl/PythonAlgorithmInterview/blob/main/06_string_manipulation/04_most_common_word.py)

### 해설

- 리스트 컴프리헨션, Counter 객체 사용


## 05 그룹 에너그램

### LEET CODE 49. Group Anagrams

[https://leetcode.com/problems/group-anagrams/](https://leetcode.com/problems/group-anagrams/)

- 내 풀이(210907 TUE) -
    - Leetcode ver

        [https://github.com/highballl/LEETCODE/blob/main/49_group_anagrams.py](https://github.com/highballl/LEETCODE/blob/main/49_group_anagrams.py)

        - code

            ```python
            Success
            Details 
            Runtime: 1672 ms, faster than 5.00% of Python3 online submissions for Group Anagrams.
            Memory Usage: 19.9 MB, less than 12.45% of Python3 online submissions for Group Anagrams.

            from collections import Counter

            class Solution:
                def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
                    
                    if strs == [""]:
                        return [[""]]
                    
                    temp = [ []*i for i in range(len(strs))]
                    counts = []
                    result = []
                    
                    for word in strs:
                        count = Counter(word)
                        if count not in counts:
                            counts.append(count)
                            idx = counts.index(count)
                            temp[idx].append(word)
                        else:
                            idx = counts.index(count)
                            temp[idx].append(word)

                    for arr in temp:
                        if len(arr) != 0:
                            result.append(arr)
                    
                    return result
            ```

    - Local ver

        [https://github.com/highballl/PythonAlgorithmInterview/blob/main/06_string_manipulation/05_group_anagrams.py](https://github.com/highballl/PythonAlgorithmInterview/blob/main/06_string_manipulation/05_group_anagrams.py)

        - code

            ```python
            from collections import Counter

            strs = ["eat","tea","tan","ate","nat","bat"]

            if strs == [""]:
                print([[""]])
                    
            temp = [ []*i for i in range(len(strs))]
            counts = []
            result = []
                    
            for word in strs:
                count = Counter(word)
                if count not in counts:
                    counts.append(count)
                    idx = counts.index(count)
                    temp[idx].append(word)
                else:
                    idx = counts.index(count)
                    temp[idx].append(word)

            for arr in temp:
                if len(arr) != 0:
                    result.append(arr)

            print(result)
            ```

### 해설

- 정렬하여 딕셔너리에 추가 - `defaultdict(list)`



