# APIs

- API stands for "Application Programming  Interface"
- API's have
- everything in JSON needs to be in double quotes " "
- AJAX  is used  to update elements on the page from a server without having to refresh the page
- classes will be used
- a promise in javascript is a proxy for a value something that will return something
    - it will be pending, fulfilled, or rejected
    - if the pending promise is fulfilled the associated then method will be called
    - promises are asynchronous
        - Synchronous code is executed in sequence – each statement waits for the previous statement to finish before executing
        - Asynchronous code doesn't have to wait – your program can continue to run. You do this to keep your site or app responsive, reducing waiting time for the user.
        - `.then()` - this code is run if the Promise is fulfilled
        - `.catch()` - this code is run if the Promise is rejected
        - `.finally()` - this code is always run, fulfilled or not

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f7c875a9-a0d3-4877-90ee-3da83d1789da/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f7c875a9-a0d3-4877-90ee-3da83d1789da/Untitled.png)

    %20 in url means there's a space

    ```jsx
    fetch(url)
    .then(res => res.json())
    .then(console.log)
      .catch(console.error)
    ```
