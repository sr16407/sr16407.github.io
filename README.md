NODE.JS



My MacBook is no longer updated by node.js and is now outdated. however, a directory is needed for the project. Inside the project directory needs an ‘index.html’ with the HTML code provided. 

A public directory is created inside the project directory. Inside the public directory, a ‘server.js’ file is needed with the code below in it. A terminal prompt should be opened and navigating to the project directory. 

The command ‘npm init -y’ should run the Node.js project. also run ‘npm install express’ and ‘node public/server.js’. Using a web browser navigate to http://localhost:3000







const express = require('express');

const path = require('path');



const app = express();

const PORT = process.env.PORT || 3000;



// Serve static files from the "public" directory

app.use(express.static('public'));



// Route for the homepage

app.get('/', (req, res) => {

    res.sendFile(path.join(__dirname, 'public', 'index.html'));

});



// Start the server

app.listen(PORT, () => {

    console.log(`Server is running on http://localhost:${PORT}`);

});
