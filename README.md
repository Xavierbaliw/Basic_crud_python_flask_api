Prerequisites

1. [https://software-engineer.thirdygayares.com/virtual-environment-and-python-package-manager](https://software-engineer.thirdygayares.com/virtual-environment-and-python-package-manager)
    
2. [https://software-engineer.thirdygayares.com/how-to-run-python-flask](https://software-engineer.thirdygayares.com/how-to-run-python-flask)
    
3. [https://software-engineer.thirdygayares.com/data-structure-again](https://software-engineer.thirdygayares.com/data-structure-again)
    

# To start,

* Create a Python Virtual Environment
    
* Activate Virtual Environment
    
* make sure Flask is installed:
    

```java
pip install Flask
```

**BLUEPRINT**

# **OUR BLUEPRINT**

```python
# TODO: import flask LIBRARY
from flask import Flask, jsonify, request

# call the flask object
app = Flask(__name__)

# create list of dictionaries
students = [{}]

# get method
@app.route('/students', methods=['GET'])
def get_students():

# get method : Get a specific student by ID
@app.route('/students/<int:student_id>', methods=['GET'])
def get_student(student_id):

# put method
@app.route('/students/<int:student_id>', methods=['PUT'])
def update_student(student_id):

# delete method
@app.route('/students/<int:student_id>', methods=['DELETE'])
def delete_student(student_id):

# Dont forget this
if __name__ == '__main__':
    app.run(debug=True)
```

### When Testing the API

* **Run the server** by executing the Python script:
    
    ```java
    python app.py
    ```
    

  

### Flask API Code

# create app.py

## **import flask**

```python
from flask import Flask, jsonify, request

app = Flask(__name__)
```

### **Create a List of Dictionaries**

```python
# Sample data: list of students
students = [
    {
        "name": "Juan Carlos",
        "section": "BSIT-4B",
        "id": 1,
        "email": "juan@gmail.com",
        "age": 22
    },
    {
        "name": "Jose Rizal",
        "section": "BSIT-2A",
        "id": 2,
        "email": "jose@gmail.com",
        "age": 21
    },
    {
        "name": "Juan Luna",
        "section": "BSIT-3A",
        "id": 3,
        "email": "juan@gmail.com",
        "age": 20
    },
    {
        "name": "Andres Bonifacio",
        "section": "BSIT-3A",
        "id": 4,
        "email": "andres@gmail.com",
        "age": 20
    },
    {
        "name": "Justin Bieber",
        "section": "BSIT-2A",
        "id": 5,
        "email": "justin@gmail.com",
        "age": 21
    },
    {
        "name": "Michael Jordan",
        "section": "BSIT-4A",
        "id": 6,
        "email": "michael@gmail.com",
        "age": 19
    },
    {
        "name": "Andrew Jordan",
        "section": "BSIT-3A",
        "id": 7,
        "email": "andrew@gmail.com",
        "age": 20
    },
    {
        "name": "Jessa Boe",
        "section": "BSIT-2B",
        "id": 8,
        "email": "jessa@gmail.com",
        "age": 18
    },
    {
        "name": "Ted Talk",
        "section": "BSIT-3B",
        "id": 9,
        "email": "ted@gmail.com",
        "age": 19
    }
]
```

### **Get All Student**

```python
@app.route('/students', methods=['GET'])
def get_students():
    return jsonify(students)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728738532945/69d714e3-c4af-4385-9255-7e696cb6b85e.png)

**Get All Students (**`GET /students`): Returns a list of all students in JSON format.

---

### GET STUDENT BY ID

```python
# READ: Get a specific student by ID
@app.route('/students/<int:student_id>', methods=['GET'])
def get_student(student_id):
    student = next((student for student in students if student["id"] == student_id), None)
    if student:
        return jsonify(student)
    else:
        return jsonify({"message": "Student not found"}), 404
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728738772655/e2c69ee1-afd5-413c-b972-8b15cbd09c66.png)

**Get a Specific Student (**`GET /students/<id>`): Returns details of a student by their `id`.

---

### ADD STUDENT

```python
@app.route('/students', methods=['POST'])
def add_student():
    new_student = request.get_json()
    new_student['id'] = max(student['id'] for student in students) + 1  # Generate new ID
    students.append(new_student)
    return jsonify(new_student), 201
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728738813590/17048f2e-b1b0-4c49-a15c-ee80e3bf63c3.png)

**Add a New Student (**`POST /students`): Accepts student details in JSON format and adds a new student with a unique `id`.

---

### UPDATE STUDENT

```python
@app.route('/students/<int:student_id>', methods=['PUT'])
def update_student(student_id):
    student = next((student for student in students if student["id"] == student_id), None)
    if student:
        data = request.get_json()
        student.update(data)
        return jsonify(student)
    else:
        return jsonify({"message": "Student not found"}), 404
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728738952551/f769be67-bc36-4d2d-95b8-2078f1499699.png)

**Update an Existing Student (**`PUT /students/<id>`): Updates the details of a student by their `id` using JSON data from the request.

---

```python
# DELETE: Remove a student by ID
@app.route('/students/<int:student_id>', methods=['DELETE'])
def delete_student(student_id):
    student = next((student for student in students if student["id"] == student_id), None)
    if student:
        students.remove(student)
        return jsonify({"message": "Student deleted"})
    else:
        return jsonify({"message": "Student not found"}), 404

if __name__ == '__main__':
    app.run(debug=True)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728739118134/66461269-da6e-4950-a812-2b69f6f1ddf1.png)

**REMEMBER ADD THIS CODE**

```python
if __name__ == '__main__':
    app.run(debug=True)
```

**Delete a Student (**`DELETE /students/<id>`): Deletes a student by their `id`.

---

* **Using Postman**, you can test each endpoint by sending the appropriate requests.
    

This API provides a simple and clean structure to manage students' data with CRUD operations.
