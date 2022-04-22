# Pagination

This assignment will have you building a backend service which allows the frontend to paginate through the data

## What you will be doing

For this assignment you will have to;

1. Complete the schema
2. Add your route
3. Optimise the `/listings` endpoints

The client (frontend) code has mostly been written, but you may wish to style it

## Folder Structure

This repository contains the `client` (frontend) as a subfolder

When you run your node server, it will automatically handle requests to serve the `/client` pages. You can view it in the browser under the URL `http://localhost:3001/`

**There is no need to serve the client separately**

## Tasks

Before starting, run the following commands to setup the npm packages for the backend and client folders

```bash
npm run setup
npm run build
```

### Task 1 - Loading the sample data

Before we can begin, we will load a sample dataset to work with.

MongoDB provides multiple sample datasets, with sample data for us.

1. Log into your MongoDB account
2. Follow the [instructions](https://docs.atlas.mongodb.com/sample-data/) on how to load the sample dataset

> Note: It may take up to 15 minutes for the dataset to completely load

After this, you should have some new databases / collections:

> sample_airbnb
> sample_analytics
> sample_geospatial
> sample_mflix
> sample_restaurants
> sample_supplies
> sample_training
> sample_weatherdata

We will be using the `sample_airbnb` database.

### Task 2 - Setting up the .env file

1. Using the `.env.example` file as a template, create a `.env` file

2. Add your database connection details to your `.env` file, filling in the details as provided to you by MongoDB
   > Hint: The key `DB_NAME` points to the name of the database you want to connect to. Use the name `sample_airbnb`. This will ensure that Mongoose will try and use the existing sample dataset you previously set up

   > Hint: The key `DB_HOST` is the **domain** of your MongoDB connection string

### Task 3 - Completing the schema

Most of the schema has already been written, but it still misses a few fields

1. Examine the `listingsAndReviews` collection
2. Modify the `/models/ListingsAndReviews.js` schema so that it includes the following missing fields:
   - amenities
   - images
   - address
   - reviews

> Hint: Some of these fields may exist as subdocuments

### Task 4 - Create a listings endpoint

We will create an endpoint to load all the airbnb listings

1. Create an endpoint with the path `/listings` in `routes/listingsAndReviews.js`. This will be a `GET` endpoint.

2. Import and use the `ListingsAndReviews` model
   - Use `find()` to get everything from the collection
   - Return the results to the user

### Task 5 - Optimising the listings endpoint with lean()

We will further optimise our query

Under the `/listings` endpoint;

1. Use `lean()` to remove all document methods, and further improve the speed

### Task 6 - Optimising the listings endpoint with limit()

If try to view the listings on the frontend [http://localhost:3001/listings](http://localhost:3001/listings), you will notice it will take some time for the results to arrive

We will now optimise the query so that it returns data in a much shorter time

Our client will send the `limit` value as a query parameter

In the `routes/listingsAndReviews.js` file, find the `/listings` endpoint;

1. Use `limit(n)` to limit the results that the endpoint returns
2. For _n_, read the **request** object's `query` parameter `limit`

> Hint: You can access parameters from the **request** object with the `params` property

> Important! `limit()` expects a number, but each property in our `query` object is a string. You should convert this into a number before using it

### Task 7 - Optimising the listings endpoint with select()

We will further optimise our query

Under the `/listings` endpoint;

1. Use `select()` to cherrypick the following fields from the collection:
   - name
   - propertyType
   - beds
   - numberOfReviews
   - price

### Task 8 - Paginating the results

Being able to skip through our results is critical for any application which uses pagination

Our client will send the `skip` value as a query parameter

1. Use the `skip(n)` method to tell our query to skip a certain number of records, where _n_ is the number of results you will skip.

> Hint: You can access query parameters from the **request** object with the `query` property

> Important! `skip()` expects a number, but each property in our `query` object is a string. You should convert this into a number before using it

# Bonus Tasks

## Styling the frontend

The frontend is severely lacking in style

1. Add your own styles to the frontend React project in `client/src/`

For your changes to take effect, you must rebuild the `client/build` folder with the command `npm run build`
