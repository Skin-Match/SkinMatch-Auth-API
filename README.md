# Architecture Overview
![architecture drawio](https://github.com/nabilmakarim11111/cc-auth-api/assets/93192525/ee501cb0-c4ed-4647-9501-c3e6367b01d5)
-
# Deploy Link
Database (Auth API): https://auth-api-dczyyawmja-et.a.run.app

ML API: https://ml-api-dczyyawmja-et.a.run.app

# [SkinMatch - C241-PS246] Auth API
The auth API provides user authentication such as login, register, update profile, and more.

## Setup 
Here is how to setup the api to run locally on your computer.

**1. Initialize Environment Variables**

```env
JWT = #JWT secret token
```

**2. Create and Generate Service Account Key**

Open Google Cloud Platform console and go to `IAM & Admin` -> `Service Accounts` -> `Create Service Account`, add your service account details and select `Firebase Admin SDK Administrator Service Agent` role and click done. Go to the newly created service account, go to `Keys` tab and create a new JSON key.

Put the newly created service account key to config folder
```
.
├── config/
│   └── service-account.json
└── app.js
└──....
```

**3. Run The API**

Install the required packages with

```
npm install
```

Run the API with either commands

```
npm run start
```

```
npm run dev
```

## List of Available Endpoint
    1. Login
    2. Register
    3. Logout
    4. Delete Account
    5. Reset Password
    6. Get User Profile
    7. Update User Profile
    8. Update Profile Image


## User
* Field Definitions:
    * `name` (string, OPTIONAL): The user's display name.
    * `email` (string, REQUIRED): The user's email address.
    * `password` (string, REQUIRED): The user's password.
    * `gambar_profil` (string, OPTIONAL): The user's prfile image.
    * `skinType` (string, OPTIONAL): The user's skin type, the valid skin type are `oily`, `dry`, and `combination`.
    * `avoided_ingredient` (string, OPTIONAL): The user's display name.
    * `token` (string, OPTIONAL): The user's token when logged in.
.
    
    
## Endpoint List
### Register

* Endpoint:
    * `POST /auth/register`

* Request Body: 
```json
{
    "name": "John Doe",
    "email": "johndoe@example.com",
    "password": "securepassword123"
}

```
* Response:
```json
{
    "status": "successful",
    "message": "User registered successfully",
    "userId": "8315b0a7-b8cd-4c81-b487-a906228a3cff"
}
```

* Notes:
    * The response is a JSON object with a `successful` field indicating the success or failure of the request.


### Login

* Endpoint:
    * `POST /auth/login`

* Request Body: 
```json
{
    "email": "johndoe@example.com",
    "password": "securepassword123"
}
```
* Response:
```json
{
    "status": "successful",
    "message": "User login successfully",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9....
}
```

* Notes:
    * The response is a JSON object with a `successful` field indicating the success or failure of the request.


### Logout

* Endpoint:
    * `POST /auth/logout`

* Request Header: 
    * Content-Type : application/json
    * Authorization : <token>
    
* Response:
```json
{
    "status": "successful",
    "message": "User logout successfully"
}
```

* Notes:
    * The response is a JSON object with a `successful` field indicating the success or failure of the request.


### Delete Account

* Endpoint:
    * `DELETE /auth/delete-account`

* Request Header: 
    * Content-Type : application/json
    * Authorization : <token>

* Response:
```json
{
    "status": "successful",
    "message": "Delete account successfully"
}
```

* Notes:
    * The response is a JSON object with a `successful` field indicating the success or failure of the request.


### Reset Password

* Endpoint:
    * `PUT /auth/reset-password`

* Request Header: 
    * Content-Type : application/json
    * Authorization : <token>

* Response:
```json
{
    "password": "newsecurepassword123"
}
```

* Notes:
    * The response is a JSON object with a `successful` field indicating the success or failure of the request.


### Get User Profile

* Endpoint:
    * `GET /user/profile-details`

* Request Header: 
    * Content-Type : application/json
    * Authorization : <token>

* Response:
```json
{
    "status": "successful",
    "message": "User get profile success",
    "userId": "2322e0df-ea05-48f8-872d-1c7ee4ade264",
    "data": {
        "avoided_ingredient": [],
        "name": "John Doe",
        "gambar_profil": null,
        "skin_type": null,
        "userId": "2322e0df-ea05-48f8-872d-1c7ee4ade264",
        "email": "johndoe@example.com"
    }
}
```

* Notes:
    * The response is a JSON object with a `successful` field indicating the success or failure of the request.


### Update User Profile

* Endpoint:
    * `PUT /user/profile-details`

* Request Header: 
    * Content-Type : application/json
    * Authorization : <token>

* Request Body: 
```json
{
    "data": {
        "skin_type": "oily"
    }
}
```
* Response:
```json
{
    "status": "successful",
    "message": "User update profile success",
    "userId": "2322e0df-ea05-48f8-872d-1c7ee4ade264",
    "data": {
        ...
        "skin_type": "oily",
        "updatedAt": {
            "_seconds": 1718613271,
            "_nanoseconds": 559000000
        }
    }
}
```

* Notes:
    * The response is a JSON object with a `successful` field indicating the success or failure of the request.

### Update Profile Image

* Endpoint:
    * `POST /user/upload-profile-image`

* Request Header: 
    * Content-Type : multipart/form-data
    * Authorization : <token>

* Request Body: 
    * from data
        * Key : profileImage - file
        * Value : image.jpg (import from local)
* Response:
```json
{
    "status": "successful",
    "message": "Profile image uploaded successfully",
    "imageUrl": "https://storage.googleapis.com/......"
```

* Notes:
    * The response is a JSON object with a `successful` field indicating the success or failure of the request.
