# Backend Development for RepoWiki

This section outlines the steps for setting up the backend for RepoWiki, including configuring a Node.js and Express server, implementing RESTful API endpoints, and integrating MongoDB for data storage.

## Set Up Node.js and Express Server

First, ensure Node.js is installed on your system. Then, create a new directory for your backend project and initialize a new Node.js project:

mkdir repowiki-backend && cd repowiki-backend
npm init -y

Install Express and other necessary packages:

npm install express mongoose dotenv body-parser cors

Create a file named `server.js` and set up a basic Express server:

const express = require('express');
const mongoose = require('mongoose');
const bodyParser = require('body-parser');
const cors = require('cors');
require('dotenv').config();

const app = express();
const PORT = process.env.PORT || 5000;

app.use(cors());
app.use(bodyParser.json());

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log('MongoDB Connected'))
  .catch(err => console.log(err));

app.get('/', (req, res) => {
  res.send('RepoWiki Backend is running');
});

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});

## Implement RESTful API Endpoints

Next, define the models and routes for user management, content management, and search functionalities. For example, to create a user model:

// models/User.js
const mongoose = require('mongoose');

const UserSchema = new mongoose.Schema({
  username: { type: String, required: true, unique: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true }
});

module.exports = mongoose.model('User', UserSchema);

And a route for registering a user:

// routes/userRoutes.js
const express = require('express');
const User = require('../models/User');

const router = express.Router();

router.post('/register', async (req, res) => {
  try {
    const newUser = new User(req.body);
    const savedUser = await newUser.save();
    res.status(201).send(savedUser);
  } catch (error) {
    res.status(500).send(error);
  }
});

module.exports = router;

In `server.js`, import and use the routes:

const userRoutes = require('./routes/userRoutes');

app.use('/api/users', userRoutes);

## Integrate MongoDB for Data Storage

Ensure you have a MongoDB database set up, either locally or hosted (e.g., MongoDB Atlas). Use the connection string provided by MongoDB to connect your database in `server.js` using mongoose:

mongoose.connect(process.env.MONGO_URI, options);

Define schemas and models for your data. For instance, besides the User model, you might have models for Documentation and Contributions. Use these models to interact with your database through the API endpoints you create.