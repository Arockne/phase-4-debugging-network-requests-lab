# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Add a new toy when the toy form is submitted

  - How I debugged:
    Using the Network tab in chrome dev tools, I made a request throught the new toy form. In doing so, the response resulted in a 500 server, meaning there is some kind of error on the server side. So checking the server logs I notice that a NameError was raised, which showed where the error was located and what raised the error. The error itself was a typo on line 10 being Toys instead of Toy, which fixed this bug.

- Update the number of likes for a toy

  - How I debugged:
  When clicking the like button on a toy card, using Network tab, I notice within the headers that there was a status code of 204, meaning no content. What that means is that the response from the server is not rendering any JSON data back to the client. How I fixed this is by using the render method and passing in the toy that was updated with a like.

- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged:
  When clicking the "Donate to GoodWill" button, the Network tab showed a 404 no_content status. Has a possble two meanings, either the id is not located within the database or the route does not exist. I first checked if the logic within the controller was correct, then I checked to see if the route actually existed within the routes. How I fixed this bug was by implementing the route that did not exist.