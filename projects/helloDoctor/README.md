# MyDoctor

## Backend

### Technologies

- NodeJs
- MongoDB
- React

## Step 1

Commands:

```console
nvm ls
nvm ls-remote
nvm install 18.17.0
```

Remove an older version

```console
cd ~/.nvm/versions/node
sudo rm -rf v18.13.0
nvm cache clear
```

Install yarn or update

```console
yarn -v
brew upgrade yarn
```

## Step 2 [Project Setup]

```console
mkdir helloDoctor
cd helloDoctor
yarn init
```

Initial `package.json` file

```json
{
  "name": "helloDoctor",
  "version": "1.0.0",
  "description": "helloDoctor Backend System",
  "main": "app.js",
  "author": "Manuj Gogoi",
  "license": "MIT"
}
```

## Step 2 [Install Express]

```console
yarn add express
```

## Step 3 [Install Nodemon]

```console
yarn add nodemon
```

### Add dev script to package.json file

```json
{
  "name": "hello-doctor-backend",
  "version": "1.0.0",
  "description": "helloDoctor Backend System",
  "main": "app.js",
  "author": "Manuj Gogoi",
  "license": "MIT",
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "nodemon": "^3.0.1"
  }
}
```

### Run dev server

```console
yarn dev
```

Test the dev by adding `console.log("Hello World");` in `app.js` file.

## Create an `Express` server:

- In `app.js` file

```js
const express = require("express");

const app = express();
const port = 5001;

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

### Environment Variable setup

- Install `dotenv` using the following command

```console
yarn add dotenv
```

- Create `.env` file in project root.
- Add the following text in the `.env` file

```env
PORT=5001
```

- Update the `index.js` file as follows:

```js
const express = require("express");
const dotenv = require("dotenv").config();

const app = express();
const port = process.env.PORT || 5000;

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

### Create first server response

- Updated `index.js` file

```js
const express = require("express");
const dotenv = require("dotenv").config();

const app = express();
const port = process.env.PORT || 5000;

app.get("/api/v1/login", (req, res) => {
  res.status(200).json({
    status: true,
    message: "Login Process",
  });
});

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

- Use postman to call the following api: `http://localhost:5001/api/v1/login`

### Create Routes

- Create a directory in project root called `routes`.
- Create a file called `contactRoutes.js` file.

`contactRoutes.js`

```js
const express = require("express");
const router = express.Router();

// Get All Records
router.route("/").get((req, res) => {
  res.status(200).json({
    status: true,
    message: "Get all contact",
  });
});

// Create a new Record
router.route("/").post((req, res) => {
  res.status(200).json({
    status: true,
    message: `Create a new contact`,
  });
});

// Get a single Record
router.route("/:id").get((req, res) => {
  res.status(200).json({
    status: true,
    message: `Retrieve the information of the contact with the ID ${req.params.id}`,
  });
});

// Update a single Record
router.route("/:id").put((req, res) => {
  res.status(200).json({
    status: true,
    message: `Update the contact with the ID ${req.params.id}`,
  });
});

// Delete a single Record
router.route("/:id").delete((req, res) => {
  res.status(200).json({
    status: true,
    message: `Delete the contact with the ID ${req.params.id}`,
  });
});

module.exports = router;
```

Updated `index.js` file

```js
const express = require("express");
const dotenv = require("dotenv").config();

const app = express();
const port = process.env.PORT || 5000;

app.use("/api/v1/contacts", require("./routes/contactRoutes"));

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

## Conrollers

- Create a directory called `controllers` in project root.
- Create `ContactController.js` file inside the `controllers` directory.

1. `ContactController.js` file

```js
// @desc Get all contacts
// @route GET /api/v1/contacts
// @access public
const getContacts = (req, res) => {
  res.status(200).json({
    status: true,
    message: "Get all contact",
  });
};

// @desc Create a new contact
// @route POST /api/v1/contacts
// @access public
const createContact = (req, res) => {
  res.status(200).json({
    status: true,
    message: `Create a new contact`,
  });
};

// @desc Get a contact
// @route GET /api/v1/contacts/:id
// @access public
const getContact = (req, res) => {
  res.status(200).json({
    status: true,
    message: `Retrieve the information of the contact with the ID ${req.params.id}`,
  });
};

// @desc Update a contact
// @route PUT /api/v1/contacts/:id
// @access public
const updateContact = (req, res) => {
  res.status(200).json({
    status: true,
    message: `Update the contact with the ID ${req.params.id}`,
  });
};

// @desc Delete a contact
// @route DELETE /api/v1/contacts/:id
// @access public
const deleteContact = (req, res) => {
  res.status(200).json({
    status: true,
    message: `Delete the contact with the ID ${req.params.id}`,
  });
};

module.exports = {
  getContacts,
  createContact,
  getContact,
  updateContact,
  deleteContact,
};
```

2. `contactRouter.js` file

```js
const express = require("express");
const router = express.Router();
const {
  getContacts,
  createContact,
  getContact,
  updateContact,
  deleteContact,
} = require("../controllers/ContactController");
// Get All Records
router.route("/").get(getContacts);

// Create a new Record
router.route("/").post(createContact);

// Get a single Record
router.route("/:id").get(getContact);

// Update a single Record
router.route("/:id").put(updateContact);

// Delete a single Record
router.route("/:id").delete(deleteContact);

module.exports = router;
```

Shorthand version of `contactRouter.js` file

```js
const express = require("express");
const router = express.Router();
const {
  getContacts,
  createContact,
  getContact,
  updateContact,
  deleteContact,
} = require("../controllers/ContactController");

router.route("/").get(getContacts).post(createContact);
router.route("/:id").get(getContact).put(updateContact).delete(deleteContact);

module.exports = router;
```

## Send data through `body` from client

- In order to accept data from client to express server we need to use a body parser so that we can parse the stream of data that we are receiving from the client. And for that we have to use a **middleware** (`express.json()`).

- In `index.js` file add the following line:

```js
app.use(express.json());

// Add the above line before the following line
app.use("/api/v1/contacts", require("./routes/contactRoutes"));
```

### Error Handling

- Create a `middleware` directory.
- Create `ErrorHandlers.js` file inside the `middleware` directory.
  `ErrorHandlers.js` file content:

```js
const { constants } = require("../constants");

const errorHandler = (err, req, res, next) => {
  const statusCode = res.statusCode ? res.statusCode : 500;
  switch (statusCode) {
    case constants.VALIDATION_ERROR:
      res.json({
        title: "Validation Failed",
        message: err.message,
        stackTrace: err.stack,
      });
      break;
    case constants.UNAUTHORIZED:
      res.json({
        title: "Unauthorized Access",
        message: err.message,
        stackTrace: err.stack,
      });
      break;
    case constants.FORBIDDEN:
      res.json({
        title: "Forbidden",
        message: err.message,
        stackTrace: err.stack,
      });
      break;
    case constants.NOT_FOUND:
      res.json({
        title: "Not Found",
        message: err.message,
        stackTrace: err.stack,
      });
      break;
    case constants.SERVER_ERROR:
      res.json({
        title: "Server Error",
        message: err.message,
        stackTrace: err.stack,
      });
      break;
    default:
      console.log("No error. All good!");
  }
  res.json({ message: err.message, stackTrace: err.stack });
};

module.exports = errorHandler;
```

Updated `index.js` file:

```js
const express = require("express");
const dotenv = require("dotenv").config();
const errorHandler = require("./middleware/ErrorHandlers");

const app = express();
const port = process.env.PORT || 5000;

app.use(express.json());
app.use("/api/v1/contacts", require("./routes/contactRoutes"));
app.use(errorHandler);

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

> Since we are going to use **`MongoDB`** and **`Mongoose`**, so, whenever we interact with the MongoDB always get a `promise`. So in order to resolve the `promise` we are going to make all methods `async` as given below.

File: ContactController.js

```js
// @desc Get all contacts
// @route GET /api/v1/contacts
// @access public
const getContacts = async (req, res) => {
  res.status(200).json({
    status: true,
    message: "Get all contact",
  });
};

// @desc Create a new contact
// @route POST /api/v1/contacts
// @access public
const createContact = async (req, res) => {
  console.log("Request Body: ", req.body);
  const { name, email, phone, address } = req.body;

  // Validation
  if (!name) {
    res.status(400);
    throw new Error("Name field is required");
  }

  if (!phone) {
    res.status(400);
    throw new Error("Phone field is required");
  }

  res.status(200).json({
    status: true,
    message: `Create a new contact`,
  });
};

// @desc Get a contact
// @route GET /api/v1/contacts/:id
// @access public
const getContact = async (req, res) => {
  res.status(200).json({
    status: true,
    message: `Retrieve the information of the contact with the ID ${req.params.id}`,
  });
};

// @desc Update a contact
// @route PUT /api/v1/contacts/:id
// @access public
const updateContact = async (req, res) => {
  res.status(200).json({
    status: true,
    message: `Update the contact with the ID ${req.params.id}`,
  });
};

// @desc Delete a contact
// @route DELETE /api/v1/contacts/:id
// @access public
const deleteContact = async (req, res) => {
  res.status(200).json({
    status: true,
    message: `Delete the contact with the ID ${req.params.id}`,
  });
};

module.exports = {
  getContacts,
  createContact,
  getContact,
  updateContact,
  deleteContact,
};
```

- Whenever we use `async` and if we want to catch an error we need to make use of a `try-catch` block. In order to use the `try-catch` block we have to add the `try-catch` block in each of the async functions. But there is a better way to do this. We can use a middleware for this - `express-async-handler`.
- Install `express-async-handler` (_Simple middleware for handling exceptions inside of async express routes and passing them to your express error handlers._)

### Step 1

```console
yarn add express-async-handler
```

### Step 2

- import in controller file.

```js
const asyncHandler = require("express-async-handler");
```

- Wrap all async methods inside the `asyncHandler` function. for example:

```js
// @desc Get all contacts
// @route GET /api/v1/contacts
// @access public
const getContacts = asyncHandler(async (req, res) => {
  res.status(200).json({
    status: true,
    message: "Get all contact",
  });
});
```

## DB Setup (MongoDB)

- MongoDB Atlas free tier
- Install Mongoose

```console
yarn add mongoose
```

- All CRUD operatins are made for Users and Contacts.

- Install `bcrypt`:

```console
yarn add bcrypt
```

- Install `jsonwebtoken` for authentication

```console
yarn add jsonwebtoken
```

# Testing the nodejs app using Jest

## Installation

```console
yarn add --dev jest supertest cross-env
```

- **jest**: Jest is a framework for testing JavaScript code. Unit testing is the main usage of it.
- **supertest**: Using Supertest, we can test endpoints and routes on HTTP servers.
- **cross-env**: You can set environmental variables inline within a command using cross-env.

Mongodb memory server for testing

```console
yarn add mongodb-memory-server
```
