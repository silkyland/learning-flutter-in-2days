# HTTP Request ใน Flutter

สำหรับการทำ HTTP Request ใน Flutter ด้วย package `http` จะมีรายละเอียดและขั้นตอนดังนี้

![alt text](/assets/images/13/httprequest.png)

1. ติดตั้ง package http ตามที่ได้อธิบายไปแล้วโดยเพิ่ม `http: ^1.2.1` ใน dependencies ของไฟล์ pubspec.yaml และรัน flutter pub get

2. ใช้งาน package ด้วยการเพิ่ม import 'package:http/http.dart' as http; ในไฟล์ Dart ที่ต้องการใช้

3. ส่ง HTTP GET request ด้วย method http.get():

```dart
Future<void> fetchData() async {
  final response = await http.get(Uri.parse('https://api.example.com/data'));

  if (response.statusCode == 200) {
    // อ่านข้อมูล JSON จาก response body
    var data = jsonDecode(response.body);
    // ทำอะไรบางอย่างกับข้อมูล เช่น print(data);
  } else {
    throw Exception('Failed to load data');
  }
}
```

โค้ดนี้จะส่ง HTTP GET request ไปยัง URL ที่กำหนด และถ้าได้ response กลับมาเป็น status code 200 ก็จะแปลงข้อมูลใน response body เป็น JSON ด้วย jsonDecode() จากนั้นก็สามารถนำข้อมูลไปใช้งานต่อได้ เช่น print หรือแสดงผลบนหน้าจอ

4. ส่ง HTTP POST request ด้วย method http.post():

```dart
Future<void> createData() async {
  final response = await http.post(
    Uri.parse('https://api.example.com/data'),
    headers: <String, String>{
      'Content-Type': 'application/json; charset=UTF-8',
    },
    body: jsonEncode(<String, String>{
      'name': 'John Doe',
      'age': '30',
    }),
  );

  if (response.statusCode == 201) {
    print('Data created successfully!');
  } else {
    throw Exception('Failed to create data');
  }
}
```

โค้ดนี้จะสร้างข้อมูลใหม่ด้วย HTTP POST request โดยส่ง headers และ request body เป็น JSON ไปด้วย ถ้าสำเร็จจะได้ status code 201 กลับมา

5. ส่ง HTTP PUT/PATCH request เพื่ออัพเดทข้อมูล ก็ทำได้ในลักษณะเดียวกันกับ POST โดยเปลี่ยนเป็น http.put() หรือ http.patch() และระบุ URL ของข้อมูลที่ต้องการอัพเดท

6. ส่ง HTTP DELETE request เพื่อลบข้อมูล ใช้ http.delete() ร่วมกับ URL ของข้อมูลที่ต้องการลบ

นอกจากนี้ ยังมีออปชันอื่นๆ ที่สามารถใช้ร่วมกับ HTTP request ใน http package เช่น:

- การส่ง query parameters
- การตั้งค่า timeout
- การอ่าน response headers
- การส่ง authorization headers สำหรับ authentication
- การอัปโหลดไฟล์
- การดาวน์โหลดไฟล์
- การจัดการ cookies

รวมถึงมี method อื่นๆ เช่น http.head() สำหรับส่ง HEAD request หรือ http.read() สำหรับอ่านข้อมูลจาก request stream ที่ส่งมาแบบ chunked

การใช้งาน HTTP request ใน package http จะคล้ายๆ กับการใช้งานบน platform อื่นๆ ทั่วไป แต่อาจมีรายละเอียดบางอย่างที่แตกต่างกันไปบ้าง ดังนั้นจึงแนะนำให้ศึกษาเพิ่มเติมจาก document ของ package ควบคู่ไปด้วย

นอกจาก package http แล้ว ยังมี package อื่นๆ ที่นิยมใช้สำหรับการส่ง HTTP request ใน Flutter ด้วย เช่น:

1. Dio - เป็น package ที่มีความสามารถและ flexibility สูง รองรับการส่ง request แบบ interceptors, การแปลง data และ error handling ที่หลากหลาย รวมถึงรองรับการส่ง FormData และ multipart requests สำหรับอัปโหลดไฟล์

2. Chopper - เป็น package ที่ออกแบบมาสำหรับสร้าง type-safe HTTP client ใน Flutter โดยใช้ annotation และ code generation ช่วยให้เขียน API client ได้ง่ายและเป็นระเบียบมากขึ้น

3. Retrofit - เป็น package ที่นำแนวคิดของ Retrofit มาใช้ใน Flutter ช่วยให้สร้าง type-safe HTTP client ได้ง่ายขึ้นเหมือนกัน โดยใช้ annotation กำหนด HTTP method, URL path, request body ของแต่ละ API endpoint

4. HttpClient - เป็น built-in HTTP client ใน Dart ที่สามารถใช้ส่ง HTTP request ได้เลย แต่มี API และฟีเจอร์ที่เรียบง่ายกว่า package อื่นๆ

5. GraphQL - สำหรับ API ที่ใช้ GraphQL นั้นจะมี package ที่ช่วยในการส่ง GraphQL query และ mutation เช่น graphql, graphql_flutter เป็นต้น

แต่ละ package ก็มีข้อดีข้อเสียแตกต่างกันไป เหมาะสำหรับความต้องการที่แตกต่างกัน เช่น Dio เหมาะสำหรับ app ที่ต้องการความยืดหยุ่นสูง ส่วน Chopper และ Retrofit เหมาะสำหรับทีมที่อยากเน้นความเป็นระเบียบของโค้ดและลด error ที่อาจเกิดขึ้นจากการเขียน HTTP request ด้วยตัวเอง

## Practice

File Server - https://github.com/silkyland/todo-app-flask/tree/main

### API Endpoints

| Endpoint          | HTTP Method | URL Path             | Description                       |
| ----------------- | ----------- | -------------------- | --------------------------------- |
| Get all todos     | GET         | /todos               | Retrieve all todo items           |
| Get a single todo | GET         | /todos/<int:todo_id> | Retrieve a single todo item by ID |
| Create a new todo | POST        | /todos               | Create a new todo item            |
| Update a todo     | PUT         | /todos/<int:todo_id> | Update an existing todo item      |
| Delete a todo     | DELETE      | /todos/<int:todo_id> | Delete a todo item by ID          |

## Request and Response Formats

- Request Body: JSON
- Response Body: JSON

มาลองสร้าง Flutter app ที่มีการส่ง HTTP request ไปยัง REST API ของ todo list กัน โดยใช้ข้อมูลจาก Endpoint ที่ให้มา และสร้างไฟล์ตาม best practice ดังนี้

File Structure:

```
lib/
  |- models/
  |   |- todo_model.dart
  |
  |- services/
  |   |- api_service.dart
  |
  |- screens/
  |   |- todo_list_screen.dart
  |   |- todo_detail_screen.dart
  |
  |- main.dart
```

1. สร้าง Data Model ใน `lib/models/todo_model.dart`:

```dart
class TodoModel {
  final int id;
  final String title;
  final bool completed;

  TodoModel({
    required this.id,
    required this.title,
    required this.completed,
  });

  factory TodoModel.fromJson(Map<String, dynamic> json) {
    return TodoModel(
      id: json['id'],
      title: json['title'],
      completed: json['completed'],
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'title': title,
      'completed': completed,
    };
  }
}
```

2. สร้าง API Service ใน `lib/services/api_service.dart`:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;
import 'package:your_app/models/todo_model.dart';

class ApiService {
  static const String _baseUrl = 'https://your-api-url.com'; // เปลี่ยนเป็น base URL ของ API ที่ใช้

  Future<List<TodoModel>> getAllTodos() async {
    final response = await http.get(Uri.parse('$_baseUrl/todos'));
    if (response.statusCode == 200) {
      final jsonList = jsonDecode(response.body) as List<dynamic>;
      return jsonList.map((json) => TodoModel.fromJson(json)).toList();
    } else {
      throw Exception('Failed to load todos');
    }
  }

  Future<TodoModel> getTodo(int id) async {
    final response = await http.get(Uri.parse('$_baseUrl/todos/$id'));
    if (response.statusCode == 200) {
      return TodoModel.fromJson(jsonDecode(response.body));
    } else {
      throw Exception('Failed to load todo $id');
    }
  }

  Future<TodoModel> createTodo(TodoModel todo) async {
    final response = await http.post(
      Uri.parse('$_baseUrl/todos'),
      headers: <String, String>{
        'Content-Type': 'application/json; charset=UTF-8',
      },
      body: jsonEncode(todo.toJson()),
    );
    if (response.statusCode == 201) {
      return TodoModel.fromJson(jsonDecode(response.body));
    } else {
      throw Exception('Failed to create todo');
    }
  }

  Future<TodoModel> updateTodo(TodoModel todo) async {
    final response = await http.put(
      Uri.parse('$_baseUrl/todos/${todo.id}'),
      headers: <String, String>{
        'Content-Type': 'application/json; charset=UTF-8',
      },
      body: jsonEncode(todo.toJson()),
    );
    if (response.statusCode == 200) {
      return TodoModel.fromJson(jsonDecode(response.body));
    } else {
      throw Exception('Failed to update todo');
    }
  }

  Future<void> deleteTodo(int id) async {
    final response = await http.delete(Uri.parse('$_baseUrl/todos/$id'));
    if (response.statusCode != 204) {
      throw Exception('Failed to delete todo');
    }
  }
}
```

3. สร้างหน้า Todo List ใน `lib/screens/todo_list_screen.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:your_app/models/todo_model.dart';
import 'package:your_app/services/api_service.dart';

class TodoListScreen extends StatefulWidget {
  @override
  _TodoListScreenState createState() => _TodoListScreenState();
}

class _TodoListScreenState extends State<TodoListScreen> {
  late Future<List<TodoModel>> _todosFuture;
  final ApiService _apiService = ApiService();

  @override
  void initState() {
    super.initState();
    _todosFuture = _apiService.getAllTodos();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Todo List'),
      ),
      body: FutureBuilder<List<TodoModel>>(
        future: _todosFuture,
        builder: (context, snapshot) {
          if (snapshot.hasData) {
            final todos = snapshot.data!;
            return ListView.builder(
              itemCount: todos.length,
              itemBuilder: (context, index) {
                final todo = todos[index];
                return ListTile(
                  title: Text(todo.title),
                  trailing: Checkbox(
                    value: todo.completed,
                    onChanged: null,
                  ),
                  onTap: () {
                    Navigator.push(
                      context,
                      MaterialPageRoute(
                        builder: (context) => TodoDetailScreen(todo: todo),
                      ),
                    );
                  },
                );
              },
            );
          } else if (snapshot.hasError) {
            return Center(child: Text('${snapshot.error}'));
          }
          return Center(child: CircularProgressIndicator());
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          Navigator.push(
            context,
            MaterialPageRoute(
              builder: (context) => TodoDetailScreen(todo: null),
            ),
          );
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

4. สร้างหน้า Todo Detail ใน `lib/screens/todo_detail_screen.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:your_app/models/todo_model.dart';
import 'package:your_app/services/api_service.dart';

class TodoDetailScreen extends StatefulWidget {
  final TodoModel? todo;

  TodoDetailScreen({this.todo});

  @override
  _TodoDetailScreenState createState() => _TodoDetailScreenState();
}

class _TodoDetailScreenState extends State<TodoDetailScreen> {
  final ApiService _apiService = ApiService();
  final _titleController = TextEditingController();
  bool _completed = false;

  @override
  void initState() {
    super.initState();
    if (widget.todo != null) {
      _titleController.text = widget.todo!.title;
      _completed = widget.todo!.completed;
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.todo == null ? 'New Todo' : 'Edit Todo'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: [
            TextField(
              controller: _titleController,
              decoration: InputDecoration(labelText: 'Title'),
            ),
            CheckboxListTile(
              title: Text('Completed'),
              value: _completed,
              onChanged: (value) {
                setState(() {
                  _completed = value ?? false;
                });
              },
            ),
            SizedBox(height: 16),
            ElevatedButton(
              onPressed: () async {
                final todo = TodoModel(
                  id: widget.todo?.id ?? 0,
                  title: _titleController.text,
                  completed: _completed,
                );
                if (widget.todo == null) {
                  await _apiService.createTodo(todo);
                } else {
                  await _apiService.updateTodo(todo);
                }
                Navigator.pop(context);
              },
              child: Text('Save'),
            ),
            SizedBox(height: 8),
            if (widget.todo != null)
              ElevatedButton(
                onPressed: () async {
                  await _apiService.deleteTodo(widget.todo!.id);
                  Navigator.pop(context);
                },
                child: Text('Delete'),
                style: ElevatedButton.styleFrom(primary: Colors.red),
              ),
          ],
        ),
      ),
    );
  }
}
```

5. อย่าลืม import ไฟล์ทั้งหมดใน `lib/main.dart` และเรียกใช้งาน `TodoListScreen` ใน `MyApp`:

```dart
import 'package:flutter/material.dart';
import 'package:your_app/screens/todo_list_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Todo App',
      home: TodoListScreen(),
    );
  }
}
```

เท่านี้เราก็จะได้ Flutter app ที่สามารถดึงข้อมูล todo list จาก REST API ผ่าน HTTP request แสดงรายการ todo ทั้งหมด เพิ่ม แก้ไข และลบ todo ได้แล้ว โดยเราแยกส่วนต่างๆ เป็น model, service, screen เพื่อให้โค้ดอ่านง่ายและเป็นระเบียบตาม best practice ในการพัฒนา Flutter app

ตรวจสอบ Code ที่เสร็จแล้วได้ที่ https://github.com/silkyland/bundit-flutter-todo
