# **Building real time chat app**

Now if you have understood the previous class then only proceed otherwise dont try to follow along

what we are building today 

<img src = "image-1.png" width=320 height=300> <img src = "image.png" width=320 height=300> 

**Whats new in this project or challenges**

The major challenge which you will face is see the below pic

<img src = "image-2.png" width=400 height=200>

although all the ROOMS (ornage, blue, red box) are connected to the same websocket server still the message present inside one room should not go to other different room but at the same time, it also should have the capability to brodacast among all the members present inside one particular room 

-> message comes from room 1 should go to everyone in room 1 only and so on with other room

If you can do the above task then **advanced version of this assignment ->** create multiple websocket server, and try to distribute the traffic(lets say put some user of room 1 connect to this websocket server and then interact with others among the room 1) among multiple websocket server made (randomly distribute it) and connect all the websocket server to the PUB SUB(read about this how it works)

architecture looks something like this :-

<img src = "image-3.png" width=400 height=200>

do all the steps present in the previous websocket pdf to initialise an empty project 

inside the `index.ts`

```javascript
import {WebSocketServer} from "ws"

const wss = new WebSocketServer({port : 8080}) // initialised a new WebSocketServer

// what will you do when a new connection will establish

wss.on("connection", (socket) => { // 2

})
```

**Explanation of `// 2` code**

:bulb:**What is `socket` ??**

-> **Its an OBJECT that lets you connect to the person or simply saying TALK to the person jo connect hua h**
+ **You can start recieving message from the person connected on this `socket`**
+ **You can start sending message to the person connected through this `socket`**

-> very similar to `req` and `res` OBJECT inside the EXPRESS 

>:pushpin:<span style="color:orange">**whenever someone will connect the callback function present inside it will Run and A NEW SOCKET will be created (similar to what happens for `req`, `res` in express)**</span>

Now coming back on the project -> lets slowly try to build the task 

-> first lets try to build something like how many users have connected to a particular `websocket` 

```javascript
import {WebSocketServer} from "ws"

const wss = new WebSocketServer({port : 8080})

let userCount = 0

wss.on("connection", (socket) => {
    userCount++ // whenever someone new will connect userCount will increase by 1
    console.log("user connected #" + userCount)

})
```
:bulb:**How will you start the `websocket` server??**

-> if it was `express` then using `app.listen()` you used to achieve it but for `websocket` case just do the below operation 

1. go to `package.json`
2. and inside the `"scripts"` write the below line 

```javascript
"scripts" : {
    "dev" : "tsc -b && node ./dist/index.ts" // tsc -b will build the ts file made and node ./dist/index.ts will run the code
}
```
3. now just run the command `npm run dev` inside the terminal and you are good to go 

Now send the connection request to the server via `Postman` and you will see the result something like this

<img src = "image-4.png" width=600 height=300>

code is working fine








