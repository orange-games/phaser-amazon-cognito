Phaser Amazon Cognito
=====================
A Phaser plugin that adds user register/login support trough amazon cognito.

Key Features:
* Works on mobile and desktop
* Included TypeScript support
* Async library with promise calls
* Easy to use as phaser plugin

Getting Started
---------------
First you want to get a fresh copy of the plugin. You can get it from this repo or from npm, ain't that handy.
```
npm install @orange-games/phaser-amazon-cognito --save-dev
```

Next up you'd want to add it to your list of js sources you load into your game:
```html
<script src="path/to/phaser-amazon-cognito.js"></script>
```

After adding the script to the page you can activate it by enabling the plugin:
```javascript
game.add.plugin(Fabrique.Plugins.Cognito);
```

#####Note
If you are using typescript, you have to user typescript 2.0.0 or higher for the promises to work.

Usage
-----
First off you want to set the user pool info using the userPoolId and clientId.
```javascript
game.cognito.setPoolInfo('<your_pool_id>', '<your_client_id>');
```

#####Registration
Register a new user to the user pool.
```javascript
game.cognito.register('<username>', '<password>', '<email>', null).then(function(user) {
    console.log('Registration worked!', user);
}).catch(function(error) {
    console.log('Registration failed:', error);
});
```

#####Confirm Registration
An account has to be confirmed after registration. The code will be in the inbox of the users email.
```javascript
game.cognito.confirmRegistration('<confirmation_code>').then(function() {
    console.log('Confirmation worked!');
}).catch(function(error) {
    console.log('Confirmation failed:', error);
});
```

#####Resend Confirmation 
Resend conformation mail to users email. Will only work if user is not confirmed yet.
```javascript
game.cognito.resendConfirmation().then(function() {
    console.log('Confirmation resend!');
}).catch(function(error) {
    console.log('Failed to resend confirmation:', error);
});
```

#####Reset Password
Sends a reset code to the user's email address.
```javascript
game.cognito.resetPassword().then(function() {
    console.log('Password has been reset!');
}).catch(function(error) {
    console.log('Failed to reset password:', error);
});
```

#####Confirm Password Reset
Use the reset code given in the reset email to change password.
```javascript
game.cognito.confirmResetPassword('<confirmation_code>', '<new_password>').then(function() {
    console.log('Password has been changed!');
}).catch(function(error) {
    console.log('Failed to change password:', error);
});
```

#####Change Password
Changes the password for the current user. The user has to be logged in.
```javascript
game.cognito.changePassword('old_password', 'new_password').then(function() {
    console.log('Password has been change!');
}).catch(function(error) {
    console.log('Failed to change password:', error);
});
```

#####Login
Logs in a user from the user pool.
```javascript
game.cognito.login('<username>', '<password>').then(function(state) {
    console.log('LoggedIn!', state.user, state.sessionToken);
}).catch(function(error) {
    console.log('Login failed:', error);
});
```

#####Logout
Logs out a user from the user pool.
```javascript
game.cognito.logout();
```

#####Loading User From LocalStorage
Loads the userState from the localStorage on the device.
```javascript
game.cognito.loadStorageUser();
```

#####Validate Session
Checks if a session has been set. Does not actually check if the user is logged in. Can be used to check if the loadedStorageUser had a session.
```javascript
game.cognito.validateSession().then(function() {
    console.log('Valid session!');
}).catch(function(error) {
    console.log('Invalid session:', error);
});
```

#####Setting User
Most commands will use the last used user, if you want to call verify on a different user for example you need to call this first. Login or register will automatically set this.
```javascript
game.cognito.setUser('<username>');
```

Credits
-------
This library uses the amazon-cognito-identity-js library provided by amazon. (https://github.com/aws/amazon-cognito-identity-js)

Disclaimer
----------
We at OrangeGames just love playing and creating awesome games. We aren't affiliated with Phaser.io. We just needed some awesome login handling in our awesome HTML5 games. Feel free to use it for enhancing your own awesome games!

Phaser Amazon Cognito is distributed under the MIT license. All 3rd party libraries and components are distributed under their
respective license terms.