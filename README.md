# forEach-with-promises
 
function promiseForEach(arr, cb) {
 var i = 0;
 var nextPromise = function () {
 if (i >= arr.length) {
 // Processing finished.
 return;
 }
 // Process next function. Wrap in `Promise.resolve` in case
 // the function does not return a promise
 var newPromise = Promise.resolve(cb(arr[i], i));
 i++;
 // Chain to finish processing.
 return newPromise.then(nextPromise);
 };
 // Kick off the chain.
 return Promise.resolve().then(nextPromise);
};
