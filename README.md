<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>HCT | 潜意识实验室</title>
    <style>
        /* 高级黑背景 */
        body {
            margin: 0; padding: 0;
            background: #0f0f0f; /* 深沉的黑色 */
            font-family: 'Helvetica Neue', Arial, sans-serif;
            display: flex; justify-content: center; align-items: center;
            min-height: 100vh; color: #e0e0e0;
        }

        .container {
            width: 90%; max-width: 400px;
            padding: 40px 25px;
            background: #1a1a1a;
            border-radius: 2px; /* 这种直角微圆的设计更有日本工业设计感 */
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            border-top: 4px solid #e74c3c; /* 标志性的红条 */
        }

        .progress-num { font-size: 10px; letter-spacing: 2px; color: #666; margin-bottom: 5px; }
        
        .bar-bg { width: 100%; height: 2px; background: #333; margin-bottom: 30px; }
        .bar-fill { height: 100%; background: #e74c3c; width: 0%; transition: 0.5s; }

        h2 { font-size: 18px; line-height: 1.6; margin-bottom: 30px; font-weight: 300; }

        .btn {
            display: block; width: 100%;
            padding: 15px; margin-bottom: 15px;
            background: transparent;
            border: 1px solid #333;
            color: #bbb; cursor: pointer;
            text-align: left; font-size: 14px;
            transition: all 0.3s;
        }

        .btn:hover { border-color: #e74c3c; color: #fff; background: #222; }

        #result-box { display: none; text-align: center; }
        .res-title { font-size: 24px; color: #e74c3c; margin-bottom: 20px; letter-spacing: 4px; }
        .res-desc { font-size: 14px; line-height: 2; color: #999; text-align: justify; }

        .unlock-btn {
            margin-top: 30px; background: #e74c3c; color: #fff;
            border: none; padding: 15px; width: 100%; cursor: pointer;
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
        <div class="res-title" id="r-title"></div>
        <div class="res-desc" id="r-desc"></div>
        <button class="unlock-btn" onclick="location.reload()">重新测试</button>
    </div>
</div>

<script>
    // 这里依然使用我们之前的 18 道题逻辑
    const questions = [
        { q: "1. 梦境投射：在一扇紧锁的门前，你直觉门后藏着什么？", options: [{ text: "一个从未见过的奇异新世界", type: 'E' }, { text: "你最珍视的宝物", type: 'G' }, { text: "一个正在看着你的“另一个自己”", type: 'C' }, { text: "解开人生谜团的答案之书", type: 'A' }] },
        // ... (后续17道题逻辑同上，为了简洁此处略，你可以直接粘贴你现有的questions数组内容)
    ];

    // (之前的逻辑代码继续...)
</script>
</body>
</html>
