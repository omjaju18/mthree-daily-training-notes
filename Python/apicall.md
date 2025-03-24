### **How to Make an API Call in Python**
You can make API calls in Python using the `requests` module. Here’s a simple step-by-step guide:

---

### **1️⃣ Install the `requests` module**
If you haven't installed it yet, install it using:
```bash
pip install requests
```

---

### **2️⃣ Making a Basic GET Request**
A **GET** request is used to fetch data from an API.
```python
import requests

# API URL (Example: Fetching data from a public API)
url = "https://jsonplaceholder.typicode.com/posts/1"

# Sending a GET request
response = requests.get(url)

# Printing the response (JSON format)
print(response.json())
```

🔹 **Explanation**:
- `requests.get(url)`: Sends a GET request to fetch data.
- `.json()`: Converts the response into a Python dictionary.

---

### **3️⃣ Making a POST Request**
A **POST** request is used to send data to an API.
```python
import requests

# API URL
url = "https://jsonplaceholder.typicode.com/posts"

# Data to send
data = {
    "title": "New Post",
    "body": "This is a test post",
    "userId": 1
}

# Sending a POST request
response = requests.post(url, json=data)

# Printing the response
print(response.json())
```

🔹 **Explanation**:
- `requests.post(url, json=data)`: Sends data to the API in JSON format.

---

### **4️⃣ Adding Headers and Authentication**
Some APIs require headers or authentication.
```python
import requests

# API URL
url = "https://api.example.com/data"

# Headers (Example: Sending an API key)
headers = {
    "Authorization": "Bearer YOUR_API_KEY",
    "Content-Type": "application/json"
}

# Sending a GET request with headers
response = requests.get(url, headers=headers)

# Printing the response
print(response.json())
```

---

### **5️⃣ Handling API Errors**
Always check for errors when making API calls.
```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/9999"  # Non-existing post

response = requests.get(url)

# Checking if request was successful
if response.status_code == 200:
    print(response.json())  # Print the data
else:
    print(f"Error: {response.status_code} - {response.reason}")
```

🔹 **Common HTTP Status Codes**:
- `200 OK` → Success ✅
- `400 Bad Request` → Client-side error ❌
- `401 Unauthorized` → Authentication required 🔒
- `404 Not Found` → Resource doesn’t exist 🚫
- `500 Internal Server Error` → API server issue ⚠️

---

### **6️⃣ Using Query Parameters**
Many APIs allow passing parameters in the URL.
```python
import requests

url = "https://jsonplaceholder.typicode.com/comments"

# Query parameters
params = {
    "postId": 1
}

# Sending request with parameters
response = requests.get(url, params=params)

# Printing response
print(response.json())
```

---

### **Summary**
| **Method** | **Use Case** |
|------------|-------------|
| `requests.get(url)` | Fetch data from an API |
| `requests.post(url, json=data)` | Send data to an API |
| `requests.put(url, json=data)` | Update existing data |
| `requests.delete(url)` | Delete a resource |
| `requests.get(url, params={})` | Send query parameters |
| `requests.get(url, headers={})` | Send headers |

---

### **Python Program Demonstrating All API Methods (GET, POST, PUT, DELETE, and Query Parameters)**  

This example interacts with the **JSONPlaceholder** API, a free test API that mimics a RESTful backend.

---

### **📌 Full Python Program**
```python
import requests

# Base API URL
BASE_URL = "https://jsonplaceholder.typicode.com/posts"

# ------------------ GET REQUEST ------------------
def get_posts():
    """Fetch all posts using GET request"""
    response = requests.get(BASE_URL)
    if response.status_code == 200:
        print("\n🔹 GET Request Successful! Here are the posts:")
        print(response.json()[:2])  # Printing only first 2 posts
    else:
        print(f"❌ GET Request Failed: {response.status_code}")

# ------------------ GET WITH PARAMETERS ------------------
def get_post_by_id(post_id):
    """Fetch a single post using query parameters"""
    response = requests.get(f"{BASE_URL}/{post_id}")
    if response.status_code == 200:
        print(f"\n🔹 GET Request with ID {post_id} Successful!")
        print(response.json())
    else:
        print(f"❌ Failed to fetch post {post_id}")

# ------------------ POST REQUEST ------------------
def create_post():
    """Create a new post using POST request"""
    new_post = {
        "title": "New API Post",
        "body": "This is a test post created via API.",
        "userId": 1
    }
    response = requests.post(BASE_URL, json=new_post)
    if response.status_code == 201:  # 201 Created
        print("\n✅ POST Request Successful! New post created:")
        print(response.json())
    else:
        print(f"❌ POST Request Failed: {response.status_code}")

# ------------------ PUT REQUEST ------------------
def update_post(post_id):
    """Update an existing post using PUT request"""
    updated_data = {
        "title": "Updated Title",
        "body": "Updated content of the post.",
        "userId": 1
    }
    response = requests.put(f"{BASE_URL}/{post_id}", json=updated_data)
    if response.status_code == 200:
        print(f"\n✅ PUT Request Successful! Post {post_id} Updated:")
        print(response.json())
    else:
        print(f"❌ PUT Request Failed: {response.status_code}")

# ------------------ DELETE REQUEST ------------------
def delete_post(post_id):
    """Delete a post using DELETE request"""
    response = requests.delete(f"{BASE_URL}/{post_id}")
    if response.status_code == 200:
        print(f"\n✅ DELETE Request Successful! Post {post_id} deleted.")
    else:
        print(f"❌ DELETE Request Failed: {response.status_code}")

# ------------------ FUNCTION CALLS ------------------
get_posts()               # Fetch all posts
get_post_by_id(1)         # Fetch post with ID 1
create_post()             # Create a new post
update_post(1)            # Update post with ID 1
delete_post(1)            # Delete post with ID 1
```

---

### **📌 Explanation**
1. **GET Request** → Fetches all posts.
2. **GET with Parameters** → Retrieves a specific post by ID.
3. **POST Request** → Creates a new post with sample data.
4. **PUT Request** → Updates an existing post.
5. **DELETE Request** → Deletes a specific post.

### **📌 Expected Output (Example)**
```
🔹 GET Request Successful! Here are the posts:
[{'userId': 1, 'id': 1, 'title': 'sunt aut facere repellat ...'}]

🔹 GET Request with ID 1 Successful!
{'userId': 1, 'id': 1, 'title': 'sunt aut facere repellat ...'}

✅ POST Request Successful! New post created:
{'title': 'New API Post', 'body': 'This is a test post ...', 'userId': 1, 'id': 101}

✅ PUT Request Successful! Post 1 Updated:
{'title': 'Updated Title', 'body': 'Updated content ...', 'userId': 1, 'id': 1}

✅ DELETE Request Successful! Post 1 deleted.
```

---

### **📌 Summary Table**
| HTTP Method | Function Name | Use Case |
|------------|--------------|----------|
| `GET` | `get_posts()` | Fetch all posts |
| `GET with params` | `get_post_by_id(post_id)` | Fetch a specific post by ID |
| `POST` | `create_post()` | Create a new post |
| `PUT` | `update_post(post_id)` | Update an existing post |
| `DELETE` | `delete_post(post_id)` | Delete a post |

---

Would you like me to add **error handling** or API key authentication to this? 🚀
