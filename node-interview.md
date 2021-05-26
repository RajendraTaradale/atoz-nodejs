
   :red_circle: What is Node JS :question: 
   
   :memo: Node.js = Runtime Environment + JavaScript Library
   
   :memo: Node.js comes with runtime environment on which a Javascript based script can be interpreted and executed
   
   :memo: Node.js is an extremely powerful framework developed on Chrome’s V8 JavaScript engine that compiles the 
          JavaScript directly into the native machine code
   
   :memo: It is a lightweight framework used for creating server-side web applications
   
   :memo: Offers server-side scripting functionalities
         
   :red_circle: Differentiate between JavaScript and Node.js :question: 

   |  Features | JavaScript |  Node Js |
   | --- | --- | --- |
   | Type | Programming Language  | Interpreter and environment for JavaScript |
   | Utility | Used for any client-side activity for a web application  | Used for accessing or performing any non-blocking operation of any operating system |
   | Running Engine | Running Engine	Spider monkey (FireFox), JavaScript Core (Safari), V8 (Google Chrome), etc.  | V8 (Google Chrome) |

    💡  https://github.com/goldbergyoni/nodebestpractices
    
   :red_circle: Node Js Architecture - Request Flow Diagram :question: 
   
    User Request ➡️ Event Queue ➡️ Event Loop ➡️ Blocking Operation & Non blocking Operations ➡️ Thread Pool ➡️ External Resources
   
   :red_circle: How Node JS middleware Works :question: 
 
   As name suggests it comes in middle of something and that is request and response cycle
   Middlewares have access to the request object (req), the response object (res) and the next() function request-response cycle.
   The next functions executes the middleware succeeding the current middleware.
 ```  
const rtLoggerMiddleware = (req,res,next) =>{
    console.log(`Application Logged  ${req.url}  ${req.method} >--> ${new Date()}`)
    next();
}

var express = require('express')
var app = express()
const router = express.Router()
const bodyParser = require('body-parser');

router.use((req,res,next)=>{
    console.log("Time:",new Date())
    next()
})

router.get('/', function (req, res) {
  res.send('Hello World!')
})

app.use(bodyParser.urlencoded({extended:false}))

app.use(bodyParser.json())

app.use(rtLoggerMiddleware)

app.use('/',router)

app.listen(3000,(req,res)=>{
    console.log('RT's server running on 3000')
})
```
Now when every time the app receives a request, it prints the message “Application Logged” to the terminal.

Types of express middleware

Application level middleware ➡️ app.use
Router level middleware  ➡️ router.use
Built-in middleware  ➡️ express.static,express.json,express.urlencoded
Error handling middleware  ➡️ app.use(err,req,res,next)
Thirdparty middleware  ➡️ bodyparser,cookieparser
   
   
   :red_circle: ffffffffffff :question: 
   :red_circle: ffffffffffff :question: 
   :red_circle: ffffffffffff :question: 
   :red_circle: ffffffffffff :question: 
  

