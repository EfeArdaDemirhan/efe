<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Soru-Cevap Oyunu (Efe❤️Yağmur)</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            background-color: #f4f4f9;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            color: #333;
            transition: background-color 0.5s, background-image 1s ease-in-out; 
            padding: 20px;
            position: relative; 
            overflow: hidden; 
            
            background-size: cover; 
            background-position: center; 
            background-attachment: fixed;
        }

        /* EVET dendiğinde aktif olacak arka plan sınıfı */
        body.yes-background {
            /* Lütfen resmin adının tam olarak 'background.jpg' olduğundan emin olun! */
            background-image: url('background.jpg'); 
            background-color: #000; 
        }

        body.yes-background::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.4); 
            z-index: 1; 
            transition: opacity 1s;
        }

        h1, button, .result, #fixed-text, .buttons {
            z-index: 2; 
            text-shadow: 0px 0px 8px rgba(0, 0, 0, 0.7), 0px 0px 3px rgba(0, 0, 0, 0.5); 
        }
        
        #fixed-text {
            position: fixed; 
            top: 10px;
            left: 15px;
            font-size: 1.5em;
            font-weight: bold;
            color: #e44d71; 
            z-index: 10; 
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.6);
        }

        h1 {
            color: #d9534f;
            margin-bottom: 30px;
            font-size: 2.5em; 
            text-align: center;
        }

        .buttons {
            display: flex;
            gap: 10px; 
            align-items: center;
            padding: 20px 0; 
        }

        button {
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease-in-out, font-size 0.1s linear;
            overflow: hidden; 
            text-overflow: clip; 
            white-space: nowrap; 
            padding: 10px 20px;
            z-index: 2; 
        }

        #yesBtn {
            background-color: #5cb85c;
            color: white;
            font-size: 1em; 
        }

        #noBtn {
            background-color: #f0ad4e;
            color: white;
            font-size: 1em; 
        }

        .result {
            margin-top: 40px;
            font-size: 2em;
            color: #2a6496;
            font-weight: bold;
            text-align: center;
            opacity: 0;
            transition: opacity 1s;
        }

        .heart-particle {
            position: absolute;
            font-size: 1.5em;
            color: #e44d71; 
            pointer-events: none; 
            opacity: 0;
            animation: burst 1.5s ease-out forwards;
        }

        @keyframes burst {
            0% {
                transform: translate(0, 0) scale(1);
                opacity: 1;
            }
            100% {
                transform: translate(var(--end-x), var(--end-y)) scale(0);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    
    <div id="fixed-text">Efe❤️Yağmur</div>

    <h1 id="questionText">Beni seviyor musun?</h1>

    <div class="buttons">
        <button id="yesBtn">Evet</button>
        <button id="noBtn">Hayır</button>
    </div>

    <p class="result" id="resultText"></p>

    <script>
        const yesBtn = document.getElementById('yesBtn');
        const noBtn = document.getElementById('noBtn');
        const questionText = document.getElementById('questionText');
        const resultText = document.getElementById('resultText');
        const fixedText = document.getElementById('fixed-text');
        const body = document.body;

        let noSize = 1; 
        let yesSize = 1; 
        let clickCount = 0;

        const noTexts = [
            "Emin misin?", "Lütfen tekrar düşün", "Ama ben seni çok seviyorum!", 
            "Gerçekten mi? Kalbim kırılacak...", "İmkansız. Yanlış butona bastın.",
            "Bu artık bir seçenek değil.", "Tekrar dene.", "Yasak buton!", 
            "Gözden kayboluyorum...", "...", "Bitti :("
        ];

        const yesTexts = [
            "Evet", "Evet!!", "Kesinlikle Evet!", "Sonsuza Kadar Evet", 
            "HAYATIMIN EVET'İ!", "Tüm Kalbimle EVET!", "Tek Seçenek EVET!", 
            "Müthiş Bir EVET!", "SÜPER EVET!", "HARİKA EVET!", 
            "MÜKEMMEL EVET!!!" 
        ];
        
        const questionTexts = [
            "Beni seviyor musun?", "Cevabın ne olursa olsun, bir şans daha verelim mi?",
            "Gönlün 'Hayır' demeye el veriyor mu?", "Unutma, her zaman bir 'Evet' seçeneği var.",
            "Hadi ama, kimseyi kırmayalım :)", "Sence de 'Evet' demenin zamanı gelmedi mi?",
            "O küçük butona dokunma.", "Tek seçenek mi var?",
            "Artık sadece bir 'Evet' var.", "Son Kararını Ver.", "..."
        ];

        function createHeartExplosion(centerX, centerY) {
            const numParticles = 20; 
            const radius = 100; 

            for (let i = 0; i < numParticles; i++) {
                const heart = document.createElement('span');
                heart.textContent = '❤️';
                heart.classList.add('heart-particle');

                const angle = Math.random() * 2 * Math.PI;
                const distance = Math.random() * radius;

                const endX = Math.cos(angle) * distance;
                const endY = Math.sin(angle) * distance;

                heart.style.left = `${centerX}px`;
                heart.style.top = `${centerY}px`;
                
                heart.style.setProperty('--end-x', `${endX}px`);
                heart.style.setProperty('--end-y', `${endY}px`);

                body.appendChild(heart);

                heart.addEventListener('animationend', () => {
                    heart.remove();
                });
            }
        }


        noBtn.addEventListener('click', () => {
            if (clickCount < noTexts.length) { 
                clickCount++;

                noSize = Math.max(0, noSize - 0.3); 
                yesSize += 0.3;
                
                noBtn.style.fontSize = `${noSize}em`;
                yesBtn.style.fontSize = `${yesSize}em`;

                let yesPadding = 10 + (yesSize * 2);
                yesBtn.style.padding = `${Math.min(25, yesPadding)}px ${Math.min(50, yesPadding * 2)}px`; 
                
                noBtn.textContent = noTexts[clickCount - 1] || "";
                yesBtn.textContent = yesTexts[Math.min(clickCount - 1, yesTexts.length - 1)];
                questionText.textContent = questionTexts[Math.min(clickCount - 1, questionTexts.length - 1)];
                
                if (noSize <= 0.1) {
                    noBtn.style.display = 'none';
                    questionText.textContent = "Gördüğün gibi, 'Hayır' butonu kayboldu. Tek seçenek 'Evet'!";
                    document.body.style.backgroundColor = '#d9edf7';
                }

            }
        });

        yesBtn.addEventListener('click', () => {
            const rect = yesBtn.getBoundingClientRect();
            const centerX = rect.left + rect.width / 2;
            const centerY = rect.top + rect.height / 2;

            createHeartExplosion(centerX, centerY);
            
            questionText.textContent = "BİLİYORDUM! Ben de seni çok seviyorum! ❤️";
            resultText.textContent = "EVET! Seni Seviyorum! 🥰";
            resultText.style.opacity = 1; 
            
            body.classList.add('yes-background');
            questionText.style.color = '#fff';
            resultText.style.color = '#ffc107';
            fixedText.style.color = '#fff';
            
            yesBtn.style.backgroundColor = 'rgba(92, 184, 92, 0.8)';
            noBtn.style.display = 'none'; 
            yesBtn.style.fontSize = '3em'; 
            yesBtn.textContent = "Mükemmel!";
            yesBtn.disabled = true; 
        });
        
    </script>

</body>
</html>
