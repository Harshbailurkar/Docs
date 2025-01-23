# Backend
*Status Code*
<br/>
<br/>

![alt text](image.png)

## Endpoints

### LinkMaster Endpoints

#### `POST` /api/v1/linkmaster

**Description:** Add a new link.

**Request Body:**
- `displayName` (String, required): The display name of the link.
- `link` (String, required): The URL of the link.
- `userType` (String, required): The user type for which the link is applicable. Possible values: "School Student", "College Student".
- `isActive` (Boolean, optional): The activation status of the link. Default is `true`.

**Response:**
- `201 Created`: Link added successfully.
  ```json
  {
    "status": 201,
    "data": {
      "_id": "linkId",
      "displayName": "displayName",
      "link": "link",
      "userType": "userType",
      "isActive": true,
      "createdAt": "timestamp",
      "updatedAt": "timestamp"
    },
    "message": "Link added successfully"
  }
  ```

**Errors:**
- `400 Bad Request`: Please provide all required fields.
- `409 Conflict`: Link with the same name or URL already exists.

#### `DELETE` /api/v1/linkmaster/:linkId

**Description:** Remove a link by ID.

**Response:**
- `200 OK`: Link removed successfully.
  ```json
  {
    "status": 200,
    "data": null,
    "message": "Link removed successfully"
  }
  ```

**Errors:**
- `404 Not Found`: Link not found.

#### `PATCH` /api/v1/linkmaster/changestatus/:linkId

**Description:** Toggle the activation status of a link by ID.

**Response:**
- `200 OK`: Link activation status toggled successfully.
  ```json
  {
    "status": 200,
    "data": {
      "_id": "linkId",
      "displayName": "displayName",
      "link": "link",
      "userType": "userType",
      "isActive": false,
      "createdAt": "timestamp",
      "updatedAt": "timestamp"
    },
    "message": "Link activation status toggled successfully"
  }
  ```

**Errors:**
- `404 Not Found`: Link not found.

### User Endpoints

#### `POST` /api/v1/user/register

**Description:** Register a new user.

**Request Body:**
- `fullName` (String, required): The full name of the user.
- `email` (String, required): The email of the user.
- `password` (String, required): The password of the user.
- `age` (Number, required): The age of the user.
- `category` (String, required): The category of the user. Possible values: "School Student", "College Student".
- `skillLevel` (String, required): The skill level of the user. Possible values: "Beginner", "Intermediate", "Advanced".

**Response:**
- `201 Created`: User registered successfully.
  ```json
  {
    "status": 201,
    "data": {
      "_id": "userId",
      "fullName": "fullName",
      "email": "email",
      "age": "age",
      "category": "category",
      "skillLevel": "skillLevel",
      "stats": {
        "completedCourses": 0,
        "completedProjects": 0,
        "totalPoints": 0,
        "level": "Bronze",
        "totalLearningHours": 0
      },
      "enrollments": [],
      "createdAt": "timestamp",
      "updatedAt": "timestamp"
    },
    "message": "User registered successfully"
  }
  ```

**Errors:**
- `400 Bad Request`: Please provide all required fields.
- `409 Conflict`: User already exists.
- `500 Internal Server Error`: Failed to create user.

#### `POST` /api/v1/user/login

**Description:** Log in a user.

**Request Body:**
- `email` (String, required): The email of the user.
- `password` (String, required): The password of the user.

**Response:**
- `200 OK`: User logged in successfully.
  ```json
  {
    "status": 200,
    "data": {
      "user": {
        "_id": "userId",
        "fullName": "fullName",
        "email": "email",
        "age": "age",
        "category": "category",
        "skillLevel": "skillLevel",
        "stats": {
          "completedCourses": 0,
          "completedProjects": 0,
          "totalPoints": 0,
          "level": "Bronze",
          "totalLearningHours": 0
        },
        "enrollments": [],
        "createdAt": "timestamp",
        "updatedAt": "timestamp"
      },
      "accessToken": "accessToken",
      "refreshToken": "refreshToken",
      "LinkMaster": [
        {
          "_id": "linkId",
          "displayName": "displayName",
          "link": "link",
          "userType": "userType",
          "isActive": true,
          "createdAt": "timestamp",
          "updatedAt": "timestamp"
        }
      ]
    },
    "message": "User logged in successfully"
  }
  ```

**Errors:**
- `400 Bad Request`: Please provide all required fields.
- `404 Not Found`: User not found.
- `401 Unauthorized`: Incorrect password.

#### `POST` /api/v1/user/logout

**Description:** Log out a user.

**Response:**
- `200 OK`: User logged out successfully.
  ```json
  {
    "status": 200,
    "data": null,
    "message": "User logged out successfully"
  }
  ```

**Errors:**
- `404 Not Found`: User not found.

### Admin Endpoints

#### `POST` /api/v1/admin/register

**Description:** Register a new admin.

**Request Body:**
- `name` (String, required): The name of the admin.
- `email` (String, required): The email of the admin.
- `password` (String, required): The password of the admin.
- `employeeId` (String, required): The employee ID of the admin.

**Response:**
- `201 Created`: Admin created successfully.
  ```json
  {
    "status": 201,
    "data": {
      "createdAdmin": {
        "_id": "adminId",
        "name": "name",
        "email": "email",
        "employeeId": "employeeId",
        "createdAt": "timestamp",
        "updatedAt": "timestamp"
      },
      "accessToken": "accessToken",
      "refreshToken": "refreshToken"
    },
    "message": "Admin created successfully"
  }
  ```

**Errors:**
- `400 Bad Request`: Please provide all required fields.
- `409 Conflict`: Admin already exists.

#### `POST` /api/v1/admin/login

**Description:** Login as admin.

**Request Body:**
- `email` (String, required): The email of the admin.
- `password` (String, required): The password of the admin.

**Response:**
- `200 OK`: Login successful.
  ```json
  {
    "status": 200,
    "data": {
      "admin": {
        "_id": "adminId",
        "name": "name",
        "email": "email",
        "employeeId": "employeeId",
        "createdAt": "timestamp",
        "updatedAt": "timestamp"
      },
      "accessToken": "accessToken",
      "refreshToken": "refreshToken"
    },
    "message": "Login successful"
  }
  ```

**Errors:**
- `404 Not Found`: Admin not found.
- `401 Unauthorized`: Invalid credentials.

#### `POST` /api/v1/admin/logout

**Description:** Logout as admin.

**Response:**
- `200 OK`: User logged out successfully.
  ```json
  {
    "status": 200,
    "data": null,
    "message": "User logged out successfully"
  }
  ```

**Errors:**
- `401 Unauthorized`: Access Token Required.

#### `POST` /api/v1/admin/sub-admins

**Description:** Get all sub-admins.

**Response:**
- `200 OK`: SubAdmins retrieved successfully.
  ```json
  {
    "status": 200,
    "data": [
      {
        "_id": "subAdminId",
        "name": "name",
        "email": "email",
        "employeeId": "employeeId",
        "createdAt": "timestamp",
        "updatedAt": "timestamp"
      }
    ],
    "message": "SubAdmins retrieved successfully"
  }
  ```

**Errors:**
- `401 Unauthorized`: Access Token Required.

#### `POST` /api/v1/admin/sub-admins/create

**Description:** Create a new sub-admin.

**Request Body:**
- `name` (String, required): The name of the sub-admin.
- `email` (String, required): The email of the sub-admin.
- `password` (String, required): The password of the sub-admin.
- `employeeId` (String, required): The employee ID of the sub-admin.

**Response:**
- `201 Created`: SubAdmin created successfully.
  ```json
  {
    "status": 201,
    "data": {
      "newSubAdmin": {
        "_id": "subAdminId",
        "name": "name",
        "email": "email",
        "employeeId": "employeeId",
        "createdAt": "timestamp",
        "updatedAt": "timestamp"
      },
      "accessToken": "accessToken",
      "refreshToken": "refreshToken"
    },
    "message": "SubAdmin created successfully"
  }
  ```

**Errors:**
- `409 Conflict`: SubAdmin already exists.

#### `DELETE` /api/v1/admin/sub-admins/{id}

**Description:** Remove a sub-admin.

**Parameters:**
- `id` (String, required): The ID of the sub-admin.

**Response:**
- `200 OK`: SubAdmin removed successfully.
  ```json
  {
    "status": 200,
    "data": null,
    "message": "SubAdmin removed successfully"
  }
  ```

**Errors:**
- `404 Not Found`: SubAdmin not found.

#### `PATCH` /api/v1/admin/sub-admins/{id}/password

**Description:** Update sub-admin password.

**Parameters:**
- `id` (String, required): The ID of the sub-admin.

**Request Body:**
- `newPassword` (String, required): The new password for the sub-admin.

**Response:**
- `200 OK`: Password updated successfully.
  ```json
  {
    "status": 200,
    "data": null,
    "message": "Password updated successfully"
  }
  ```

**Errors:**
- `400 Bad Request`: New password is required.
- `404 Not Found`: SubAdmin not found.

### SubAdmin Endpoints

#### `POST` /api/v1/sadmin/login

**Description:** Login as sub-admin.

**Request Body:**
- `email` (String, required): The email of the sub-admin.
- `password` (String, required): The password of the sub-admin.

**Response:**
- `200 OK`: Login successful.
  ```json
  {
    "status": 200,
    "data": {
      "subAdmin": {
        "_id": "subAdminId",
        "name": "name",
        "email": "email",
        "employeeId": "employeeId",
        "createdAt": "timestamp",
        "updatedAt": "timestamp"
      },
      "accessToken": "accessToken",
      "refreshToken": "refreshToken"
    },
    "message": "Login successful"
  }
  ```

**Errors:**
- `404 Not Found`: SubAdmin not found.
- `401 Unauthorized`: Invalid credentials.

#### `POST` /api/v1/sadmin/logout

**Description:** Logout as sub-admin.

**Response:**
- `200 OK`: User logged out successfully.
  ```json
  {
    "status": 200,
    "data": null,
    "message": "User logged out successfully"
  }
  ```

**Errors:**
- `401 Unauthorized`: Access Token Required.

### Project Endpoints

#### `POST` /api/v1/projects/create

**Description:** Create a new project.

**Request Body:**
- `title` (String, required): The title of the project.
- `description` (String, required): The description of the project.
- `difficulty` (String, required): The difficulty level of the project. Possible values: "Beginner", "Intermediate", "Advanced".
- `recommendedFor` (String, required): The recommended user type for the project. Possible values: "School Student", "College Student".
- `category` (String, required): The category of the project.
- `thumbnail` (File, optional): The thumbnail image file for the project.
- `videoLink` (File, optional): The video file for the project.
- `kitIncluded` (Boolean, optional): Whether the project includes a kit. Default is `false`.
- `kitDetails` (String, optional): Details about the kit.
- `prerequisites` (Array of Strings, optional): Prerequisites for the project.
- `additionalResources` (Array of Objects, optional): Additional resources for the project.
- `tags` (Array of Strings, optional): Tags for the project.
- `steps` (Array of Objects, optional): Steps for the project.

**Response:**
- `201 Created`: Project created successfully.
  ```json
  {
    "status": 201,
    "data": {
      // ...project data...
    },
    "message": "Project created successfully"
  }
  ```

**Errors:**
- `400 Bad Request`: Please provide all required fields.
- `500 Internal Server Error`: Failed to create project.

#### `GET` /api/v1/projects

**Description:** Get all projects.

**Response:**
- `200 OK`: Projects retrieved successfully.
  ```json
  {
    "status": 200,
    "data": [
      // ...projects data...
    ],
    "message": "Projects retrieved successfully"
  }
  ```

**Errors:**
- `500 Internal Server Error`: Failed to retrieve projects.

#### `GET` /api/v1/projects/:id

**Description:** Get a project by ID.

**Response:**
- `200 OK`: Project retrieved successfully.
  ```json
  {
    "status": 200,
    "data": {
      // ...project data...
    },
    "message": "Project retrieved successfully"
  }
  ```

**Errors:**
- `404 Not Found`: Project not found.
- `500 Internal Server Error`: Failed to retrieve project.

#### `PATCH` /api/v1/projects/:id

**Description:** Update a project by ID.

**Request Body:**
- `title` (String, optional): The title of the project.
- `description` (String, optional): The description of the project.
- `difficulty` (String, optional): The difficulty level of the project. Possible values: "Beginner", "Intermediate", "Advanced".
- `recommendedFor` (String, optional): The recommended user type for the project. Possible values: "School Student", "College Student".
- `category` (String, optional): The category of the project.
- `thumbnail` (File, optional): The thumbnail image file for the project.
- `videoLink` (File, optional): The video file for the project.
- `kitIncluded` (Boolean, optional): Whether the project includes a kit. Default is `false`.
- `kitDetails` (String, optional): Details about the kit.
- `prerequisites` (Array of Strings, optional): Prerequisites for the project.
- `additionalResources` (Array of Objects, optional): Additional resources for the project.
- `tags` (Array of Strings, optional): Tags for the project.
- `steps` (Array of Objects, optional): Steps for the project.

**Response:**
- `200 OK`: Project updated successfully.
  ```json
  {
    "status": 200,
    "data": {
      // ...updated project data...
    },
    "message": "Project updated successfully"
  }
  ```

**Errors:**
- `404 Not Found`: Project not found.
- `500 Internal Server Error`: Failed to update project.

#### `DELETE` /api/v1/projects/:id

**Description:** Delete a project by ID.

**Response:**
- `200 OK`: Project deleted successfully.
  ```json
  {
    "status": 200,
    "data": null,
    "message": "Project deleted successfully"
  }
  ```

**Errors:**
- `404 Not Found`: Project not found.
- `500 Internal Server Error`: Failed to delete project.

#### `GET` /api/v1/projects/difficulty/:difficulty

**Description:** Get projects by difficulty.

**Response:**
- `200 OK`: Projects retrieved successfully.
  ```json
  {
    "status": 200,
    "data": [
      // ...projects data...
    ],
    "message": "Projects retrieved successfully"
  }
  ```

**Errors:**
- `500 Internal Server Error`: Failed to retrieve projects.

#### `GET` /api/v1/projects/recommended/:recommendedFor

**Description:** Get projects by recommended user type.

**Response:**
- `200 OK`: Projects retrieved successfully.
  ```json
  {
    "status": 200,
    "data": [
      // ...projects data...
    ],
    "message": "Projects retrieved successfully"
  }
  ```

**Errors:**
- `500 Internal Server Error`: Failed to retrieve projects.

#### `GET` /api/v1/projects/popular

**Description:** Get the most popular project.

**Response:**
- `200 OK`: Most popular project retrieved successfully.
  ```json
  {
    "status": 200,
    "data": [
      // ...project data...
    ],
    "message": "Most popular project retrieved successfully"
  }
  ```

**Errors:**
- `500 Internal Server Error`: Failed to retrieve project.

#### `GET` /api/v1/projects/kit-included

**Description:** Get projects with kit included.

**Response:**
- `200 OK`: Projects retrieved successfully.
  ```json
  {
    "status": 200,
    "data": [
      // ...projects data...
    ],
    "message": "Projects retrieved successfully"
  }
  ```

**Errors:**
- `500 Internal Server Error`: Failed to retrieve projects.

#### `GET` /api/v1/projects/category/:category

**Description:** Get projects by category.

**Response:**
- `200 OK`: Projects retrieved successfully.
  ```json
  {
    "status": 200,
    "data": [
      // ...projects data...
    ],
    "message": "Projects retrieved successfully"
  }
  ```

**Errors:**
- `500 Internal Server Error`: Failed to retrieve projects.

#### `GET` /api/v1/projects/tag/:tag

**Description:** Get projects by tag.

**Response:**
- `200 OK`: Projects retrieved successfully.
  ```json
  {
    "status": 200,
    "data": [
      // ...projects data...
    ],
    "message": "Projects retrieved successfully"
  }
  ```

**Errors:**
- `500 Internal Server Error`: Failed to retrieve projects.

#### `POST` /api/v1/projects/:projectId/steps

**Description:** Add a step to a project.

**Request Body:**
- `stepNumber` (Number, required): The step number.
- `title` (String, required): The title of the step.
- `description` (String, required): The description of the step.
- `stepVideoLink` (File, optional): The video file for the step.

**Response:**
- `200 OK`: Step added successfully.
  ```json
  {
    "status": 200,
    "data": {
      // ...updated project data...
    },
    "message": "Step added successfully"
  }
  ```

**Errors:**
- `500 Internal Server Error`: Failed to add step.

#### `PATCH` /api/v1/projects/:projectId/:stepNumber

**Description:** Update the visibility of a step.

**Response:**
- `200 OK`: Step visibility updated successfully.
  ```json
  {
    "status": 200,
    "data": {
      // ...updated project data...
    },
    "message": "Step visibility updated successfully"
  }
  ```

**Errors:**
- `404 Not Found`: Step not found.
- `500 Internal Server Error`: Failed to update step visibility.

#### `DELETE` /api/v1/projects/:projectId/:stepNumber

**Description:** Delete a step from a project.

**Response:**
- `200 OK`: Step deleted successfully.
  ```json
  {
    "status": 200,
    "data": {
      // ...updated project data...
    },
    "message": "Step deleted successfully"
  }
  ```

**Errors:**
- `404 Not Found`: Step not found.
- `500 Internal Server Error`: Failed to delete step.