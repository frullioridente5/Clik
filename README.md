<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Click Game</title>
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background: linear-gradient(135deg, #8e44ad, #3498db);
            overflow: hidden;
            color: white;
        }
        .container {
            text-align: center;
            background: rgba(255, 255, 255, 0.2);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(10px);
        }
        .points {
            font-size: 32px;
            font-weight: bold;
            margin-bottom: 20px;
            color: #f1c40f;
            text-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        }
        .click-btn {
            padding: 15px 50px;
            font-size: 22px;
            background-color: #e74c3c;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 20px;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        .click-btn:hover {
            background-color: #c0392b;
            transform: scale(1.1);
        }
        .click-btn:active {
            transform: scale(1);
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.3);
        }
        .particles {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            z-index: -1;
        }
        .particle {
            position: absolute;
            background-color: white;
            width: 10px;
            height: 10px;
            opacity: 0.7;
            border-radius: 50%;
            animation: float 6s ease-in-out infinite;
        }
        @keyframes float {
            0% {
                transform: translateY(0) rotate(0deg);
                opacity: 0.5;
            }
            50% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100vh) rotate(720deg);
                opacity: 0;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <div class="points">Points: <span id="score">0</span></div>
        <button class="click-btn" onclick="incrementScore()">Click me!</button>
    </div>

    <div class="particles"></div>

    <!-- Aggiungi l'elemento audio per il suono del click -->
    <audio id="clickSound">
        <source src="click-sound.mp3" type="audio/mpeg">
        <!-- Un messaggio se il browser non supporta l'audio -->
        Your browser does not support the audio element.
    </audio>

    <script>
        let score = 0;
        const maxScore = 10000000000000000; // Limite massimo per il reset

        // Ripristina il punteggio salvato quando la pagina viene caricata
        window.onload = function() {
            if (localStorage.getItem('score')) {
                score = parseInt(localStorage.getItem('score'));
                document.getElementById('score').textContent = score;
            }
        };

        // Incrementa il punteggio e riproduci il suono del click
        function incrementScore() {
            score++;
            if (score >= maxScore) {
                score = 0; // Resetta il punteggio se raggiunge o supera il limite
            }
            document.getElementById('score').textContent = score;

            // Riproduci il suono del click
            const clickSound = document.getElementById('clickSound');
            clickSound.play();

            // Salva il nuovo punteggio nel localStorage
            localStorage.setItem('score', score);
        }

        // Crea particelle fluttuanti
        function createParticle() {
            const particle = document.createElement('div');
            particle.classList.add('particle');
            document.querySelector('.particles').appendChild(particle);

            // Posizionamento casuale
            particle.style.left = Math.random() * 100 + 'vw';
            particle.style.animationDuration = Math.random() * 2 + 5 + 's';

            // Rimuovi la particella dopo l'animazione
            setTimeout(() => {
                particle.remove();
            }, 6000);
        }

        // Crea particelle continuamente
        setInterval(createParticle, 300);
    </script>

</body>
</html>
