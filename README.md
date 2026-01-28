# Jaiswal-Ji-video
Jaiswal Ji video 
<!DOCTYPE html>
<html>
  <head>
    <title>Jaiswal Ji Video Maker</title>
  </head>
  <body>
    <h1>Paste Story → Get 10 Minute Video</h1>

    <textarea id="input" placeholder="Paste story here"></textarea>
    <button onclick="generate()">Generate Video</button>

    <p id="output"></p>

    <script>
      async function generate() {
        let story = document.getElementById("input").value;

        let res = await fetch("/generate", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ story })
        });

        let data = await res.json();
        document.getElementById("output").innerText = data.message;
      }
    </script>
  </body>
</html>
import express from "express";
import cors from "cors";
import dotenv from "dotenv";
dotenv.config();

const app = express();
app.use(cors());
app.use(express.json());

app.get("/", (req, res) => {
  res.send("Jaiswal Ji Video Generator LIVE");
});

app.post("/generate", (req, res) => {
  const { story } = req.body;

  if (!story) {
    return res.json({ error: "Story not provided" });
  }

  return res.json({
    message: "Your 10 minute video is generating...",
    story
  });
});

app.listen(process.env.PORT || 3000, () => {
  console.log("Server running...");
});{
  "name": "jaiswalji-video",
  "version": "1.0.0",
  "main": "server.js",
  "type": "module",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "cors": "^2.8.5",
    "dotenv": "^16.3.1"
  }
}
