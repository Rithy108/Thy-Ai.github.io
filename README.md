<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cyberpunk Neon Clock</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Courier New', Courier, monospace;
        }

        body {
            background: #0a0a12;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            perspective: 1000px;
        }

        /* Background Grid Lines */
        body::before {
            content: '';
            position: absolute;
            width: 200%;
            height: 200%;
            background-image: 
                linear-gradient(rgba(0, 242, 254, 0.05) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 242, 254, 0.05) 1px, transparent 1px);
            background-size: 40px 40px;
            transform: rotateX(60deg);
            top: -50%;
            z-index: 1;
            animation: gridMove 20s linear infinite;
        }

        @keyframes gridMove {
            0% { background-position: 0 0; }
            100% { background-position: 0 800px; }
        }

        /* Clock Container */
        .clock-container {
            position: relative;
            z-index: 2;
            background: rgba(10, 10, 18, 0.85);
            padding: 40px 60px;
            border-radius: 16px;
            border: 2px solid #00f2fe;
            box-shadow: 0 0 20px rgba(0, 242, 254, 0.2),
                        inset 0 0 20px rgba(0, 242, 254, 0.2);
            backdrop-filter: blur(10px);
            transition: transform 0.1s ease;
            transform-style: preserve-3d;
        }

        .clock-container:hover {
            box-shadow: 0 0 35px rgba(255, 0, 128, 0.4),
                        inset 0 0 20px rgba(255, 0, 128, 0.2);
            border-color: #ff0080;
        }

        /* Time Display */
        .time {
            font-size: 5rem;
            font-weight: bold;
            color: #fff;
            text-shadow: 0 0 10px #00f2fe,
                         0 0 20px #00f2fe,
                         0 0 40px #00f2fe;
            letter-spacing: 4px;
            transition: text-shadow 0.5s ease, color 0.5s;
        }

        .clock-container:hover .time {
            color: #fff;
            text-shadow: 0 0 10px #ff0080,
                         0 0 20px #ff0080,
                         0 0 40px #ff0080;
        }

        /* Date Display */
        .date {
            text-align: center;
            margin-top: 15px;
            font-size: 1.2rem;
            color: #00f2fe;
            text-transform: uppercase;
            letter-spacing: 6px;
            opacity: 0.8;
        }

        .clock-container:hover .date {
            color: #ff0080;
        }

        /* Cyberpunk Tag */
        .tag {
            position: absolute;
            top: -12px;
            left: 30px;
            background: #ff0080;
            color: #fff;
            padding: 2px 10px;
            font-size: 0.75rem;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 2px;
            box-shadow: 0 0 10px #ff0080;
        }

        .clock-container:hover .tag {
            background: #00f2fe;
            box-shadow: 0 0 10px #00f2fe;
        }
    </style>
</head>
<body>

    <div class="clock-container" id="clock">
        <div class="tag">System Status: Online</div>
        <div class="time" id="time-display">00:00:00</div>
        <div class="date" id="date-display">LOADING...</div>
    </div>

    <script>
        // 1. មុខងារដំណើរការម៉ោង និងថ្ងៃខែ
        function updateClock() {
            const now = new Date();
            
            // ទាញយកម៉ោង នាទី វិនាទី
            let hours = String(now.getHours()).padStart(2, '0');
            let minutes = String(now.getMinutes()).padStart(2, '0');
            let seconds = String(now.getSeconds()).padStart(2, '0');
            
            document.getElementById('time-display').textContent = `${hours}:${minutes}:${seconds}`;
            
            // ទាញយកថ្ងៃខែឆ្នាំ
            const options = { year: 'numeric', month: 'short', day: 'numeric' };
            document.getElementById('date-display').textContent = now.toLocaleDateString('en-US', options);
        }

        setInterval(updateClock, 1000);
        updateClock(); // ហៅឱ្យដើរភ្លាមៗពេលបើក Page

        // 2. មុខងារធ្វើឱ្យប្រអប់ម៉ោងមានចលនា 3D តាមកូអរដោនេម៉ៅស៍ (Mouse Move Effect)
        const clock = document.getElementById('clock');
        document.addEventListener('mousemove', (e) => {
            const xAxis = (window.innerWidth / 2 - e.pageX) / 25;
            const yAxis = (window.innerHeight / 2 - e.pageY) / 25;
            clock.style.transform = `rotateY(${xAxis}deg) rotateX(${yAxis}deg)`;
        });

        // ពេលដកម៉ៅស៍ចេញ ឱ្យវាត្រឡប់មកសភាពដើមវិញ
        document.addEventListener('mouseleave', () => {
            clock.style.transform = `rotateY(0deg) rotateX(0deg)`;
        });
    </script>
</body>
</html>
