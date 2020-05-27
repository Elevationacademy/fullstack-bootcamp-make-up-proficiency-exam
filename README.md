### INTRO

Over the last four weeks you've learned HTML, CSS and CSS Grid, JavaScript basics and ES6 array methods, git version control, jQuery, Handlebars, OOP, APIs, Node JS, Express and a few more things here and there.

It's time to put your skills to practice by creating a movies search app!

Your app will take a title of a movie and display a list of relevant movies on the page. You should also have the ability to 'like' movies and save them in your favorites.

Click [here](https://kernel-files.s3.eu-west-1.amazonaws.com/images/0374078b.png) to see how your app should look - more or less, design is up to you - in the end.

We'll be taking you through this step by step. So follow the instructions and use what you've learned thus far. You can reference previous code you've written, notes, and of course Google.

Good luck!

* * * * *

### 1\. SET UP YOUR PROJECT

-   Create your local directory with Git and NPM. You should have a `server.js` file and a dist folder

-   Inside your dist folder you should have an `index.html`, `style.css`, `main.js`, `MovieManager.js` and `Renderer.js`

-   Install jquery, handlebars, express, and urllib with NPM, we'll be using these packages in the project
-   Don't forget to add `node_modules` to your `.gitignore` file!
-   Make your new repository on github and call it bootcamp-movies. Link your repo to your local directory, then commit your files for your initial commit

* * * * *

### 2\. SET UP YOUR SERVER

Create a server using express on port 8080. Don't forget to use your `dist` and `node_modules` folders.

Create a get route called `/sanity` that responds with "OK" to make sure your server is set up properly.

* * * * *

### 3\. REQUEST TO THE MOVIE API

We'll be making requests to the [OMDB](http://www.omdbapi.com/#usage) API from our server. This API gives us access to many movies.

-   Set up a get route called `/movies` that receives a `title` parameter
-   This route should make a request to the Movie API, and send back the data it receives

-   Use the `title` param in this request - in the API docs you'll notice you can search any movie with the 's' parameter
- You should also use this as the API KEY: `a2e2ca53`

-   `console.log` to make sure you're getting your results back

Important: Make sure you are paying attention to casing.

Suggestion: use Postman to test this route

Hint: If you're having trouble with getting your results back from urllib, check out the [documentation](https://www.npmjs.com/package/urllib).
You can also try the [request package](https://www.npmjs.com/package/request)

 Commit your code!

* * * * *

### 4\. CLIENT SETUP

- Create a class called `MovieManager` in the `MovieManager.js` file. The `MovieManager` class should have the following:
    - a `movies` property
    - a `getMovies` method that:
        - receives a parameter, `title`
        - makes a request to the `/movies` route with the title
        - You should receive an object with an array of movies from this request
        - Updates the `movies` array in the class with the array of movies from the response
-   Setup your HTML boilerplate with all the relevant scripts
-   Create an input for a movie title, and a Search! button
-   In `main.js`:
    - Create an instance of your `MovieManager` class
    - Add a click listener so that when the button is clicked, you take the value of the input (with jQuery) and invoke the `getMovies` method with the input value
    - Remember the `getMovies` method does something asynchronous. Make sure to `console.log()` the `movies` property after invoking the function to make sure you are dealing with the asynchronous code correctly

The `movies` property in the `MovieManager` instance should now be an array of movies. This array should have several objects, each with:

-   An id
-   A title
-   A poster - a URL of an image
-   A year

* * * * *

### CHECK-POINT

This is the most important part of the project - client server communication.

 Commit your code!

* * * * *

### 5\. RENDERER

-   Create a new class for your Renderer
-   Add a `render` method to the class for rendering movies

-   This method should receive one parameter: `data`
-   It should then use Handlebars to render the data on the page

Remember that you can only call the render method when you have access to your data from the server.

You'll need to create a Handlebars template which can process this data.

-   Each Movie should be in it's own div with a `data-id` attribute with the movie's id (received from the api). The movie div should display the following:
    -   The title of the movie
    -   The movie's cover image
    -   The year the movie was released
    -   An empty unordered list (this will be user later)

 Commit your code!

* * * * *

### 6\. CHECK-POINT

So far:

-   On the click of your button, your client should send a GET request to your server
-   Your server should send a request to the API and get data back
- The server should then send that data back to the client
-   Your client should get the data back from the server, and then it should call a method that renders the movies, using Handlebars

* * * * *

### 7\. Database

Ok, so let's add a database to this bad boy!

- Start off with creating a `Movie Schema`. Each movie should have a `title`, `imdbId`, `poster`, and `year` (each of them are strings).
- Connect your server to a DB called `MoviesDB` using `mongoose.connect()` (in your `server.js`).
- Create a `post` route in your `api.js` file called `/movie` that:
    - Receives a movie object in its' `body`
    - Saves the movie in the database
    - Responds with the newly saved movie (make sure the response includes the MongoDB `_id`)
- Create a `get` route in your `api.js` file call `/movie` that:
    - Receives **no** paramters
    - Queries the DB for all the movies that are saved in the DB
    - Responds with the array of movies (found in the DB)

Now it's time to add support for this on the client. The goal is to have a button that, when clicked, displays all the saved movies. To do this you must update a few things:

#### `MoviesManager` class

- Add a `getMoviesFromDB` method to your  class. This method should:
    - Make a `get` request to your server's `/movies` route
    - Reassign the class's `movies` property with the data that cam back from the request
    - (remember some of this is async)
- Add a `saveMovie` method to your class. This method should:
    - Receive one paramter, `title`
    - Finds the movie (object) with that title in the class's `movie` property
    - Makes a `post` request to your `/movie` route with the movie found above


#### `HTML`

- Add a `show favorites` button to the `html`
- Add an `add to favorites` button to each movie in your Handlebars template

#### `main.js`

- Add an event listener so that when a user clicks the `add to favorites` button, you:
    - Traverse the DOM to find the title of the current movie
    - Invoke the `MovieManager`'s `saveMovie` method with the title found above
- Add an event listener so that when a user clicks the `show favorites` button, you:
    - Invoke the `MovieManager`'s `getMoviesFromDB` method
    - Render all the saved movies from `MovieManager`

Now, after searching some movies, you should be able to click `add to favorites` to add the movie to the DB. Then, when clicking, on `show favorites` you should see all the movies that were saved in the DB.

* * * * *

### 8\. DESIGN & GRID

The design is mainly up to you, but make sure to use CSS Grid.

Please do not spend too long on this section. You should have some reasonable layout - don't go crazy about every pixel.

* * * * *

### 9\. Deleting a Movie