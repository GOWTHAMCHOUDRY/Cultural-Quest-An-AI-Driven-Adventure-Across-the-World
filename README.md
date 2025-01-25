# Cultural-Quest-An-AI-Driven-Adventure-Across-the-World
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AI Adaptive Quest Game</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f0f0f0;
      text-align: center;
      margin-top: 50px;
    }
    .container {
      width: 50%;
      margin: 0 auto;
      padding: 20px;
      background-color: white;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      margin: 10px;
      cursor: pointer;
      border: none;
      background-color: #007bff;
      color: white;
      border-radius: 5px;
    }
    button:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>AI Adaptive Quest Game</h1>
    <p>Welcome to the game! Please choose your region and cultural values.</p>
    
    <label for="region">Select your region:</label>
    <select id="region">
      <option value="North America">North America</option>
      <option value="Europe">Europe</option>
      <option value="Asia">Asia</option>
      <option value="Africa">Africa</option>
      <option value="South America">South America</option>
    </select>

    <br><br>

    <label for="culture">Select your cultural preference:</label>
    <select id="culture">
      <option value="Adventure">Adventure</option>
      <option value="Nature">Nature</option>
      <option value="Technology">Technology</option>
      <option value="Community">Community</option>
    </select>

    <br><br>

    <button onclick="submitPreferences()">Start Game</button>

    <div id="quest-area" style="display: none;">
      <h2>Your Adaptive Quest:</h2>
      <p id="quest"></p>
      <button onclick="completeQuest()">Complete Quest</button>
    </div>
  </div>

  <script>
    function submitPreferences() {
      const region = document.getElementById('region').value;
      const culture = document.getElementById('culture').value;

      fetch('/start_game', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ region, culture })
      })
      .then(response => response.json())
      .then(data => {
        if (data.quest) {
          document.getElementById('quest-area').style.display = 'block';
          document.getElementById('quest').innerText = data.quest;
        } else {
          alert("Error fetching quest. Please try again.");
        }
      })
      .catch(error => {
        console.error('Error:', error);
        alert("There was an error processing your request.");
      });
    }

    function completeQuest() {
      alert("Quest completed! You earned a reward.");
    }
  </script>
</body>
</html>
