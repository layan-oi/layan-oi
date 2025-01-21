<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>اختيار الفائز</title>
    <style>
        body {
            text-align: center;
            direction: rtl;
            font-family: Arial, sans-serif;
            background-color: #ffffff;
            color: #333;
            margin: 0;
            padding: 0;
        }

        header {
            background-color: #FA9C28;
            padding: 20px;
        }

        header h1 {
            color: white;
            margin: 0;
            font-size: 28px;
        }

        button {
            background-color: #FA9C28;
            color: white;
            border: none;
            padding: 15px 30px;
            font-size: 20px;
            font-weight: bold;
            border-radius: 10px;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.2s;
        }

        button:hover {
            background-color: #F87C1A;
            transform: scale(1.1);
        }

        #winner {
            font-size: 48px;
            font-weight: bold;
            color: #FA9C28;
            margin-top: 20px;
            background-color: #FFFFFF;
            padding: 20px;
            border: 3px solid #FA9C28;
            border-radius: 10px;
            display: inline-block;
            animation: fadeIn 1s ease-in-out, pulse 1.5s infinite;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        @keyframes pulse {
            0%, 100% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.1);
            }
        }

        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <header>
        <h1>اختيار الفائز</h1>
    </header>

    <textarea id="names" placeholder="أدخل أسماء العملاء هنا، كل اسم في سطر جديد" style="width: 80%; height: 150px; margin-top: 20px; padding: 10px; font-size: 16px;"></textarea>
    <br>
    <button onclick="drawWinner()">إبدأ السحب</button>
    <h2 id="winner" class="hidden"></h2>

    <script>
        function drawWinner() {
            const namesTextarea = document.getElementById("names");
            const winnerElement = document.getElementById("winner");
            const names = namesTextarea.value.trim().split("\n").filter(name => name.trim() !== "");

            if (names.length > 0) {
                let currentIndex = 0;
                winnerElement.classList.add("hidden");

                const interval = setInterval(() => {
                    winnerElement.innerText = names[currentIndex];
                    winnerElement.classList.remove("hidden");
                    currentIndex = (currentIndex + 1) % names.length;
                }, 100);

                setTimeout(() => {
                    clearInterval(interval);
                    const winner = names[Math.floor(Math.random() * names.length)];
                    winnerElement.innerText = `🎉 الفائز هو: ${winner} 🎉`;
                    winnerElement.style.color = "#FA9C28";
                    winnerElement.style.animation = "pulse 1.5s infinite";
                }, 3000);
            } else {
                alert("يرجى إدخال أسماء العملاء!");
            }
        }
    </script>
</body>
</html>
