 

### Step 1: Set Up the Project Directory

Create the project directory and navigate into it:

```bash
mkdir stopwatch_app
cd stopwatch_app
```

### Step 2: Initialize the Project

Initialize the Node.js project:

```bash
npm init -y
```

### Step 3: Install Required Packages

Install Express and EJS for the project:

```bash
npm install express ejs
```

### Step 4: Create the Project Structure

Create the necessary directories and files:

```bash
mkdir views
nano server.js
```

### Step 5: Write the Server Code

In the `server.js` file, paste the following code:

```javascript
const express = require('express');
const path = require('path');
const app = express();
const PORT = 3000;

app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, 'views'));

app.get('/', (req, res) => {
    res.render('stopwatch');
});

app.listen(PORT, () => {
    console.log(`Server running at http://localhost:${PORT}/`);
});
```

Save the file by pressing `Ctrl + O`, then `Enter`, and `Ctrl + X` to exit the nano editor.

### Step 6: Create the EJS View

Create the `stopwatch.ejs` file inside the `views` directory:

```bash
nano views/stopwatch.ejs
```

Paste the following code into the `stopwatch.ejs` file:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch</title>
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
    <style>
        .stopwatch {
            text-align: center;
            margin-top: 50px;
        }
        .time {
            font-size: 48px;
            font-weight: bold;
        }
        .buttons {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="container stopwatch">
        <div class="time" id="time">00:00:00</div>
        <div class="buttons">
            <button class="btn btn-success" onclick="start()">Start</button>
            <button class="btn btn-danger" onclick="stop()">Stop</button>
            <button class="btn btn-secondary" onclick="reset()">Reset</button>
        </div>
    </div>

    <script>
        let timer;
        let startTime;
        let elapsedTime = 0;

        function start() {
            startTime = Date.now() - elapsedTime;
            timer = setInterval(updateTime, 1000);
        }

        function stop() {
            clearInterval(timer);
            elapsedTime = Date.now() - startTime;
        }

        function reset() {
            clearInterval(timer);
            elapsedTime = 0;
            document.getElementById('time').textContent = '00:00:00';
        }

        function updateTime() {
            elapsedTime = Date.now() - startTime;
            let totalSeconds = Math.floor(elapsedTime / 1000);

            let hours = Math.floor(totalSeconds / 3600);
            let minutes = Math.floor((totalSeconds % 3600) / 60);
            let seconds = totalSeconds % 60;

            hours = String(hours).padStart(2, '0');
            minutes = String(minutes).padStart(2, '0');
            seconds = String(seconds).padStart(2, '0');

            document.getElementById('time').textContent = `${hours}:${minutes}:${seconds}`;
        }
    </script>
</body>
</html>
```

Save the file by pressing `Ctrl + O`, then `Enter`, and `Ctrl + X` to exit the nano editor.

### Step 7: Run the Application

Start the server by running the following command:

```bash
node server.js
```

You should see the output:

```
Server running at http://localhost:3000/
```

### Step 8: Access the Stopwatch

Open your browser and navigate to `http://your-ec2-public-ip:3000/` to see the stopwatch application. You can start, stop, and reset the timer using the buttons provided.

 
