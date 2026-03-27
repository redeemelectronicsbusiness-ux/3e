<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Troisièmes Easter Revisions - Emergence Secondary</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f1f5f9; padding: 20px; color: #1e293b; }
        .container { max-width: 900px; margin: auto; background: white; padding: 30px; border-radius: 20px; box-shadow: 0 10px 25px rgba(0,0,0,0.05); border-top: 10px solid #7c3aed; }
        .header-branding { text-align: center; margin-bottom: 25px; }
        .school-logo { width: 100px; height: auto; border-radius: 50%; margin-bottom: 10px; }
        .school-title { font-size: 24px; color: #4c1d95; margin: 0; font-weight: 800; }
        .location { margin: 5px 0; color: #64748b; font-size: 14px; }
        h1.main-title { color: #0f172a; text-align: center; font-size: 26px; margin-top: 20px; }
        .module-btn { background: #fff; color: #334155; border: 2px solid #e2e8f0; padding: 20px; margin: 10px 0; width: 100%; border-radius: 12px; cursor: pointer; font-size: 16px; transition: 0.2s; text-align: left; display: flex; justify-content: space-between; align-items: center; }
        .module-btn:hover:not(:disabled) { border-color: #7c3aed; background: #f5f3ff; }
        .module-btn.passed { background: #f0fdf4; border-color: #22c55e; color: #166534; }
        .options button { display: block; width: 100%; padding: 15px; margin: 10px 0; border: 1px solid #e2e8f0; border-radius: 10px; background: #fff; cursor: pointer; text-align: left; font-size: 16px; }
        .options button:hover { background: #f5f3ff; border-color: #7c3aed; }
        .hint-box { display: none; background: #fffbeb; border: 1px solid #fde68a; color: #92400e; padding: 15px; border-radius: 10px; margin: 15px 0; font-size: 14px; }
        .grade-badge { font-size: 60px; font-weight: 900; margin: 20px 0; color: #7c3aed; }
        .btn-nav { padding: 12px 20px; border-radius: 8px; cursor: pointer; border: none; font-weight: 600; }
        .btn-home { background: #64748b; color: white; }
        .btn-hint { background: #f59e0b; color: white; flex-grow: 1; margin-left: 10px; }
        .btn-reset { background: #ef4444; color: white; width: 100%; margin-top: 30px; }
    </style>
</head>
<body>

<div class="container">
    <div id="menu">
        <div class="header-branding">
            <img src="logo.jpg" alt="Logo" class="school-logo">
            <h2 class="school-title">Emergence Secondary School</h2>
            <p class="location">Logbessou Douala</p>
        </div>
        <h1 class="main-title">Level: Troisième</h1>
        <p style="text-align: center; font-weight: bold;">Easter Break Intensive Revision</p>
        <div id="module-list"></div>
        <button class="btn-nav btn-reset" onclick="resetProgress()">Reset Progress</button>
    </div>

    <div id="quiz-area" style="display:none">
        <h2 id="module-title" style="color:#7c3aed;"></h2>
        <div id="question-container"></div>
        <div id="hint-display" class="hint-box"></div>
        <div style="display: flex; margin-top: 20px;">
            <button class="btn-nav btn-home" onclick="showMenu()">Menu</button>
            <button class="btn-nav btn-hint" onclick="toggleHint()">Hint 💡</button>
        </div>
    </div>

    <div id="result-area" style="display:none; text-align: center;">
        <h2 id="result-status"></h2>
        <div id="grade-container" class="grade-badge"></div>
        <p id="score-text"></p>
        <button id="action-btn" class="btn-nav" style="width: 100%; padding: 20px; font-size: 18px; color: white;"></button>
    </div>
</div>

<script>
    const allModules = [
        { 
            title: "Module 1: National Integration & Diversity", 
            questions: Array.from({length: 40}, (_, i) => ({
                q: [
                    "We must accept peers from other __.", "Cameroon is a country of cultural __.", "Which word is an ellipsis for 'I went to the market and he went too'?", "I socialize with neighbors of other __.", "We should __ people from different tribes.",
                    "Neither my brother __ my sister likes okra.", "I have __ been to Foumban.", "Although it was raining, __ went to the feast.", "Christmas is a __ celebration.", "You can either stay __ go.",
                    "National __ promotes peace.", "Tribalism is the opposite of __.", "We celebrate New __ Day on January 1st.", "Unity in __ is Cameroon's strength.", "The Bamileke and Bakweri are __ in Cameroon.",
                    "I __ also a member of the choir.", "She has __ seen a traditional dance.", "Respecting others __ a duty.", "Living together __ harmony is vital.", "He didn't come, and __ did she.",
                    "We use __ to avoid repeating words.", "I like your culture, and you like __.", "Peace is __ than war.", "We are all __ citizens.", "Tolerance means __ others.",
                    "___ you ever visited the North?", "They are __ Cameroonians.", "A __ is a group with shared culture.", "Inter-tribal __ promotes unity.", "Language __ diversity.",
                    "Don't __ people based on religion.", "We share the __ national anthem.", "Unity makes us __.", "Diversity is a __.", "I enjoy __ food.",
                    "___ nor his friend arrived.", "I also like __ music.", "Wait __ I finish my speech.", "She is only __ child.", "Unity is __."
                ][i % 40],
                options: [
                    ["tribes", "tribalism", "tributes"], ["diversity", "unity", "division"], ["too", "went", "market"], ["religions", "regions", "tribes"], ["tolerate", "ignore", "fight"],
                    ["nor", "or", "and"], ["never", "ever", "always"], ["he", "she", "we"], ["cross-national", "local", "personal"], ["or", "nor", "and"],
                    ["integration", "separation", "isolation"], ["integration", "unity", "peace"], ["Year", "Month", "Week"], ["diversity", "unity", "money"], ["tribes", "religions", "countries"],
                    ["am", "is", "are"], ["never", "always", "just"], ["is", "are", "am"], ["in", "on", "at"], ["neither", "either", "so"],
                    ["ellipsis", "nouns", "verbs"], ["mine", "my", "me"], ["better", "good", "best"], ["equal", "different", "rich"], ["accepting", "hating", "avoiding"],
                    ["Have", "Has", "Do"], ["proudly", "proud", "pride"], ["tribe", "house", "shop"], ["marriage", "fighting", "games"], ["is", "are", "am"],
                    ["judge", "love", "help"], ["same", "different", "old"], ["stronger", "weaker", "bigger"], ["blessing", "curse", "problem"], ["traditional", "fast", "bad"],
                    ["Neither", "Either", "Both"], ["modern", "noise", "old"], ["while", "during", "for"], ["one", "a", "the"], ["strength", "weak", "power"]
                ][i % 40],
                answer: [
                    "tribes", "diversity", "too", "religions", "tolerate", "nor", "never", "he", "cross-national", "or", "integration", "integration", "Year", "diversity", "tribes", "am", "never", "is", "in", "neither", "ellipsis", "mine", "better", "equal", "accepting", "Have", "proudly", "tribe", "marriage", "is", "judge", "same", "stronger", "blessing", "traditional", "Neither", "modern", "while", "one", "strength"
                ][i % 40],
                hint: "Focus: Ellipsis, adjuncts (neither/nor), and national integration vocabulary."
            }))
        },
        { 
            title: "Module 2: Consumer Rights & Responsibility", 
            questions: Array.from({length: 40}, (_, i) => ({
                q: [
                    "A consumer has the right to __.", "Check the __ date before buying.", "Don't buy __ products.", "The __ protects consumers.", "I prefer __ to locally made ones.",
                    "If I __ enough money, I would buy it.", "If you eat bad food, you __ sick.", "I __ have bought that if I knew.", "Prices are __ today than yesterday.", "This is the __ shop in town.",
                    "A __ is a document showing payment.", "Always ask for a __.", "Consumer __ is important.", "The shopkeeper was __ (polite).", "I __ (to buy) this last week.",
                    "If the price __ lower, I will buy it.", "Expired food is __.", "Advertising __ our choices.", "Comparison __ helps save money.", "Quality is __ than quantity.",
                    "The __ was very expensive.", "I am __ about the service.", "They __ (to sell) fresh bread.", "How __ does this cost?", "I have __ money left.",
                    "A __ is a person who buys things.", "Don't __ your money.", "Save money __ the bank.", "___ products are often cheaper.", "Check the __ on the can.",
                    "If she __ here, she would help.", "I wish I __ more money.", "The __ is always right.", "Prices __ gone up.", "I __ (not like) bad service.",
                    "This milk is __.", "Where is the __?", "Can I have a __?", "It is __ to buy healthily.", "I __ (to pay) by cash."
                ][i % 40],
                options: [
                    ["safety", "theft", "danger"], ["expiry", "entry", "birth"], ["expired", "fresh", "new"], ["law", "police", "thief"], ["imported", "export", "local"],
                    ["had", "have", "has"], ["will get", "got", "gets"], ["would", "will", "should"], ["higher", "high", "highest"], ["best", "better", "good"],
                    ["receipt", "book", "paper"], ["discount", "theft", "fine"], ["rights", "wrongs", "fights"], ["impolite", "polite", "kind"], ["bought", "buy", "buys"],
                    ["is", "was", "were"], ["dangerous", "good", "sweet"], ["influences", "stops", "hates"], ["shopping", "running", "eating"], ["better", "worse", "same"],
                    ["item", "person", "place"], ["complaining", "happy", "excited"], ["sell", "sells", "sold"], ["much", "many", "old"], ["no", "any", "some"],
                    ["consumer", "seller", "driver"], ["waste", "save", "keep"], ["at", "in", "on"], ["Local", "Global", "Far"], ["label", "color", "size"],
                    ["were", "is", "was"], ["had", "have", "has"], ["customer", "boss", "boy"], ["have", "has", "are"], ["don't", "doesn't", "didn't"],
                    ["sour", "sweet", "good"], ["market", "school", "office"], ["refund", "fine", "bill"], ["wise", "bad", "stupid"], ["paid", "pay", "pays"]
                ][i % 40],
                answer: [
                    "safety", "expiry", "expired", "law", "imported", "had", "will get", "would", "higher", "best", "receipt", "discount", "rights", "impolite", "bought", "is", "dangerous", "influences", "shopping", "better", "item", "complaining", "sell", "much", "no", "consumer", "waste", "at", "Local", "label", "were", "had", "customer", "have", "don't", "sour", "market", "refund", "wise", "paid"
                ][i % 40],
                hint: "Focus: Conditionals (Type 1 & 2), comparatives, and consumer vocabulary."
            }))
        },
        { 
            title: "Module 3: Environment & Hygiene", 
            questions: Array.from({length: 40}, (_, i) => ({
                q: [
                    "We must __ the environment.", "Stop __ trees.", "The Earth is getting __.", "Plastic is __ for the soil.", "Recycle your __.",
                    "If we __ trees, we save the air.", "Water __ causes diseases.", "Global __ is a threat.", "I __ (not throw) litter.", "She __ (to clean) the yard.",
                    "Hygiene prevents __.", "Keep the surroundings __.", "___ is the study of environment.", "Air __ comes from smoke.", "Protect the __ species.",
                    "If people __ trash, the city stays clean.", "We __ (past) the school garden.", "Planting trees is __.", "Use a __ to clean.", "Don't __ water.",
                    "Environmental __ is necessary.", "The __ is very hot.", "Wash your hands __.", "Clean water is __.", "Diseases __ spread by flies.",
                    "I __ (to see) a clean park.", "The forest is __.", "We need __ energy.", "Solar power is __.", "Animals need a __.",
                    "If it __, the plants grow.", "Save the __.", "___ is better than cure.", "Use __ bags.", "The __ is melting.",
                    "Trash should go in the __.", "Nature is __.", "Respect the __.", "I am __ about nature.", "Earth is our __."
                ][i % 40],
                options: [
                    ["protect", "destroy", "burn"], ["cutting", "planting", "watering"], ["warmer", "colder", "smaller"], ["bad", "good", "useful"], ["waste", "food", "money"],
                    ["plant", "cut", "burn"], ["pollution", "cleaning", "drinking"], ["warming", "cooling", "staying"], ["don't throw", "throw", "throws"], ["cleaned", "clean", "cleans"],
                    ["illness", "health", "growth"], ["clean", "dirty", "wet"], ["Ecology", "Math", "History"], ["pollution", "purity", "smell"], ["endangered", "safe", "new"],
                    ["don't throw", "throw", "throws"], ["planted", "plant", "plants"], ["beneficial", "bad", "hard"], ["broom", "pen", "spoon"], ["waste", "save", "keep"],
                    ["protection", "destruction", "waste"], ["climate", "weather", "day"], ["regularly", "never", "rarely"], ["safe", "dangerous", "bad"], ["are", "is", "am"],
                    ["saw", "see", "seen"], ["beautiful", "ugly", "small"], ["green", "black", "old"], ["clean", "dirty", "loud"], ["habitat", "house", "cage"],
                    ["rains", "rain", "raining"], ["planet", "star", "moon"], ["Prevention", "Fighting", "Running"], ["reusable", "plastic", "paper"], ["ice", "water", "fire"],
                    ["bin", "floor", "street"], ["fragile", "strong", "hard"], ["wildlife", "cars", "toys"], ["passionate", "angry", "sad"], ["home", "office", "car"]
                ][i % 40],
                answer: [
                    "protect", "cutting", "warmer", "bad", "waste", "plant", "pollution", "warming", "don't throw", "cleaned", "illness", "clean", "Ecology", "pollution", "endangered", "don't throw", "planted", "beneficial", "broom", "waste", "protection", "climate", "regularly", "safe", "are", "saw", "beautiful", "green", "clean", "habitat", "rains", "planet", "Prevention", "reusable", "ice", "bin", "fragile", "wildlife", "passionate", "home"
                ][i % 40],
                hint: "Focus: Conditional Type 1, environment vocabulary, and hygiene."
            }))
        },
        { 
            title: "Module 4: School Life & Citizenship", 
            questions: Array.from({length: 40}, (_, i) => ({
                q: [
                    "The student __ won the prize is happy.", "This is the school __ I study.", "We must __ the school rules.", "A good citizen __ taxes.", "Respect the __.",
                    "The prefect __ badge is silver.", "I __ (to be) late yesterday.", "She __ (to have) a lot of friends.", "We __ (to do) a project.", "The teacher __ is kind.",
                    "___ your homework on time.", "Don't __ in class.", "The school __ is green.", "We sing the __ anthem.", "The __ is in charge.",
                    "The boy __ bag is red.", "I love the __ of my school.", "Be __ to your peers.", "Bullying is __.", "Follow the __.",
                    "A citizen has __ and duties.", "The country needs __.", "Vote for the __.", "___ is a duty.", "I am a __ of Cameroon.",
                    "The school __ is large.", "We have __ subjects.", "Study __ for exams.", "Success requires __.", "Don't __ during tests.",
                    "The girl __ sits there is smart.", "This is the pen __ I lost.", "I __ (to see) the principal.", "He __ (to go) home.", "They __ (to play) football.",
                    "Respect __.", "Be __.", "School is __.", "Knowledge is __.", "I __ my school."
                ][i % 40],
                options: [
                    ["who", "which", "where"], ["where", "who", "which"], ["obey", "break", "ignore"], ["pays", "steals", "hides"], ["flag", "ball", "pen"],
                    ["whose", "who", "which"], ["was", "were", "am"], ["has", "had", "have"], ["did", "do", "done"], ["who", "which", "whose"],
                    ["Finish", "Start", "Leave"], ["talk", "sleep", "eat"], ["uniform", "car", "hat"], ["national", "local", "personal"], ["principal", "student", "cook"],
                    ["whose", "who", "which"], ["spirit", "ghost", "noise"], ["kind", "mean", "rude"], ["wrong", "right", "good"], ["rules", "games", "songs"],
                    ["rights", "fights", "money"], ["peace", "war", "noise"], ["prefect", "thief", "lazy"], ["Voting", "Sleeping", "Eating"], ["citizen", "stranger", "guest"],
                    ["yard", "room", "box"], ["many", "few", "no"], ["hard", "lazy", "fast"], ["effort", "luck", "money"], ["cheat", "help", "work"],
                    ["who", "which", "whose"], ["which", "who", "where"], ["saw", "see", "seen"], ["went", "go", "gone"], ["played", "play", "playing"],
                    ["authority", "friends", "toys"], ["punctual", "late", "slow"], ["important", "bad", "easy"], ["power", "heavy", "gold"], ["love", "hate", "like"]
                ][i % 40],
                answer: [
                    "who", "where", "obey", "pays", "flag", "whose", "was", "has", "did", "who", "Finish", "talk", "uniform", "national", "principal", "whose", "spirit", "kind", "wrong", "rules", "rights", "peace", "prefect", "Voting", "citizen", "yard", "many", "hard", "effort", "cheat", "who", "which", "saw", "went", "played", "authority", "punctual", "important", "power", "love"
                ][i % 40],
                hint: "Focus: Relative pronouns (who, which, whose, where) and school-based vocabulary."
            }))
        },
        { 
            title: "Module 5: Modern Technology Utilities", 
            questions: Array.from({length: 40}, (_, i) => ({
                q: [
                    "I want to __ to a data bundle.", "Please __ on the router.", "My phone is __ out of battery.", "I have a __ with the network.", "Can you help me __ up this app?",
                    "I am __ (good) at gaming than him.", "This is the __ (fast) internet.", "If I __ a credit card, I'd pay.", "I am __ about the slow speed.", "The service __ is poor.",
                    "___ up your password.", "Don't __ suspicious links.", "Android phones are __.", "I use an __ for my work.", "The __ is very clear.",
                    "I __ (past) the software.", "She __ (past) an email.", "The __ is expensive.", "I like __ games.", "The __ is down.",
                    "I __ (to buy) a new tablet.", "How __ is the data?", "It __ (to cost) 5000 frs.", "I need a __.", "My phone __ (to break).",
                    "The __ is large.", "I __ (to search) online.", "___ is a gadget.", "I love __.", "Be __ online.",
                    "If the signal __ better, I'd call.", "I wish I __ a laptop.", "The screen __ broken.", "I __ (not like) lags.", "The battery __ fast.",
                    "___ your phone.", "___ the volume.", "The __ is loud.", "Technology is __.", "I __ ICT."
                ][i % 40],
                options: [
                    ["subscribe", "buy", "sell"], ["turn", "get", "put"], ["running", "walking", "going"], ["complaint", "joy", "peace"], ["set", "get", "put"],
                    ["better", "good", "best"], ["fastest", "faster", "fast"], ["had", "have", "has"], ["unhappy", "happy", "excited"], ["quality", "color", "size"],
                    ["Back", "Set", "Go"], ["click", "see", "touch"], ["gadgets", "toys", "books"], ["iPad", "pen", "ruler"], ["display", "noise", "weight"],
                    ["updated", "update", "updating"], ["sent", "send", "sending"], ["subscription", "gift", "card"], ["video", "paper", "board"], ["network", "road", "water"],
                    ["bought", "buy", "buys"], ["expensive", "long", "heavy"], ["cost", "costs", "costing"], ["charger", "book", "bag"], ["broke", "break", "breaks"],
                    ["memory", "room", "yard"], ["searched", "search", "searching"], ["Tablet", "Pen", "Paper"], ["innovation", "old", "bad"], ["careful", "lazy", "fast"],
                    ["were", "is", "was"], ["had", "have", "has"], ["is", "are", "am"], ["don't", "doesn't", "didn't"], ["drains", "fills", "stops"],
                    ["Charge", "Wash", "Eat"], ["Increase", "Turn", "Stop"], ["speaker", "screen", "key"], ["useful", "bad", "hard"], ["study", "hate", "run"]
                ][i % 40],
                answer: [
                    "subscribe", "turn", "running", "complaint", "set", "better", "fastest", "had", "unhappy", "quality", "Back", "click", "gadgets", "iPad", "display", "updated", "sent", "subscription", "video", "network", "bought", "expensive", "cost", "charger", "broke", "memory", "searched", "Tablet", "innovation", "careful", "were", "had", "is", "don't", "drains", "Charge", "Increase", "speaker", "useful", "study"
                ][i % 40],
                hint: "Focus: Phrasal verbs (turn on, set up), conditionals, and tech vocabulary."
            }))
        }
    ];

    let unlocked = 0;
    let currentMod = null;
    let currentQ = 0;
    let score = 0;
    let currentShuffled = [];

    if(localStorage.getItem('easter3emeProg')) unlocked = parseInt(localStorage.getItem('easter3emeProg'));

    function resetProgress() {
        if(confirm("Reset all Troisième progress?")) {
            localStorage.removeItem('easter3emeProg');
            unlocked = 0;
            showMenu();
        }
    }

    function showMenu() {
        document.getElementById('menu').style.display = 'block';
        document.getElementById('quiz-area').style.display = 'none';
        document.getElementById('result-area').style.display = 'none';
        const list = document.getElementById('module-list');
        list.innerHTML = '';
        allModules.forEach((m, i) => {
            const b = document.createElement('button');
            b.className = `module-btn ${i < unlocked ? 'passed' : ''}`;
            b.disabled = i > unlocked;
            b.innerHTML = `<span><strong>Module ${i+1}:</strong> ${m.title}</span> <span>${i < unlocked ? '✅' : (i === unlocked ? '▶️' : '🔒')}</span>`;
            b.onclick = () => start(i);
            list.appendChild(b);
        });
    }

    function start(i) {
        currentMod = i; currentQ = 0; score = 0;
        currentShuffled = [...allModules[i].questions].sort(() => 0.5 - Math.random());
        document.getElementById('menu').style.display = 'none';
        document.getElementById('quiz-area').style.display = 'block';
        document.getElementById('module-title').innerText = allModules[i].title;
        loadQ();
    }

    function loadQ() {
        const q = currentShuffled[currentQ];
        const c = document.getElementById('question-container');
        document.getElementById('hint-display').innerText = q.hint;
        document.getElementById('hint-display').style.display = 'none';
        c.innerHTML = `<p>Question ${currentQ+1}/40</p><h3>${q.q}</h3><div class="options">${q.options.sort(() => 0.5 - Math.random()).map(o => `<button onclick="check('${o.replace(/'/g, "\\'")}')">${o}</button>`).join('')}</div>`;
    }

    function check(o) {
        if(o === currentShuffled[currentQ].answer) score++;
        currentQ++;
        if(currentQ < 40) loadQ(); else finish();
    }

    function toggleHint() { 
        const h = document.getElementById('hint-display'); 
        h.style.display = h.style.display === 'block' ? 'none' : 'block'; 
    }

    function finish() {
        document.getElementById('quiz-area').style.display = 'none';
        document.getElementById('result-area').style.display = 'block';
        const pass = score >= 32; // Pass mark: 80% (32 out of 40)
        document.getElementById('result-status').innerText = pass ? "Great Job! 🎓" : "Keep Practicing!";
        document.getElementById('grade-container').innerText = `${score}/40`;
        document.getElementById('score-text').innerText = pass ? "Module complete! You are ready for the next one." : "You need at least 32/40 to unlock the next module.";
        const b = document.getElementById('action-btn');
        if(pass) {
            b.innerText = "NEXT MODULE"; b.style.background = "#22c55e";
            b.onclick = () => { if(currentMod === unlocked) unlocked++; localStorage.setItem('easter3emeProg', unlocked); showMenu(); };
        } else {
            b.innerText = "RETRY MODULE"; b.style.background = "#ef4444";
            b.onclick = () => start(currentMod);
        }
    }
    showMenu();
</script>
</body>
</html>
