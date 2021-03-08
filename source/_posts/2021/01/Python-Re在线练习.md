---
title: Python-Re在线练习
tags:
  - re
  - Python
categories: Python
abbrlink: 37238
date: 2021-01-12 10:42:37
---

###  Python-Re在线练习

+ 在线网站: <a href="https://regexone.com/lesson/letters_and_digits?">前往练习</a>

+ 规则

  ```bash
  Lesson Notes
  abc…	Letters
  123…	Digits
  \d	Any Digit
  \D	Any Non-digit character
  .	Any Character
  \.	Period
  [abc]	Only a, b, or c
  [^abc]	Not a, b, nor c
  [a-z]	Characters a to z
  [0-9]	Numbers 0 to 9
  \w	Any Alphanumeric character
  \W	Any Non-alphanumeric character
  {m}	m Repetitions
  {m,n}	m to n Repetitions
  *	Zero or more repetitions
  +	One or more repetitions
  ?	Optional character
  \s	Any Whitespace
  \S	Any Non-whitespace character
  ^…$	Starts and ends
  (…)	Capture Group
  (a(bc))	Capture Sub-group
  (.*)	Capture all
  (abc|def)	Matches abc or def
  ```

  

###  基础练习

####  或 ：

+ 练习一

  | Task  |     Text     |
  | :---: | :----------: |
  | Match |  abc123xyz   |
  | Match | define"123"  |
  | Match | var g =  123 |

  {% hideBlock 查看 %}

  个人: `[a-z]+ | \s [\d]+ | ["123"]`

  {% endhideBlock %}

+ 练习二

  | Task  | Text |
  | :---: | :--: |
  | Match | cat. |
  | Match | 896. |
  | Match | ?=+. |
  | Skip  | abc1 |

  {% hideBlock 查看 %}

  答案: `...\.`

  {% endhideBlock %}

+ 练习三

  | Task  | Text |
  | :---: | :--: |
  | Match | can  |
  | Match | man  |
  | Match | fan  |
  | Skip  | dan  |
  | Skip  | ran  |
  | Skip  | pan  |

  {% hideBlock 查看 %}

  理解:  `Skip是排除在外的`

  个人答案: `[cmf]an`

  {% endhideBlock %}

+ 练习三

  | Task  | Text |
  | :---: | :--: |
  | Match | hog  |
  | Match | dog  |
  | Skip  | bog  |

  {% hideBlock 查看 %}

  个人答案: `[hd]og`

  {% endhideBlock %}

####  非:

+ 练习一

  | Task  | Text |
  | :---: | :--: |
  | Match | Ana  |
  | Match | Bob  |
  | Match | Cpc  |
  | Skip  | aax  |
  | Skip  | bby  |
  | Skip  | ccz  |

  {% hideBlock 查看 %}

  个人答案:  [^(a-c)]

  {% endhideBlock %}

+ 练习二

  | Task  |  Text   |
  | :---: | :-----: |
  | Match | aaaabcc |
  | Match | aabbbbc |
  | Match |  aacc   |
  | Skip  |    a    |

  {% hideBlock 查看 %}

  个人答案:  `a*b*c`

  {% endhideBlock %}