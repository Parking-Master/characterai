# characterai
An unofficial API wrapper for Character.AI. Works in Node.js using WebSocket requests.

## Install
First install it using NPM:
```
$ npm install @parking-master/node_characterai
```

Then continue with the rest of the documentation.

## Quick start
There are only three steps to set up this API:
- Authenticate your account
- Set up your character
- Send a message

### Get all the required info
All the required info you need is: Your HTTP token, author id, author name, character id, and chat id.

To get this info, go to your character's chat page and open the [web console](https://screenful.com/guide/how-to/how-to-open-the-browser-developer-console) using <kbd>Ctrl/Cmd</kbd>+<kbd>Shift/Alt</kbd>+<kbd>I</kbd>.

Make sure you're on another chat page, not the default. For example, the URL should show "/chat2?char=..." instead of "/chat?char=...".

Then reload the page.

Then, go to the _Network_ tab, reload the page, search for "ws" and click on the neo.character.ai request. This is where all the info is. Send a message to your character to show the info.

Then do the following steps to get the info you need.

#### Authenticate
Go to _Cookies_, and go to the root URL. Then, in the tables show all the cookies in the console, find the cookie "HTTP_AUTHORIZATION". The part after "Token ..." is your auth token. Copy this.

#### Character ID
The character's ID is shown in the URL of the chat page. The "char" parameter contains the id. For example:
> https://beta.character.ai/chat2?char=6HhWfeDjetnxESEcThlBQtEUo0O8YHcXyHqCgN7b2hY

"6HhWfeDjetnxESEcThlBQtEUo0O8YHcXyHqCgN7b2hY" is the chaarcter ID.

#### Chat ID
Send a message to your character and the info will be displayed in the console. Grab the value of "chat_id" and you're good to go.

#### Author ID
Still in the console, when you sent the message, find "author_id" and get the value as a number.

#### Author name
The Author name will just be your profile username. Copy that as well.

### Setup the API
Now, if you have all the info, you can set up the API.

First authenticate your account by doing this:
```javascript
characterAI.authenticate(YOUR_AUTH_TOKEN);
```

```javascript
characterAI.setup(CHARACTER_ID, CHAT_ID, AUTHOR_ID, AUTHOR_NAME);
```

_Replace all the required fields with your info._

Now, you can send a message:
```javascript
(async () => {
  let response = await characterAI.send("Hello!");
  console.log(response);
})();
```

### Example
Here's a full example that has been tested and works:
```javascript
const characterAI = require("@parking-master/node_characterai");

characterAI.authenticate("xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx");
characterAI.setup("6HhWfeDjetnxESEcThlBQtEUo0O8YHcXyHqCgN7b2hY", "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", 18378286, "myname123");

(async () => {
  let response = await characterAI.send("Testing...");
  console.log(response);
})();
```

## License
MIT
