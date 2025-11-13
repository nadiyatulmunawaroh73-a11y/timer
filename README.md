# timer
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Timer Sederhana</title>
    
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }
        .timer-container {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            text-align: center;
        }
        #display {
            font-size: 4em;
            margin-bottom: 20px;
            color: #333;
        }
        input[type="number"] {
            padding: 10px;
            font-size: 1.2em;
            width: 150px;
            text-align: center;
            border: 1px solid #ccc;
            border-radius: 5px;
            margin-bottom: 15px;
        }
        button {
            padding: 10px 20px;
            font-size: 1.1em;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            margin: 5px;
            transition: background-color 0.3s;
        }
        #startBtn {
            background-color: #4CAF50;
            color: white;
        }
        #startBtn:hover {
            background-color: #45a049;
        }
        #stopBtn {
            background-color: #f44336;
            color: white;
        }
        #stopBtn:hover {
            background-color: #da190b;
        }
    </style>
</head>

<body>

    <div class="timer-container">
        
        <h1>Timer Hitung Mundur</h1>
        
        <input type="number" id="duration" placeholder="Masukkan detik (mis: 60)" value="60">
        
        <div id="display">01:00</div> 
        
        <button id="startBtn">Mulai Timer</button>
        <button id="stopBtn">Stop</button>
        
    </div>

    <script>
        let timerInterval;
        let timeRemaining;
        const display = document.getElementById('display');
        const durationInput = document.getElementById('duration');
        const startBtn = document.getElementById('startBtn');
        const stopBtn = document.getElementById('stopBtn');

        // Fungsi untuk format waktu dari detik ke MM:SS
        function formatTime(totalSeconds) {
            const minutes = Math.floor(totalSeconds / 60);
            const seconds = totalSeconds % 60;
            // PadStart memastikan format dua digit (misalnya: 5 -> 05)
            const formattedMinutes = String(minutes).padStart(2, '0');
            const formattedSeconds = String(seconds).padStart(2, '0');
            return `${formattedMinutes}:${formattedSeconds}`;
        }

        // Fungsi utama untuk memulai hitungan mundur
        function startTimer() {
            // Mengambil durasi dari input dan mengubahnya menjadi bilangan bulat
            const duration = parseInt(durationInput.value);
            if (isNaN(duration) || duration <= 0) {
                alert("Mohon masukkan durasi dalam detik yang valid.");
                return;
            }

            // Hentikan timer sebelumnya jika ada
            clearInterval(timerInterval);
            
            timeRemaining = duration;
            display.textContent = formatTime(timeRemaining);
            
            // Logika inti: menjalankan fungsi updateTimer setiap 1000 milidetik (1 detik)
            timerInterval = setInterval(updateTimer, 1000);
        }

        // Fungsi untuk memperbarui tampilan waktu
        function updateTimer() {
            timeRemaining--;
            
            if (timeRemaining < 0) {
                clearInterval(timerInterval);
                display.textContent = "Waktu Habis!";
                alert("Waktu Habis!");
                return;
            }
            
            display.textContent = formatTime(timeRemaining);
        }

        // Fungsi untuk menghentikan timer
        function stopTimer() {
            clearInterval(timerInterval);
        }

        // Event Listeners: Menghubungkan tombol dengan fungsi
        startBtn.addEventListener('click', startTimer);
        stopBtn.addEventListener('click', stopTimer);
        
        // Inisialisasi tampilan awal
        display.textContent = formatTime(parseInt(durationInput.value));

    </script>
</body>
</html>
