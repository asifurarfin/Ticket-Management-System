Bank Support Ticket API

All Endpoints:

1.Authentication Endpoints:
[POST] /user/register
[POST] /manager/register
[POST] /itdesk/register
[POST] /login
[POST] /logout

2.Branch Endpoints:
[POST] /branch/create
[GET] /branch/list
[POST] /branch/update/{id}
[POST] /branch/delete/{id}

3.User Endpoints:
[GET] /user/list

4.Category Endpoints:
[POST] /category/create
[GET] /category/list
[POST] /category/update/{id}
[POST] /category/delete/{id}

5.Subcategory Endpoints:
[POST] /subcategory/create
[POST] /subcategory/update/{id}
[POST] /subcategory/delete/{id}

6.Ticket Endpoints:
[POST] /ticket/create
[GET] /ticket/list
[POST] /ticket/update/{id}
[POST] /ticket/delete/{id}

7.Endpoint: user/register, manager/register, or itdesk/register
Method: POST

Description:

This endpoint is used to register a new user, manager, or IT desk user.
Request Body Parameters:

name: (Required) The name of the user. It must be a string with a maximum length of 255 characters.
email: (Required) The email address of the user. It must be a valid email format and unique in the users table, with a maximum length of 255 characters.
password: (Required) The password of the user. It must be a string with a minimum length of 3 characters.
branch_id: (optional) The ID of the branch the user belongs to. It must be an integer with a minimum value of 1.
mobile: (Optional) The mobile number of the user. It must be an integer.
Example Request:
{
    "name": "John Doe",
    "email": "johndoe@example.com",
    "password": "secretpassword",
    "branch_id": 1,
    "mobile": 1234567890
}
Example Response:
Success (200 OK):

{
    "message": "This is your auth token"
}
Error (4xx, 5xx):

{
    "error": "Error message describing the issue."
}

8.Endpoint: /login
Method: POST

Description:

This endpoint is used for user login.

Request Body Parameters:

email: (Required) The email address of the user. It must be a valid email format with a maximum length of 255 characters.
password: (Required) The password of the user. It must be a string with a minimum length of 3 characters.
Example Request:
{
    "email": "johndoe@example.com",
    "password": "secretpassword"
}
Example Response:
Success (200 OK):

{
    "message": "Login Successful",
    "token": "generated_token_here"
}
Error (4xx, 5xx):

{
    "error": "Invalid credentials"
}

9.Endpoint: /branch/create
Method: POST

Description:

This endpoint is used to create a new branch.

Request Body Parameters:

name: (Required) The name of the branch. It must be a string with a maximum length of 255 characters and must be unique among existing branch names.
address: (Optional) The address of the branch. It must be a string with a maximum length of 255 characters.
routing: (Required) The routing number of the branch. It must be an integer.
Example Request:
{
    "name": "Branch Name",
    "address": "Branch Address",
    "routing": 123456789
}
Example Response:
Success (200 OK):

{
    "message": "Branch Name branch created successfully"
}
Error (4xx, 5xx):

{
    "error": "Error message describing the issue"
}
10.Endpoint: /branch/list
Method: GET

Description:

This endpoint is used to retrieve a list of all branches along with their associated users and tickets.

Example Response:
Success (200 OK):

[
    {
        "id": 1,
        "name": "Branch 1",
        "address": "Address 1",
        "routing": 123456789,
        "created_at": "2022-03-25T12:00:00Z",
        "updated_at": "2022-03-25T12:00:00Z",
        "users": [
            {
                "id": 1,
                "name": "User 1",
                "email": "user1@example.com",
                "created_at": "2022-03-25T12:00:00Z",
                "updated_at": "2022-03-25T12:00:00Z"
            },
            {
                "id": 2,
                "name": "User 2",
                "email": "user2@example.com",
                "created_at": "2022-03-25T12:00:00Z",
                "updated_at": "2022-03-25T12:00:00Z"
            }
        ],
        "ticket": [
            {
                "id": 1,
                "subject": "Ticket 1",
                "details": "Details of Ticket 1",
                "status": "in_progress",
                "created_at": "2022-03-25T12:00:00Z",
                "updated_at": "2022-03-25T12:00:00Z"
            },
            {
                "id": 2,
                "subject": "Ticket 2",
                "details": "Details of Ticket 2",
                "status": "approved",
                "created_at": "2022-03-25T12:00:00Z",
                "updated_at": "2022-03-25T12:00:00Z"
            }
        ]
    },
    {
        "id": 2,
        "name": "Branch 2",
        "address": "Address 2",
        "routing": 987654321,
        "created_at": "2022-03-25T12:00:00Z",
        "updated_at": "2022-03-25T12:00:00Z",
        "users": [],
        "ticket": []
    }
]
Error (4xx, 5xx):

{
    "error": "Error message describing the issue"
}

11.Endpoint: /branch/update/{id}
Method: POST

Description:

This endpoint is used to update an existing branch with the specified ID.

Path Parameters:

id: (Required) The ID of the branch to be updated.
Request Body Parameters:

name: (Optional) The updated name of the branch. It must be a string with a maximum length of 255 characters and must be unique among existing branch names.
address: (Optional) The updated address of the branch. It must be a string with a maximum length of 255 characters.
routing: (Optional) The updated routing number of the branch. It must be an integer.
Example Request:
{
    "name": "Updated Branch Name",
    "address": "Updated Branch Address",
    "routing": 987654321
}
Example Response:
Success (200 OK):

{
    "message": "Updated Branch Name updated"
}
Error (4xx, 5xx):

{
    "error": "Error message describing the issue"
}
Endpoint: /branch/delete/{id}
Method: POST

Description:

This endpoint is used to delete an existing branch with the specified ID.

Path Parameters:

id: (Required) The ID of the branch to be deleted.
Example Response:
Success (200 OK):

{
    "message": "Branch Name deleted"
}
Error (4xx, 5xx):

{
    "error": "Error message describing the issue"
}

12.Endpoint: /user/list
Method: GET

Description:

This endpoint is used to retrieve a list of users based on their roles.

Request Body Parameters:

Example Response:
Success (200 OK):

{
    "user": [
        {
            "id": 1,
            "name": "User 1",
            "email": "user1@example.com",
            "role": "manager",
            "created_at": "2022-03-25T12:00:00Z",
            "updated_at": "2022-03-25T12:00:00Z",
            "tickets": [
                {
                    "id": 1,
                    "subject": "Ticket 1",
                    "details": "Details of Ticket 1",
                    "status": "in_progress",
                    "created_at": "2022-03-25T12:00:00Z",
                    "updated_at": "2022-03-25T12:00:00Z"
                },
                {
                    "id": 2,
                    "subject": "Ticket 2",
                    "details": "Details of Ticket 2",
                    "status": "approved",
                    "created_at": "2022-03-25T12:00:00Z",
                    "updated_at": "2022-03-25T12:00:00Z"
                }
            ],
            "branch": {
                "id": 1,
                "name": "Branch 1",
                "address": "Address 1",
                "routing": 123456789,
                "created_at": "2022-03-25T12:00:00Z",
                "updated_at": "2022-03-25T12:00:00Z"
            }
        },
        {
            "id": 2,
            "name": "User 2",
            "email": "user2@example.com",
            "role": "itdesk",
            "created_at": "2022-03-25T12:00:00Z",
            "updated_at": "2022-03-25T12:00:00Z",
            "tickets": [],
            "branch": null
        }
    ]
}
Error (4xx, 5xx):

{
    "error": "Error message describing the issue"
}

13.Endpoint: /category/create
Method: POST

Description:

This endpoint is used to create a new category.

Request Body Parameters:

title: (Required) The title of the category. It must be a string with a maximum length of 255 characters.
Example Request:
{
    "title": "New Category"
}
Example Response:
Success (200 OK):

{
    "message": "New Category Created successfully"
}
Error (4xx, 5xx):

{
    "message": "Error message describing the issue"
}

14.Endpoint: /category/list
Method: GET

Description:

This endpoint is used to retrieve a list of all categories along with their associated subcategories.

Example Response:
Success (200 OK):Returns a JSON array containing information about all categories and their associated subcategories.

[
    {
        "id": 1,
        "title": "Category 1",
        "created_at": "2022-03-25T12:00:00Z",
        "updated_at": "2022-03-25T12:00:00Z",
        "subcategories": [
            {
                "id": 1,
                "title": "Subcategory 1",
                "category_id": 1,
                "created_at": "2022-03-25T12:00:00Z",
                "updated_at": "2022-03-25T12:00:00Z"
            },
            {
                "id": 2,
                "title": "Subcategory 2",
                "category_id": 1,
                "created_at": "2022-03-25T12:00:00Z",
                "updated_at": "2022-03-25T12:00:00Z"
            }
        ]
    },
    {
        "id": 2,
        "title": "Category 2",
        "created_at": "2022-03-25T12:00:00Z",
        "updated_at": "2022-03-25T12:00:00Z",
        "subcategories": []
    }
]
Error (4xx, 5xx):

{
    "error": "You are not authorized to view categories."
}
