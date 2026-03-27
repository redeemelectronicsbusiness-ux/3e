<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Emergence Secondary - Student Portal</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, sans-serif; background: #f0f2f5; color: #1e293b; padding: 20px; }
        .container { max-width: 900px; margin: auto; background: white; padding: 30px; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
        .school-header { text-align: center; border-bottom: 3px solid #7c3aed; padding-bottom: 20px; margin-bottom: 25px; }
        .school-name { font-size: 28px; color: #4c1d95; font-weight: 800; margin: 0; text-transform: uppercase; }
        .info-bar { display: flex; justify-content: space-around; background: #f8fafc; padding: 10px; border-radius: 10px; margin-top: 10px; font-weight: 600; font-size: 14px; }
        .section-header { background: #7c3aed; color: white; padding: 5px 15px; border-radius: 20px; font-size: 12px; display: inline-block; margin-bottom: 10px; }
        .module-grid { display: grid; grid-template-columns: 1fr; gap: 15px; }
        .module-card { border: 2px solid #e2e8f0; border-radius: 15px; padding: 20px; display: flex; justify-content: space-between; align-items: center; transition: 0.3s; background: white; }
        .unlocked { border-color: #7c3aed; cursor: pointer; }
        .locked { opacity: 0.5; cursor: not-allowed; background: #f1f5f9; }
        .passed { background: #f0fdf4; border-color: #22c55e; }
        .answer-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-top: 15px; }
        .ans-btn { padding: 18px; border: 2px solid #cbd5e1; border-radius: 12px; background: white; cursor: pointer; font-size: 16px; transition: 0.2s; text-align: center; font-weight: 500; }
        .ans-btn:hover { border-color: #7c3aed; background: #f5f3ff; }
        .ans-selected { background: #7c3aed !important; color: white !important; border-color: #4c1d95 !important; }
        .btn { padding: 12px 25px; border-radius: 8px; border: none; font-weight: 700; cursor: pointer; text-transform: uppercase; }
        .btn-next { background: #7c3aed; color: white; }
        .btn-back { background: #94a3b8; color: white; }
        textarea { width: 100%; height: 200px; border-radius: 10px; border: 2px solid #cbd5e1; padding: 15px; font-size: 16px; margin-top: 15px; resize: none; box-sizing: border-box; line-height: 1.5; }
    </style>
</head>
<body>

<div class="container">
    <div id="header-area" style="display:none">
        <div class="school-header">
            <h1 class="school-name">Emergence Secondary School</h1>
            <div class="info-bar">
                <span>Subject: English Language</span>
                <span>Tutor: Mr. Cedric Elie Toubi</span>
                <span>Student: <span id="student-identity" style="color:#7c3aed; font-weight:bold;"></span></span>
            </div>
        </div>
    </div>

    <div id="screen-login" style="text-align: center; padding: 50px 0;">
        <h2 style="color:#4c1d95">Troisième Assessment Portal</h2>
        <input type="text" id="name-input" placeholder="Enter Full Name..." style="width:80%; padding:15px; border-radius:10px; border:2px solid #cbd5e1; font-size:18px;">
        <br><br>
        <button class="btn btn-next" style="width: 80%; padding: 20px;" onclick="login()">Begin Evaluation</button>
    </div>

    <div id="screen-dashboard" style="display:none">
        <h3>Evaluation Modules</h3>
        <p>You must answer all 40 questions correctly to unlock the Module Conclusion writing task.</p>
        <div id="module-list" class="module-grid"></div>
    </div>

    <div id="screen-quiz" style="display:none">
        <div style="display:flex; justify-content:space-between; align-items:center;">
            <div>
                <div id="section-tag" class="section-header"></div>
                <h3 id="mod-title" style="color:#7c3aed; margin:0;"></h3>
            </div>
            <span id="q-counter" style="font-weight:bold; color:#64748b"></span>
        </div>
        <div id="quiz-body">
            <h2 id="question-text" style="margin: 20px 0; min-height: 60px;"></h2>
            <div id="answer-container" class="answer-grid"></div>
        </div>
        <div style="display:flex; justify-content:space-between; margin-top:30px;">
            <button class="btn btn-back" id="back-btn" onclick="nav(-1)">Back</button>
            <button class="btn btn-next" id="next-btn" onclick="nav(1)">Next</button>
        </div>
    </div>

    <div id="screen-writing" style="display:none">
        <h2 style="color:#7c3aed">Module Conclusion: Writing Task</h2>
        <div style="background:#fffbeb; padding:20px; border-left:5px solid #f59e0b; border-radius:5px;">
            <p id="writing-prompt" style="font-weight:600; margin:0; line-height: 1.4;"></p>
        </div>
        <textarea id="writing-input" placeholder="Write your paragraph here..."></textarea>
        <button class="btn btn-next" style="width:100%; margin-top:20px; padding:20px;" onclick="finishModule()">Submit and Unlock Next Module</button>
    </div>

    <div id="screen-result" style="display:none; text-align:center;">
        <h1 id="score-text" style="font-size:72px; margin:0; color:#7c3aed;"></h1>
        <p id="result-msg" style="font-size:18px; color:#64748b;"></p>
        <button class="btn btn-next" id="result-action" style="width:100%; margin-top:20px; padding:20px;"></button>
    </div>
</div>

<script>
    let studentName = "";
    let unlocked = 0;
    let currentMod = 0;
    let currentQIdx = 0;
    let studentAnswers = {};
    let activeQuestions = [];

    const modules = [
        { title: "National Integration & Diversity", prompt: "Write a paragraph explaining why respecting different tribes and cultures is essential for peace in Cameroon." },
        { title: "Consumer Rights & Responsibilities", prompt: "Explain your rights as a consumer when you buy a faulty electronic product. What steps do you take?" },
        { title: "Environment & Hygiene", prompt: "Describe the impact of plastic waste on our environment and suggest three ways to keep the campus clean." },
        { title: "School Life & Citizenship", prompt: "Discuss the role of a class prefect in maintaining discipline and promoting citizenship." },
        { title: "Utilities of Modern Technology", prompt: "Discuss the advantages and disadvantages of using smartphones for school research." }
    ];

    // Core Question Database - No Repetition across 40 slots
    const questionData = {
        grammar: [
            ["He said he would come, but he didn't __.", "...", "did", "to", "come"],
            ["If I __ a student leader, I would improve the library.", "were", "am", "was", "be"],
            ["The homework __ by the student yesterday.", "was done", "did", "is done", "does"],
            ["This is the man __ car was stolen.", "whose", "who", "which", "whom"],
            ["Please __ the computer when you are finished.", "shut down", "shut up", "shut in", "shut out"],
            ["I have been studying English __ five years.", "for", "since", "while", "during"],
            ["Neither the boy __ his friend was present.", "nor", "or", "and", "but"],
            ["By the time he arrived, the class __.", "had started", "starts", "starting", "start"],
            ["The tree __ by the wind last night.", "was blown down", "blow down", "is blowing", "blows"],
            ["You __ wash your hands before eating.", "must", "might", "could", "may"],
            ["The student __ won the prize is my cousin.", "who", "which", "whose", "whom"],
            ["She likes music; he __ too.", "does", "liking", "is", "do"],
            ["I need to ____ a new internet bundle.", "subscribe to", "log into", "shut down", "pick up"],
            ["The computer ____ by the technician now.", "is being fixed", "fixes", "was fixed", "is fixing"],
            ["Can you ____ the volume? It's too loud.", "turn down", "turn up", "turn on", "turn off"],
            ["____ you ever used an iPhone?", "Have", "Has", "Did", "Do"],
            ["This is the file ____ I downloaded.", "that", "who", "whom", "whose"],
            ["She doesn't like ICT, and ____ do I.", "neither", "either", "so", "too"],
            ["I wish I ____ a faster internet connection.", "had", "have", "am having", "will have"],
            ["Don't forget to ____ before you leave.", "log out", "log in", "sign up", "scroll up"]
        ],
        vocabulary: [
            ["Cameroon has over 200 different __ groups.", "ethnic", "plastic", "digital", "modern"],
            ["Always check the __ date on milk before drinking it.", "expiry", "birthday", "arrival", "meeting"],
            ["Littering causes __ in our streets.", "pollution", "wealth", "health", "growth"],
            ["A good citizen obeys the __ of the land.", "laws", "games", "songs", "weather"],
            ["To surf the web, you need a stable __ connection.", "internet", "battery", "plastic", "paper"],
            ["A person from your own country is a __.", "compatriot", "foreigner", "stranger", "tourist"],
            ["A __ is a person who buys goods and services.", "consumer", "vendor", "shopkeeper", "tutor"],
            ["When water is not safe to drink, it is __.", "contaminated", "purified", "bottled", "chilled"],
            ["To 'log in' to a computer, you need a __.", "password", "keyboard", "monitor", "mouse"],
            ["A ____ is used to move the cursor.", "mouse", "monitor", "printer", "scanner"],
            ["The brain of the computer is the ____.", "CPU", "RAM", "USB", "SSD"],
            ["A portable computer is called a ____.", "laptop", "desktop", "server", "mainframe"],
            ["____ is a popular mobile operating system.", "Android", "Windows", "Office", "Chrome"],
            ["To save files externally, use a ____.", "USB drive", "monitor", "speaker", "webcam"],
            ["The physical parts of a computer are ____.", "hardware", "software", "data", "apps"],
            ["____ allows computers to connect wirelessly.", "Wi-Fi", "Bluetooth", "Ethernet", "Infrared"],
            ["An ____ is a program for mobile phones.", "app", "operating system", "hardware", "driver"],
            ["The screen of the computer is the ____.", "monitor", "keyboard", "tower", "mousepad"],
            ["An ____ is a message sent digitally.", "email", "letter", "telegram", "fax"],
            ["To type, you use a ____.", "keyboard", "mouse", "mic", "printer"]
        ]
    };

    function generateModuleQuestions(modIdx) {
        let q = [];
        // Map 20 Grammar items
        questionData.grammar.forEach((item, i) => {
            q.push({
                id: `g${i}`,
                type: "GRAMMAR",
                text: item[0],
                correct: item[1],
                options: item.slice(1).sort(() => Math.random() - 0.5)
            });
        });
        // Map 20 Vocab items
        questionData.vocabulary.forEach((item, i) => {
            q.push({
                id: `v${i}`,
                type: "VOCABULARY",
                text: item[0],
                correct: item[1],
                options: item.slice(1).sort(() => Math.random() - 0.5)
            });
        });
        return q;
    }

    function login() {
        studentName = document.getElementById('name-input').value;
        if(!studentName) return alert("Please enter your name.");
        document.getElementById('screen-login').style.display = 'none';
        document.getElementById('header-area').style.display = 'block';
        document.getElementById('student-identity').innerText = studentName;
        showDashboard();
    }

    function showDashboard() {
        hideScreens();
        document.getElementById('screen-dashboard').style.display = 'block';
        const list = document.getElementById('module-list');
        list.innerHTML = "";
        modules.forEach((m, i) => {
            const card = document.createElement('div');
            const state = i < unlocked ? "passed" : (i === unlocked ? "unlocked" : "locked");
            card.className = `module-card ${state}`;
            card.innerHTML = `<div><strong>Module ${i+1}</strong><br>${m.title}</div> <div>${i < unlocked ? '✅ Complete' : '40 Items'}</div>`;
            if(state !== "locked") card.onclick = () => {
                currentMod = i;
                activeQuestions = generateModuleQuestions(i);
                currentQIdx = 0;
                studentAnswers = {};
                showQuiz();
            };
            list.appendChild(card);
        });
    }

    function showQuiz() {
        hideScreens();
        document.getElementById('screen-quiz').style.display = 'block';
        document.getElementById('mod-title').innerText = modules[currentMod].title;
        renderQuestion();
    }

    function renderQuestion() {
        const q = activeQuestions[currentQIdx];
        document.getElementById('section-tag').innerText = q.type;
        document.getElementById('q-counter').innerText = `Item ${currentQIdx + 1} of 40`;
        document.getElementById('question-text').innerText = q.text;
        
        const container = document.getElementById('answer-container');
        container.innerHTML = "";
        q.options.forEach(opt => {
            const btn = document.createElement('button');
            btn.className = `ans-btn ${studentAnswers[q.id] === opt ? 'ans-selected' : ''}`;
            btn.innerText = opt;
            btn.onclick = () => { 
                studentAnswers[q.id] = opt; 
                renderQuestion(); 
            };
            container.appendChild(btn);
        });

        document.getElementById('back-btn').disabled = currentQIdx === 0;
        document.getElementById('next-btn').innerText = currentQIdx === 39 ? "Submit Evaluation" : "Next";
    }

    function nav(dir) {
        if(dir === 1 && currentQIdx === 39) evaluate();
        else { currentQIdx += dir; renderQuestion(); }
    }

    function evaluate() {
        const failed = activeQuestions.filter(q => studentAnswers[q.id] !== q.correct);
        hideScreens();
        document.getElementById('screen-result').style.display = 'block';
        
        if(failed.length === 0) {
            document.getElementById('score-text').innerText = "100%";
            document.getElementById('result-msg').innerText = "Well done! You have mastered the objective items.";
            const btn = document.getElementById('result-action');
            btn.innerText = "Begin Writing Task";
            btn.onclick = () => {
                hideScreens();
                document.getElementById('screen-writing').style.display = 'block';
                document.getElementById('writing-prompt').innerText = modules[currentMod].prompt;
            };
        } else {
            document.getElementById('score-text').innerText = `${40 - failed.length}/40`;
            document.getElementById('result-msg').innerText = "You must correct your errors to reach 100%.";
            activeQuestions = failed;
            currentQIdx = 0;
            const btn = document.getElementById('result-action');
            btn.innerText = "Review Mistakes";
            btn.onclick = showQuiz;
        }
    }

    function finishModule() {
        if(!document.getElementById('writing-input').value) return alert("Please complete your paragraph.");
        alert("Evaluation successfully completed.");
        document.getElementById('writing-input').value = "";
        if(currentMod === unlocked) unlocked++;
        showDashboard();
    }

    function hideScreens() {
        ['screen-login', 'screen-dashboard', 'screen-quiz', 'screen-writing', 'screen-result'].forEach(s => {
            document.getElementById(s).style.display = 'none';
        });
    }
</script>
</body>
</html>
