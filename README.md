# Greatchickengame.github.io
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Custom Image Shooter</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      overflow: hidden;
      background-color: #e0f7fa;
    }
    #character {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 100px;
      height: auto;
      transform: translate(-50%, -50%);
    }
    .bullet {
      position: absolute;
      width: 10px;
      height: 10px;
      background-color: red;
      border-radius: 50%;
    }
  </style>
</head>
<body>
  <img id="character" src="https://ih1.redbubble.net/image.5426235696.4598/raf,360x360,075,t,fafafa:ca443f4786.u4.jpg">

  <script>
    const character = document.getElementById("character");
    let topPosition = window.innerHeight / 2;
    let leftPosition = window.innerWidth / 2;

    // Move character
    function moveCharacter(event) {
      const step = 10; // Pixels to move per key press
      switch (event.key) {
        case "ArrowUp":
          topPosition -= step;
          break;
        case "ArrowDown":
          topPosition += step;
          break;
        case "ArrowLeft":
          leftPosition -= step;
          break;
        case "ArrowRight":
          leftPosition += step;
          break;
        case " ": // Space bar for shooting
          shoot();
          return;
      }
      character.style.top = `${topPosition}px`;
      character.style.left = `${leftPosition}px`;
    }

    // Shoot a bullet
    function shoot() {
      const bullet = document.createElement("div");
      bullet.classList.add("bullet");
      document.body.appendChild(bullet);

      // Position bullet at the character's current position
      bullet.style.top = `${topPosition}px`;
      bullet.style.left = `${leftPosition + 50}px`;

      // Move bullet to the right
      let bulletInterval = setInterval(() => {
        const currentLeft = parseInt(bullet.style.left);
        bullet.style.left = `${currentLeft + 10}px`;

        // Remove the bullet when it goes off-screen
        if (currentLeft > window.innerWidth) {
          bullet.remove();
          clearInterval(bulletInterval);
        }
      }, 20); // Speed of bullet
    }

    // Listen for key presses
    document.addEventListener("keydown", moveCharacter);
  </script>
</body>
</html>
