# Testing-an-API
This report outlines the testing process for the Todo API, focusing on validating the  functionality based on the provided user stories and performance requirements. The  goal is to identify bugs and ensure the API meets the expected behavior.
Detailed Command-Line and Tool Usage for Testing the Todo API
1. Testing with curl
curl is a command-line tool used to send HTTP requests to the API. Below are examples of how to use curl to test each user story.

User Story 1: Create a New Todo Item
Endpoint: POST /todos
Command:

bash
Copy
curl -X POST https://api.todo.com/v1/todos \
-H "Content-Type: application/json" \
-d '{
  "title": "Buy groceries",
  "description": "Milk, eggs, bread",
  "dueDate": "2023-12-01",
  "tags": ["shopping", "personal"],
  "status": "pending"
}'
Explanation:

-X POST: Specifies the HTTP method (POST).

-H "Content-Type: application/json": Sets the request header to indicate JSON data.

-d '{...}': Provides the JSON payload for the todo item.

Expected Output:

json
Copy
{
  "id": "1",
  "title": "Buy groceries",
  "description": "Milk, eggs, bread",
  "dueDate": "2023-12-01",
  "tags": ["shopping", "personal"],
  "status": "pending"
}
User Story 2: Retrieve All Todo Items
Endpoint: GET /todos
Command:

bash
Copy
curl -X GET https://api.todo.com/v1/todos
Explanation:

-X GET: Specifies the HTTP method (GET).

Expected Output:

json
Copy
[
  {
    "id": "1",
    "title": "Buy groceries",
    "description": "Milk, eggs, bread",
    "dueDate": "2023-12-01",
    "tags": ["shopping", "personal"],
    "status": "pending"
  }
]
User Story 3: Update an Existing Todo Item
Endpoint: PUT /todos/{id}
Command:

bash
Copy
curl -X PUT https://api.todo.com/v1/todos/1 \
-H "Content-Type: application/json" \
-d '{
  "title": "Buy groceries",
  "description": "Milk, eggs, bread, butter",
  "status": "completed"
}'
Explanation:

-X PUT: Specifies the HTTP method (PUT).

-d '{...}': Provides the updated JSON payload.

Expected Output:

json
Copy
{
  "id": "1",
  "title": "Buy groceries",
  "description": "Milk, eggs, bread, butter",
  "dueDate": "2023-12-01",
  "tags": ["shopping", "personal"],
  "status": "completed"
}
User Story 4: Delete a Todo Item
Endpoint: DELETE /todos/{id}
Command:

bash
Copy
curl -X DELETE https://api.todo.com/v1/todos/1
Explanation:

-X DELETE: Specifies the HTTP method (DELETE).

Expected Output:

No content (204 No Content response).

User Story 5: Mark a Todo Item as Completed
Endpoint: PATCH /todos/{id}
Command:

bash
Copy
curl -X PATCH https://api.todo.com/v1/todos/1 \
-H "Content-Type: application/json" \
-d '{
  "status": "completed"
}'
Explanation:

-X PATCH: Specifies the HTTP method (PATCH).

-d '{...}': Provides the updated status.

Expected Output:

json
Copy
{
  "id": "1",
  "title": "Buy groceries",
  "description": "Milk, eggs, bread, butter",
  "dueDate": "2023-12-01",
  "tags": ["shopping", "personal"],
  "status": "completed"
}
User Story 6: Categorize Todo Items with Tags
Endpoint: GET /todos?tag={tag}
Command:

bash
Copy
curl -X GET "https://api.todo.com/v1/todos?tag=shopping"
Explanation:

?tag=shopping: Filters todo items by the shopping tag.

Expected Output:

json
Copy
[
  {
    "id": "1",
    "title": "Buy groceries",
    "description": "Milk, eggs, bread, butter",
    "dueDate": "2023-12-01",
    "tags": ["shopping", "personal"],
    "status": "completed"
  }
]
User Story 7: Set Due Dates for Todo Items
Endpoint: GET /todos?dueDate={date}
Command:

bash
Copy
curl -X GET "https://api.todo.com/v1/todos?dueDate=2023-12-01"
Explanation:

?dueDate=2023-12-01: Filters todo items by the specified due date.

Expected Output:

json
Copy
[
  {
    "id": "1",
    "title": "Buy groceries",
    "description": "Milk, eggs, bread, butter",
    "dueDate": "2023-12-01",
    "tags": ["shopping", "personal"],
    "status": "completed"
  }
]
User Story 10: Search Todo Items by Keyword
Endpoint: GET /todos?search={keyword}
Command:

bash
Copy
curl -X GET "https://api.todo.com/v1/todos?search=groceries"
Explanation:

?search=groceries: Searches todo items containing the keyword "groceries".

Expected Output:

json
Copy
[
  {
    "id": "1",
    "title": "Buy groceries",
    "description": "Milk, eggs, bread, butter",
    "dueDate": "2023-12-01",
    "tags": ["shopping", "personal"],
    "status": "completed"
  }
]
2. Testing with Postman
Postman is a GUI-based tool for API testing. Below are the steps to test the API using Postman:

Create a New Todo Item:

Set the request method to POST.

Enter the URL: https://api.todo.com/v1/todos.

Add the JSON payload in the "Body" tab:

json
Copy
{
  "title": "Buy groceries",
  "description": "Milk, eggs, bread",
  "dueDate": "2023-12-01",
  "tags": ["shopping", "personal"],
  "status": "pending"
}
Click "Send" and verify the response.

Retrieve All Todo Items:

Set the request method to GET.

Enter the URL: https://api.todo.com/v1/todos.

Click "Send" and verify the response.

Update a Todo Item:

Set the request method to PUT.

Enter the URL: https://api.todo.com/v1/todos/1.

Add the updated JSON payload in the "Body" tab:

json
Copy
{
  "title": "Buy groceries",
  "description": "Milk, eggs, bread, butter",
  "status": "completed"
}
Click "Send" and verify the response.

Delete a Todo Item:

Set the request method to DELETE.

Enter the URL: https://api.todo.com/v1/todos/1.

Click "Send" and verify the response.

3. Performance Testing with JMeter
JMeter is a tool for load and performance testing. Below are the steps to test the API's performance:

Setup:

Open JMeter and create a new test plan.

Add a Thread Group with 100 users and a duration of 5 minutes.

Add HTTP Requests:

Add an HTTP Request sampler for each endpoint (e.g., GET /todos, POST /todos).

Configure the request details (e.g., URL, method, headers, body).

Add Listeners:

Add a "View Results Tree" listener to view individual responses.

Add a "Summary Report" listener to view performance metrics.

Run the Test:

Start the test and monitor the response times and error rates.

Verify Results:

Ensure the average response time is under 300ms.

Ensure the error rate is 0%.

4. Summary of Commands and Tools
Tool	Command/Steps	Purpose
curl	curl -X POST https://api.todo.com/v1/todos -H "Content-Type: application/json" -d '{...}'	Send HTTP requests from the command line.
Postman	Use the GUI to configure and send requests.	Test API endpoints interactively.
JMeter	Configure Thread Groups, HTTP Requests, and Listeners.	Perform load and performance testing.
This detailed approach ensures thorough testing of the Todo API using both command-line tools and GUI-based tools.
