getusermedia-to-node
====================

just messing around with sending audio data directly to node over sockets

testing sockets...

        <script src="/socket.io/socket.io.js"></script>
        <script>
          var socket = io('http://localhost');
        function gotStream(stream) {
        
            window.AudioContext = window.AudioContext || window.webkitAudioContext;
            var audioContext = new AudioContext();
        
            var mediaStreamSource = audioContext.createMediaStreamSource(stream);
        
        
            var pipe = audioContext.createScriptProcessor(1024, 2, 2);
        
            pipe.onaudioprocess = function(e){
                console.log('sending data... ');
                var buffer = e.inputBuffer.getChannelData(0);
                socket.emit('audio', { data: buffer });
            }
        
            mediaStreamSource.connect(pipe);
        
            pipe.connect(audioContext.destination);
        }
        
        function err(){
         console.log('err:', arguments);
        }
        
        navigator.webkitGetUserMedia({audio:true}, gotStream, err);
        </script>


hit localhost/8080 in browser


        
        var app = require('http').createServer(handler)
        var io = require('socket.io')(app);
        var fs = require('fs');
        
        app.listen(8080);
        
        function handler (req, res) {
          fs.readFile(__dirname + '/index.html',
          function (err, data) {
            if (err) {
              res.writeHead(500);
              return res.end('Error loading index.html');
            }
        
            res.writeHead(200, {'Content-Type': 'text/html' });
            res.end(data);
          });
        }
        
        io.on('connection', function (socket) {
        	socket.on('audio', function(data){
        		console.log(data);
        	})
        });
        
        
