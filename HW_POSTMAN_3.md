ДЗ_3 Postman
=====

1) **POST**<br>
http://162.55.220.72:5005/login<br>
**login** : str (кроме /)<br>
**password** : str<br>

![alt text](https://github.com/anastasiya-pv/Testing/blob/main/%D0%91%D0%B5%D0%B7%D1%8B%D0%BC%D1%8F%D0%BD%D0%BD%D1%8B%D0%B9.png "postman view")

Приходящий токен необходимо передать во все остальные запросы.<br>
`pm.environment.set("token", "recieved_token_text")`


2) http://162.55.220.72:5005/user_info<br>
**req. (RAW JSON)<br>
POST<br>
age:** int<br>
**salary:** int<br>
**name:** str<br>
**auth_token** - <br>
```
{
"age": 19,
"salary":200,
"name":"Alina",
"auth_token":"{{token}}"
}
```

```
resp.
{'start_qa_salary':salary,
 'qa_salary_after_6_months': salary * 2,
 'qa_salary_after_12_months': salary * 2.9,
 'person': {'u_name':[user_name, salary, age],
                                'u_age':age,
                                'u_salary_1.5_year': salary * 4}
                                }
```

**Тесты:**<br>
**1)	Статус код 200**<br>
```
pm.test("Status code is 200", function(){
    pm.response.to.have.status(200);
});
```
**2) Проверка структуры json в ответе.**<br>
```
let jsonData = pm.response.json()

let schema  = {
    "$schema": "http://json-schema.org/draft-07/schema",
    "$id": "http://example.com/example.json",
    "type": "object",
    "title": "The root schema",
    "description": "The root schema comprises the entire JSON document.",
    "default": {},
    "examples": [
        {
            "person": {
                "u_age": 19,
                "u_name": [
                    "Alina",
                    200,
                    19
                ],
                "u_salary_1_5_year": 800
            },
            "qa_salary_after_12_months": 580.0,
            "qa_salary_after_6_months": 400,
            "start_qa_salary": 200
        }
    ],
    "required": [
        "person",
        "qa_salary_after_12_months",
        "qa_salary_after_6_months",
        "start_qa_salary"
    ],
    "properties": {
        "person": {
            "$id": "#/properties/person",
            "type": "object",
            "title": "The person schema",
            "description": "An explanation about the purpose of this instance.",
            "default": {},
            "examples": [
                {
                    "u_age": 19,
                    "u_name": [
                        "Alina",
                        200,
                        19
                    ],
                    "u_salary_1_5_year": 800
                }
            ],
            "required": [
                "u_age",
                "u_name",
                "u_salary_1_5_year"
            ],
            "properties": {
                "u_age": {
                    "$id": "#/properties/person/properties/u_age",
                    "type": "integer",
                    "title": "The u_age schema",
                    "description": "An explanation about the purpose of this instance.",
                    "default": 0,
                    "examples": [
                        19
                    ]
                },
                "u_name": {
                    "$id": "#/properties/person/properties/u_name",
                    "type": "array",
                    "title": "The u_name schema",
                    "description": "An explanation about the purpose of this instance.",
                    "default": [],
                    "examples": [
                        [
                            "Alina",
                            200
                        ]
                    ],
                    "additionalItems": true,
                    "items": {
                        "$id": "#/properties/person/properties/u_name/items",
                        "anyOf": [
                            {
                                "$id": "#/properties/person/properties/u_name/items/anyOf/0",
                                "type": "string",
                                "title": "The first anyOf schema",
                                "description": "An explanation about the purpose of this instance.",
                                "default": "",
                                "examples": [
                                    "Alina"
                                ]
                            },
                            {
                                "$id": "#/properties/person/properties/u_name/items/anyOf/1",
                                "type": "integer",
                                "title": "The second anyOf schema",
                                "description": "An explanation about the purpose of this instance.",
                                "default": 0,
                                "examples": [
                                    200,
                                    19
                                ]
                            }
                        ]
                    }
                },
                "u_salary_1_5_year": {
                    "$id": "#/properties/person/properties/u_salary_1_5_year",
                    "type": "integer",
                    "title": "The u_salary_1_5_year schema",
                    "description": "An explanation about the purpose of this instance.",
                    "default": 0,
                    "examples": [
                        800
                    ]
                }
            },
            "additionalProperties": true
        },
        "qa_salary_after_12_months": {
            "$id": "#/properties/qa_salary_after_12_months",
            "type": "number",
            "title": "The qa_salary_after_12_months schema",
            "description": "An explanation about the purpose of this instance.",
            "default": 0.0,
            "examples": [
                580.0
            ]
        },
        "qa_salary_after_6_months": {
            "$id": "#/properties/qa_salary_after_6_months",
            "type": "integer",
            "title": "The qa_salary_after_6_months schema",
            "description": "An explanation about the purpose of this instance.",
            "default": 0,
            "examples": [
                400
            ]
        },
        "start_qa_salary": {
            "$id": "#/properties/start_qa_salary",
            "type": "integer",
            "title": "The start_qa_salary schema",
            "description": "An explanation about the purpose of this instance.",
            "default": 0,
            "examples": [
                200
            ]
        }
    },
    "additionalProperties": true
}

pm.test('Schema is valid', function () {
    pm.expect(tv4.validate(jsonData, schema)).to.be.true;
});
```
3) **В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент**.<br>
```
let post_raw = JSON.parse(request.data)
let salary = post_raw.salary
pm.test("Check the calculation in qa_salary_after_6_months", function(){
    pm.expect(jsonData.qa_salary_after_6_months).to.eql(salary*2);
});
pm.test("Check the calculation in qa_salary_after_12_months", function(){
    pm.expect(jsonData.qa_salary_after_12_months).to.eql(salary*2.9);
});
pm.test("Check the calculation in u_salary_1.5_year", function(){
    pm.expect(jsonData.person.u_salary_1_5_year).to.eql(salary*4);
});
pm.test("Check the calculation in start_qa_salary", function(){
    pm.expect(jsonData.start_qa_salary).to.eql(salary);
});
```
**4) Достать значение из поля 'u_salary_1.5_year' и передать в поле salary запроса**
```
pm.environment.set('u_salary_1.5_year', jsonData.person.u_salary_1_5_year)
pm.sendRequest('http://162.55.220.72:5005/get_test_user', (error, response) => {
  if (error) {
    console.log(error);
  } else {
  pm.environment.get('u_salary_1.5_year');
  }
});
```
3) http://162.55.220.72:5005/new_data
req.
POST
age: int
salary: int
name: str
auth_token

```Resp.
{'name':name,
  'age': int(age),
  'salary': [salary, str(salary*2), str(salary*3)]}
```

**1) Статус код 200**
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
**2) Проверка структуры json в ответе.**
```
let jsonData= pm.response.json()
let schema_3  = {   "$schema": "http://json-schema.org/draft-07/schema",
    "$id": "http://example.com/example.json",
    "type": "object",
    "title": "The root schema",
    "description": "The root schema comprises the entire JSON document.",
    "default": {},
    "examples": [
        {
            "age": 19,
            "name": "Sasha",
            "salary": [
                20,
                "40",
                "60"
            ]
        }
    ],
    "required": [
        "age",
        "name",
        "salary"
    ],
    "properties": {
        "age": {
            "$id": "#/properties/age",
            "type": "integer",
            "title": "The age schema",
            "description": "An explanation about the purpose of this instance.",
            "default": 0,
            "examples": [
                19
            ]
        },
        "name": {
            "$id": "#/properties/name",
            "type": "string",
            "title": "The name schema",
            "description": "An explanation about the purpose of this instance.",
            "default": "",
            "examples": [
                "Sasha"
            ]
        },
        "salary": {
            "$id": "#/properties/salary",
            "type": "array",
            "title": "The salary schema",
            "description": "An explanation about the purpose of this instance.",
            "default": [],
            "examples": [
                [
                    20,
                    "40"
                ]
            ],
            "additionalItems": true,
            "items": {
                "$id": "#/properties/salary/items",
                "anyOf": [
                    {
                        "$id": "#/properties/salary/items/anyOf/0",
                        "type": "integer",
                        "title": "The first anyOf schema",
                        "description": "An explanation about the purpose of this instance.",
                        "default": 0,
                        "examples": [
                            20
                        ]
                    },
                    {
                        "$id": "#/properties/salary/items/anyOf/1",
                        "type": "string",
                        "title": "The second anyOf schema",
                        "description": "An explanation about the purpose of this instance.",
                        "default": "",
                        "examples": [
                            "40",
                            "60"
                        ]
                    }
                ]
            }
        }
    },
    "additionalProperties": true
}


pm.test('Schema is valid', function () {
    pm.expect(tv4.validate(jsonData, schema_3)).to.be.true;
});
```
**3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.**
```

let body_req = request.data
let salary = +body_req.salary

pm.test("Check the calculation_1", function(){
    pm.expect(jsonData.salary[0]).to.eql(salary);
});
//jsonData.salary[1] is a string
let salary_1 = +jsonData.salary[1]
pm.test("Check the calculation_2", function(){
    pm.expect(salary_1).to.eql(salary*2);
});
//jsonData.salary[2] is a string
let salary_2 = +jsonData.salary[2]
pm.test("Check the calculation_3", function(){
    pm.expect(salary_2).to.eql(salary*3);
});
```
**4) проверить, что 2-й элемент массива salary больше 1-го и 0-го**
```
//JUST FOR YOURSELF
if (salary_2>salary_1, salary_2>jsonData.salary[0]) {
  console.log("passed");
} else {
  console.log("failed");
}

  // TEST OPTION

pm.test("jsonData.salary [0]", function(){
 pm.expect(salary_2).to.be.above(jsonData.salary[0])
});
//
 pm.test("jsonData.salary [1]] ", function(){
pm.expect(salary_2).to.be.above(salary_1);
});
```
