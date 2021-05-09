## React Authentication
Authentication is an essential feature in website. In this project, I will use Firebase to be a database keeping user data for creating authentication in React.

### Technologies
React, React-Router, Firebase

### Firebase authentication
1. create new project
2. choose authentication session
3. choose sign-in method and Email/Password provider
4. Then, edit the status to be enabled by toggle the first toggle button
5. Open this documentation about sign up and sign in [Firebase Authentication](https://firebase.google.com/docs/reference/rest/auth#section-create-email-password)

Tools: useContext, useHistory, react-router-dom

### Sign up
Firebase provide sign up feature with POST request to url which totally convenient.
You can use fetch API (Vanilla JS) to send sign up request and if there are error with sign up such as password is too easy, Firebase will send error message to us. We can use that error message to display on user screen to let user know their mistake.

```javascript
 fetch("https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=AIzaSyCaQ4y6_QLzv5A7qF02ka9hdflrVpnUDCk",
    {
        method: "POST",
        body: JSON.stringify({
        email: enteredEmail,
        password: enteredPassword,
        returnSecureToken: true,
        }),
        headers: {
        "Content-Type": "application/json",
        },
    }
    ).then((response) => {
        if (response.ok) {
          //
        } else {
            response.json().then((data) => {
                // show an error message
                if (data && data.error && data.error.message) {
                setErrorOccurred(true);
                setErrorMessage(data.error.message);
                }
            });
        }
    });
```

### Sign in
Firebase provide sign in feature with POST request as well but with different URL. If the user fill in email and password correctly, our website will receive id token and other data. 

### Using token for requests to protect resources

### Redirecting user
Use router and conditional render to redirect user into desired page.

### Logout
No need to send request to the server. You can just remove token and set login state to false.

### Protecting Frontend Pages
If you type direct route to the web browser, it will change to that url without sign in and this could be the problem. We can use navigation guards to protect go to the unauthorized route.

### Protect state is disappeared when reload page
store token in cookie or local storage. In context, we can initialize state of the token to be the token in the local storage or cookie. If there is no token in the local storage or cookie, it will set null to the state. 
   * login - save token in local storage or cookie
   * logout - remove token in local storage or cookie 

### Auto-logout
