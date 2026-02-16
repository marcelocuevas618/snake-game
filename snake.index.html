<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>经典贪吃蛇 - 网页版</title>
    <style>
        /* CSS 样式部分：负责界面美化 */
        body {
            background-color: #2c3e50;
            color: white;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            overflow: hidden; /* 防止按方向键时页面滚动 */
        }

        h1 {
            margin-top: 0;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }

        .game-container {
            position: relative;
            box-shadow: 0 10px 20px rgba(0,0,0,0.5);
            border-radius: 4px;
            overflow: hidden;
        }

        canvas {
            background-color: #000;
            display: block;
            border: 4px solid #34495e;
        }

        .score-board {
            margin-bottom: 10px;
            font-size: 1.5rem;
            display: flex;
            gap: 20px;
        }

        /* 游戏结束/开始的覆盖层 */
        .overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.85);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 10;
        }

        .overlay h2 {
            font-size: 3rem;
            margin: 0 0 20px 0;
            color: #e74c3c;
        }

        .hidden {
            display: none !important;
        }

        button {
            padding: 12px 30px;
            font-size: 1.2rem;
            background-color: #27ae60;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background 0.3s;
            outline: none;
        }

        button:hover {
            background-color: #2ecc71;
        }

        .controls-hint {
            margin-top: 15px;
            font-size: 0.9rem;
            color: #bdc3c7;
        }
    </style>
</head>
<body>

    <h1>贪吃蛇大作战</h1>

    <div class="score-board">
        <span>分数: <span id="score">0</span></span>
        <span>最高分: <span id="highScore">0</span></span>
    </div>

    <div class="game-container">
        <canvas id="gameCanvas" width="400" height="400"></canvas>
        
        <!-- 开始界面 -->
        <div id="startScreen" class="overlay">
            <button onclick="startGame()">开始游戏</button>
            <p class="controls-hint">使用方向键或 WASD 控制移动</p>
        </div>

        <!-- 游戏结束界面 -->
        <div id="gameOverScreen" class="overlay hidden">
            <h2>游戏结束!</h2>
            <p style="font-size: 1.5rem; margin-bottom: 20px;">最终得分: <span id="finalScore">0</span></p>
            <button onclick="startGame()">再玩一次</button>
        </div>
    </div>

    <script>
        /** JavaScript 逻辑部分 **/

        // 1. 获取DOM元素
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const scoreEl = document.getElementById('score');
        const highScoreEl = document.getElementById('highScore');
        const finalScoreEl = document.getElementById('finalScore');
        const startScreen = document.getElementById('startScreen');
        const gameOverScreen = document.getElementById('gameOverScreen');

        // 2. 游戏配置参数
        const TILE_SIZE = 20; // 每个格子的大小
        const TILE_COUNT = canvas.width / TILE_SIZE; // 格子数量 (20x20)
        const GAME_SPEED = 100; // 刷新速度(毫秒)，越小越快

        // 3. 游戏变量
        let score = 0;
        let highScore = localStorage.getItem('snakeHighScore') || 0;
        let snake = [];
        let apple = { x: 5, y: 5 };
        let dx = 0; // X轴速度
        let dy = 0; // Y轴速度
        let gameInterval;
        let isGameRunning = false;
        let nextDirection = { x: 0, y: 0 }; // 缓存下一次按键，防止快速按键bug

        // 初始化最高分显示
        highScoreEl.innerText = highScore;

        // 4. 核心功能函数

        // 开始游戏
        function startGame() {
            // 重置状态
            snake = [{ x: 10, y: 10 }, { x: 10, y: 11 }, { x: 10, y: 12 }]; // 初始蛇身
            score = 0;
            dx = 0;
            dy = -1; // 初始向上走
            nextDirection = { x: 0, y: -1 };
            scoreEl.innerText = score;
            
            // 隐藏界面层
            startScreen.classList.add('hidden');
            gameOverScreen.classList.add('hidden');
            
            isGameRunning = true;
            generateApple();

            // 清除旧的循环并开始新的循环
            if (gameInterval) clearInterval(gameInterval);
            gameInterval = setInterval(gameLoop, GAME_SPEED);
        }

        // 游戏主循环 (每一帧执行一次)
        function gameLoop() {
            if (!isGameRunning) return;

            update();
            draw();
        }

        // 更新逻辑 (移动、碰撞检测)
        function update() {
            // 应用缓存的方向（防止一帧内多次按键导致掉头自杀）
            // 例如：当前向右，快速按上再左，如果不缓存，蛇会直接向左撞死自己
            if (nextDirection.x !== 0 || nextDirection.y !== 0) {
                dx = nextDirection.x;
                dy = nextDirection.y;
            }

            // 计算新的头部位置
            const head = { x: snake[0].x + dx, y: snake[0].y + dy };

            // 1. 检查撞墙
            if (head.x < 0 || head.x >= TILE_COUNT || head.y < 0 || head.y >= TILE_COUNT) {
                gameOver();
                return;
            }

            // 2. 检查撞自己
            for (let i = 0; i < snake.length; i++) {
                if (head.x === snake[i].x && head.y === snake[i].y) {
                    gameOver();
                    return;
                }
            }

            // 将新头加入数组最前面
            snake.unshift(head);

            // 3. 检查吃苹果
            if (head.x === apple.x && head.y === apple.y) {
                score++;
                scoreEl.innerText = score;
                generateApple();
                // 吃苹果时不移除尾部，蛇身变长
            } else {
                // 没吃到苹果，移除尾部，保持移动
                snake.pop();
            }
        }

        // 渲染画面
        function draw() {
            // 清空画布
            ctx.fillStyle = 'black';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            // 画网格线 (可选，增加复古感)
            /*
            ctx.strokeStyle = '#111';
            for(let i=0; i<TILE_COUNT; i++) {
                ctx.beginPath();
                ctx.moveTo(i*TILE_SIZE, 0);
                ctx.lineTo(i*TILE_SIZE, canvas.height);
                ctx.stroke();
                ctx.beginPath();
                ctx.moveTo(0, i*TILE_SIZE);
                ctx.lineTo(canvas.width, i*TILE_SIZE);
                ctx.stroke();
            }
            */

            // 画苹果
            ctx.fillStyle = '#e74c3c'; // 红色
            ctx.shadowBlur = 10;
            ctx.shadowColor = "red";
            // 稍微画圆一点
            ctx.beginPath();
            ctx.arc(
                apple.x * TILE_SIZE + TILE_SIZE / 2, 
                apple.y * TILE_SIZE + TILE_SIZE / 2, 
                TILE_SIZE / 2 - 2, 
                0, 
                Math.PI * 2
            );
            ctx.fill();
            ctx.shadowBlur = 0; // 重置阴影

            // 画蛇
            ctx.fillStyle = '#2ecc71'; // 绿色
            snake.forEach((part, index) => {
                // 蛇头颜色稍微不同
                if (index === 0) ctx.fillStyle = '#27ae60';
                else ctx.fillStyle = '#2ecc71';

                ctx.fillRect(part.x * TILE_SIZE + 1, part.y * TILE_SIZE + 1, TILE_SIZE - 2, TILE_SIZE - 2);
            });
        }

        // 生成随机苹果
        function generateApple() {
            while (true) {
                let newApple = {
                    x: Math.floor(Math.random() * TILE_COUNT),
                    y: Math.floor(Math.random() * TILE_COUNT)
                };
                
                // 确保苹果没有生成在蛇身上
                let collision = false;
                for (let part of snake) {
                    if (part.x === newApple.x && part.y === newApple.y) {
                        collision = true;
                        break;
                    }
                }
                
                if (!collision) {
                    apple = newApple;
                    break;
                }
            }
        }

        // 游戏结束逻辑
        function gameOver() {
            isGameRunning = false;
            clearInterval(gameInterval);
            
            // 更新最高分
            if (score > highScore) {
                highScore = score;
                localStorage.setItem('snakeHighScore', highScore);
                highScoreEl.innerText = highScore;
            }

            finalScoreEl.innerText = score;
            gameOverScreen.classList.remove('hidden');
        }

        // 5. 键盘监听
        document.addEventListener('keydown', changeDirection);

        function changeDirection(event) {
            // 阻止方向键滚动页面
            if(["ArrowUp","ArrowDown","ArrowLeft","ArrowRight"].indexOf(event.code) > -1) {
                event.preventDefault();
            }

            // 这里的判断逻辑是：如果当前正在向右走(dx=1)，则不能按左键；
            // 我们检查 nextDirection 而不是 dx/dy，是为了处理快速连续按键的情况
            
            // 确定当前实际上正在移动的方向（由上一次已经处理的逻辑决定）
            // 但为了简单和响应快，通常对比当前速度
            const LEFT_KEY = 37;
            const RIGHT_KEY = 39;
            const UP_KEY = 38;
            const DOWN_KEY = 40;
            const W_KEY = 87;
            const A_KEY = 65;
            const S_KEY = 83;
            const D_KEY = 68;

            const keyPressed = event.keyCode;
            
            // 当前是否向上或向下
            const goingUp = dy === -1;
            const goingDown = dy === 1;
            const goingRight = dx === 1;
            const goingLeft = dx === -1;

            if ((keyPressed === LEFT_KEY || keyPressed === A_KEY) && !goingRight) {
                nextDirection = { x: -1, y: 0 };
            }
            if ((keyPressed === UP_KEY || keyPressed === W_KEY) && !goingDown) {
                nextDirection = { x: 0, y: -1 };
            }
            if ((keyPressed === RIGHT_KEY || keyPressed === D_KEY) && !goingLeft) {
                nextDirection = { x: 1, y: 0 };
            }
            if ((keyPressed === DOWN_KEY || keyPressed === S_KEY) && !goingUp) {
                nextDirection = { x: 0, y: 1 };
            }
        }
    </script>
</body>
</html>