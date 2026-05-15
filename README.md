<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>The Speed Typer</title>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #111;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    overflow: hidden;
}

.container {
    text-align: center;
    width: 90%;
    max-width: 500px;
}

.word {
    font-size: 40px;
    margin: 20px 0;
    font-weight: bold;
}

input {
    padding: 12px;
    width: 80%;
    font-size: 18px;
    border: none;
    border-radius: 8px;
    text-align: center;
    outline: none;
}

.score {
    margin-top: 15px;
    font-size: 18px;
}

/* benar = flash hijau */
.flash {
    animation: flashGreen 0.3s;
}

@keyframes flashGreen {
    0% { background: #111; }
    50% { background: #00c853; }
    100% { background: #111; }
}

/* salah = shake */
.shake {
    animation: shake 0.3s;
}

@keyframes shake {
    0% { transform: translate(2px, 2px); }
    25% { transform: translate(-2px, -2px); }
    50% { transform: translate(2px, -2px); }
    75% { transform: translate(-2px, 2px); }
    100% { transform: translate(0, 0); }
}
</style>
</head>

<body id="body">

<div class="container">
    <h1>The Speed Typer</h1>
    <div class="word" id="word"></div>
    <input type="text" id="input" placeholder="type here..." autocomplete="off">
    <div class="score">Score: <span id="score">0</span></div>
</div>

<script>
const words = [
    "apple","banana","school","computer","keyboard",
    "internet","speed","random","code","javascript",
    "developer","mouse","window","challenge","typing"
];

let word = "";
let score = 0;

const wordEl = document.getElementById("word");
const inputEl = document.getElementById("input");
const scoreEl = document.getElementById("score");
const body = document.getElementById("body");

function newWord() {
    word = words[Math.floor(Math.random() * words.length)];
    wordEl.textContent = word;
    inputEl.value = "";
}

function flash() {
    body.classList.add("flash");
    setTimeout(() => body.classList.remove("flash"), 300);
}

function shake() {
    body.classList.add("shake");
    setTimeout(() => body.classList.remove("shake"), 300);
}

inputEl.addEventListener("input", () => {
    const typed = inputEl.value;

    if (typed === word) {
        score++;
        scoreEl.textContent = score;
        flash();
        newWord();
    } 
    else if (!word.startsWith(typed)) {
        shake();
    }
});

newWord();
</script>

</body>
</html>
