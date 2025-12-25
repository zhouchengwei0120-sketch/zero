# Happy everyday
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>HCT 探索 | 灵魂原型深度分析</title>
    <style>
        /* 动态流动背景 */
        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        body {
            font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(-45deg, #f8f8f8, #f0f0f0, #e8e8e8, #ffffff);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            color: #2c3e50;
        }

        .card {
            width: 90%;
            max-width: 450px;
            background: rgba(255, 255, 255, 0.95);
            padding: 40px 30px;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.3);
            position: relative;
        }

        /* 进度条 */
        .progress-container {
            width: 100%;
            height: 4px;
            background: #eee;
            border-radius: 2px;
            margin-bottom: 30px;
        }
        .progress-bar {
            height: 100%;
            background: #e74c3c; /* HCT 红色 */
            width: 0%;
            transition: width 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }

        h2 { font-size: 22px; margin-bottom: 25px; line-height: 1.4; text-align: left; font-weight: 600; }

        .option-btn {
            display: block;
            width: 100%;
            padding: 18px 20px;
            margin-bottom: 12px;
            background: #fff;
            border: 1px solid #eee;
            border-radius: 12px;
            cursor: pointer;
            font-size: 16px;
            text-align: left;
            transition: all 0.2s;
            color: #444;
        }

        .option-btn:hover {
            border-color: #e74c3c;
            background: #fffafa;
            transform: translateX(5px);
        }

        .option-btn:active { transform: scale(0.98); }

        /* 结果页样式 */
        #result-page { display: none; text-align: center; }
        .result-title { font-size: 28px; color: #e74c3c; margin-bottom: 20px; font-weight: bold; }
        .result-text { 
            font-size: 16px; 
            line-height: 1.8; 
            text-align: left; 
            color: #555; 
            min-height: 100px;
        }

        .typing::after {
            content: '|';
            animation: blink 0.7s infinite;
        }
        @keyframes blink { 50% { opacity: 0; } }

        .unlock-btn {
            margin-top: 30px;
            background: #2c3e50;
            color: white;
            border: none;
            padding: 15px 40px;
            border-radius: 30px;
            font-size: 16px;
            cursor: pointer;
            width: 100%;
        }

        footer {
            position: absolute;
            bottom: -50px;
            left: 0;
            width: 100%;
            text-align: center;
            font-size: 12px;
            color: #999;
        }
    </style>
</head>
<body>

<div class="card">
    <div id="quiz-page">
        <div class="progress-container"><div class="progress-bar" id="bar"></div></div>
        <p style="font-size: 12px; color: #999; margin-bottom: 10px;" id="q-num">STEP 1/18</p>
        <h2 id="q-text">正在唤醒潜意识...</h2>
        <div id="options"></div>
    </div>

    <div id="result-page">
        <div id="unlock-box">
            <h2 style="text-align:center">分析报告已生成</h2>
            <p style="color:#7f8c8d">深度计算已完成，请解锁您的灵魂原型</p>
            <button class="unlock-btn" onclick="startTyping()">点击观看视频解锁报告</button>
        </div>
        
        <div id="report-box" style="display:none">
            <div class="result-title" id="r-title"></div>
            <div class="result-text" id="r-desc"></div>
            <button class="unlock-btn" style="background:#eee; color:#666; margin-top:40px;" onclick="location.reload()">重新探索</button>
        </div>
    </div>

    <footer>© HENGBIN HCT PSYCHOLOGY LAB</footer>
</div>

<script>
    const questions = [
        { q: "1. 梦境投射：在一扇紧锁的门前，你直觉门后藏着什么？", options: [{ text: "一个从未见过的奇异新世界", type: 'E' }, { text: "你最珍视的宝物", type: 'G' }, { text: "一个正在看着你的“另一个自己”", type: 'C' }, { text: "解开人生谜团的答案之书", type: 'A' }] },
        { q: "2. 冲突应对：当有人强烈质疑你的核心信念时，你第一反应是？", options: [{ text: "兴奋：终于有人来挑战我了", type: 'E' }, { text: "警惕：他可能会破坏稳定", type: 'G' }, { text: "愤怒：他根本不懂我的价值", type: 'C' }, { text: "冷静：分析他的逻辑漏洞", type: 'A' }] },
        { q: "3. 孤岛生存：如果你被困荒岛，你最先寻找的是？", options: [{ text: "未知的出口", type: 'E' }, { text: "安全的住所", type: 'G' }, { text: "表达心境的工具", type: 'C' }, { text: "岛屿的地图", type: 'A' }] },
        { q: "4. 面对黑暗：停电时，你脑海中浮现的第一个念头是？", options: [{ text: "寻找蜡烛探索", type: 'E' }, { text: "检查门窗锁好没", type: 'G' }, { text: "享受这份宁静", type: 'C' }, { text: "思考断电原因", type: 'A' }] },
        { q: "5. 礼物选择：你会送给自己哪种礼物？", options: [{ text: "一张去远方的机票", type: 'E' }, { text: "一套高品质寝具", type: 'G' }, { text: "一件定制艺术品", type: 'C' }, { text: "一台精密观测仪", type: 'A' }] },
        { q: "6. 时间旅行：如果你有时光机，你会去？", options: [{ text: "从未听闻的未来", type: 'E' }, { text: "最繁荣平稳的盛世", type: 'G' }, { text: "文艺复兴时期", type: 'C' }, { text: "宇宙起源的一刻", type: 'A' }] },
        { q: "7. 社交聚会：在嘈杂的晚会上，你更倾向于？", options: [{ text: "认识每一个新面孔", type: 'E' }, { text: "照顾熟悉的朋友", type: 'G' }, { text: "独自观察角落", type: 'C' }, { text: "分析社交链条", type: 'A' }] },
        { q: "8. 规则看法：面对一项不合理的规定，你会？", options: [{ text: "直接打破它", type: 'E' }, { text: "默默忍受保持秩序", type: 'G' }, { text: "用艺术方式嘲讽", type: 'C' }, { text: "寻找规则漏洞", type: 'A' }] },
        { q: "9. 评价在意：你最不能接受别人评价你？", options: [{ text: "你很平庸无趣", type: 'E' }, { text: "你很不靠谱", type: 'G' }, { text: "你没有个性", type: 'C' }, { text: "你很无知", type: 'A' }] },
        { q: "10. 宠物选择：如果你能养一只奇幻生物，是？", options: [{ text: "能飞的巨龙", type: 'E' }, { text: "温顺的独角兽", type: 'G' }, { text: "变幻莫测的精灵", type: 'C' }, { text: "通晓语言的狮身人面", type: 'A' }] },
        { q: "11. 任务执行：面对复杂任务，你的习惯是？", options: [{ text: "直接上手摸索", type: 'E' }, { text: "先写个稳妥计划", type: 'G' }, { text: "加入自己的创意", type: 'C' }, { text: "查阅所有相关资料", type: 'A' }] },
        { q: "12. 电影类型：你最喜欢看的电影是？", options: [{ text: "动作探险片", type: 'E' }, { text: "家庭伦理片", type: 'G' }, { text: "独立文艺片", type: 'C' }, { text: "硬核科幻悬疑", type: 'A' }] },
        { q: "13. 核心渴望：你认为人生的终极意义是？", options: [{ text: "体验一切可能", type: 'E' }, { text: "建立温馨港湾", type: 'G' }, { text: "留下独特印记", type: 'C' }, { text: "理解世界真相", type: 'A' }] },
        { q: "14. 金钱看法：对你来说，钱最重要的是？", options: [{ text: "购买自由的通行证", type: 'E' }, { text: "生活的保障金", type: 'G' }, { text: "支撑梦想的燃料", type: 'C' }, { text: "衡量价值的尺度", type: 'A' }] },
        { q: "15. 面对失败：失败后你通常会？", options: [{ text: "换个跑道继续冲", type: 'E' }, { text: "反思哪里没做稳", type: 'G' }, { text: "感到自我价值受损", type: 'C' }, { text: "分析失败的数据", type: 'A' }] },
        { q: "16. 理想居住：你向往的居住地是？", options: [{ text: "漂浮的房车", type: 'E' }, { text: "宁静的小镇别墅", type: 'G' }, { text: "艺术感公寓", type: 'C' }, { text: "极简实验室", type: 'A' }] },
        { q: "17. 情绪管理：感到压力大时，你会？", options: [{ text: "去剧烈运动", type: 'E' }, { text: "回家大睡一场", type: 'G' }, { text: "写日记或画画", type: 'C' }, { text: "研究减压科学", type: 'A' }] },
        { q: "18. 最终告别：你希望墓志铭上写着？", options: [{ text: "他从未停下", type: 'E' }, { text: "他守护了所爱", type: 'G' }, { text: "他独特且鲜活", type: 'C' }, { text: "他看透了真相", type: 'A' }] }
    ];

    const results = {
        'E': { title: "深渊凝视者 (Explorer)", desc: "你的内在没有边界感。对你而言，生活不是用来守护的，而是用来挥霍和探索的。你的潜意识里藏着一种“流浪者”基因，任何试图禁锢你的围墙都会让你窒息。你的天赋在于能在混乱中找到新出路，但孤独也是你必须支付的代价。" },
        'G': { title: "永恒守望者 (Guardian)", desc: "你是秩序的化身，是抵御混乱的最后防线。你的潜意识里认为，世界是脆弱的，需要你的守护。你对风险极其敏感，这让你成为最可靠的伴侣和伙伴。但在保护别人的同时，别忘了偶尔也卸下盔甲，让你自己的灵魂透透气。" },
        'C': { title: "镜中创造者 (Creator)", desc: "你不需要去寻找世界，因为你本身就在创造世界。你的潜意识里，真实生活往往是平庸的，唯有通过你的感知重塑后的世界才值得一活。你拥有极高的审美敏感度和共情力，但也容易陷入自我纠结的深渊。你是天生的异类，更是纯粹的灵魂。" },
        'A': { title: "真理架构师 (Analyst)", desc: "感性对你来说是一种干扰信号。你的潜意识渴望看穿表象下的齿轮是如何运作的。你习惯于保持距离观察人类，这种上帝视角让你拥有惊人的洞察力。然而，最深层的真相往往不藏在代码里，而是在那些无法被逻辑解释的瞬间。" }
    };

    let current = 0;
    let scores = { 'E':0, 'G':0, 'C':0, 'A':0 };

    function initQuiz() {
        if(current >= questions.length) {
            document.getElementById('quiz-page').style.display='none';
            document.getElementById('result-page').style.display='block';
            return;
        }
        let q = questions[current];
        document.getElementById('q-num').innerText = `STEP ${current+1}/18`;
        document.getElementById('q-text').innerText = q.q;
        document.getElementById('bar').style.width = ((current+1)/18*100) + '%';
        
        const container = document.getElementById('options');
        container.innerHTML = '';
        q.options.forEach(o => {
            const btn = document.createElement('button');
            btn.className = 'option-btn';
            btn.innerText = o.text;
            btn.onclick = () => { scores[o.type]++; current++; initQuiz(); };
            container.appendChild(btn);
        });
    }

    function startTyping() {
        document.getElementById('unlock-box').style.display = 'none';
        document.getElementById('report-box').style.display = 'block';
        
        let max = 0, type = 'E';
        for(let t in scores) { if(scores[t] > max) { max = scores[t]; type = t; } }
        const res = results[type];
        
        document.getElementById('r-title').innerText = res.title;
        const descEl = document.getElementById('r-desc');
        descEl.classList.add('typing');
        
        let i = 0;
        function typeWriter() {
            if (i < res.desc.length) {
                descEl.innerHTML += res.desc.charAt(i);
                i++;
                setTimeout(typeWriter, 50);
            } else {
                descEl.classList.remove('typing');
            }
        }
        typeWriter();
    }

    initQuiz();
</script>
</body>
</html>
