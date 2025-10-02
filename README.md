<!DOCTYPE html>
<html lang="kk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Тарихи карталар</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #1a2a6c, #2a3a7c);
            color: #f0f0f0;
            line-height: 1.6;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 15px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
        }

        h1 {
            font-size: 2.8rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
            background: linear-gradient(to right, #ffd700, #ffec8b);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .subtitle {
            font-size: 1.3rem;
            opacity: 0.9;
            max-width: 800px;
            margin: 0 auto;
        }

        .main-content {
            display: flex;
            flex-wrap: wrap;
            gap: 25px;
            margin-bottom: 30px;
        }

        .map-container {
            flex: 1;
            min-width: 300px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
            position: relative;
            overflow: hidden;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .controls {
            width: 320px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .map-selector {
            margin-bottom: 25px;
        }

        .map-selector h3 {
            margin-bottom: 15px;
            color: #ffd700;
            font-size: 1.4rem;
            text-align: center;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
            padding-bottom: 10px;
        }

        .map-buttons {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .map-btn {
            background: rgba(0, 0, 0, 0.3);
            color: #f0f0f0;
            border: none;
            padding: 12px;
            border-radius: 10px;
            cursor: pointer;
            font-size: 1rem;
            transition: all 0.3s ease;
            text-align: left;
            border-left: 4px solid transparent;
        }

        .map-btn:hover {
            background: rgba(255, 215, 0, 0.2);
            transform: translateX(3px);
        }

        .map-btn.active {
            background: rgba(255, 215, 0, 0.3);
            border-left: 4px solid #ffd700;
            font-weight: bold;
        }

        .control-group {
            margin-bottom: 25px;
        }

        .control-group h3 {
            margin-bottom: 15px;
            color: #ffd700;
            font-size: 1.3rem;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
            padding-bottom: 8px;
        }

        .tool-buttons {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }

        .tool-btn {
            flex: 1;
            background: rgba(0, 0, 0, 0.3);
            color: #f0f0f0;
            border: none;
            padding: 10px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            transition: all 0.3s ease;
        }

        .tool-btn:hover {
            background: rgba(255, 215, 0, 0.2);
        }

        .tool-btn.active {
            background: rgba(255, 215, 0, 0.3);
            font-weight: bold;
        }

        .color-options {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 15px;
        }

        .color-option {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            cursor: pointer;
            border: 2px solid transparent;
            transition: transform 0.2s;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        }

        .color-option:hover {
            transform: scale(1.15);
        }

        .color-option.active {
            border-color: white;
            transform: scale(1.15);
        }

        .eraser {
            background: #ff4d4d;
            position: relative;
        }

        .eraser::after {
            content: "✕";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: white;
            font-weight: bold;
        }

        .brush-size {
            width: 100%;
            margin: 15px 0;
            accent-color: #ffd700;
        }

        .size-value {
            text-align: center;
            font-size: 1.1rem;
            margin-top: 5px;
        }

        button {
            background: linear-gradient(135deg, #ffd700, #ffec8b);
            color: #1a2a6c;
            border: none;
            padding: 14px;
            border-radius: 10px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: bold;
            transition: all 0.3s ease;
            width: 100%;
            margin-bottom: 12px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }

        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3);
        }

        .history-buttons {
            display: flex;
            gap: 10px;
        }

        .history-buttons button {
            flex: 1;
        }

        #mapCanvas {
            width: 100%;
            height: 650px;
            background-color: #2a4a7c;
            border-radius: 10px;
            cursor: crosshair;
            display: block;
            box-shadow: inset 0 0 20px rgba(0, 0, 0, 0.5);
        }

        .map-title {
            text-align: center;
            margin-bottom: 15px;
            font-size: 1.6rem;
            color: #ffd700;
            text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.5);
        }

        .loading {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100%;
            font-size: 1.2rem;
            color: #ffd700;
            gap: 15px;
        }

        .loading-progress {
            width: 80%;
            height: 10px;
            background: rgba(255,255,255,0.2);
            border-radius: 5px;
            overflow: hidden;
        }

        .loading-bar {
            height: 100%;
            background: #ffd700;
            width: 0%;
            transition: width 0.3s ease;
        }

        .error-message {
            background: rgba(255,0,0,0.2);
            padding: 15px;
            border-radius: 10px;
            margin-top: 15px;
            text-align: center;
            border: 1px solid rgba(255,0,0,0.5);
        }

        .reload-btn {
            background: linear-gradient(135deg, #ff6b6b, #ff8e8e);
            margin-top: 10px;
        }

        footer {
            text-align: center;
            margin-top: 30px;
            padding: 20px;
            color: rgba(255, 255, 255, 0.7);
            font-size: 1rem;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
        }

        @media (max-width: 1100px) {
            .main-content {
                flex-direction: column;
            }
            
            .controls {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Тарихи карталар</h1>
            <p class="subtitle">Сізге қажет тарихи карталар сызу мүмкіндігімен</p>
        </header>
        
        <div class="main-content">
            <div class="map-container">
                <div class="map-title" id="mapTitle">Карта жүктелуде...</div>
                <canvas id="mapCanvas"></canvas>
                <div id="loadingMessage" class="loading">
                    <div>Карталар жүктелуде, күтіңіз...</div>
                    <div class="loading-progress">
                        <div class="loading-bar" id="loadingBar"></div>
                    </div>
                    <div id="loadedCount">0/8 карта жүктелді</div>
                </div>
                <div id="errorMessage" class="error-message" style="display: none;">
                    <div>Кейбір карталар жүктелмеді</div>
                    <button class="reload-btn" id="reloadBtn">Қайта жүктеу</button>
                </div>
            </div>
            
            <div class="controls">
                <div class="map-selector">
                    <h3>Картаны таңдау</h3>
                    <div class="map-buttons">
                        <button class="map-btn active" data-map="1">1936 Еуропа</button>
                        <button class="map-btn" data-map="2">1938 Аншлюс</button>
                        <button class="map-btn" data-map="3">Мюнхен келісімі</button>
                        <button class="map-btn" data-map="4">Молотов-Риббентроп пактісі</button>
                        <button class="map-btn" data-map="5">1940 жыл Еуропа</button>
                        <button class="map-btn" data-map="6">Германияның КСРО-ға шабуылы</button>
                        <button class="map-btn" data-map="7">1945 жыл Германияның жеңілуі</button>
                        <button class="map-btn" data-map="8">Шығыс Азия 1936 жыл</button>
                    </div>
                </div>
                
                <div class="control-group">
                    <h3>Құралдар</h3>
                    <div class="tool-buttons">
                        <button class="tool-btn active" data-tool="brush">Қылқалам</button>
                        <button class="tool-btn eraser" data-tool="eraser">Өшіргіш</button>
                    </div>
                    
                    <div class="color-options">
                        <div class="color-option active" style="background-color: #ff0000;" data-color="#ff0000"></div>
                        <div class="color-option" style="background-color: #0000ff;" data-color="#0000ff"></div>
                        <div class="color-option" style="background-color: #00ff00;" data-color="#00ff00"></div>
                        <div class="color-option" style="background-color: #ffff00;" data-color="#ffff00"></div>
                        <div class="color-option" style="background-color: #ff00ff;" data-color="#ff00ff"></div>
                        <div class="color-option" style="background-color: #000000;" data-color="#000000"></div>
                    </div>
                    
                    <div>
                        <h4>Қылқалам өлшемі: <span id="brushSizeValue">5</span>px</h4>
                        <input type="range" min="1" max="20" value="5" class="brush-size" id="brushSize">
                    </div>
                </div>
                
                <div class="control-group">
                    <h3>Әрекет тарихы</h3>
                    <div class="history-buttons">
                        <button id="undoBtn">← Артқа</button>
                        <button id="redoBtn">Алға →</button>
                    </div>
                </div>
                
                <div class="control-group">
                    <h3>Әрекеттер</h3>
                    <button id="clearBtn">Сызбаны тазалау</button>
                    <button id="saveBtn">Суретті сақтау</button>
                </div>
                
                <div class="control-group">
                    <h3>Нұсқаулық</h3>
                    <p>Тізімнен картаны таңдаңыз. Белгілер қосу үшін қылқаламды, жою үшін өшіргішті пайдаланыңыз. "Артқа" және "Алға" түймелері әрекеттерді болдырмауға және қайтаруға мүмкіндік береді.<br><br>Және бұл сайтты жасағандар: DeepSeek және Ахмет</p>
                </div>
            </div>
        </div>
        
        <footer>
            <p>Тарихи карталар © 2025</p>
        </footer>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const canvas = document.getElementById('mapCanvas');
            const ctx = canvas.getContext('2d');
            const colorOptions = document.querySelectorAll('.color-option');
            const brushSizeSlider = document.getElementById('brushSize');
            const brushSizeValue = document.getElementById('brushSizeValue');
            const clearBtn = document.getElementById('clearBtn');
            const saveBtn = document.getElementById('saveBtn');
            const undoBtn = document.getElementById('undoBtn');
            const redoBtn = document.getElementById('redoBtn');
            const mapButtons = document.querySelectorAll('.map-btn');
            const toolButtons = document.querySelectorAll('.tool-btn');
            const mapTitle = document.getElementById('mapTitle');
            const loadingMessage = document.getElementById('loadingMessage');
            const loadingBar = document.getElementById('loadingBar');
            const loadedCount = document.getElementById('loadedCount');
            const errorMessage = document.getElementById('errorMessage');
            const reloadBtn = document.getElementById('reloadBtn');
            
            // Установка размеров canvas
            function setCanvasSize() {
                const container = canvas.parentElement;
                canvas.width = container.clientWidth - 40;
                canvas.height = 650;
                if (mapsLoaded) {
                    drawCurrentMap();
                }
            }
            
            // Переменные для рисования
            let isDrawing = false;
            let lastX = 0;
            let lastY = 0;
            let currentColor = '#ff0000';
            let currentBrushSize = 5;
            let currentTool = 'brush';
            let currentMap = '1';
            let mapsLoaded = false;
            let hasErrors = false;
            
            // История действий для каждой карты
            const mapsHistory = {
                '1': { actions: [], redoActions: [] },
                '2': { actions: [], redoActions: [] },
                '3': { actions: [], redoActions: [] },
                '4': { actions: [], redoActions: [] },
                '5': { actions: [], redoActions: [] },
                '6': { actions: [], redoActions: [] },
                '7': { actions: [], redoActions: [] },
                '8': { actions: [], redoActions: [] }
            };
            
            // Названия карт
            const mapTitles = {
                '1': '1936 Еуропа',
                '2': '1938 Аншлюс',
                '3': 'Мюнхен келісімі',
                '4': 'Молотов-Риббентроп пактісі',
                '5': '1940 жыл Еуропа',
                '6': 'Германияның КСРО-ға шабуылы',
                '7': '1945 жыл Германияның жеңілуі',
                '8': 'Шығыс Азия 1936 жыл'
            };
            
            // Прямые ссылки на карты с прокси
            const mapUrls = {
                1: 'https://i.yapx.ru/ayIyB.png',
                2: 'https://i.yapx.ru/ayIwj.png',
                3: 'https://i.yapx.ru/ayIyJ.png',
                4: 'https://i.yapx.ru/ayIyH.jpg',
                5: 'https://i.yapx.ru/ayIwV.png',
                6: 'https://i.yapx.ru/ayIwT.png',
                7: 'https://i.yapx.ru/ayIwQ.png',
                8: 'https://i.yapx.ru/ayIw5.png'
            };
            
            // Изображения карт
            const mapImages = {};
            let loadedImagesCount = 0;
            const totalImages = 8;
            
            // Функция для создания изображения с таймаутом
            function loadImageWithTimeout(url, timeout = 10000) {
                return new Promise((resolve, reject) => {
                    const img = new Image();
                    const timer = setTimeout(() => {
                        reject(new Error('Таймаут'));
                    }, timeout);
                    
                    img.onload = function() {
                        clearTimeout(timer);
                        resolve(img);
                    };
                    
                    img.onerror = function() {
                        clearTimeout(timer);
                        reject(new Error('Жүктеу сәтсіз аяқталды'));
                    };
                    
                    img.src = url;
                });
            }
            
            // Загрузка изображений карт
            async function loadMapImages() {
                loadedImagesCount = 0;
                hasErrors = false;
                loadingBar.style.width = '0%';
                loadedCount.textContent = '0/8 карта жүктелді';
                errorMessage.style.display = 'none';
                
                for (let i = 1; i <= totalImages; i++) {
                    try {
                        mapImages[i] = await loadImageWithTimeout(mapUrls[i], 15000);
                        loadedImagesCount++;
                        updateProgress();
                        
                        if (loadedImagesCount === totalImages) {
                            finishLoading();
                        }
                    } catch (error) {
                        console.error(`Карта ${i} жүктелмеді:`, error);
                        mapImages[i] = null;
                        loadedImagesCount++;
                        hasErrors = true;
                        updateProgress();
                        
                        if (loadedImagesCount === totalImages) {
                            finishLoading();
                        }
                    }
                }
            }
            
            function updateProgress() {
                const progress = (loadedImagesCount / totalImages) * 100;
                loadingBar.style.width = progress + '%';
                loadedCount.textContent = `${loadedImagesCount}/8 карта жүктелді`;
            }
            
            function finishLoading() {
                mapsLoaded = true;
                
                if (hasErrors) {
                    errorMessage.style.display = 'block';
                } else {
                    loadingMessage.style.display = 'none';
                }
                
                mapTitle.textContent = mapTitles[currentMap];
                drawCurrentMap();
            }
            
            // Инициализация canvas
            setCanvasSize();
            window.addEventListener('resize', setCanvasSize);
            loadMapImages();
            
            // Обработчики событий для рисования
            canvas.addEventListener('mousedown', startDrawing);
            canvas.addEventListener('mousemove', draw);
            canvas.addEventListener('mouseup', stopDrawing);
            canvas.addEventListener('mouseout', stopDrawing);
            
            // Обработчики для касаний (мобильные устройства)
            canvas.addEventListener('touchstart', handleTouchStart);
            canvas.addEventListener('touchmove', handleTouchMove);
            canvas.addEventListener('touchend', stopDrawing);
            
            function handleTouchStart(e) {
                e.preventDefault();
                const touch = e.touches[0];
                const mouseEvent = new MouseEvent('mousedown', {
                    clientX: touch.clientX,
                    clientY: touch.clientY
                });
                canvas.dispatchEvent(mouseEvent);
            }
            
            function handleTouchMove(e) {
                e.preventDefault();
                const touch = e.touches[0];
                const mouseEvent = new MouseEvent('mousemove', {
                    clientX: touch.clientX,
                    clientY: touch.clientY
                });
                canvas.dispatchEvent(mouseEvent);
            }
            
            function startDrawing(e) {
                if (!mapsLoaded) return;
                
                isDrawing = true;
                [lastX, lastY] = getMousePos(canvas, e);
                
                // Начинаем новое действие в истории
                mapsHistory[currentMap].redoActions = [];
                mapsHistory[currentMap].actions.push({
                    type: 'path',
                    points: [[lastX, lastY]],
                    color: currentTool === 'eraser' ? '#2a4a7c' : currentColor,
                    width: currentBrushSize,
                    tool: currentTool
                });
            }
            
            function draw(e) {
                if (!isDrawing || !mapsLoaded) return;
                
                const [x, y] = getMousePos(canvas, e);
                
                ctx.beginPath();
                ctx.moveTo(lastX, lastY);
                ctx.lineTo(x, y);
                ctx.strokeStyle = currentTool === 'eraser' ? '#2a4a7c' : currentColor;
                ctx.lineWidth = currentBrushSize;
                ctx.lineCap = 'round';
                ctx.lineJoin = 'round';
                ctx.stroke();
                
                if (mapsHistory[currentMap].actions.length > 0) {
                    const currentAction = mapsHistory[currentMap].actions[mapsHistory[currentMap].actions.length - 1];
                    currentAction.points.push([x, y]);
                }
                
                [lastX, lastY] = [x, y];
            }
            
            function stopDrawing() {
                isDrawing = false;
            }
            
            function getMousePos(canvas, evt) {
                const rect = canvas.getBoundingClientRect();
                let clientX, clientY;
                
                if (evt.type.includes('touch')) {
                    clientX = evt.touches[0].clientX;
                    clientY = evt.touches[0].clientY;
                } else {
                    clientX = evt.clientX;
                    clientY = evt.clientY;
                }
                
                return [
                    clientX - rect.left,
                    clientY - rect.top
                ];
            }
            
            // Обработчики для элементов управления
            colorOptions.forEach(option => {
                option.addEventListener('click', function() {
                    colorOptions.forEach(opt => opt.classList.remove('active'));
                    this.classList.add('active');
                    currentColor = this.getAttribute('data-color');
                    currentTool = 'brush';
                    
                    toolButtons.forEach(btn => {
                        if (btn.getAttribute('data-tool') === 'brush') {
                            btn.classList.add('active');
                        } else {
                            btn.classList.remove('active');
                        }
                    });
                });
            });
            
            brushSizeSlider.addEventListener('input', function() {
                currentBrushSize = this.value;
                brushSizeValue.textContent = this.value;
            });
            
            toolButtons.forEach(button => {
                button.addEventListener('click', function() {
                    toolButtons.forEach(btn => btn.classList.remove('active'));
                    this.classList.add('active');
                    currentTool = this.getAttribute('data-tool');
                });
            });
            
            clearBtn.addEventListener('click', function() {
                if (confirm('Барлық сызбаны тазалағыңыз келе ме?')) {
                    mapsHistory[currentMap].actions = [];
                    mapsHistory[currentMap].redoActions = [];
                    drawCurrentMap();
                }
            });
            
            saveBtn.addEventListener('click', function() {
                const link = document.createElement('a');
                link.download = `tarihi_karta_${currentMap}.png`;
                link.href = canvas.toDataURL();
                link.click();
            });
            
            undoBtn.addEventListener('click', function() {
                const history = mapsHistory[currentMap];
                if (history.actions.length > 0) {
                    const lastAction = history.actions.pop();
                    history.redoActions.push(lastAction);
                    redrawCanvas();
                }
            });
            
            redoBtn.addEventListener('click', function() {
                const history = mapsHistory[currentMap];
                if (history.redoActions.length > 0) {
                    const nextAction = history.redoActions.pop();
                    history.actions.push(nextAction);
                    redrawCanvas();
                }
            });
            
            reloadBtn.addEventListener('click', function() {
                loadingMessage.style.display = 'flex';
                loadMapImages();
            });
            
            // Обработчики для переключения карт
            mapButtons.forEach(button => {
                button.addEventListener('click', function() {
                    if (!mapsLoaded) return;
                    
                    mapButtons.forEach(btn => btn.classList.remove('active'));
                    this.classList.add('active');
                    currentMap = this.getAttribute('data-map');
                    mapTitle.textContent = mapTitles[currentMap];
                    drawCurrentMap();
                });
            });
            
            // Функция отрисовки текущей карты
            function drawCurrentMap() {
                if (!mapsLoaded) return;
                
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                ctx.fillStyle = '#2a4a7c';
                ctx.fillRect(0, 0, canvas.width, canvas.height);
                
                const img = mapImages[currentMap];
                if (img && img.complete && img.naturalHeight !== 0) {
                    const scale = Math.min(canvas.width / img.width, canvas.height / img.height);
                    const x = (canvas.width - img.width * scale) / 2;
                    const y = (canvas.height - img.height * scale) / 2;
                    
                    ctx.drawImage(img, x, y, img.width * scale, img.height * scale);
                } else {
                    drawPlaceholderMap();
                }
                
                redrawCanvas();
            }
            
            function drawPlaceholderMap() {
                ctx.fillStyle = 'rgba(255, 255, 255, 0.1)';
                ctx.fillRect(0, 0, canvas.width, canvas.height);
                
                ctx.fillStyle = '#ffffff';
                ctx.font = '24px Arial';
                ctx.textAlign = 'center';
                ctx.fillText(mapTitles[currentMap], canvas.width / 2, canvas.height / 2 - 30);
                
                ctx.font = '16px Arial';
                ctx.fillText('Карта жүктелмеді', canvas.width / 2, canvas.height / 2 + 10);
            }
            
            function redrawCanvas() {
                const actions = mapsHistory[currentMap].actions;
                
                for (const action of actions) {
                    if (action.type === 'path' && action.points.length > 1) {
                        ctx.beginPath();
                        ctx.moveTo(action.points[0][0], action.points[0][1]);
                        
                        for (let i = 1; i < action.points.length; i++) {
                            ctx.lineTo(action.points[i][0], action.points[i][1]);
                        }
                        
                        ctx.strokeStyle = action.color;
                        ctx.lineWidth = action.width;
                        ctx.lineCap = 'round';
                        ctx.lineJoin = 'round';
                        ctx.stroke();
                    }
                }
            }
        });
    </script>
</body>
</html>
