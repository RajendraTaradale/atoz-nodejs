
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
   
   
   :red_circle: Serial Promises vs Parallel Promises :question: 
   
   Promise.all() function takes in an array of Promise objects as parameter and tries to resolve them all, 
   and then returns the resolved object. If any one promise object in the array gets rejected, the entire Promise.all() gets rejected.
   
   How does Promise.all() works internally ?
   
   promise resolution follows a serial order of execution.
   promise.all() is internally a foreach ‘kind of’ loop which iterates over the iterable we provide. This loop preserves the order of items 
   in the iterables. The resolved promise values are also in order regardless of when its got resolved. Thus we can concede that
   the Promise.all() method executes the promises in series
   
   JavaScript runtime is single-threaded. We do not have access to thread in JavaScript. 
   Even if you have multi-core CPU you still can't run tasks in parallel using JavaScript.
   
   Differences 👬
   Promise.all will reject as soon as one of the Promises in the array rejects.
   Promise.allSettled will never reject, it will resolve once all Promises in the array have either rejected or resolved.

   :red_circle: How to localization in node.js with express :question: 
   ```
   npm install i18next --save
   npm install i18next-express-middleware --save
   npm install i18next-node-fs-backend --save
   
   const i18next = require('i18next');
   const i18nextMiddleware = require('i18next-express-middleware');
   
   app.use(i18nextMiddleware.handle(i18next));
   --Add language resource files
   So you can perform translations in the controller by using the t method: req.i18n.t("home.title").
   ---
   ```
   ```
   var i18n = require("i18n");
   i18n.configure({
  locales:['en', 'de'],
  directory: __dirname + '/server/locales'
  });
    app.use(i18n.init);
    //In your controller
    res__('RTSAPP_KEY_Name')
```
▶️ In Request just set the HTTP header Accept-Language with value 'en', 'it' or any

💡 https://github.com/noveogroup-amorgunov/localizify

   :red_circle: What is default expire time for JWT token :question: 
   
   Access token expiration is set to 24 hours by default. but it dependce on how it has been configured in the identity server
   
   :red_circle: ffffffffffff :question: 
   :red_circle: ffffffffffff :question: 
   :red_circle: ffffffffffff :question: 
   :red_circle: ffffffffffff :question: 
  

