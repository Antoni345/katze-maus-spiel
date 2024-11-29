# katze-maus-spiel
#<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Katzen vs. Maus Spiel</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            background-color: #ffc0cb; /* Pinker Hintergrund */
            overflow: hidden; /* Kein Scrollen erlaubt */
        }

        header {
            position: fixed;
            width: 100%;
            background-color: #ff69b4; /* Helleres Pink */
            color: white;
            text-align: center;
            padding: 10px 0;
            z-index: 1000;
        }

        header h1 {
            margin: 0;
        }

        #game-area {
            position: absolute;
            top: 50px; /* Platz für den Header */
            left: 0;
            width: 100%;
            height: calc(100vh - 50px); /* Ganzer Bildschirm abzüglich Header */
        }

        .cat {
            position: absolute;
            width: 50px;
            height: 50px;
            background-color: orange;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 24px;
            color: #fff;
        }

        .mouse {
            position: absolute;
            width: 30px;
            height: 30px;
            background-color: gray;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 18px;
            color: #fff;
        }

        footer {
            position: fixed;
            bottom: 0;
            width: 100%;
            background-color: #ff69b4;
            color: white;
            text-align: center;
            padding: 5px 0;
            z-index: 1000;
        }
    </style>
</head>
<body>
    <header>
        <h1>Katzen vs. Maus</h1>
        <p>Steuere die Katze mit den Pfeiltasten, um die Maus zu fangen!</p>
    </header>

    <div id="game-area">
        <div id="cat" class="cat">🐱</div>
        <div id="mouse" class="mouse">🐭</div>
    </div>

    <footer>
        <p>Viel Spaß beim Spielen!</p>
    </footer>

    <script>
        const cat = document.getElementById('cat');
        const mouse = document.getElementById('mouse');
        const gameArea = document.getElementById('game-area');

        let catPosition = { x: 10, y: 10 };
        let mousePosition = { x: 300, y: 200 };

        // Zufällige Mausbewegung
        function moveMouse() {
            mousePosition.x = Math.random() * (gameArea.clientWidth - 30);
            mousePosition.y = Math.random() * (gameArea.clientHeight - 30);
            mouse.style.left = mousePosition.x + 'px';
            mouse.style.top = mousePosition.y + 'px';
        }

        // Bewegung der Katze mit Pfeiltasten
        document.addEventListener('keydown', (event) => {
            const step = 15;
            if (event.key === 'ArrowUp') catPosition.y = Math.max(catPosition.y - step, 0);
            if (event.key === 'ArrowDown') catPosition.y = Math.min(catPosition.y + step, gameArea.clientHeight - 50);
            if (event.key === 'ArrowLeft') catPosition.x = Math.max(catPosition.x - step, 0);
            if (event.key === 'ArrowRight') catPosition.x = Math.min(catPosition.x + step, gameArea.clientWidth - 50);

            cat.style.left = catPosition.x + 'px';
            cat.style.top = catPosition.y + 'px';

            // Prüfen, ob die Katze die Maus gefangen hat
            if (
                catPosition.x < mousePosition.x + 30 &&
                catPosition.x + 50 > mousePosition.x &&
                catPosition.y < mousePosition.y + 30 &&
                catPosition.y + 50 > mousePosition.y
            ) {
                alert('Du hast die Maus gefangen!');
                moveMouse();
            }
        });

        // Starte das Spiel mit einer Mausbewegung alle 2 Sekunden
        setInterval(moveMouse, 2000);
        moveMouse();
    </script>
</body>
</html>
