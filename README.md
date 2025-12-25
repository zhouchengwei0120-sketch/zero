# zero[1index.html](https://github.com/user-attachments/files/24340650/1index.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>HCT 心理探索 | 你的潜意识原型分析</title>
    <style>
        /* --- 模仿 hengbinhct.com 的基础风格 --- */
        body {
            font-family: 'Helvetica Neue', Helvetica, Arial, 'PingFang SC', 'Microsoft YaHei', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f8f8f8; /* 浅灰色背景 */
            color: #333;
            line-height: 1.6;
        }
        .container {
            max-width: 960px;
            margin: 0 auto;
            padding: 20px;
        }
        header {
            background-color: #fff;
            padding: 20px 0;
            border-bottom: 1px solid #eee;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
            margin-bottom: 20px;
            text-align: center;
        }
        .logo {
            font-size: 28px;
            font-weight: bold;
            color: #2c3e50; /* 深蓝色，模仿HCT */
            text-decoration: none;
        }
        .logo span {
            color: #e74c3c; /* 红色点缀，模仿HCT */
        }
        h1, h2, h3 {
            color: #2c3e50;
            text-align: center;
            margin-bottom: 20px;
        }
        p {
            margin-bottom: 15px;
            text-align: justify;
        }
        .section {
            background-color: #fff;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
            margin-bottom: 30px;
        }
        .main-btn {
            display: inline-block;
            background-color: #e74c3c; /* HCT 的红色 */
            color: #fff;
            padding: 12px 25px;
            border-radius: 5px;
            text-decoration: none;
            font-size: 18px;
            font-weight: bold;
            transition: background-color 0.3s ease;
            cursor: pointer;
            border: none;
        }
        .main-btn:hover {
            background-color: #c0392b;
        }

        /* --- 心理测试特定样式 --- */
        #quiz-container {
            padding: 0; /* 移除额外内边距，让内容更紧凑 */
        }
        .question-header {
            font-size: 18px;
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 20px;
            text-align: left;
        }
        .progress-bar {
            height: 8px;
            background: #eee;
            border-radius: 4px;
            margin-bottom: 25px;
            overflow: hidden;
        }
        .progress-fill {
            height: 100%;
            background: #e74c3c; /* HCT 红色 */
            width: 0%;
            transition: width 0.3s ease;
            border-radius: 4px;
        }
        .option-btn {
            display: block;
            width: 100%;
            padding: 15px 20px;
            margin: 10px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
            background: #fff;
            color: #555;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.2s ease;
            text-align: left;
            box-shadow: none; /* 移除阴影，更扁平 */
        }
        .option-btn:hover {
            background: #f5f5f5;
            border-color: #e74c3c; /* 鼠标悬停时边框变红 */
            color: #2c3e50;
        }
        .option-btn:active {
            transform: translateY(1px);
        }

        /* 插图 */
        .intro-illustration {
            width: 100%;
            height: 250px;
            background-image: url('https://via.placeholder.com/960x250/34495e/ffffff?text=HCT+Psychology+Test+Intro'); /* 占位图 */
            background-size: cover;
            background-position: center;
            border-radius: 8px;
            margin-bottom: 20px;
        }
        .result-illustration {
            width: 100%;
            height: 200px;
            background-image: url('https://via.placeholder.com/960x200/e74c3c/ffffff?text=Your+Archetype+Revealed'); /* 占位图 */
            background-size: cover;
            background-position: center;
            border-radius: 8px;
            margin-bottom: 20px;
        }

        /* 结果页 */
        #result-area { display: none; text-align: center; }
        .result-title {
            font-size: 24px;
            color: #e74c3c;
            margin-bottom: 10px;
        }
        .result-desc {
            text-align: left;
            background-color: #f9f9f9;
            border: 1px solid #eee;
            padding: 20px;
            border-radius: 8px;
            color: #555;
            margin-bottom: 20px;
        }
        .ad-placeholder {
            background-color: #ecf0f1;
            padding: 25px;
            margin: 25px 0;
            border: 1px dashed #bdc3c7;
            color: #7f8c8d;
            font-size: 15px;
            border-radius: 8px;
        }
    </style>
</head>
<body>

    <header>
        <a href="#" class="logo">HCT <span>探索</span></a>
    </header>

    <div class="container">
        <div id="intro-page" class="section">
            <div class="intro-illustration"></div>
            <h2>潜意识投影：你的心灵原型深度测试</h2>
            <p>基于弗洛伊德心理学等理论，我们设计了 18 道精心挑选的问题，旨在揭示你隐藏在潜意识深处的核心驱动力、恐惧与渴望。</p>
            <p>这不是简单的性格分析，而是一场关于你灵魂原型的深度探索。通过对日常情境、梦境和本能反应的选择，我们将为你揭开内心最真实的画像。</p>
            <p style="text-align: center; margin-top: 30px;">
                <button class="main-btn" onclick="startQuiz()">开始深度探索</button>
            </p>
        </div>

        <div id="quiz-page" class="section" style="display: none;">
            <div class="progress-bar"><div class="progress-fill" id="p-fill"></div></div>
            <p class="question-header" id="q-progress">问题 1/18</p>
            <p class="question-text" id="q-text">加载中...</p>
            <div id="options-container"></div>
        </div>

        <div id="result-area" class="section">
            <div class="result-illustration"></div>
            <h2>分析完成！</h2>
            <p>你的潜意识原型已浮现...</p>
            
            <div class="ad-placeholder" id="ad-lock-box">
                【此处接入广告代码】<br>
                观看视频，解锁你的完整深度报告
            </div>
            <button class="main-btn" style="width: 100%; margin-top: 15px;" onclick="unlockResult()" id="unlock-btn">观看广告解锁报告</button>

            <div id="final-content" style="display:none;">
                 <h3 class="result-title" id="r-title"></h3>
                 <div class="result-desc" id="r-desc"></div>
                 <p style="text-align: center; margin-top: 30px;">
                     <button class="main-btn" style="background-color: #555; color: #fff;" onclick="location.reload()">重新测试</button>
                 </p>
            </div>
        </div>
    </div>

<script>
    // --- 数据配置区 (题目和结果文案，请继续补充到18题和4个结果类型) ---
    const questions = [
        {
            q: "Q1. 梦境投射：在一扇紧锁的门前，你直觉门后藏着什么？",
            options: [
                { text: "一个从未见过的奇异新世界。", type: 'E' },
                { text: "你最珍视的宝物或需要保护的人。", type: 'G' },
                { text: "一个正在看着你的“另一个自己”。", type: 'C' },
                { text: "解开你人生所有谜团的答案之书。", type: 'A' }
            ]
        },
        {
            q: "Q2. 冲突应对：当有人强烈质疑你的核心信念时，你的第一内在反应是？",
            options: [
                { text: "兴奋：终于有人来挑战我了。", type: 'E' },
                { text: "警惕：他可能会破坏现有的稳定。", type: 'G' },
                { text: "愤怒：他根本不懂我的独特价值。", type: 'C' },
                { text: "冷静：分析他的逻辑漏洞在哪里。", type: 'A' }
            ]
        },
        // TODO: 请继续在这里添加剩余的 16 道题目，格式同上
        // 为了演示，这里只放了两道题
    ];

    const results = {
        'E': {
            title: "深渊凝视者 (The Explorer)",
            desc: "<strong>潜意识素描：</strong><br>你的内在没有边界感，对“未知”有着近乎病态的迷恋。你不害怕黑暗，因为你认为真相往往藏在最深处。你表面的随和只是一种伪装，你的内心始终在策划下一次逃离平庸的冒险。<br><br><strong>天赋诅咒：</strong><br>拥有惊人的直觉和破局能力，但很难在一段极其稳定的关系或环境中长久停留。"
        },
        'G': {
            title: "秩序守护者 (The Guardian)",
            desc: "<strong>潜意识素描：</strong><br>你的核心驱动力是对抗混乱。你不仅保护自己，也试图为你周围的人建立安全壁垒。你极其敏锐地察觉风险，但也容易因此陷入焦虑。你深沉的爱往往通过“控制”和“担忧”来表达。<br><br><strong>天赋诅咒：</strong><br>是极其可靠的伙伴和基石，但有时会因为过度防御而错失成长的机会。"
        },
        'C': {
            title: "镜中造物主 (The Creator)",
            desc: "<strong>潜意识素描：</strong><br>你终其一生都在寻找最真实的自我表达。你恐惧被淹没在人海中失去个性。你的情感体验极其丰富剧烈，世界对你来说不是客观的存在，而是你主观情绪的画布。<br><br><strong>天赋诅咒：</strong><br>拥有化腐朽为神奇的创造力，但也容易陷入自我中心的深井，难以接受批评。"
        },
        'A': {
            title: "真理架构师 (The Analyst)",
            desc: "<strong>潜意识素描：</strong><br>你对情绪持怀疑态度，认为知识和逻辑才是掌控世界的唯一权杖。你的潜意识里有一种智性傲慢，渴望看穿一切表象背后的机制。你像一个置身事外的观察者，解剖着生活。<br><br><strong>天赋诅咒：</strong><br>拥有看透本质的智慧眼光，但在需要情感连接的时刻显得过于冷漠和疏离。"
        }
    };

    // --- 程序逻辑区 ---
    let currentStep = 0;
    let scores = { 'E': 0, 'G': 0, 'C': 0, 'A': 0 };

    function startQuiz() {
        document.getElementById('intro-page').style.display = 'none';
        document.getElementById('quiz-page').style.display = 'block';
        loadQuestion();
    }

    function loadQuestion() {
        if (currentStep >= questions.length) {
            showResultPage();
            return;
        }

        const q = questions[currentStep];
        document.getElementById('q-progress').innerText = `问题 ${currentStep + 1}/${questions.length}`;
        document.getElementById('q-text').innerText = q.q;
        
        let progress = ((currentStep) / questions.length) * 100;
        document.getElementById('p-fill').style.width = progress + '%';

        const container = document.getElementById('options-container');
        container.innerHTML = ''; 

        q.options.forEach(opt => {
            const btn = document.createElement('button');
            btn.className = 'option-btn';
            btn.innerText = opt.text;
            btn.onclick = () => nextStep(opt.type);
            container.appendChild(btn);
        });
    }

    function nextStep(type) {
        scores[type]++;
        currentStep++;
        loadQuestion();
    }

    function showResultPage() {
        document.getElementById('quiz-page').style.display = 'none';
        document.getElementById('result-area').style.display = 'block';
        document.getElementById('p-fill').style.width = '100%'; // 进度条拉满
    }

    function unlockResult() {
        document.getElementById('unlock-btn').innerText = "正在分析中...";
        document.getElementById('unlock-btn').disabled = true;
        
        setTimeout(() => {
            document.getElementById('ad-lock-box').style.display = 'none';
            document.getElementById('unlock-btn').style.display = 'none';
            document.getElementById('final-content').style.display = 'block';
            
            calculateAndDisplayResult();
        }, 1500); // 模拟1.5秒延迟
    }

    function calculateAndDisplayResult() {
        let maxScore = 0;
        let resultType = 'E'; 
        for (let type in scores) {
            if (scores[type] > maxScore) {
                maxScore = scores[type];
                resultType = type;
            }
        }
        
        let topTypes = [];
        for (let type in scores) {
             if (scores[type] === maxScore) topTypes.push(type);
        }
        if (topTypes.length > 1) {
            resultType = topTypes[Math.floor(Math.random() * topTypes.length)];
        }

        const res = results[resultType];
        document.getElementById('r-title').innerHTML = res.title;
        document.getElementById('r-desc').innerHTML = res.desc;
    }
</script>

</body>
</html>
