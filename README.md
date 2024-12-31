<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>11-11-surprise-jar</title>
    <style>
        /* General body styles */
        body {
            font-family: 'Arial', sans-serif;
            background-color: #fce4ec; /* Soft pinkish hue for love vibes */
            color: #6a1b9a; /* Dark violet for text */
            text-align: center;
            margin: 0;
            padding: 0;
            transition: background-color 0.5s ease;
        }

        /* Header styles */
        header {
            background-color: #ff80ab;
            color: white;
            padding: 20px;
            font-size: 2em;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }

        /* Jar container */
        .jar-container {
            margin: 50px auto;
            width: 300px;
            position: relative;
        }

        /* Interactive jar */
        .jar {
            width: 100%;
            height: 300px;
            background: url('https://via.placeholder.com/300x300.png?text=11:11') no-repeat center;
            background-size: cover;
            border: 3px solid #ff80ab;
            border-radius: 50%;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
            cursor: pointer;
            position: relative;
            overflow: hidden;
            animation: jarBounce 1s infinite alternate;
        }

        @keyframes jarBounce {
            from {
                transform: translateY(0);
            }
            to {
                transform: translateY(-10px);
            }
        }

        /* Note pop-up */
        .note {
            display: none;
            position: absolute;
            top: 10%;
            left: 50%;
            transform: translateX(-50%) scale(0);
            background-color: #ffffff;
            color: #6a1b9a;
            padding: 20px;
            border: 2px solid #ff80ab;
            border-radius: 5px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            z-index: 10;
            animation: fadeIn 0.5s ease-in-out forwards;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateX(-50%) scale(0.5);
            }
            to {
                opacity: 1;
                transform: translateX(-50%) scale(1);
            }
        }

        /* Happy New Year Button */
        .new-year-container {
            margin: 20px auto;
        }

        .new-year-button {
            padding: 10px 20px;
            font-size: 1.2em;
            background-color: #ffcc00;
            color: #6a1b9a;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s ease;
        }

        .new-year-button:hover {
            transform: scale(1.1);
        }

        /* Fireworks Overlay */
        .fireworks-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1000;
            text-align: center;
        }

        .fireworks-message {
            position: relative;
            top: 50%;
            transform: translateY(-50%);
            font-size: 2em;
            color: #ffcc00;
            animation: fadeIn 1s ease-in-out;
        }

        /* Mood buttons */
        .mood-container {
            margin: 30px auto;
        }

        .mood-button {
            padding: 10px 20px;
            margin: 5px;
            border: none;
            background-color: #ff80ab;
            color: white;
            border-radius: 5px;
            cursor: pointer;
            transition: transform 0.2s ease;
        }

        .mood-button:active {
            transform: scale(0.95);
        }

        /* Sticky note */
        .sticky-note {
            position: absolute;
            bottom: 20%;
            right: 5%;
            padding: 10px;
            background-color: #fff9c4;
            font-size: 1.2em;
            color: #6a1b9a;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
            border-radius: 5px;
        }
    </style>
</head>
<body>

<header>This jar holds pieces of my heart for you. Whenever you need a memory, a smile, or a kind word, open it.</header>

<div class="sticky-note">I will take care of me for you, you take care of you for me...</div>

<div class="mood-container">
    <p>How are you feeling today?</p>
    <button class="mood-button" onclick="showNote('happy')">Happy</button>
    <button class="mood-button" onclick="showNote('sad')">Sad</button>
    <button class="mood-button" onclick="showNote('random')">Surprise Me</button>
</div>

<div class="jar-container">
    <div class="jar" onclick="showNote('random')"></div>
    <div class="note" id="note">
        <p id="note-content"></p>
        <button class="close-note" onclick="closeNote()">Close</button>
    </div>
</div>

<div class="new-year-container">
    <button class="new-year-button" onclick="showFireworks()">🎉 Happy New Year 🎉</button>
</div>

<div class="fireworks-overlay" id="fireworks">
    <p class="fireworks-message">🎆 Happy New Year, Walla! 🎆</p>
</div>

<script>
    const messages = {
        happy: [
            "I'm truly happy that you chose happy.",
            "Awww, my heart's happy today, I love you, honey.",
            "Mmmmmuaahhhhh.",
            "Seems like my prayers are paying off, huh? Keep smiling, love.",
            "You know it's midnight when I'm working on this web."
        ],
        sad: [
            "You know, love, it feels good even being under the same sky as you.",
            "C'mon sweetie, what happened? Chin up, miss.",
            "I wish I could be there to wipe those tears, but do me a favor, do it for me, love.",
            "Love, don't worry, everything's gonna be fine.",
            "I'm sorry, Walla, forgive me for not being there.",
            "Want me to make you sleep? C'mon cutie, close your beautiful eyes, let them rest a bit."
        ],
        random: [
            "I love you...",
            "Love... I'm missing you.",
            "You know, right now I'm probably on Namaz and praying for the love of my life.",
            "BOOO... silly right? I know, I know :)",
            "I'm still thinking about 11 kids ><",
            "Making this website reminds me of your birthday, remember how I made that silly video?",
            "You eating well, right babe?"
        ]
    };

    function showNote(mood) {
        const noteContainer = document.getElementById('note');
        const noteContent = document.getElementById('note-content');
        
        let selectedMessages = messages[mood];
        if (mood === 'random') {
            selectedMessages = Object.values(messages).flat();
        }

        const randomMessage = selectedMessages[Math.floor(Math.random() * selectedMessages.length)];
        noteContent.textContent = randomMessage;

        noteContainer.style.display = 'block';
    }

    function closeNote() {
        const noteContainer = document.getElementById('note');
        noteContainer.style.display = 'none';
    }

    function showFireworks() {
        const fireworks = document.getElementById('fireworks');
        fireworks.style.display = 'block';

        setTimeout(() => {
            fireworks.style.display = 'none';
        }, 5000);
    }
</script>

</body>
</html>

