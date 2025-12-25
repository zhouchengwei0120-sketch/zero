<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>ZERO | 潜意识实验室</title>
    <style>
        body {
            margin: 0; padding: 0;
            background: #0a0a0a;
            font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
            display: flex; justify-content: center; align-items: center;
            min-height: 100vh; color: #d0d0d0;
        }
        .container {
            width: 85%; max-width: 400px;
            padding: 40px 30px;
            background: #111;
            border-radius: 4px;
            box-shadow: 0 15px 50px rgba(0,0,0,0.8);
            border-top: 3px solid #e74c3c;
        }
        .progress-num { font-size: 10px; letter-spacing: 3px; color: #555; margin-bottom: 8px; }
        .bar-bg { width: 100%; height: 1px; background: #222; margin-bottom: 35px; }
        .bar-fill { height: 100%; background: #e74c3c; width: 0%; transition: 0.6s cubic-bezier(0.4, 0, 0.2, 1); }
        h2 { font-size: 18px; line-height: 1.7; margin-bottom: 35px; font-weight: 400; letter-spacing: 0.5px; }
        .btn {
            display: block; width: 100%;
            padding: 16px 20px; margin-bottom: 12px;
            background: transparent;
            border: 1px solid #222;
            color: #999; cursor: pointer;
            text-align: left; font-size: 14px;
            transition: all 0.3s ease;
        }
        .btn:hover { border-color: #e74c3c; color: #fff; background: #161616; padding-left: 25px; }
        #result-box { display: none; text-align: center; }
        .res-title { font-size: 26px; color: #e74c3c; margin-bottom: 25px; letter-spacing: 5px; font-weight: bold; }
        .res-desc { font-size: 14px; line-height: 2; color: #888; text-align: justify; margin-bottom: 30px; }
        .reload-btn {
            background: #e74c3c; color: #fff; border: none;
            padding: 15px; width: 100%; cursor: pointer; font-size: 14px; letter-spacing: 2px;
        }
    </style>
</head>
<body>

<div class="container">
    <div id="quiz">
        <div class="progress-num" id="p-num">LOADING 01/18</div>
        <div class="bar-bg"><div class="bar-fill" id="p-bar"></div></div>
        <h2 id="q-text">正在初始化深度心理模型...</h2>
        <div id="options"></div>
    </div>

    <div id="result-box">
        <p style="font-size: 10px; color: #555; letter-spacing: 2px;">ANALYSIS RESULT</p>
        <div class="res-title" id="r-title"></div>
        <div class="res-desc" id="r-desc"></div>
        <button class="reload-btn" onclick="location.reload()">RESTART TEST</button>
    </div>
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
        'E': { title: "探索者", desc: "你天生对未知充满渴望。你的潜意识里认为，生命在于不断的扩张和体验。你无视束缚，是那种能在危机中发现新大陆的人。但也请注意，有时停下来巩固已有成果也很重要。" },
        'G': { title: "守护者", desc: "你追求秩序与安全感。你是社会和家庭的基石，极其可靠。你的潜意识里，保护你所爱的一切是最高使命。你拥有强大的风控能力，但有时会因为过度谨慎而显得保守。" },
        'C': { title: "创作者", desc: "你是独特的代名词。你的内心有一面多棱镜，能看到别人看不到的色彩。你通过表达自我来获得存在感。你极其敏感，这给了你无限的灵感，但也让你容易受情绪波动影响。" },
        'A': { title: "分析师", desc: "逻辑和真相是你的盔甲。你不轻易被情绪煽动，习惯于拆解事物背后的真相。你的潜意识里，知识就是力量。你可能是冷静的观察者，但别忘了生活除了逻辑，还有温情。" }
    };

    let current = 0;
    let scores = { 'E':0, 'G':0, 'C':0, 'A':0 };

    function render() {
        if(current >= questions.length) {
            document.getElementById('quiz').style.display = 'none';
            document.getElementById('result-box').style.display = 'block';
            let max = 0, type = 'E';
            for(let t in scores) { if(scores[t] > max) { max = scores[t]; type = t; } }
            document.getElementById('r-title').innerText = results[type].title;
            document.getElementById('r-desc').innerText = results[type].desc;
            return;
        }
        const q = questions[current];
        document.getElementById('p-num').innerText = `LOADING ${String(current+1).padStart(2, '0')}/18`;
        document.getElementById('p-bar').style.width = ((current+1)/18*100) + '%';
        document.getElementById('q-text').innerText = q.q;
        const opts = document.getElementById('options');
        opts.innerHTML = '';
        q.options.forEach(o => {
            const b = document.createElement('button');
            b.className = 'btn';
            b.innerText = o.text;
            b.onclick = () => { scores[o.type]++; current++; render(); };
            opts.appendChild(b);
        });
    }
    render();
</script>
</body>
</html>
