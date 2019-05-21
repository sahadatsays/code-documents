```javascript

const express = require('express');
const path = require('path');

const app = express();

app.use(express.json());
app.use(express.urlencoded({ extended: false }));

// GET Request
app.get('/', (req, res) => {
    res.json({"msg" : "Hello JSON Message !"});
});


// Connect Server
app.listen(5000, () => console.log(`Server started at port 5000`));

```