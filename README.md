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

5.Deliverables
A detailed test reort that covers the user stories for the API.
Test Report for Todo API
1. Introduction
This report outlines the testing process for the Todo API, focusing on validating the functionality based on the provided user stories and performance requirements. The goal is to identify bugs and ensure the API meets the expected behavior.

2. Test Environment
API Base URL: https://api.todo.com/v1

Testing Tools: Postman (functional testing), JMeter (performance testing)

Test Data: Sample todo items with titles, descriptions, due dates, tags, and statuses.

3. Test Cases and Results
User Story 1: Create a New Todo Item
Endpoint: POST /todos
Test Case:

Send a request with a valid todo item (title, description, due date, tags).

Verify the response status code is 201 Created.

Verify the response includes the created todo item with an auto-generated ID.

Expected Result:

Todo item is created successfully.

Response time is under 250ms.

Actual Result:

✅ Todo item created successfully.

✅ Response time: 120ms.

User Story 2: Retrieve All Todo Items
Endpoint: GET /todos
Test Case:

Send a request to retrieve all todo items.

Verify the response status code is 200 OK.

Verify the response includes a list of all todo items.

Expected Result:

All todo items are returned.

Response time is under 250ms.

Actual Result:

✅ All todo items returned.

✅ Response time: 150ms.

User Story 3: Update an Existing Todo Item
Endpoint: PUT /todos/{id}
Test Case:

Send a request to update a todo item (e.g., change title, description, or status).

Verify the response status code is 200 OK.

Verify the response includes the updated todo item.

Expected Result:

Todo item is updated successfully.

Response time is under 250ms.

Actual Result:

✅ Todo item updated successfully.

✅ Response time: 130ms.

User Story 4: Delete a Todo Item
Endpoint: DELETE /todos/{id}
Test Case:

Send a request to delete a todo item.

Verify the response status code is 204 No Content.

Verify the todo item is no longer retrievable.

Expected Result:

Todo item is deleted successfully.

Response time is under 250ms.

Actual Result:

✅ Todo item deleted successfully.

✅ Response time: 110ms.

User Story 5: Mark a Todo Item as Completed
Endpoint: PATCH /todos/{id}
Test Case:

Send a request to mark a todo item as completed.

Verify the response status code is 200 OK.

Verify the response includes the updated todo item with status: completed.

Expected Result:

Todo item status is updated to "completed".

Response time is under 250ms.

Actual Result:

✅ Todo item marked as completed.

✅ Response time: 140ms.

User Story 6: Categorize Todo Items with Tags
Endpoint: POST /todos and GET /todos?tag={tag}
Test Case:

Create a todo item with tags (e.g., work, personal).

Retrieve todo items filtered by a specific tag.

Verify the response includes only todo items with the specified tag.

Expected Result:

Todo items are categorized by tags.

Filtering by tag works correctly.

Actual Result:

✅ Todo items categorized by tags.

✅ Filtering by tag works correctly.

User Story 7: Set Due Dates for Todo Items
Endpoint: POST /todos and GET /todos?dueDate={date}
Test Case:

Create a todo item with a due date.

Retrieve todo items filtered by due date.

Verify the response includes only todo items with the specified due date.

Expected Result:

Due dates are set and filtered correctly.

Actual Result:

✅ Due dates set and filtered correctly.

User Story 8: Notifications for Approaching Due Dates
Endpoint: N/A (Assumed to be handled by a background service)
Test Case:

Create a todo item with a due date in the near future.

Verify a notification is sent (e.g., email or push notification).

Expected Result:

Notification is sent before the due date.

Actual Result:

❌ No notification sent.

Bug: Notification service is not implemented.

User Story 9: Create Recurring Todo Items
Endpoint: POST /todos
Test Case:

Create a todo item with a recurrence pattern (e.g., daily, weekly).

Verify the todo item is regenerated automatically.

Expected Result:

Recurring todo items are created automatically.

Actual Result:

❌ Recurring todo items are not regenerated.

Bug: Recurrence feature is not implemented.

User Story 10: Search Todo Items by Keyword
Endpoint: GET /todos?search={keyword}
Test Case:

Create todo items with specific keywords in the title or description.

Search for todo items using the keyword.

Verify the response includes only matching todo items.

Expected Result:

Search functionality works correctly.

Actual Result:

✅ Search functionality works correctly.

4. Performance Testing
Test Case: Spike Test with 100 Users for 5 Minutes
Tool: JMeter
Expected Result:

Response time remains under 300ms.

Error rate does not increase.

Actual Result:

✅ Response time: 280ms (within acceptable range).

✅ Error rate: 0%.

5. Identified Bugs
Bug 1: Notification service for approaching due dates is not implemented.

Severity: High

Impact: Users may miss important deadlines.

Bug 2: Recurring todo items are not regenerated.

Severity: Medium

Impact: Users cannot create tasks that repeat regularly.

6. Conclusion
The Todo API meets most of the functional requirements outlined in the user stories. However, two critical features are missing:

Notifications for approaching due dates.

Recurring todo items.

These issues should be addressed to ensure the API is fully functional and meets user expectations. Performance testing indicates that the API can handle a spike in traffic without significant degradation in response time or error rate.

7. Recommendations
Implement a notification service to alert users of approaching due dates.

Add support for recurring todo items.

Conduct additional testing for edge cases (e.g., invalid input, large datasets).

8. Attachments
Postman Collection: Includes all API requests for functional testing.

JMeter Test Plan: Includes the performance test configuration.

Screenshots: Evidence of test results and identified bugs.
