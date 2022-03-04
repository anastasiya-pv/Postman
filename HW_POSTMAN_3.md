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
