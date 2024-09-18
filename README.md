# Live Scoreboard API

## Overview

This is a simple API architecture structure designed to manage the live scoreboard. This API enables real-time score updates, ensuring that user actions are reflected promptly on the scoreboard. It also includes robust security features to prevent unauthorized manipulation of scores and ensures that only valid users can update or access scores.

## API Endpoints

### 1. Update Score

- **Endpoint:** `POST /api/score/update`
- **Description:** Updates the user's score when they complete an action.
- **Request Body:**
  ```json
  {
    "user_id": "string",
    "action_id": "string",
    "auth_token": "string",
    "timestamp": "string"
  }
- **Response:**

  - **Success:** Returns the status of the operation.
    ```json
    {
      "status": "success",
    }
    ```

  - **Error:** Returns an error message if the update fails.
    ```json
    {
      "status": "error",
      "message": "Invalid authentication token"
    }
    ```

### 2. Get Top 10 Scores

- **Endpoint:** `GET /api/score/top10`
- **Description:** Returns the top 10 scores from the scoreboard.
- **Request Body:**
  ```json
  {
    "user_id": "string",
    "auth_token": "string",
    "timestamp": "string"
  }
- **Response:**
    - **Success:** Returns the top 10 scores.
        ```json
        {
            "status": "success",
            "top_10_scores": [
            {"user_id": "string", "score": "integer"},
            ...
            ]
        }
        ```
      - **Error:** Returns an error message if the update fails.
        ```json
        {
        "status": "error",
        "message": "Invalid authentication token"
        }
        ```
    
    

## Authentication and Security

### Auth Token Validation
- Each request must include a valid `auth_token`.
- The `auth_token` will be verified by the server to ensure the request is legitimate.
- Tokens will have a limited lifetime and must be renewed periodically.

### Action Validation
- The `action_id` must be verified to ensure that the action was indeed performed by the user.

### Encryption
- All sensitive data, including `auth_token`,`user_id` and `action_id`, will be encrypted to prevent unauthorized access.

## Error Handling
- The API will return appropriate error messages for invalid requests or unauthorized access.
- Error messages will be informative and help the user understand the issue.


## Database Schema

### Users Table
- `user_id` (Primary Key)
- `username` (String)
- `email` (String)
- `score` (Integer)
- `auth_token` (String)


### Scores Table
- `score_id` (Primary Key)
- `user_id` (Foreign Key)
- `score` (Integer)
- `timestamp` (DateTime)

### Actions Table
- `action_id` (Primary Key)
- `user_id` (Foreign Key)
- `action_type` (String)
- `timestamp` (DateTime)


## Diagramm Illustrating the flow of the API

![API Diagram]( /API%20diagramm.drawio.png )

