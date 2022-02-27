***HW_2 Postman***


http://162.55.220.72:5005/first
1. Отправить запрос.
2. Статус код 200
3. Проверить, что в body приходит правильный string. - This is the first responce from server!

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Body is correct", function () {
    pm.response.to.have.body("This is the first responce from server!");
});




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

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

var jsonData = pm.response.json()
let salary_response = +jsonData.salary
var age_response = +jsonData.age

pm.test("Check name", function () {
    pm.expect(jsonData.name).to.eql("Nastya");
});

pm.test("Check age_response", function () {
    pm.expect(age_response).to.eql(26);
});

pm.test("Check salary", function () {
    pm.expect(jsonData.salary).to.eql(600);
});

var request = request.data

pm.test("The name in request is equal to the name in response", function () {
    pm.expect(jsonData.name).to.eql(request.name);
});

var request_age = +request.age
pm.test("The age in requset is equal to the age in response", function () {
    pm.expect(age_response).to.eql(request_age);
});
var request_salary= +request.salary
pm.test("The salary in requset is equal to the salary in response", function () {
    pm.expect(salary_response).to.eql(request_salary);
});
console.log(jsonData.family)

var salary_1_5_year=jsonData.family.u_salary_1_5_year
pm.test("The u_salary_1_5_year  is equal to salary from request * 4", function () {
    pm.expect(salary_1_5_year).to.eql(salary_response*4);
});



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
18. Передать в окружение переменную name
19. Передать в окружение переменную age
20. Передать в окружение переменную salary
21. Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.
