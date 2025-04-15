<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Carbon Catcher</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
    <style>
      @font-face {
        font-family: 'LucideIcons';
        src: url(https://cdn.jsdelivr.net/npm/lucide-static@latest/font/Lucide.ttf) format('truetype');
      }
      .lucide-icon {
        font-family: 'LucideIcons';
        font-size: 1.25rem; /* Adjust size as needed */
        line-height: 1;
      }
      /* Custom styles */
      body {
        font-family: 'Press Start 2P', cursive;
        overflow: hidden; /* Prevent scrollbars */
      }
      canvas {
        display: block;
        background-color: #87ceeb; /* Default sky blue */
        cursor: none; /* Hide default cursor over canvas */
      }
      .game-ui-element {
         text-shadow: 2px 2px #000; /* Simple text shadow for readability */
      }
      .game-button {
        border: 4px solid black;
        box-shadow: 4px 4px 0px black;
        transition: all 0.1s ease-out;
      }
      .game-button:active {
        box-shadow: 1px 1px 0px black;
        transform: translate(3px, 3px);
      }
    </style>
</head>
<body class="bg-gray-800 flex flex-col items-center justify-center min-h-screen text-white p-4">

    <h1 class="text-3xl mb-2 game-ui-element">Carbon Catcher</h1>
    <p class="mb-4 text-sm game-ui-element">Clean the sky, secure the future.</p>

    <div class="flex justify-between w-full max-w-2xl mb-2 text-lg px-2">
        <div class="game-ui-element">Score: <span id="score">0</span></div>
        <div class="game-ui-element">Missed: <span id="missed">0</span> / <span id="miss-limit">10</span></div>
    </div>

    <div class="relative w-full max-w-2xl aspect-[4/3] border-4 border-black rounded-lg overflow-hidden shadow-lg">
        <canvas id="gameCanvas" class="w-full h-full"></canvas>

        <div id="gameOverScreen" class="absolute inset-0 bg-black bg-opacity-75 flex-col items-center justify-center text-center p-8 rounded-lg hidden">
            <h2 id="gameOverText" class="text-4xl mb-6 game-ui-element">Game Over!</h2>
            <p id="finalScoreText" class="text-xl mb-6 game-ui-element">Your final score: 0</p>
            <button id="restartButton" class="game-button bg-green-500 hover:bg-green-600 text-black font-bold py-3 px-6 rounded-md text-xl flex items-center gap-2">
                <span class="lucide-icon">&#xea11;</span> Play Again </button>
        </div>
         <div id="startScreen" class="absolute inset-0 bg-black bg-opacity-75 flex flex-col items-center justify-center text-center p-8 rounded-lg">
            <h2 class="text-2xl mb-6 game-ui-element">Move Mouse to Catch!</h2>
            <p class="text-lg mb-6 game-ui-element">Use the net to catch CO₂ before 10 clouds escape.</p>
            <button id="startButton" class="game-button bg-blue-500 hover:bg-blue-600 text-black font-bold py-3 px-6 rounded-md text-xl">
                Start Game
            </button>
        </div>
    </div>

    <script>
        // --- Game Setup ---
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const scoreDisplay = document.getElementById('score');
        const missedDisplay = document.getElementById('missed');
        const missLimitDisplay = document.getElementById('miss-limit');
        const gameOverScreen = document.getElementById('gameOverScreen');
        const gameOverText = document.getElementById('gameOverText');
        const finalScoreText = document.getElementById('finalScoreText');
        const restartButton = document.getElementById('restartButton');
        const startScreen = document.getElementById('startScreen');
        const startButton = document.getElementById('startButton');

        let score = 0;
        let missed = 0;
        const missLimit = 10;
        let clouds = []; // { x, y, speed, radius, state: 'rising' | 'captured' }
        let gameRunning = false;
        let animationFrameId;
        let baseCloudSpawnRate = 1200;
        let lastSpawnTime = 0;

        // --- Horizon & Ground ---
        let horizonY;
        const earthColor = '#8b4513';
        const grassColor = '#228b22';

        // --- Character Properties ---
        const character = {
            x: 0, y: 0, width: 30, height: 40, color: '#f0e68c',
            net: {
                offsetX: 0, offsetY: -50, width: 55, height: 45,
                stickLength: 50, stickWidth: 6, color: '#a0522d',
                hoopColor: '#808080', netColor: '#d3d3d3'
            }
        };
        let mouseX = 0;

        // --- Cloud Properties ---
        const baseCloudRadius = 20;
        const cloudColor = '#6b7280';
        const capturedCloudSpeed = 5;

        // --- Canvas Sizing ---
        function resizeCanvas() {
            const container = canvas.parentElement;
            canvas.width = container.clientWidth;
            canvas.height = container.clientHeight;
            horizonY = canvas.height * (2 / 3);
            character.y = horizonY + 5; // Y pos of character semicircle center
            character.x = canvas.width / 2;
            mouseX = character.x;
        }
        window.addEventListener('resize', resizeCanvas);

        // --- Game Functions ---

        function updateSkyBackground() {
            const clarity = Math.max(0, 1 - (missed / missLimit));
            const pollutedColor = '#4a5568'; const clearColor = '#87ceeb';
            const r1 = parseInt(pollutedColor.slice(1, 3), 16), g1 = parseInt(pollutedColor.slice(3, 5), 16), b1 = parseInt(pollutedColor.slice(5, 7), 16);
            const r2 = parseInt(clearColor.slice(1, 3), 16), g2 = parseInt(clearColor.slice(3, 5), 16), b2 = parseInt(clearColor.slice(5, 7), 16);
            const r = Math.round(r1 + (r2 - r1) * clarity), g = Math.round(g1 + (g2 - g1) * clarity), b = Math.round(b1 + (b2 - b1) * clarity);
            const skyColor = `rgb(${r},${g},${b})`;
            const gradient = ctx.createLinearGradient(0, 0, 0, horizonY);
            gradient.addColorStop(0, skyColor);
            gradient.addColorStop(1, `rgb(${Math.min(255, r + 50)}, ${Math.min(255, g + 50)}, ${Math.min(255, b + 50)})`);
            ctx.fillStyle = gradient;
            ctx.fillRect(0, 0, canvas.width, horizonY);
        }

        function drawGround() {
            ctx.fillStyle = earthColor;
            ctx.fillRect(0, horizonY, canvas.width, canvas.height - horizonY);
            ctx.fillStyle = grassColor;
            ctx.fillRect(0, horizonY, canvas.width, 15);
        }

        // *** MODIFIED drawCharacter Function for Denser Net Mesh ***
        function drawCharacter() {
            // --- Draw Character Body ---
            ctx.fillStyle = character.color;
            ctx.beginPath();
            ctx.arc(character.x, character.y, character.width / 2, Math.PI, 0);
            ctx.fill();

            // --- Calculate Stick Position ---
            const stickBaseX = character.x + character.net.offsetX;
            const stickBaseY = horizonY - 5;
            const stickTopX = stickBaseX;
            const stickTopY = stickBaseY - character.net.stickLength;

            // --- Draw Stick ---
            ctx.fillStyle = character.net.color;
            ctx.fillRect(stickTopX - character.net.stickWidth / 2, stickTopY, character.net.stickWidth, character.net.stickLength);
            ctx.strokeStyle = '#654321'; // Darker brown shadow/highlight
            ctx.lineWidth = 1;
            ctx.beginPath();
            ctx.moveTo(stickTopX - character.net.stickWidth / 2 + 1, stickTopY);
            ctx.lineTo(stickTopX - character.net.stickWidth / 2 + 1, stickBaseY);
            ctx.stroke();

            // --- Calculate Hoop Position ---
            const hoopCenterX = stickTopX;
            const hoopCenterY = stickTopY - character.net.height / 2;
            const hoopWidth = character.net.width;
            const hoopHeight = character.net.height;
            const hoopRadiusX = hoopWidth / 2;
            const hoopRadiusY = hoopHeight / 2;

            // --- Draw Hoop ---
            ctx.strokeStyle = character.net.hoopColor;
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.ellipse(hoopCenterX, hoopCenterY, hoopRadiusX, hoopRadiusY, 0, 0, Math.PI * 2);
            ctx.stroke();

            // --- Draw Denser Mesh ---
            ctx.strokeStyle = character.net.netColor;
            ctx.lineWidth = 1; // Thin lines for mesh

            // Increase number of lines for denser mesh
            const numVerticalLines = 8; // Increased
            for (let i = 1; i < numVerticalLines; i++) {
                const x = hoopCenterX - hoopRadiusX + (hoopWidth * i / numVerticalLines);
                // Calculate precise top/bottom points on the ellipse for this x
                const dy = Math.sqrt(Math.max(0, (1 - Math.pow((x - hoopCenterX) / hoopRadiusX, 2)) * Math.pow(hoopRadiusY, 2)));
                const y1 = hoopCenterY - dy;
                const y2 = hoopCenterY + dy;
                ctx.beginPath();
                ctx.moveTo(x, y1);
                // Use quadratic curve with control point towards center for gentle curve
                ctx.quadraticCurveTo(x, hoopCenterY, x, y2);
                ctx.stroke();
            }

            const numHorizontalLines = 7; // Increased
            for (let i = 1; i < numHorizontalLines; i++) {
                const y = hoopCenterY - hoopRadiusY + (hoopHeight * i / numHorizontalLines);
                // Calculate precise left/right points on the ellipse for this y
                const dx = Math.sqrt(Math.max(0, (1 - Math.pow((y - hoopCenterY) / hoopRadiusY, 2)) * Math.pow(hoopRadiusX, 2)));
                const x1 = hoopCenterX - dx;
                const x2 = hoopCenterX + dx;
                ctx.beginPath();
                ctx.moveTo(x1, y);
                // Use quadratic curve with control point towards center
                ctx.quadraticCurveTo(hoopCenterX, y, x2, y);
                ctx.stroke();
            }

            // Reset line width
            ctx.lineWidth = 1;
        }


         function updateCharacterPosition() {
            const halfBodyWidth = character.width / 2;
            character.x = Math.max(halfBodyWidth, Math.min(canvas.width - halfBodyWidth, mouseX));
        }


        function spawnCloud() {
            if (!gameRunning) return;
            const radius = baseCloudRadius * (0.8 + Math.random() * 0.4);
            const x = Math.random() * (canvas.width - radius * 2) + radius;
            const y = canvas.height + radius; // Start just below the canvas
            const speed = 1 + Math.random() * 1.5 + (score * 0.01);
            clouds.push({ x, y, speed, radius, state: 'rising' });
        }

        function updateClouds(deltaTime) {
            const hoopCenterX = character.x + character.net.offsetX;
            const hoopCenterY = (horizonY - 5 - character.net.stickLength) - character.net.height / 2;
            const netTopY = hoopCenterY - character.net.height / 2;
            const netBottomY = hoopCenterY + character.net.height / 2;
            const netLeftX = hoopCenterX - character.net.width / 2;
            const netRightX = hoopCenterX + character.net.width / 2;
            const dtFactor = deltaTime / 16.67;

            for (let i = clouds.length - 1; i >= 0; i--) {
                const cloud = clouds[i];
                if (cloud.state === 'rising') {
                    cloud.y -= cloud.speed * dtFactor; // Move up
                    // Collision check
                    if (cloud.x > netLeftX && cloud.x < netRightX && cloud.y > netTopY && cloud.y < netBottomY) {
                        const distSq = Math.pow((cloud.x - hoopCenterX) / (character.net.width / 2), 2) +
                                       Math.pow((cloud.y - hoopCenterY) / (character.net.height / 2), 2);
                        if (distSq < 1.1) { // Check if center is within ellipse bounds
                            cloud.state = 'captured';
                            score++;
                            scoreDisplay.textContent = score;
                        }
                    } else if (cloud.y < -cloud.radius) { // Escape check
                        clouds.splice(i, 1);
                        missed++;
                        missedDisplay.textContent = missed;
                        updateSkyBackground();
                        if (missed >= missLimit) gameOver("Too much pollution!");
                    }
                } else if (cloud.state === 'captured') { // Capture animation
                    cloud.y += capturedCloudSpeed * dtFactor;
                    cloud.radius *= 0.98;
                    if (cloud.y > horizonY || cloud.radius < 2) clouds.splice(i, 1);
                }
            }
        }

        function drawClouds() {
            ctx.fillStyle = cloudColor;
            ctx.shadowColor = 'rgba(0, 0, 0, 0.3)'; ctx.shadowBlur = 4;
            ctx.shadowOffsetX = 1; ctx.shadowOffsetY = 1;
            clouds.forEach(cloud => {
                ctx.beginPath();
                ctx.arc(cloud.x, cloud.y, cloud.radius, 0, Math.PI * 2);
                ctx.fill();
            });
            ctx.shadowColor = 'transparent'; ctx.shadowBlur = 0;
            ctx.shadowOffsetX = 0; ctx.shadowOffsetY = 0;
        }

        function handleMouseMove(event) {
             if (!gameRunning) return;
             const rect = canvas.getBoundingClientRect();
             mouseX = event.clientX - rect.left;
        }

        function gameOver(reason) {
            gameRunning = false;
            cancelAnimationFrame(animationFrameId);
            gameOverText.textContent = reason;
            finalScoreText.textContent = `Your final score: ${score}`;
            gameOverScreen.classList.remove('hidden'); gameOverScreen.classList.add('flex');
            canvas.style.cursor = 'default';
        }

        function resetGame() {
            score = 0; missed = 0; clouds = [];
            scoreDisplay.textContent = score; missedDisplay.textContent = missed;
            missLimitDisplay.textContent = missLimit;
            gameOverScreen.classList.add('hidden'); gameOverScreen.classList.remove('flex');
            startScreen.classList.remove('hidden'); startScreen.classList.add('flex');
            lastSpawnTime = 0;
            resizeCanvas();
            updateSkyBackground();
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            drawGround();
        }

        function startGame() {
            startScreen.classList.add('hidden'); startScreen.classList.remove('flex');
            score = 0; missed = 0; clouds = [];
            scoreDisplay.textContent = score; missedDisplay.textContent = missed;
            gameRunning = true;
            lastSpawnTime = performance.now();
            resizeCanvas(); updateSkyBackground();
            canvas.style.cursor = 'none';
            lastTime = performance.now();
            gameLoop(lastTime);
        }

        // --- Game Loop ---
        let lastTime = 0;
        function gameLoop(timestamp) {
            if (!gameRunning) return;
            const deltaTime = timestamp - lastTime;
            lastTime = timestamp;
            ctx.clearRect(0, 0, canvas.width, horizonY); // Clear sky
            updateSkyBackground(); drawGround(); // Redraw background
            if (timestamp - lastSpawnTime > baseCloudSpawnRate) { spawnCloud(); lastSpawnTime = timestamp; } // Spawn
            updateCharacterPosition(); // Update character
            updateClouds(deltaTime);   // Update clouds
            drawClouds(); drawCharacter(); // Draw elements
            animationFrameId = requestAnimationFrame(gameLoop); // Next frame
        }

        // --- Event Listeners ---
        canvas.addEventListener('mousemove', handleMouseMove);
        restartButton.addEventListener('click', resetGame);
        startButton.addEventListener('click', startGame);

        // --- Initial Setup ---
        resizeCanvas(); updateSkyBackground(); drawGround(); resetGame();

    </script>

</body>
</html>
