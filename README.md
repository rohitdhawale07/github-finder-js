# github-finder-js
## Hosted Link :-
## Overview
The GitHub Finder project is a simple web application that allows users to search for GitHub profiles  
and view detailed information about users and their repositories. 
This project is built using HTML, CSS, and JavaScript and uses the GitHub REST API to fetch user data.

## Features
Search GitHub Users: Enter a GitHub username to search for a user's profile.
Display User Information: View detailed information about the user, including their avatar, username, name, bio, location, and more.
List User Repositories: See a list of the user's repositories with details like repository name, description, stars, and forks.
Responsive Design: The application is designed to work well on both desktop and mobile devices.

## Technologies Used
HTML: The structure of the web page.
CSS: Styling and layout.
JavaScript: Dynamic functionality and data fetching.
GitHub REST API: To fetch user data and repositories.

## HTML Code
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Github Finder</title>
    <link rel="stylesheet" href="./style.css">
</head>
<body>
    <header>
        <h2>Github Finder</h2>
      </header>
      <form>
        <input type="search" name="Search bar" id="searchbar" />
        <div>
          <button id="SearchButton">Search</button>
          <button id="getAllUsers">Get all Users</button>
        </div>
      </form>
  
      <div id="cardContainer"></div>
    <script src="./index.js"></script>
</body>
</html>
```
## CSS code
```
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  body {
    background-color:white;
    color: black;
  }
  
  header {
    border-radius: 5px;
    height: 10vh;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 1.5rem;
  }
  
  form {
    margin-top: 1rem;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    height: 20vh;
  }
  
  form input {
    width: 100ch;
    padding: 0.6rem 1rem;
    font-size: 1rem;
    background-color: rgb(247, 247, 247);
    color: black;
    font-weight: 600;
    outline: none;
    border: none;
    border-radius: 10px;
  }
  
  form button {
    box-shadow: 3px 3px 3px 3px black;
    background-color: blue;
    color: white;
    padding: 0.5rem 1rem;
    margin: 1rem;
    font-weight: 600;
  }
  
  form button:hover {
    cursor: pointer;
    transform: scale(1.04);
     background-color: white;
     color: black;
}
  
  #cardContainer {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
  
  #cardContainer div {
    margin: 2rem;
    padding: 1rem;
    box-shadow: 3px 3px 10px black;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border-radius: 5px;
  }
  
  img {
    width: 200px;
    height: 200px;
    border-radius: 50%;
    filter: drop-shadow(4px 4px 10px 10px black);
  }
  
  a {
    text-decoration: none;
    color: blue;
    padding: 0.8rem 1rem;
    box-shadow: 1px 1px 9px black, inset 2px 2px 9px black;
    font-size: 0.8rem;
    margin-top: 1rem;
  }
  a:hover{
    scale: 1.04;
  }
  
  h2 {
    margin-top: 1rem;
  }

  .mode {
    margin-left: 80rem;
    margin-top: 2rem;
}
.change {
    cursor: pointer;
    border: 1px solid #555;
    border-radius: 40%;
    width: 20px;
    text-align: center;
    padding: 5px;
    margin-left: 8px;
}

```
For Javascript part In this example, we create a basic GitHub User Finder project. Users can enter a GitHub username, 
click the "Search" button, and the application fetches and displays the user's avatar, username, bio, and a link to 
their GitHub profile. 
If the user is not found or an error occurs, appropriate messages are displayed.

You can enhance this project by adding more features, such as searching for repositories, pagination, and styling improvements.
## JAVASCRIPT Code
```
const searchBar = document.getElementById("searchbar");
const searchButton = document.getElementById("SearchButton");
const getAllUsers = document.getElementById("getAllUsers");
const cardContainer = document.getElementById("cardContainer");

function getUser(searchValue) {
  let apiUrl;
  if (searchValue === undefined) {
    apiUrl = `https://api.github.com/users`;
  } else {
    apiUrl = `https://api.github.com/users/${searchValue}`;
  }
  
  const users = fetch(apiUrl);
  users.then((response) => {
      return response.json();
    }).then((data) => {
      let result = data;
      if (searchValue === undefined) {
        result.map((ele) => {
          const card = document.createElement("div");
          const heading = document.createElement("h2");
          const img = document.createElement("img");
          const link = document.createElement("a");
          link.innerHTML = "GitHub Link";
          heading.innerText = ele.login;
          img.src = ele.avatar_url;
          link.href = ele.html_url;
          card.appendChild(img);
          card.appendChild(heading);
          card.appendChild(link);
          cardContainer.appendChild(card);
        });
      } else {
        cardContainer.innerHTML = "";
        console.log(result);
        if (result.message === "Not Found") {
          const heading = document.createElement("h1");
          heading.innerText = "User not found";
          cardContainer.appendChild(heading);
        } else {
          const card = document.createElement("div");
          const heading = document.createElement("h2");
          const img = document.createElement("img");
          const link = document.createElement("a");
          link.innerHTML = "Github Link";
          heading.innerText = result.login;
          img.src = result.avatar_url;
          link.href = result.html_url;
          card.appendChild(img);
          card.appendChild(heading);
          card.appendChild(link);
          cardContainer.appendChild(card);
        }
      }
    });
}

searchButton.addEventListener("click", (e) => {
  e.preventDefault();
  const searchValue = searchBar.value;
  getUser(searchValue);
});

getAllUsers.addEventListener("click", (e) => {
  e.preventDefault();
  cardContainer.innerHTML = "";
  getUser();
});


```

