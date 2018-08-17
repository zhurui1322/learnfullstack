# NodeJS

## 1. NodeJS的特性

Node.js is a single-threaded but highly scalable system that utilizes JavaScript as its scripting language. It uses asynchronous, event-driven I/O instead of separate processes or threads. It is able to achieve high output via single-threaded event loop and non-blocking I/O.  


node us build on google chrome’s V8 javascript runtime and sites as the server-side platform written by C++ compare to Apache server which is multi threaded, Node is asynchronous and single threaded node uses only one thread to handle all requests

## 2. Promise.all failed one 

A major complaint of JS Promises is that it can be pretty simple to ‘swallow errors’, meaning that a sneaky `catch()` can handle an error without our code ever finding it. This could be the case here if we were expecting all promises generated with `apiRequest()` to fail or reject any time the actual http request fails.

As it stands now, or previous case has a catch at the end of the Promise.all which will never actually catch anything since it is being handled in a catch in the apiRequest function, so it is important to note this implementation would be for our specific use-case.



```javascript
function apiRequest(url) {
    return new Promise(function (resolve, reject) {

        //our fake api simply returns the string passed as the 'url'
        if (url) {
            resolve(url);
        } else {
            //if no url is passed to the function, it will fail
            reject('apiRequest failed!');
        }
    })
    .catch(function(err){
        //return error;
        return err;
    });
}

var p1 = apiRequest('urlOne');

//this one will fail
var p2 = apiRequest();

var p3 = apiRequest('urlThree');

Promise.all([p1, p2, p3])
.then(function(res){
    console.log('Promise.all', res);
})
.catch(function(err){
    console.error('err', err);
});

//Promise.all [ 'urlOne', 'apiRequest failed!', 'urlThree' ]
```

## 3



