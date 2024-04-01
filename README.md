# HCI_Finals
Revised Pokemon Game



//HTML//
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pokemon Fight</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="container">
    <div class="pokemon" id="pokemon1">
      <h2>Pikachu</h2>
      <div class="health-bar">
        <div class="health-bar-inner" style="width: 100%;" id="health1"></div>
      </div>
      <img src="pokemon1.png" alt="Pokemon 1">
      <div class="skills">
        <button class="skill" onclick="useSkill(10)">Thunder Shock</button>
        <button class="skill" onclick="useSkill(😎">Quick Attack</button>
        <button class="skill" onclick="useSkill(15)">Thunderbolt</button>
      </div>
    </div>
    <div class="pokemon" id="pokemon2">
      <h2>Charmander</h2>
      <div class="health-bar">
        <div class="health-bar-inner" style="width: 100%;" id="health2"></div>
      </div>
      <img src="pokemon2.png" alt="Pokemon 2">
    </div>
  </div>
  <script src="script.js"></script>
</body>
</html>





//CSS//
body {
  background-image: url('background.jpg');
  background-size: cover;
  background-repeat: no-repeat;
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
  margin-top: 50px;
}

.pokemon {
  text-align: center;
  margin: 20px;
}

.health-bar {
  background-color: #ddd;
  border-radius: 5px;
  height: 20px;
  margin-bottom: 10px;
}

.health-bar-inner {
  background-color: #4CAF50;
  border-radius: 5px;
  height: 100%;
}

button {
  padding: 20px 40px;
  font-size: 20px;
  cursor: pointer;
  border: none;
  border-radius: 5px;
  background-color: #4CAF50;
  color: white;
  transition: background-color 0.3s ease;
  margin-top: 20px;
}

button:hover {
  background-color: #45a049;
}

.skills {
  margin-top: 40px;
}

.skill {
  margin: 10px 10px;
  padding: 15px 30px;
  border: 1px solid #000;
  cursor: pointer;
  font-size: 16px;
}

.skill:hover {
  background-color: #4CAF50;
  color: white;
}

/* Animation */
@keyframes shakeAnimation {
  0% { transform: translateX(0); }
  25% { transform: translateX(-5px) rotate(-5deg); }
  50% { transform: translateX(5px) rotate(5deg); }
  75% { transform: translateX(-5px) rotate(-5deg); }
  100% { transform: translateX(0); }
}

.pokemon.shake {
  animation: shakeAnimation 0.5s ease;
}





//JAVASCRIPT//
function fight() {
  var health1 = document.getElementById('health1');
  var health2 = document.getElementById('health2');

  var damage1 = Math.floor(Math.random() * 10) + 1;
  var damage2 = Math.floor(Math.random() * 10) + 1;

  var currentHealth1 = parseInt(health1.style.width);
  var currentHealth2 = parseInt(health2.style.width);

  currentHealth1 -= damage2;
  currentHealth2 -= damage1;

  if (currentHealth1 <= 0) {
    currentHealth1 = 0;
    alert("Charmander wins!");
  } else if (currentHealth2 <= 0) {
    currentHealth2 = 0;
    alert("Pikachu wins!");
  }

  health1.style.width = currentHealth1 + '%';
  health2.style.width = currentHealth2 + '%';
}

function useSkill(damage) {
  var health1 = document.getElementById('health1');
  var health2 = document.getElementById('health2');
  var pokemon1 = document.getElementById('pokemon1');
  var pokemon2 = document.getElementById('pokemon2');

  var currentHealth1 = parseInt(health1.style.width);
  var currentHealth2 = parseInt(health2.style.width);

  currentHealth2 -= damage;

  if (currentHealth2 <= 0) {
    currentHealth2 = 0;
    alert("Pikachu wins!");
  }

  health2.style.width = currentHealth2 + '%';

  // Animation for pokemon2
  pokemon2.classList.add('shake');
  setTimeout(function() {
    pokemon2.classList.remove('shake');
  }, 500);

  // Opponent's turn
  var damage1 = Math.floor(Math.random() * 10) + 1;
  currentHealth1 -= damage1;

  if (currentHealth1 <= 0) {
    currentHealth1 = 0;
    alert("Charmander wins!");
  }

  health1.style.width = currentHealth1 + '%';

  // Animation for pokemon1
  pokemon1.classList.add('shake');
  setTimeout(function() {
    pokemon1.classList.remove('shake');
  }, 500);
}
