# Let's Build a Multiplayer Realtime Tic Tac Toe Game with Socket.io and Vue.js
[![Skills](https://img.shields.io/badge/Socket.io-010101?&style=for-the-badge&logo=Socket.io&logoColor=white)](https://www.apple.com/macos/catalina-preview)
[![Skills](https://img.shields.io/badge/Vue.js-35495E?style=for-the-badge&logo=vuedotjs&logoColor=4FC08D)](https://www.apple.com/macos/catalina-preview)
[![Skills](https://img.shields.io/badge/eslint-3A33D1?style=for-the-badge&logo=eslint&logoColor=white)]
[![Skills](https://img.shields.io/badge/prettier-1A2C34?style=for-the-badge&logo=prettier&logoColor=F7BA3E)]
[![Skills](https://img.shields.io/badge/Webpack-8DD6F9?style=for-the-badge&logo=Webpack&logoColor=white)]
[![Skills](	https://img.shields.io/badge/Babel-F9DC3E?style=for-the-badge&logo=babel&logoColor=white)]




#Vuejs #JavaScript #Game development #Programming.

1) Developed a Tic-Tac-toe game from scratch using Vue.js. 
2) We will integrate the real-time feature with socket.io, so that two players can play the game from different browsers at the same time.

# Project creation
First, create a blank Vue project and in the app.vue,remove the hello world component and add the HTML for the grid. I copied the CSS from this tutorial.

We will define 9 blocks with id block_0 to block_8 with class block for each block.

# Draw X and O on click
Now, we will define two variables in the data section:

content
turn

Content will be an array of length 9, one element for each block of HTML, initialized with the empty string. When we click one block, we will change the value at that index of the content. Let’s define the function @click, and use it.

We will draw the X and O based on the content array and on the click will trigger the draw function in each block.

Now, let’s define the draw function in the methodsection. If the value of turnis true, we will draw X, else we will draw O and change the value of turn. So, first, click we draw X andturn becomes false. So, on the second click, we draw O and turn becomes true and so on...

# Calculate Winner
Now, after every call in the draw function, we have to calculate if the game is finished or not. If finished, we can find who is the winner and display it.

We will declare three variables more in the data section.

Now, we are ready to define calculateWinner function. The logic is if the same row, column or diagonals are occupied by the same player, he/she wins.

# Calculate Tie
Now we will define the tie function. The logic is even if there is an empty block, the game is not tied.


We will define this function in the method section and call it from the draw method.

Entire script section till now.

# Reset Board
Now, when the game is tied or over, we have to show an option to reset the board.


We will define the resetBoard function next. We reset the content array and all the other variables.


You can't perform that action at this time. You signed in with another tab or window. You signed out in another tab or…
github.com

# Multiplayer mode using Socket.io
Now, we will integrate the project with Socket.io, so that two players can play the game at the same time. When one player clicks X, it should appear on the second player’s screen and when the second player clicks O, it should appear on the first player’s screen. How to implement it?

# Set up server for socket.io
We will first create a folder outside the Vue project. Create a file server.js inside the folder. We will create an express server inside the folder.

Run $ npm init. It will set a package.json file.

Then run

$ npm i socket.io

It will install socket.io in the project.

server.js
Now, let's create a server and integrate socket.io.


We will set the CORS rule, so that our Vue.js project running on port 8080 can access the server.

We will emit an event from the server and our Vue client should listen to it and receive it.

# Run the server with : 

$ node server.js

App.vue
Now, we will set up socket.io on the client-side.

# Run npm i socket.io-client inside the Vue.js project from the terminal.

We will import the library by:

import io from ‘socket.io-client’
const socket = io(“http://localhost:3000")
inside the script section.

In the created hook, we will listen to the event.


You will see “youtube tutorial” will appear in the console.

The client can also talk to the server in the same way.

# Game Logic with Socket.io
After we call the draw function, player 1 client will send the event to the server.
When the server receives it, it will broadcast it to the player 2.
Player 2 will then update the grid.
Then player 2 will click O and call the draw function, it will send the event to the server.
The server will broadcast it to player 1.
The game will keep going like this.


We also need to pass a parameter, drawFromOther, in the draw function. Depending upon this flag, we will emit the event again. If the drawFromOther flag is set to false, we will send the play event.

Now, we will update the template. We will send the drawFromOtheras false, which means the event will be sent to the server.


Server.jswill receive the event and broadcast it.


Now, the client will receive the event in created hook.


It will receive the event and draw at the index, but we pass drawFromOther param as true, so that the event does not again get sent to the server.

That's it. The multiplayer game is ready to be played. Open localhost:8080 in two different browsers and click alternatively. The game should work.

![new Screenshot (17)](https://user-images.githubusercontent.com/93249038/211185751-87d543fb-020c-4f11-88c8-a87904fcc678.png)

