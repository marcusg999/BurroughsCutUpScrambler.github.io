<html><head><base href="https://websim.ai/cut-up-scrambler-deluxe"><title>Burroughs' Digital Dreamscape - Cut-Up Scrambler Deluxe</title><style>
    @import url('https://fonts.googleapis.com/css2?family=Courier+Prime&family=Major+Mono+Display&display=swap');

    body {
        font-family: 'Courier Prime', monospace;
        line-height: 1.6;
        color: #00ff00;
        background-color: #000000;
        margin: 0;
        padding: 20px;
        overflow-x: hidden;
    }
    .container {
        max-width: 800px;
        margin: 0 auto;
        position: relative;
    }
    h1 {
        font-family: 'Major Mono Display', monospace;
        color: #00ff00;
        text-align: center;
        font-size: 2.5em;
        text-shadow: 0 0 10px #00ff00;
        animation: glitch 1s linear infinite;
    }
    @keyframes glitch {
        2%, 64% { transform: translate(2px,0) skew(0deg); }
        4%, 60% { transform: translate(-2px,0) skew(0deg); }
        62% { transform: translate(0,0) skew(5deg); }
    }
    textarea, #output {
        width: 100%;
        height: 150px;
        margin-bottom: 20px;
        padding: 10px;
        background-color: #0a0a0a;
        color: #00ff00;
        border: 1px solid #00ff00;
        box-shadow: 0 0 10px #00ff00;
        font-family: 'Courier Prime', monospace;
    }
    #output {
        overflow-y: auto;
        resize: vertical;
        min-height: 150px;
        max-height: 400px;
    }
    button {
        display: block;
        width: 100%;
        padding: 15px;
        background-color: #00ff00;
        color: #000000;
        border: none;
        cursor: pointer;
        font-size: 18px;
        font-family: 'Major Mono Display', monospace;
        text-transform: uppercase;
        transition: all 0.3s ease;
    }
    button:hover {
        background-color: #000000;
        color: #00ff00;
        box-shadow: 0 0 20px #00ff00;
    }
    #output {
        white-space: pre-wrap;
        word-wrap: break-word;
    }
    .explanation {
        background-color: #0a0a0a;
        border-left: 5px solid #00ff00;
        padding: 20px;
        margin-top: 30px;
        box-shadow: 0 0 15px #00ff00;
    }
    .typewriter {
        overflow: hidden;
        border-right: .15em solid #00ff00;
        white-space: nowrap;
        margin: 0 auto;
        letter-spacing: .15em;
        animation: typing 3.5s steps(40, end), blink-caret .75s step-end infinite;
    }
    @keyframes typing {
        from { width: 0 }
        to { width: 100% }
    }
    @keyframes blink-caret {
        from, to { border-color: transparent }
        50% { border-color: #00ff00; }
    }
    .matrix-bg {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        pointer-events: none;
        z-index: -1;
    }
    /* Customized scrollbar for #output */
    #output::-webkit-scrollbar {
        width: 12px;
    }
    #output::-webkit-scrollbar-track {
        background: #0a0a0a;
    }
    #output::-webkit-scrollbar-thumb {
        background-color: #00ff00;
        border-radius: 6px;
        border: 3px solid #0a0a0a;
    }
</style></head><body>
    <div class="container">
        <h1>Burroughs' Digital Dreamscape</h1>
        <div class="typewriter">
            <p>Welcome to the Cut-Up Scrambler Deluxe...</p>
        </div>
        <textarea id="input" placeholder="Enter your reality here..."></textarea>
        <button onclick="scramble()">Deconstruct Reality</button>
        <div id="output"></div>
        <div class="explanation">
            <h3>The Digital Cut-Up Manifesto</h3>
            <p>In the spirit of William S. Burroughs and the Beat Generation, this Cut-Up Scrambler slices through the fabric of conventional narrative. It's not just a tool; it's a portal to linguistic chaos and accidental prophecy.</p>
            <p>Feed it your words, your thoughts, your dreams. Watch as it disassembles and reassembles, creating new realities from the fragments of the old. This is not just text manipulation - it's reality hacking.</p>
            <p>Remember: "When you cut into the present, the future leaks out." - William S. Burroughs</p>
        </div>
    </div>

    <canvas id="matrix" class="matrix-bg"></canvas>

<script>
function scramble() {
    let text = document.getElementById('input').value;
    let punctuation = text.match(/[.,!?;]/g) || [];
    let words = text.replace(/[.,!?;]/g, '').split(/\s+/);
    
    for (let i = words.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [words[i], words[j]] = [words[j], words[i]];
    }
    
    let scrambled = words.join(' ');
    
    punctuation.forEach(punct => {
        let insertPos = Math.floor(Math.random() * scrambled.length);
        scrambled = scrambled.slice(0, insertPos) + punct + scrambled.slice(insertPos);
    });
    
    let output = document.getElementById('output');
    output.innerText = '';
    let i = 0;
    let interval = setInterval(() => {
        output.innerText += scrambled[i];
        output.scrollTop = output.scrollHeight;
        i++;
        if (i >= scrambled.length) {
            clearInterval(interval);
        }
    }, 20);
}

// Matrix rain effect
const canvas = document.getElementById('matrix');
const ctx = canvas.getContext('2d');

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const katakana = 'アァカサタナハマヤャラワガザダバパイィキシチニヒミリヰギジヂビピウゥクスツヌフムユュルグズブヅプエェケセテネヘメレヱゲゼデベペオォコソトノホモヨョロヲゴゾドボポヴッン';
const latin = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
const nums = '0123456789';
const alphabet = katakana + latin + nums;

const fontSize = 16;
const columns = canvas.width / fontSize;

const rainDrops = [];

for (let x = 0; x < columns; x++) {
    rainDrops[x] = 1;
}

const draw = () => {
    ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    ctx.fillStyle = '#00ff00';
    ctx.font = fontSize + 'px monospace';

    for (let i = 0; i < rainDrops.length; i++) {
        const text = alphabet.charAt(Math.floor(Math.random() * alphabet.length));
        ctx.fillText(text, i * fontSize, rainDrops[i] * fontSize);

        if (rainDrops[i] * fontSize > canvas.height && Math.random() > 0.975) {
            rainDrops[i] = 0;
        }
        rainDrops[i]++;
    }
};

setInterval(draw, 30);
</script>

<footer>
   
</footer>

</body></html>
