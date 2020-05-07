#### INTRO

Over the last four weeks you've learned HTML, CSS and CSS Grid, JavaScript basics and ES6 array methods, git version control, jQuery, Handlebars, OOP, APIs, Node JS, Express and a few more things here and there.

It's time to put your skills to practice by creating a movies search app!

Your app will take a title of a movie and display a list of relevant movies on the page.

Click [here](https://kernel-files.s3.eu-west-1.amazonaws.com/images/0374078b.png) to see how your app should look - more or less, design is up to you - in the end.

We'll be taking you through this step by step. So follow the instructions and use what you've learned thus far. You can reference previous code you've written, notes, and of course Google.

Good luck!

* * * * *

#### 1\. SET UP YOUR PROJECT

-   Create your local directory with Git and NPM. You should have a `server.js` file and a dist folder

-   Inside your dist folder you should have an `index.html`, `style.css`, `main.js`, and `Renderer.js`

-   Install jquery, handlebars, express, and urllib with NPM, we'll be using these packages in the project
-   Don't forget to add `node_modules` to your `.gitignore` file!
-   Make your new repository on github and call it bootcamp-movies. Link your repo to your local directory, then commit your files for your initial commit

* * * * *

#### 2\. SET UP YOUR SERVER

Create a server using express on port 8080. Don't forget to use your `dist` and `node_modules` folders.

Create a get route called `/sanity` that responds with "OK" to make sure your server is set up properly.

* * * * *

#### 3\. REQUEST TO THE MOVIE API

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

#### 4\. CLIENT SETUP

-   Setup your HTML boilerplate with all the relevant scripts
-   Create an input for a movie title, and a Search! button
-   When the button is clicked, take the value of the input (with jQuery) and make a request to `/movies`
    -   The value from the input should be your `title` parameter

You should receive an object with an array of movies from this request. This array should have several objects, each with:

-   An id
-   A title
-   A poster - a URL of an image
-   A year

* * * * *

#### CHECK-POINT

This is the most important part of the project - client server communication.

 Commit your code!

* * * * *

#### 5\. RENDERER

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

#### 6\. CHECK-POINT

So far:

-   On the click of your button, your client should send a GET request to your server
-   Your server should send a request to the API and get data back
- The server should then send that data back to the client
-   Your client should get the data back from the server, and then it should call a method that renders the movies, using Handlebars

* * * * *

#### 7\. DOM TRAVERSAL

Now, we are going to display the ratings for a movie when clicking on it's image. For this you should:

- Add a click listener to each image. When the image is clicked, get the id of that movie (from the `data-id` attribute in the movie div).
- Once you have the id, make a new request to the Movie API (you can do this directly from the client).
- *Note*: You can use the 'i' paramter to search for a specific movie by id (check out the [docs](http://www.omdbapi.com/#usage))
- The API should respond with one movie object, where one of the keys will be an array of ratings.
- Loop through the ratings and append each one of the ratings as an `li` in the `ul` (created earlier) of that movie.

*Important Note*: You can do this without Handlebars if you want (meaning just jQuery), whatever works for you.

* * * * *

#### 8\. DESIGN & GRID

The design is mainly up to you, but make sure to use CSS Grid.

Please do not spend too long on this section. You should have some reasonable layout - don't go crazy about every pixel.

* * * * *

#### 9\. COMMIT AND PUSH YOUR PROJECT TO GITHUB

If you are about to push code that doesn't work, make a note in the commit message. Something like "works until part 7"

* * * * *

#### 10\. DONE

Take a breath. All is well. Give yourself a pat on the back.