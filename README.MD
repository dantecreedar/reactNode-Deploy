# ReactNode Deploy

## Client $$ server

- client:
    - public
    - src
    - package.json
    - README.MD

- server:
    - data
    - index
    -.gitignore
    - package.json
    - README.MD
# Image:
<img src='./react-node-deploy/img/Screenshot_1.png'/>

## server
``` javascript
// server/index.js
const path = require("path")
const express = require("express");
const data = require("./data/pokemon.json")

const PORT = process.env.PORT || 3001;

const app = express();

app.use(express.static(path.resolve(__dirname, "../client/build")))

app.get("/api", (req, res) => {
    res.json(data);
});

app.get("*", (req, res) => {
    res.sendFile(path.resolve(__dirname, '../client/build', "index.html"))
})

app.listen(PORT, () => {
    console.log(`Server listening on http://localhost:${PORT}`);
});
```
## App FrontEnd
```javascript
// client/src/App.js

import React from "react";
import "./App.css";

function App() {
  const [data, setData] = React.useState(null);

  React.useEffect(() => {
    fetch("/api")
      .then((res) => res.json())
      .then((data) => {
        setData(data)

      });
  }, []);

  if (!data) return <p>"Loading..."</p>

  return data && (
    <>
      <h1>Hola</h1>
      <ul>

        {data.slice(0, 20).map((el) => <li key={el.id}>{el.name.english}</li>)}
      </ul>
    </>

  );
}

export default App;
```
