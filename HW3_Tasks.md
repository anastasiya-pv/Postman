# Homework 3
***
### Exercise 1
http://162.55.220.72:5005/login<br>
**Method: POST(form-data)**<br>
**login : str (кроме /)**<br>
**password : str**<br>
- **Приходящий токен необходимо передать во все остальные запросы**
---
### Exercise 2
http://162.55.220.72:5005/user_info<br>
**Method: POST(raw→JSON)<br>
POST<br>
age: int<br>
salary: int<br>
name: str<br>
auth_token**

**Resp:**
```
{'start_qa_salary':salary,
 'qa_salary_after_6_months': salary * 2,
 'qa_salary_after_12_months': salary * 2.9,
 'person': {'u_name':[user_name, salary, age],
                                'u_age':age,
                                'u_salary_1.5_year': salary * 4}
                                }
```
- **Статус код 200**
- **Проверка структуры json в ответе**
- **В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент**
- **Достать значение из поля 'u_salary_1.5_year' и передать в поле salary запроса http://162.55.220.72:5005/get_test_user**
---
### Exercise 3
http://162.55.220.72:5005/new_data<br>
**Method: POST(form-data)**<br>
**age: int<br>
salary: int<br>
name: str<br>
auth_token**<br>

**Resp:**
```
{'name':name,
  'age': int(age),
  'salary': [salary, str(salary*2), str(salary*3)]}
  ```
- **Статус код 200**
- **Проверка структуры json в ответе**
- **В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент**
- **Проверить, что 2-й элемент массива salary больше 1-го и 0-го**
---
### Exercise 4
http://162.55.220.72:5005/test_pet_info<br>
**Method: POST(form-data)**<br>
**age: int<br>
weight: int<br>
name: str<br>
auth_token**<br>
**Resp:**
```
{'name': name,
 'age': age,
 'daily_food':weight * 0.012,
 'daily_sleep': weight * 2.5}
```
- **Статус код 200**
- **Проверка структуры json в ответе**
- **В ответе указаны коэффициенты умножения weight, напишите тесты по проверке правильности результата перемножения на коэффициент**
---
### Exercise 5
http://162.55.220.72:5005/get_test_user<br>
**Method: POST(form-data)**<br>
**age: int<br>
salary: int<br>
name: str<br>
auth_token**<br>
**Resp:**
```
{'name': name,
 'age':age,
 'salary': salary,
 'family':{'children':[['Alex', 24],['Kate', 12]],
 'u_salary_1.5_year': salary * 4}
  }
  ```
- **Статус код 200**
- **Проверка структуры json в ответе**
- **Проверить что занчение поля name = значению переменной name из окружения**
- **Проверить что занчение поля age в ответе соответсвует отправленному в запросе значению поля age**
