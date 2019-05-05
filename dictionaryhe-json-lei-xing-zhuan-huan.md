# python dictionary和json对象的相互转换

Python之dict(或对象)与json之间的互相转化
在Python语言中，json数据与dict字典以及对象之间的转化，是必不可少的操作。

在Python中自带json库。通过import json导入。

在json模块有2个方法，

loads()：将json数据转化成dict数据
dumps()：将dict数据转化成json数据
load()：读取json文件数据，转成dict数据
dump()：将dict数据转化成json数据后写入json文件
下面是具体的示例：

dict字典转json数据
```py
import json

def dict_to_json():
    dict = {}
    dict['name'] = 'many'
    dict['age'] = 10
    dict['sex'] = 'male'
    print(dict)  # 输出：{'name': 'many', 'age': 10, 'sex': 'male'}
    j = json.dumps(dict)
    print(j)  # 输出：{"name": "many", "age": 10, "sex": "male"}


if __name__ == '__main__':
    dict_to_json()
```

对象转json数据
```py
import json

def obj_to_json():
    stu = Student('007', '007', 28, 'male', '13000000000', '123@qq.com')
    print(type(stu))  # <class 'json_test.student.Student'>
    stu = stu.__dict__  # 将对象转成dict字典
    print(type(stu))  # <class 'dict'>
    print(stu)  # {'id': '007', 'name': '007', 'age': 28, 'sex': 'male', 'phone': '13000000000', 'email': '123@qq.com'}
    j = json.dumps(obj=stu)
    print(j)  # {"id": "007", "name": "007", "age": 28, "sex": "male", "phone": "13000000000", "email": "123@qq.com"}


if __name__ == '__main__':
    obj_to_json()

```

json数据转成dict字典
```py
import json

def json_to_dict():
    j = '{"id": "007", "name": "007", "age": 28, "sex": "male", "phone": "13000000000", "email": "123@qq.com"}'
    dict = json.loads(s=j)
    print(dict)  # {'id': '007', 'name': '007', 'age': 28, 'sex': 'male', 'phone': '13000000000', 'email': '123@qq.com'}


if __name__ == '__main__':
    json_to_dict()
```

json数据转成对象
```py
import json

def json_to_obj():
    j = '{"id": "007", "name": "007", "age": 28, "sex": "male", "phone": "13000000000", "email": "123@qq.com"}'
    dict = json.loads(s=j)
    stu = Student()
    stu.__dict__ = dict
    print('id: ' + stu.id + ' name: ' + stu.name + ' age: ' + str(stu.age) + ' sex: ' + str(
        stu.sex) + ' phone: ' + stu.phone + ' email: ' + stu.email)  # id: 007 name: 007 age: 28 sex: male phone: 13000000000 email: 123@qq.com


if __name__ == '__main__':
    json_to_obj()
    
```


> 转自——https://blog.csdn.net/qq_33689414/article/details/78307018 