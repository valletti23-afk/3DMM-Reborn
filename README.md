#3DMM Reborn#
3DMM Reborn è un progetto derivato da 3DMM, creato per standardizzare questo vecchio software per i moderni Windows 10, 8 e 11.
**NUOVE COSE**
Stanco del limitato classico? C'è di più qui! Il Movie Maker Entertaintment Pack permette di giocare a giochi classici, come SkiFree o Chip's Challenge; Altri personaggi sono nella band, come Garfield, Sonic o Tails (**NOTA** io non possedo i personaggi: gli esempi sono di Paws, Inc e SEGA)! E c'è di più!
Niente più noiose pause a mettere un altro programma con MMEP!
Scegli ora oltre 100 attori!
#NOTE DI COMPATIBILITà#
Io non ho ancora modernizzato questo programma. Quando io editerò il README in "APPENA MODERNIZZATO", sarà pronto per le installazioni e usi su Windows XP, 8, 10, 11 e altri OS futuri. Non funzionerà se lo installi su un Linux o un MacOS, purchè modificherò il codice in modo che apparirà un messaggio che dirà che "Il software è un prodotto Microsoft e non può funzionare se installato su Mac o Linux". Inoltre, se si forza a girarlo su Linux o MacOS, il programma potrebbe crashare, emettere un suono "BEEEEEEEEP" anche se c'è la intro o addirittura crashare l'OS esterno a Windows per la pesantezza del codice inserito. 
Se qualcuno lo mette su un DOS (molto datato) non funzionerà, purchè i bit saranno 64 e il codice nella cartella Kauai sarà così pesante che crasherà il DOS.
Ritorniamo alla spiegazione...
Inserisci questo codice per vedere un prodotto in arrivo il 2027!
<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yahtzee Emoji 🎲</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; text-align: center; background-color: #f0f2f5; padding: 20px; }
        .container { max-width: 400px; margin: auto; background: white; padding: 20px; border-radius: 20px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); }
        .dice-container { display: flex; justify-content: center; gap: 10px; margin: 20px 0; }
        .die { font-size: 3.5rem; cursor: pointer; border: 3px solid transparent; border-radius: 12px; transition: 0.2s; user-select: none; }
        .die.held { border-color: #ff4757; background-color: #ffeef0; transform: scale(1.1); }
        button { padding: 12px 24px; font-size: 1.2rem; cursor: pointer; background: #2ed573; color: white; border: none; border-radius: 10px; font-weight: bold; width: 100%; }
        button:disabled { background: #ccc; }
        .stats { margin-top: 20px; font-size: 1.1rem; display: flex; justify-content: space-around; background: #f8f9fa; padding: 10px; border-radius: 10px; }
        #message { height: 30px; margin: 15px 0; font-weight: bold; color: #57606f; }
    </style>
</head>
<body>

<div class="container">
    <h1>Yahtzee! 🎲</h1>
    <p>Tocca i dadi per bloccarli 🛑</p>

    <div class="dice-container" id="dice-box">
        <div class="die" onclick="toggleHold(0)">❓</div>
        <div class="die" onclick="toggleHold(1)">❓</div>
        <div class="die" onclick="toggleHold(2)">❓</div>
        <div class="die" onclick="toggleHold(3)">❓</div>
        <div class="die" onclick="toggleHold(4)">❓</div>
    </div>

    <p id="message">Lancia i dadi per iniziare!</p>
    <button id="roll-btn" onclick="rollDice()">Lancia! (3 rimasti)</button>

    <div class="stats">
        <div>Punti: <span id="total-score">0</span></div>
        <div>Lanci: <span id="rolls-left">3</span></div>
    </div>

    <button onclick="resetGame()" style="margin-top:20px; background: #747d8c; font-size: 0.9rem;">Reset 🔄</button>
</div>

<script>
    const visualDice = ["", "1️⃣", "2️⃣", "3️⃣", "4️⃣", "5️⃣", "6️⃣"];
    let dice = [0, 0, 0, 0, 0];
    let held = [false, false, false, false, false];
    let rollsLeft = 3;
    let totalScore = 0;

    function rollDice() {
        if (rollsLeft > 0) {
            for (let i = 0; i < 5; i++) {
                if (!held[i]) dice[i] = Math.floor(Math.random() * 6) + 1;
            }
            rollsLeft--;
            updateUI();
            checkScore();
        }
    }

    function toggleHold(i) {
        if (dice[0] === 0 || rollsLeft === 3) return;
        held[i] = !held[i];
        updateUI();
    }

    function updateUI() {
        const diceEls = document.querySelectorAll('.die');
        dice.forEach((val, i) => {
            if (val > 0) diceEls[i].textContent = visualDice[val];
            diceEls[i].className = held[i] ? 'die held' : 'die';
        });
        document.getElementById('roll-btn').textContent = `Lancia! (${rollsLeft} rimasti)`;
        document.getElementById('roll-btn').disabled = (rollsLeft === 0);
        document.getElementById('rolls-left').textContent = rollsLeft;
    }

    function checkScore() {
        const counts = {};
        dice.forEach(x => counts[x] = (counts[x] || 0) + 1);
        const maxSame = Math.max(...Object.values(counts));

        if (maxSame === 5) {
            document.getElementById('message').innerHTML = "✨ YAHTZEE! ✨ (+50)";
            totalScore += 50;
            rollsLeft = 0;
        } else if (rollsLeft === 0) {
            document.getElementById('message').textContent = "Turno finito!";
        } else {
            document.getElementById('message').textContent = "Scegli cosa tenere...";
        }
        document.getElementById('total-score').textContent = totalScore;
        if(rollsLeft === 0) updateUI();
    }

    function resetGame() {
        dice = [0, 0, 0, 0, 0];
        held = [false, false, false, false, false];
        rollsLeft = 3;
        totalScore = 0;
        document.getElementById('message').textContent = "Nuova partita! Lancia.";
        document.querySelectorAll('.die').forEach(el => el.textContent = "❓");
        updateUI();
    }
</script>

</body>
</html>
non è fantastico?
Inserisci il disco e... VOlià!
(C) Microsoft e Big Blue Dot, Inc.
