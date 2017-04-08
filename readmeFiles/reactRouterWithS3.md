## Making S3 to work with React-Router

I am assuming that you have deployed your React App to S3 using this [link](https://github.com/lakshmantgld/route53-CloudFront-S3-Setup/blob/master/readmeFiles/s3Setup.md). Lets say your website is **http://lakshman.com**. Now, all your react routes will work properly. When you directly navigate to a nested react route like **http://lakshman.com/resume**, the browser searches for resume file in S3. This is normal behavior of any webServer. But we have to do a small hack to make react-router get the path **resume** and navigate that.

Now, you need to add some redirection rules under **static web hosting** in your bucket properties tab. So, when 404 occurs, S3 needs to redirect to **index.html**, but this can be done only by adding some prefix like **#!**. Now, when you reload the page with any react route, instead of going to **error.html**, the same url will be loaded but with a prefix **#!**. Click **Edit redirection rules** and add the following code:

```
 <RoutingRules>
     <RoutingRule>
         <Condition>
             <HttpErrorCodeReturnedEquals>404</HttpErrorCodeReturnedEquals>
         </Condition>
         <Redirect>
             <HostName> [YOUR_ENDPOINT] </HostName>      
             <ReplaceKeyPrefixWith>#!/</ReplaceKeyPrefixWith>
         </Redirect>
     </RoutingRule>
 </RoutingRules>
```

Replace **[YOUR_ENDPOINT]** with the static website endpoint of the deployed react app.

In client side(react app), we need to remove that prefix and push the route to original route. Here is the change you need to do in react app. I have my **main.js** file, which is the starting point of react app. Add a listener to **browserHistory** like this:

 ```js
 browserHistory.listen(location => {
   const path = (/#!(\/.*)$/.exec(location.hash) || [])[1];
   if (path) {
       history.replace(path);
    }
  });
```

The above code will remove the prefix and push the history to the correct route (HTML 5 browser history). For eg: something like this **http://lakshman.com/#!/resume** will change to **http://lakshman.com/resume**. Doing that makes **react-router** to understand and change the route accordingly. Here is my **main.js** file for better understanding:

```js
 import React from 'react';
 import ReactDOM from 'react-dom';
 import {createStore, compose, applyMiddleware} from 'redux';
 import {Provider} from 'react-redux'
 import {Router, Route, IndexRoute, browserHistory, useRouterHistory} from 'react-router';
 import {syncHistoryWithStore} from 'react-router-redux';
 import createLogger from 'redux-logger';
 import thunk from 'redux-thunk';


 const logger = createLogger();
 const createStoreWithMiddleware = applyMiddleware(thunk, logger)(createStore);
 const store = createStoreWithMiddleware(reducers);
 const history = syncHistoryWithStore(browserHistory, store);


 browserHistory.listen(location => {
   const path = (/#!(\/.*)$/.exec(location.hash) || [])[1];
   if (path) {
       history.replace(path);
    }
  });
```

So uploading the browserified or webpacked react app(app.js file) will do the required need.
