#getusermedia-to-node

This is a proof in concept of sending raw Microphone data to Node.js using getusermedia, and web sockets.

##Usage

###1 - Install and run the server

```bash
git clone https://github.com/F1LT3R/getusermedia-to-node.git
npm install
node server.js
```

###2 -  Run the client in your browser

http://0.0.0.0:8080/index.html

When the page has loaded, click "Allow" to begin capturing the microphone.

###3 - Look in your console

Now you should see audio data in the console where you ran _node server.js_:

```javascript
{
    '155': -2.6510391659684274e-9,
    '156': 5.5610143157025504e-9,
    '157': 5.7803970499037405e-9,
    '158': -2.242444274713762e-8,
    '159': 1.9714875065801607e-8,
    '160': 2.8081043268457506e-8,
    '161': -8.760064673651868e-8,
    '162': 6.128099983016e-8,
    '163': 9.751599350238394e-8,
    '164': -2.4895354044929263e-7
}
```

##Details

It works like this...

    getUserMedia[Microphone] > WebAudioStream[ScriptProcessor] > WebSocket > Node.js


