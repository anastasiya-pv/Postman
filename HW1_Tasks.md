# Homework 2
***
### Exercise 1  
http://162.55.220.72:5005
**Method: GET  
EndPoint: /get_method**

**Request url params:   
 name: str  
 age: int**
![Exercise_1](https://github.com/anastasiya-pv/Testing/blob/main/Screenshots/1.png)

**Resp:**
```
[
    “Str”,
    “Str”
]
```
---
### Exercise 2 
http://162.55.220.72:5005  
**Method: POST  
EndPoint: /user_info_3** 

**Request form data:   
 name: str  
 age: int  
 salary: int**  
 ![Exercise_2](https://github.com/anastasiya-pv/Testing/blob/main/Screenshots/2.png)
 
**Resp:**
```
{'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'u_salary_1_5_year': salary * 4}}
```
---
### Exercise 3
http://162.55.220.72:5005
**Method: GET  
EndPoint: /object_info_1**

**Request url params:   
 name: str  
 age: int  
 weight: int**  
![Exercise_3](https://github.com/anastasiya-pv/Testing/blob/main/Screenshots/3.png)

**Resp:**
```
{'name': name,
          'age': age,
          'daily_food': weight * 0.012,
          'daily_sleep': weight * 2.5}
```
---
### Exercise 4
http://162.55.220.72:5005
**Method: GET  
EndPoint: /object_info_2**  

**Request url params:   
 name: str  
 age: int  
 salary: int**  
 ![Exercise_4](https://github.com/anastasiya-pv/Testing/blob/main/Screenshots/4.png)
 
**Resp:**
```
{'start_qa_salary': salary,
          'qa_salary_after_6_months': salary * 2,
          'qa_salary_after_12_months': salary * 2.7,
          'qa_salary_after_1.5_year': salary * 3.3,
          'qa_salary_after_3.5_years': salary * 3.8,
          'person': {'u_name': [user_name, salary, age],
                     'u_age': age,
                     'u_salary_5_years': salary * 4.2}
          }
```
---
### Exercise 5
http://162.55.220.72:5005
**Method: GET  
EndPoint: /object_info_3**  

**Request url params:  
 name: str  
 age: int  
 salary: int**  
![Exercise_5](https://github.com/anastasiya-pv/Testing/blob/main/Screenshots/5.png)

**Resp:**
```
{'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'pets': {'cat':{'name':'Sunny',
                                     'age': 3},
                              'dog':{'name':'Luky',
                                     'age': 4}},
                     'u_salary_1_5_year': salary * 4}
          }
```
---
### Exercise 6
http://162.55.220.72:5005
**Method: GET  
EndPoint: /object_info_4**

**Request url params:   
 name: str  
 age: int  
 salary: int**  
 ![Exercise_6](https://github.com/anastasiya-pv/Testing/blob/main/Screenshots/6.png)
 
**Resp:**
```
{'name': name,
          'age': int(age),
          'salary': [salary, str(salary * 2), str(salary * 3)]}
```
---
### Exercise 7
**Method: POST  
EndPoint: /user_info_2**  

**Request form data:   
 name: str  
 age: int  
 salary: int**  
![Exercise_7](https://github.com/anastasiya-pv/Testing/blob/main/Screenshots/7.png)

**Resp:**
```
{'start_qa_salary': salary,
          'qa_salary_after_6_months': salary * 2,
          'qa_salary_after_12_months': salary * 2.7,
          'qa_salary_after_1.5_year': salary * 3.3,
          'qa_salary_after_3.5_years': salary * 3.8,
          'person': {'u_name': [user_name, salary, age],
                     'u_age': age,
                     'u_salary_5_years': salary * 4.2}
          }
```
