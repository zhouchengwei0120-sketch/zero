<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ZERO AI | 全球领先的数字人与多语言视频转换平台</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background-color: #050505; color: #ffffff; font-family: 'Inter', sans-serif; }
        .hero-gradient {
            background: radial-gradient(circle at 50% 50%, #1e1e1e 0%, #050505 100%);
        }
        .accent-color { color: #3b82f6; }
        .glass-card {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.05);
            transition: all 0.3s ease;
        }
        .glass-card:hover {
            border-color: #3b82f6;
            transform: translateY(-5px);
        }
        .api-code {
            background: #111;
            padding: 20px;
            border-radius: 8px;
            font-family: 'Courier New', Courier, monospace;
            font-size: 14px;
            color: #10b981;
        }
    </style>
</head>
<body class="hero-gradient">

    <nav class="flex justify-between items-center px-8 py-6 max-w-7xl mx-auto">
        <div class="text-2xl font-bold tracking-tighter">ZERO <span class="accent-color">AI</span></div>
        <div class="hidden md:flex space-x-8 text-sm text-gray-400">
            <a href="#services" class="hover:text-white">核心服务</a>
            <a href="#api" class="hover:text-white">API 文档</a>
            <a href="#pricing" class="hover:text-white">价格方案</a>
        </div>
        <button class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded-full text-sm transition">立即开始</button>
    </nav>

    <header class="max-w-7xl mx-auto px-8 py-20 text-center">
        <h1 class="text-5xl md:text-7xl font-extrabold mb-6 leading-tight">
            让您的视频 <br> <span class="accent-color">通晓全球语言</span>
        </h1>
        <p class="text-gray-400 text-lg mb-10 max-w-2xl mx-auto">
            利用尖端 AI 技术，实现数字人全自动化建模与视频多语言一键转换。打破文化隔阂，助力品牌全球出海。
        </p>
        
        <div class="relative w-full max-w-4xl mx-auto aspect-video glass-card rounded-2xl flex items-center justify-center overflow-hidden">
            <div class="absolute inset-0 bg-gradient-to-tr from-blue-900/20 to-transparent"></div>
            <div class="text-center">
                <div class="w-16 h-16 bg-blue-600 rounded-full flex items-center justify-center mx-auto mb-4 cursor-pointer hover:scale-110 transition">
                    <svg class="w-8 h-8 text-white" fill="currentColor" viewBox="0 0 20 20"><path d="M4.5 3.5l11 6.5-11 6.5z"></path></svg>
                </div>
                <p class="text-sm text-gray-500">点击观看 AI 演示效果</p>
            </div>
        </div>
    </header>

    <section id="services" class="max-w-7xl mx-auto px-8 py-20">
        <div class="grid md:grid-cols-3 gap-8">
            <div class="glass-card p-8 rounded-2xl">
                <div class="w-12 h-12 bg-blue-500/10 rounded-lg flex items-center justify-center mb-6">
                    <svg class="w-6 h-6 accent-color" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path d="M3 5h12M9 19H5a2 2 0 01-2-2V7a2 2 0 012-2h4m10 0h2a2 2 0 012 2v10a2 2 0 01-2 2h-2m-4-8a4 4 0 11-8 0 4 4 0 018 0z"></path></svg>
                </div>
                <h3 class="text-xl font-bold mb-4">视频多语言翻译</h3>
                <p class="text-gray-400 text-sm leading-relaxed">一键将原视频翻译为 40+ 种语言，完美克隆原声，口型同步率高达 99%。</p>
            </div>
            <div class="glass-card p-8 rounded-2xl">
                <div class="w-12 h-12 bg-purple-500/10 rounded-lg flex items-center justify-center mb-6">
                    <svg class="w-6 h-6 text-purple-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"></path></svg>
                </div>
                <h3 class="text-xl font-bold mb-4">企业级数字人定制</h3>
                <p class="text-gray-400 text-sm leading-relaxed">根据照片或真人口述，分钟级生成超写实数字人模型，支持 24/7 自动播报。</p>
            </div>
            <div class="glass-card p-8 rounded-2xl">
                <div class="w-12 h-12 bg-green-500/10 rounded-lg flex items-center justify-center mb-6">
                    <svg class="w-6 h-6 text-green-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"></path></svg>
                </div>
                <h3 class="text-xl font-bold mb-4">AI 创作 API</h3>
                <p class="text-gray-400 text-sm leading-relaxed">强大的 Restful API 接口，支持将我们的 AI 能力无缝集成到您的自有业务系统中。</p>
            </div>
        </div>
    </section>

    <section id="api" class="max-w-7xl mx-auto px-8 py-20 bg-[#080808] rounded-3xl border border-white/5">
        <div class="grid md:grid-cols-2 gap-12 items-center">
            <div>
                <h2 class="text-3xl font-bold mb-6">专为开发者设计</h2>
                <p class="text-gray-400 mb-6">我们的 API 简单、高效。只需几行代码，即可在您的服务器上调用全球最顶尖的视频处理模型。</p>
                <ul class="space-y-4 text-sm text-gray-300">
                    <li class="flex items-center"><svg class="w-4 h-4 mr-2 text-green-500" fill="currentColor" viewBox="0 0 20 20"><path d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"></path></svg> 毫秒级响应速度</li>
                    <li class="flex items-center"><svg class="w-4 h-4 mr-2 text-green-500" fill="currentColor" viewBox="0 0 20 20"><path d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"></path></svg> 全球 CDN 加速部署</li>
                </ul>
            </div>
            <div class="api-code">
                <span class="text-gray-500">// POST /v1/video/translate</span><br>
                {<br>
                &nbsp;&nbsp;"video_url": "https://zero-ai.com/demo.mp4",<br>
                &nbsp;&nbsp;"source_lang": "zh",<br>
                &nbsp;&nbsp;"target_lang": "jp",<br>
                &nbsp;&nbsp;"avatar_sync": true<br>
                }<br><br>
                <span class="text-gray-500">// Response: 200 OK</span><br>
                { "status": "processing", "id": "task_8892" }
            </div>
        </div>
    </section>

    <footer class="max-w-7xl mx-auto px-8 py-12 text-center text-gray-600 text-xs border-t border-white/5 mt-20">
        <p>© 2025 ZERO AI LABS. 全球多语言视频处理专家.</p>
        <p class="mt-2">日本 · 东京 | 海外市场业务部</p>
    </footer>

</body>
</html>
