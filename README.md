<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Key Generator with Custom Duration</title>
  <style>
    :root {
      --primary-color: #00ffff;
      --bg-color: #1a1a1a;
      --text-color: #eee;
      --input-bg: rgba(255, 255, 255, 0.1);
      --border-radius: 8px;
    }
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      background: linear-gradient(135deg, var(--bg-color), #000);
      font-family: 'Poppins', sans-serif;
      color: var(--text-color);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      padding: 20px;
    }
    .container {
      background: rgba(0, 0, 0, 0.85);
      border: 2px solid var(--primary-color);
      border-radius: var(--border-radius);
      width: 100%;
      max-width: 400px;
      padding: 30px;
      text-align: center;
      box-shadow: 0 8px 16px rgba(0,0,0,0.5);
    }
    h1 {
      margin-bottom: 20px;
      color: var(--primary-color);
      text-transform: uppercase;
      letter-spacing: 1px;
    }
    .key-output {
      margin: 20px 0;
      padding: 12px;
      background: var(--input-bg);
      border: 1px solid var(--primary-color);
      border-radius: var(--border-radius);
      font-size: 18px;
      letter-spacing: 1px;
      word-break: break-all;
    }
    .timer {
      margin: 10px 0;
      font-size: 16px;
    }
    .duration-input {
      margin: 15px 0;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      font-size: 16px;
    }
    .duration-input input {
      width: 80px;
      padding: 8px;
      background: var(--input-bg);
      border: 1px solid var(--primary-color);
      border-radius: var(--border-radius);
      color: var(--text-color);
      text-align: center;
    }
    button {
      width: 100%;
      padding: 12px;
      background: var(--primary-color);
      border: none;
      border-radius: var(--border-radius);
      color: var(--bg-color);
      font-size: 18px;
      font-weight: bold;
      cursor: pointer;
      transition: background 0.3s ease;
      margin-top: 15px;
    }
    button:hover {
      background: #00cccc;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Key Generator</h1>
    <div class="key-output" id="keyOutput">Your key will appear here</div>
    <div class="timer" id="keyTimer">Key valid for: -- seconds</div>
    <div class="duration-input">
      <label for="duration">Set Duration (sec):</label>
      <input type="number" id="duration" value="300" min="10">
    </div>
    <button id="generateBtn">Generate Key</button>
  </div>

  <script>
    let countdownInterval;

    // Function to generate a random alphanumeric key of a given length
    function generateRandomString(length) {
      const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
      let key = '';
      for (let i = 0; i < length; i++) {
        key += chars.charAt(Math.floor(Math.random() * chars.length));
      }
      return key;
    }

    // Function to start the countdown timer using a custom duration (in seconds)
    function startTimer(duration) {
      let timeRemaining = duration;
      const timerDisplay = document.getElementById('keyTimer');
      timerDisplay.textContent = `Key valid for: ${timeRemaining} seconds`;

      clearInterval(countdownInterval);
      countdownInterval = setInterval(() => {
        timeRemaining--;
        if (timeRemaining <= 0) {
          clearInterval(countdownInterval);
          timerDisplay.textContent = "Key expired. Generate a new key.";
          document.getElementById('keyOutput').textContent = "Key expired. Please generate a new key.";
        } else {
          timerDisplay.textContent = `Key valid for: ${timeRemaining} seconds`;
        }
      }, 1000);
    }

    // Generate key and start timer using the duration provided by the user
    function generateKeys() {
      const durationInput = document.getElementById('duration');
      const duration = parseInt(durationInput.value, 10);
      const newKey = generateRandomString(16); // Generate a key of length 16
      document.getElementById('keyOutput').textContent = newKey;
      startTimer(duration);
    }

    document.getElementById('generateBtn').addEventListener('click', generateKeys);
  </script>
</body>
</html>
