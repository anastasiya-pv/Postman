HW_2 Postman
========================

http://162.55.220.72:5005/first
1. Отправить запрос.
2. Статус код 200
3. Проверить, что в body приходит правильный string. - This is the first responce from server!
```
//Статус код 200
pm.test("Status code is 200", function(){
    pm.response.to.have.status(200);
});
//Проверить, что в body приходит правильный string. - 
pm.test("Body is correct", function(){
    pm.response.to.have.body("This is the first responce from server!")
});
```


http://162.55.220.72:5005/user_info_3
1. Отправить запрос. +
2. Статус код 200 +
3. Спарсить response body в json. +
4. Проверить, что name в ответе равно name s request (name вбить руками.) +
5. Проверить, что age в ответе равно age s request (age вбить руками.) +
6. Проверить, что salary в ответе равно salary s request (salary вбить руками.) +
7. Спарсить request.
8. Проверить, что name в ответе равно name s request (name забрать из request.)
9. Проверить, что age в ответе равно age s request (age забрать из request.)
10. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
11. Вывести в консоль параметр family из response.
12. Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)
```
//Статус код 200 +
pm.test("Status code is 200", function(){
    pm.response.to.have.status(200);
});
//Спарсить response body в json. +
let jsonData=pm.response.json()
//Проверить, что name в ответе равно name s request (name вбить руками.) 
pm.test("Name is equal to typed name from request", function(){
    pm.expect(jsonData.name).to.eql("Nastya");
});
//Проверить, что age в ответе равно age s request (age вбить руками.). Age from response is  "string"
let age=+jsonData.age
pm.test("Age is equal to typed age from request", function(){
    pm.expect(age).to.eql(26);
});
//Проверить, что salary в ответе равно salary s request (salary вбить руками.). Salary from response is number
pm.test("Salary is equal to typed salary from request", function(){
    pm.expect(jsonData.salary).to.eql(600);
});
//Спарсить request
let post_form_data = request.data
//Проверить, что name в ответе равно name s request (name забрать из request.)
pm.test("Name from resp is equal to name from req", function(){
    pm.expect(jsonData.name).to.eql(post_form_data.name);
});
//Проверить, что age в ответе равно age s request (age забрать из request.). Age from response and age from requst are "strings"
pm.test("Age from resp is equal to age from req", function(){
    pm.expect(jsonData.age).to.eql(post_form_data.age);
});
//Проверить, что salary в ответе равно salary s request (salary забрать из request.). Salary from response is number while salary from request is "string"
salary=+post_form_data.salary
pm.test("Salary from resp is equal to salary from req", function(){
    pm.expect(jsonData.salary).to.eql(salary);
});
//Вывести в консоль параметр family из response.
console.log(jsonData.family)
//Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)
pm.test("u_salary_1_5_year from resp is eql to salary from req * 4", function(){
    pm.expect(jsonData.family.u_salary_1_5_year).to.eql(salary*4);
});
```


http://162.55.220.72:5005/object_info_3
1. Отправить запрос.
2. Статус код 200
3. Спарсить response body в json.
4. Спарсить request.
5. Проверить, что name в ответе равно name s request (name забрать из request.)
6. Проверить, что age в ответе равно age s request (age забрать из request.)
7. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
8. Вывести в консоль параметр family из response.
9. Проверить, что у параметра dog есть параметры name.
10. Проверить, что у параметра dog есть параметры age.
11. Проверить, что параметр name имеет значение Luky.
12. Проверить, что параметр age имеет значение 4.
```
//Статус код 200
pm.test("Status code is 200", function(){
    pm.response.to.have.status(200);
});
//Спарсить response body в json.
let jsonData=pm.response.json()
//Спарсить request.
let get_params=pm.request.url.query.toObject()
//Проверить, что name в ответе равно name s request (name забрать из request.)
pm.test("Name from resp is eql to name from req", function(){
    pm.expect(jsonData.name).to.eql(get_params.name);
});
//Проверить, что age в ответе равно age s request (age забрать из request.)JsonData.age and get_params.age are "string"
pm.test("Age from resp is eql to age from req", function(){
    pm.expect(jsonData.age).to.eql(get_params.age);
});

//Проверить, что salary в ответе равно salary s request (salary забрать из request).Salary from response is number while salary from request is "string"
let salary=+get_params.salary
pm.test("Salary from resp is eql to salary from req", function(){
    pm.expect(jsonData.salary).to.eql(salary);
});
//Вывести в консоль параметр family из response.
console.log(jsonData.family)
//Проверить, что у параметра dog есть параметры name.
pm.test("Parameter \"Dog\" has property\"name\"", function(){
    pm.expect(jsonData.family.pets.dog).to.have.property("name");
});
//Проверить, что у параметра dog есть параметры age.
pm.test("Parameter \"Dog\" has property\"age\"", function(){
    pm.expect(jsonData.family.pets.dog).to.have.any.keys("age");
});
//Проверить, что параметр name имеет значение Luky.
pm.test("Parameter \"name\ is Luky", function(){
    pm.expect(jsonData.family.pets.dog.name).to.eql("Luky");
});
//Проверить, что параметр age имеет значение 4.
pm.test("Parameter \"age\" is 4", function() {
   pm.expect(jsonData.family.pets.dog.age).to.eql(4);
});
```

http://162.55.220.72:5005/object_info_4
1. Отправить запрос.
2. Статус код 200
3. Спарсить response body в json.
4. Спарсить request.
5. Проверить, что name в ответе равно name s request (name забрать из request.)
6. Проверить, что age в ответе равно age из request (age забрать из request.)
7. Вывести в консоль параметр salary из request.
8. Вывести в консоль параметр salary из response.
9. Вывести в консоль 0-й элемент параметра salary из response.
10. Вывести в консоль 1-й элемент параметра salary параметр salary из response.
11. Вывести в консоль 2-й элемент параметра salary параметр salary из response.
12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)
13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)
14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)
15. Создать в окружении переменную name
16. Создать в окружении переменную age
17. Создать в окружении переменную salary
18. Передать в окружение переменную name - 
19. Передать в окружение переменную age
20. Передать в окружение переменную salary
21. Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.
```
//Статус код 200
pm.test("Status code is 200", function(){
    pm.response.to.have.status(200);
});
//Спарсить response body в json.
let jsonData=pm.response.json()
//Спарсить request
let get_params=pm.request.url.query.toObject()
//Проверить, что name в ответе равно name s request (name забрать из request.)
pm.test("Name from resp is eql to name from req", function(){
    pm.expect(jsonData.name).to.eql(get_params.name);
});
//Проверить, что age в ответе равно age из request (age забрать из request.Age from resp is number while age from req is string.
let age= +get_params.age
pm.test("Age from resp is eql to age from req", function(){
    pm.expect(jsonData.age).to.eql(age);
});
//Вывести в консоль параметр salary из request.
console.log(get_params.salary)
//Вывести в консоль параметр salary из response.
console.log(jsonData.salary)
//Вывести в консоль 0-й элемент параметра salary из response.
console.log(jsonData.salary[0])
//Вывести в консоль 1-й элемент параметра salary параметр salary из response.
console.log(jsonData.salary[1])
//Вывести в консоль 2-й элемент параметра salary параметр salary из response.
console.log(jsonData.salary[2])
//Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.).The salary[0] from response is number while  salary from request is string. 
salary=+get_params.salary
pm.test("Salary[0] is eql to salary from req", function(){
    pm.expect(jsonData.salary[0]).to.eql(salary);
});
//Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)The salary[1] from response and the  salary from request are strings. 
let resp_salary=+jsonData.salary[1]
pm.test("Salary[1] is eql to salary*2 from req", function(){
    pm.expect(resp_salary).to.eql(salary*2);
});
//Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)The salary[2] from response and the  salary from request are strings. 
let resp_salary_2=+jsonData.salary[2]
pm.test("Salary[2] is eql to salary*3 from req", function(){
    pm.expect(resp_salary_2).to.eql(salary*3);
});
// Создать в окружении переменную name
pm.environment.set("name", get_params.name);
// Создать в окружении переменную age
pm.environment.set("age", get_params.age);
// Создать в окружении переменную salary
pm.environment.set("salary", get_params.salary);

//Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.
for(let i=0;i < jsonData.salary.length; i++)
console.log(jsonData.salary[i])
//or
jsonData.salary.forEach(element => (
    console.log(element)));
```


http://162.55.220.72:5005/user_info_2
1. Вставить параметр salary из окружения в request – {{salary}}
2. Вставить параметр age из окружения в age-{{age}}
3. Вставить параметр name из окружения в name-{{name}}
4. Отправить запрос.
5. Статус код 200
6. Спарсить response body в json.
7. Спарсить request.
8. Проверить, что json response имеет параметр start_qa_salary
9. Проверить, что json response имеет параметр qa_salary_after_6_months
10. Проверить, что json response имеет параметр qa_salary_after_12_months
11. Проверить, что json response имеет параметр qa_salary_after_1.5_year
12. Проверить, что json response имеет параметр qa_salary_after_3.5_years
13. Проверить, что json response имеет параметр person
14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)
15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)
16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)
17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)
18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)
19. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)
20. Проверить, что что параметр u_age равен age из request (age забрать из request.)
21. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)
22. ***Написать цикл который выведет в консоль по порядку элементы списка из параметра person.

```
//Статус код 200
pm.test("status code is 200", function(){
    pm.response.to.have.status(200);
});
//Спарсить response body в json.
let jsonData = pm.response.json()
//Спарсить request
let post_form_data = request.data
//Проверить, что json response имеет параметр start_qa_salary
pm.test("Response has propetry start_qa_salary", function(){
    pm.expect(jsonData).to.have.property("start_qa_salary");
});
//Проверить, что json response имеет параметр qa_salary_after_6_months
pm.test("Response has propetry qa_salary_after_6_months", function(){
    pm.expect(jsonData).to.have.property("qa_salary_after_6_months");
});
//Проверить, что json response имеет параметр qa_salary_after_12_months
pm.test("Response has propetry qa_salary_after_12_months", function(){
    pm.expect(jsonData).to.have.property("qa_salary_after_12_months");
});
//Проверить, что json response имеет параметр qa_salary_after_1.5_year

pm.test("Response has propetry qa_salary_after_1.5_year", function(){
    pm.expect(jsonData).to.have.property("qa_salary_after_1.5_year");
});
//Проверить, что json response имеет параметр qa_salary_after_3.5_years
pm.test("Response has propetry qa_salary_after_3.5_years", function(){
    pm.expect(jsonData).to.have.property("qa_salary_after_3.5_years");
});
//Проверить, что json response имеет параметр person
pm.test("Response has person", function(){
pm.expect(jsonData).to.have.any.keys("person");
});
//Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)Salary from req is string while start_qa_salary is number
let salary = +post_form_data.salary
pm.test("start_qa_salary from resp is eql to salary from req", function(){
    pm.expect(jsonData.start_qa_salary).to.eql(salary);
});
//Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)Salary from req is string while start_qa_salary is number
pm.test("qa_salary_after_6_months from resp is eql to salary from req", function(){
    pm.expect(jsonData.qa_salary_after_6_months).to.eql(salary*2);
});
//Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)
pm.test("qa_salary_after_12_months from resp is eql to salary from req", function(){
    pm.expect(jsonData.qa_salary_after_12_months).to.eql(salary*2.7);
});
// Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)
pm.test("qa_salary_after_1.5_year is equal to salary*3.3 from request", function(){
    pm.expect(jsonData["qa_salary_after_1.5_year"]).to.eql(salary*3.3);
});

//Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)
pm.test("qa_salary_after_3.5_years is equal to salary*3.8 from request", function(){pm.expect(jsonData["qa_salary_after_3.5_years"]).to.eql(salary*3.8);
});

//Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)
pm.test("u_name[1] is eql to salary from req", function(){
    pm.expect(jsonData.person.u_name[1]).to.eql(salary);
});

//Проверить, что что параметр u_age равен age из request (age забрать из request.). Age from req is string while age from resp is number. 

let age=+post_form_data.age
pm.test("u_age is eql to age from req", function(){
    pm.expect(jsonData.person.u_age).to.eql(age);
});

// Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)
pm.test("Check u_salary_5_years", function(){
    pm.expect(jsonData.person.u_salary_5_years).to.eql(salary*4.2);
});

////***Написать цикл который выведет в консоль по порядку элементы списка из параметра person.
for (let i = 0; i < jsonData.person.length; i++)
console.log(jsonData.person[i])
//or
Object.keys(jsonData.person).forEach(i => {
  console.log(i, jsonData.person[i]);
});
//or
for (const [key, value] of Object.entries(jsonData.person)) {
  console.log(`${key}: ${value}`);
};
```
