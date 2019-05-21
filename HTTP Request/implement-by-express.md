###Request Example

```javascript
const express = require('express');
const path = require('path');

const app = express();

app.use(express.json());
app.use(express.urlencoded({ extended: false }));

// GET Request
app.get('/', (req, res) => {
    // res.json({"msg" : "Hello JSON Message !"});
    let data = {
        "host" : req.header('host'),
        "user-agent" : req.header('user-agent'),
        "row-headers" : req.rawHeaders,
    }
    res.json(data);
});

app.post('/contact', (req, res) => {
    let data = {
        'body': req.body,
        'name' : req.body.name,
        'content-type' : req.header('Content-Type'),
    };
    res.send(data);
});

app.post('/login', (req, res) => {
    if(!req.header('x-auth-token')) {
        return res.status(400).send('No token Found !');
    }

    if(req.header('x-auth-token') != '123456') {
        return res.status(401).send('Un-authorization Token');
    }
    res.send('Logged in');
});

app.put('/post/:id', (req, res) => {
    let data = {
        'id' : req.params.id,
        'title' : req.body.title,
        'content' : req.body.content,
        'user-agent' : req.header('user-agent'),
        'content-length' : req.header('Content-Length')
    };
    res.send(data);
});

app.delete("/post/delete/:id", (req, res) => {

    res.send(`Deleted Post Id : ${req.params.id}`);
});


// Connect Server
app.listen(5000, () => console.log(`Server started at port 5000`));

```