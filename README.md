<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>武汉 · 江湖之城</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@300;400;500;700;900&display=swap" rel="stylesheet">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        :root {
            --primary: #c41e3a;
            --secondary: #1a5f7a;
            --accent: #e8b923;
            --dark: #1a1a2e;
            --light: #f8f9fa;
            --text: #2d3436;
            --text-light: #636e72;
        }
        
        body {
            font-family: 'Noto Sans SC', -apple-system, BlinkMacSystemFont, 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
            background: var(--light);
            color: var(--text);
            overflow-x: hidden;
            -webkit-tap-highlight-color: transparent;
            line-height: 1.6;
        }
        
        /* 加载动画 */
        .loader {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: var(--dark);
            z-index: 9999;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            transition: opacity 0.8s ease, visibility 0.8s;
        }
        .loader.hidden { opacity: 0; visibility: hidden; pointer-events: none; }
        .loader-text {
            color: var(--accent);
            font-size: 32px;
            font-weight: 900;
            letter-spacing: 12px;
            animation: pulse 1.5s ease-in-out infinite;
            font-family: 'Noto Sans SC', sans-serif;
        }
        .loader-sub {
            color: rgba(255,255,255,0.5);
            font-size: 13px;
            margin-top: 16px;
            letter-spacing: 6px;
            font-weight: 300;
        }
        @keyframes pulse {
            0%, 100% { opacity: 0.3; transform: scale(0.95); }
            50% { opacity: 1; transform: scale(1.05); }
        }
        
        /* 导航 */
        .nav {
            position: fixed;
            top: 0; left: 0; width: 100%;
            padding: 12px 20px;
            z-index: 100;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.4s ease;
        }
        .nav.scrolled {
            background: rgba(26,26,46,0.92);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            box-shadow: 0 2px 20px rgba(0,0,0,0.15);
        }
        .nav-logo {
            color: white;
            font-size: 18px;
            font-weight: 900;
            letter-spacing: 4px;
            font-family: 'Noto Sans SC', sans-serif;
        }
        .nav-menu {
            display: flex;
            gap: 20px;
        }
        .nav-menu a {
            color: rgba(255,255,255,0.85);
            text-decoration: none;
            font-size: 13px;
            font-weight: 500;
            transition: all 0.3s;
            position: relative;
        }
        .nav-menu a::after {
            content: '';
            position: absolute;
            bottom: -4px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--accent);
            transition: width 0.3s;
            border-radius: 1px;
        }
        .nav-menu a:hover { color: var(--accent); }
        .nav-menu a:hover::after { width: 100%; }
        
        /* 首屏 */
        .hero {
            height: 100vh;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }
        .hero-bg-img {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            object-fit: cover;
            filter: brightness(0.35);
            transform: scale(1.1);
            animation: heroZoom 20s ease-in-out infinite alternate;
        }
        @keyframes heroZoom {
            0% { transform: scale(1.1) translate(0,0); }
            50% { transform: scale(1.15) translate(-1%, -1%); }
            100% { transform: scale(1.1) translate(1%, 1%); }
        }
        .hero-overlay {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(to bottom, rgba(26,26,46,0.4) 0%, rgba(26,26,46,0.7) 60%, rgba(26,26,46,0.95) 100%);
            z-index: 1;
        }
        
        .hero-content {
            position: relative;
            z-index: 2;
            text-align: center;
            padding: 0 24px;
            max-width: 520px;
        }
        .hero-badge {
            display: inline-block;
            padding: 6px 18px;
            border: 1px solid rgba(232,185,35,0.6);
            color: var(--accent);
            font-size: 12px;
            font-weight: 500;
            letter-spacing: 4px;
            margin-bottom: 28px;
            border-radius: 20px;
            animation: fadeInUp 1s ease;
            font-family: 'Noto Sans SC', sans-serif;
        }
        .hero-title {
            font-size: 56px;
            color: white;
            font-weight: 900;
            letter-spacing: 14px;
            margin-bottom: 16px;
            line-height: 1.2;
            animation: fadeInUp 1s ease 0.2s both;
            text-shadow: 0 4px 30px rgba(0,0,0,0.4);
            font-family: 'Noto Sans SC', sans-serif;
        }
        .hero-title span {
            display: block;
            font-size: 22px;
            letter-spacing: 8px;
            color: var(--accent);
            margin-top: 12px;
            font-weight: 400;
            text-shadow: none;
        }
        .hero-desc {
            color: rgba(255,255,255,0.75);
            font-size: 15px;
            line-height: 1.9;
            max-width: 340px;
            margin: 0 auto 36px;
            animation: fadeInUp 1s ease 0.4s both;
            font-weight: 300;
        }
        .hero-btn {
            display: inline-block;
            padding: 14px 44px;
            background: var(--primary);
            color: white;
            text-decoration: none;
            border-radius: 30px;
            font-size: 15px;
            font-weight: 700;
            letter-spacing: 3px;
            animation: fadeInUp 1s ease 0.6s both;
            box-shadow: 0 6px 24px rgba(196,30,58,0.4);
            transition: all 0.3s;
            border: none;
            cursor: pointer;
        }
        .hero-btn:active { transform: scale(0.96); box-shadow: 0 2px 12px rgba(196,30,58,0.3); }
        
        .scroll-hint {
            position: absolute;
            bottom: 32px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 2;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
            animation: bounce 2s infinite;
            color: rgba(255,255,255,0.5);
            font-size: 12px;
            letter-spacing: 2px;
            font-weight: 300;
        }
        .scroll-hint::after {
            content: '↓';
            font-size: 20px;
        }
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateX(-50%) translateY(0); }
            40% { transform: translateX(-50%) translateY(-10px); }
            60% { transform: translateX(-50%) translateY(-5px); }
        }
        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* 通用板块 */
        .section {
            padding: 60px 20px;
            max-width: 520px;
            margin: 0 auto;
        }
        .section-header {
            text-align: center;
            margin-bottom: 44px;
        }
        .section-tag {
            display: inline-block;
            color: var(--primary);
            font-size: 11px;
            letter-spacing: 4px;
            margin-bottom: 10px;
            font-weight: 700;
            text-transform: uppercase;
        }
        .section-title {
            font-size: 30px;
            font-weight: 900;
            color: var(--dark);
            letter-spacing: 3px;
            font-family: 'Noto Sans SC', sans-serif;
        }
        .section-desc {
            color: var(--text-light);
            font-size: 14px;
            margin-top: 10px;
            font-weight: 400;
        }
        
        /* 数据卡片 */
        .stats-bar {
            display: flex;
            justify-content: space-around;
            padding: 28px 16px;
            background: white;
            margin: -30px 16px 0;
            border-radius: 20px;
            box-shadow: 0 12px 40px rgba(0,0,0,0.08);
            position: relative;
            z-index: 10;
        }
        .stat-item {
            text-align: center;
        }
        .stat-num {
            font-size: 26px;
            font-weight: 900;
            color: var(--primary);
            display: block;
            font-family: 'Noto Sans SC', sans-serif;
            letter-spacing: 1px;
        }
        .stat-label {
            font-size: 11px;
            color: var(--text-light);
            margin-top: 4px;
            font-weight: 400;
        }
        
        /* 景点卡片 */
        .spot-card {
            background: white;
            border-radius: 20px;
            overflow: hidden;
            margin-bottom: 24px;
            box-shadow: 0 4px 24px rgba(0,0,0,0.06);
            opacity: 0;
            transform: translateY(40px);
            transition: all 0.7s cubic-bezier(0.25, 0.46, 0.45, 0.94);
        }
        .spot-card.visible {
            opacity: 1;
            transform: translateY(0);
        }
        .spot-img-wrap {
            width: 100%;
            height: 220px;
            position: relative;
            overflow: hidden;
            background: #e0e0e0;
        }
        .spot-img-wrap img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
            transition: transform 0.6s ease;
        }
        .spot-card:active .spot-img-wrap img { transform: scale(1.05); }
        .spot-img-title {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            padding: 40px 20px 16px;
            background: linear-gradient(to top, rgba(0,0,0,0.7), transparent);
            color: white;
            font-size: 22px;
            font-weight: 900;
            letter-spacing: 3px;
            font-family: 'Noto Sans SC', sans-serif;
        }
        .spot-body {
            padding: 22px;
        }
        .spot-tags {
            display: flex;
            gap: 8px;
            margin-bottom: 14px;
            flex-wrap: wrap;
        }
        .spot-tag {
            padding: 5px 12px;
            background: rgba(196,30,58,0.06);
            color: var(--primary);
            font-size: 11px;
            font-weight: 500;
            border-radius: 20px;
            border: 1px solid rgba(196,30,58,0.1);
        }
        .spot-text {
            color: #555;
            font-size: 14px;
            line-height: 1.8;
            font-weight: 400;
        }
        .spot-meta {
            display: flex;
            justify-content: space-between;
            margin-top: 18px;
            padding-top: 18px;
            border-top: 1px solid #f0f0f0;
        }
        .spot-meta-item {
            text-align: center;
            flex: 1;
        }
        .spot-meta-label {
            font-size: 11px;
            color: #aaa;
            margin-bottom: 4px;
            font-weight: 400;
        }
        .spot-meta-value {
            font-size: 13px;
            color: var(--dark);
            font-weight: 700;
        }
        
        /* 轮播图 */
        .carousel-section { padding-top: 20px; }
        .carousel {
            position: relative;
            overflow: hidden;
            border-radius: 20px;
            margin-bottom: 16px;
            box-shadow: 0 8px 30px rgba(0,0,0,0.12);
        }
        .carousel-track {
            display: flex;
            transition: transform 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
        }
        .carousel-slide {
            min-width: 100%;
            height: 260px;
            position: relative;
            overflow: hidden;
        }
        .carousel-slide img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
        }
        .carousel-slide-overlay {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(to bottom, rgba(0,0,0,0.2), rgba(0,0,0,0.6));
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: white;
            text-align: center;
            padding: 20px;
        }
        .carousel-slide-title {
            font-size: 22px;
            font-weight: 900;
            letter-spacing: 4px;
            margin-bottom: 8px;
            text-shadow: 0 2px 10px rgba(0,0,0,0.3);
            font-family: 'Noto Sans SC', sans-serif;
        }
        .carousel-slide-sub {
            font-size: 13px;
            opacity: 0.9;
            font-weight: 300;
            letter-spacing: 2px;
        }
        .carousel-dots {
            display: flex;
            justify-content: center;
            gap: 8px;
            margin-top: 16px;
        }
        .carousel-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: #ddd;
            transition: all 0.3s;
            cursor: pointer;
        }
        .carousel-dot.active {
            background: var(--primary);
            width: 24px;
            border-radius: 4px;
        }
        
        /* 美食板块 */
        .food-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 14px;
        }
        .food-card {
            background: white;
            border-radius: 16px;
            overflow: hidden;
            box-shadow: 0 2px 16px rgba(0,0,0,0.05);
            opacity: 0;
            transform: scale(0.92);
            transition: all 0.5s ease;
        }
        .food-card.visible {
            opacity: 1;
            transform: scale(1);
        }
        .food-img-wrap {
            width: 100%;
            height: 130px;
            overflow: hidden;
            background: #f0f0f0;
        }
        .food-img-wrap img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
            transition: transform 0.4s ease;
        }
        .food-card:active .food-img-wrap img { transform: scale(1.08); }
        .food-body {
            padding: 14px;
            text-align: center;
        }
        .food-name {
            font-size: 15px;
            font-weight: 700;
            color: var(--dark);
            margin-bottom: 6px;
            font-family: 'Noto Sans SC', sans-serif;
        }
        .food-desc {
            font-size: 12px;
            color: var(--text-light);
            line-height: 1.5;
            font-weight: 400;
        }
        
        /* 门店推荐 */
        .shop-section {
            margin-top: 40px;
        }
        .shop-section .section-header {
            margin-bottom: 24px;
        }
        .shop-card {
            background: white;
            border-radius: 16px;
            overflow: hidden;
            margin-bottom: 16px;
            box-shadow: 0 2px 16px rgba(0,0,0,0.06);
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.6s ease;
        }
        .shop-card.visible {
            opacity: 1;
            transform: translateY(0);
        }
        .shop-img-wrap {
            width: 100%;
            height: 180px;
            overflow: hidden;
            background: #e8e8e8;
        }
        .shop-img-wrap img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
        }
        .shop-body {
            padding: 18px;
        }
        .shop-name {
            font-size: 17px;
            font-weight: 900;
            color: var(--dark);
            margin-bottom: 6px;
            font-family: 'Noto Sans SC', sans-serif;
        }
        .shop-address {
            font-size: 13px;
            color: var(--text-light);
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 4px;
        }
        .shop-tags {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }
        .shop-tag {
            padding: 4px 12px;
            background: rgba(196,30,58,0.06);
            color: var(--primary);
            font-size: 12px;
            border-radius: 20px;
            font-weight: 500;
            border: 1px solid rgba(196,30,58,0.08);
        }
        .shop-note {
            margin-top: 12px;
            padding-top: 12px;
            border-top: 1px dashed #eee;
            font-size: 12px;
            color: #888;
            line-height: 1.6;
        }
        
        /* 地图容器 */
        .map-wrap {
            background: white;
            border-radius: 16px;
            overflow: hidden;
            margin: 20px 0;
            box-shadow: 0 4px 20px rgba(0,0,0,0.06);
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.6s ease;
        }
        .map-wrap.visible {
            opacity: 1;
            transform: translateY(0);
        }
        .map-wrap img {
            width: 100%;
            display: block;
        }
        .map-caption {
            padding: 14px 18px;
            font-size: 13px;
            color: #666;
            text-align: center;
            border-top: 1px solid #f5f5f5;
            background: #fafafa;
            font-weight: 400;
        }
        
        /* 攻略时间轴 */
        .timeline {
            position: relative;
            padding-left: 32px;
        }
        .timeline::before {
            content: '';
            position: absolute;
            left: 9px;
            top: 0;
            bottom: 0;
            width: 2px;
            background: linear-gradient(to bottom, var(--primary), var(--accent));
            border-radius: 1px;
        }
        .timeline-item {
            position: relative;
            margin-bottom: 28px;
            opacity: 0;
            transform: translateX(-20px);
            transition: all 0.6s ease;
        }
        .timeline-item.visible {
            opacity: 1;
            transform: translateX(0);
        }
        .timeline-dot {
            position: absolute;
            left: -27px;
            top: 6px;
            width: 18px;
            height: 18px;
            border-radius: 50%;
            background: white;
            border: 3px solid var(--primary);
            box-shadow: 0 0 0 4px rgba(196,30,58,0.08);
            z-index: 2;
        }
        .timeline-content {
            background: white;
            padding: 20px;
            border-radius: 16px;
            box-shadow: 0 2px 16px rgba(0,0,0,0.04);
        }
        .timeline-day {
            color: var(--primary);
            font-size: 12px;
            font-weight: 900;
            margin-bottom: 8px;
            letter-spacing: 2px;
            font-family: 'Noto Sans SC', sans-serif;
        }
        .timeline-title {
            font-size: 17px;
            font-weight: 700;
            margin-bottom: 10px;
            color: var(--dark);
            font-family: 'Noto Sans SC', sans-serif;
        }
        .timeline-text {
            font-size: 13px;
            color: #666;
            line-height: 1.8;
            font-weight: 400;
        }
        .timeline-map {
            margin-top: 14px;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 2px 8px rgba(0,0,0,0.06);
            background: #f8f9fa;
        }
        .timeline-map img {
            width: 100%;
            display: block;
        }
        .timeline-map-caption {
            padding: 10px;
            font-size: 12px;
            color: #888;
            text-align: center;
            background: white;
        }
        
        /* 交通卡片 */
        .trans-card {
            background: white;
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 14px;
            display: flex;
            align-items: center;
            gap: 18px;
            box-shadow: 0 2px 16px rgba(0,0,0,0.04);
            transition: transform 0.3s;
        }
        .trans-card:active { transform: scale(0.98); }
        .trans-icon {
            width: 50px;
            height: 50px;
            border-radius: 14px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 26px;
            flex-shrink: 0;
            background: #f8f9fa;
        }
        .trans-info h4 {
            font-size: 15px;
            font-weight: 700;
            margin-bottom: 4px;
            color: var(--dark);
            font-family: 'Noto Sans SC', sans-serif;
        }
        .trans-info p {
            font-size: 13px;
            color: var(--text-light);
            font-weight: 400;
        }
        
        /* 页脚 */
        .footer {
            background: var(--dark);
            color: white;
            padding: 48px 24px;
            text-align: center;
            margin-top: 20px;
        }
        .footer-logo {
            font-size: 26px;
            font-weight: 900;
            letter-spacing: 8px;
            margin-bottom: 14px;
            font-family: 'Noto Sans SC', sans-serif;
        }
        .footer-text {
            color: rgba(255,255,255,0.45);
            font-size: 13px;
            line-height: 2;
            font-weight: 300;
        }
        .footer-divider {
            width: 40px;
            height: 2px;
            background: var(--accent);
            margin: 20px auto;
            border-radius: 1px;
        }
        
        /* 返回顶部 */
        .back-top {
            position: fixed;
            bottom: 28px;
            right: 24px;
            width: 48px;
            height: 48px;
            border-radius: 50%;
            background: var(--primary);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            box-shadow: 0 6px 20px rgba(196,30,58,0.4);
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.3s;
            z-index: 99;
            cursor: pointer;
            border: none;
            font-weight: 700;
        }
        .back-top.show {
            opacity: 1;
            transform: translateY(0);
        }
    </style>
</head>
<body>

    <!-- 加载页 -->
    <div class="loader" id="loader">
        <div class="loader-text">武汉</div>
        <div class="loader-sub">江湖之城 · 等你探索</div>
    </div>

    <!-- 导航 -->
    <nav class="nav" id="nav">
        <div class="nav-logo">武汉</div>
        <div class="nav-menu">
            <a href="#spots">景点</a>
            <a href="#food">美食</a>
            <a href="#guide">攻略</a>
        </div>
    </nav>

    <!-- 首屏 -->
    <section class="hero">
        <img class="hero-bg-img" src="https://kimi-web-img.moonshot.cn/img/picn.huitu.com/edcdd47837ea8ec3e9a10e064b17b041de26ba72.jpg" alt="武汉长江大桥夜景">
        <div class="hero-overlay"></div>
        <div class="hero-content">
            <div class="hero-badge">WUHAN · 2025</div>
            <h1 class="hero-title">
                武汉
                <span>大江大湖大武汉</span>
            </h1>
            <p class="hero-desc">
                黄鹤楼前吹玉笛，江城五月落梅花。<br>
                一座承载千年记忆的城市，等你来看樱花、吃热干面。
            </p>
            <a href="#spots" class="hero-btn">开始探索</a>
        </div>
        <div class="scroll-hint">滑动探索</div>
    </section>

    <!-- 数据栏 -->
    <div class="stats-bar">
        <div class="stat-item">
            <span class="stat-num">3500+</span>
            <div class="stat-label">年建城史</div>
        </div>
        <div class="stat-item">
            <span class="stat-num">166</span>
            <div class="stat-label">湖泊数量</div>
        </div>
        <div class="stat-item">
            <span class="stat-num">11</span>
            <div class="stat-label">跨江大桥</div>
        </div>
        <div class="stat-item">
            <span class="stat-num">130万</span>
            <div class="stat-label">在校大学生</div>
        </div>
    </div>

    <!-- 景点 -->
    <section class="section" id="spots">
        <div class="section-header">
            <div class="section-tag">DESTINATION</div>
            <h2 class="section-title">必游景点</h2>
            <p class="section-desc">江城最美的风景，都在这里</p>
        </div>

        <div class="spot-card">
            <div class="spot-img-wrap">
                <img src="https://kimi-web-img.moonshot.cn/img/p5.img.cctvpic.com/38a3781f27bb51fdc7e443d0cf76899c08b4b0b2.jpg" alt="黄鹤楼">
                <div class="spot-img-title">黄鹤楼</div>
            </div>
            <div class="spot-body">
                <div class="spot-tags">
                    <span class="spot-tag">5A景区</span>
                    <span class="spot-tag">历史古迹</span>
                    <span class="spot-tag">江南三大名楼</span>
                </div>
                <p class="spot-text">
                    "昔人已乘黄鹤去，此地空余黄鹤楼"。始建于三国时期，历代文人墨客在此留下千古名篇。登楼远眺，武汉三镇尽收眼底，长江大桥飞架南北。
                </p>
                <div class="spot-meta">
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">门票</div>
                        <div class="spot-meta-value">¥70</div>
                    </div>
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">建议时长</div>
                        <div class="spot-meta-value">2-3小时</div>
                    </div>
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">最佳时间</div>
                        <div class="spot-meta-value">傍晚</div>
                    </div>
                </div>
            </div>
        </div>

        <div class="spot-card">
            <div class="spot-img-wrap">
                <img src="https://kimi-web-img.moonshot.cn/img/bpic.588ku.com/b4d885ea09039d398b286f47be0f56716e8b5a77" alt="东湖风景区">
                <div class="spot-img-title">东湖风景区</div>
            </div>
            <div class="spot-body">
                <div class="spot-tags">
                    <span class="spot-tag">5A景区</span>
                    <span class="spot-tag">城市湖泊</span>
                    <span class="spot-tag">骑行圣地</span>
                </div>
                <p class="spot-text">
                    中国第二大城中湖，水域面积达33平方公里。东湖绿道全长101.98公里，是国内首条城区内5A级旅游景区绿道。磨山樱花园拥有上万株樱花，春季必打卡。
                </p>
                <div class="spot-meta">
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">门票</div>
                        <div class="spot-meta-value">免费</div>
                    </div>
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">建议时长</div>
                        <div class="spot-meta-value">半天</div>
                    </div>
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">最佳时间</div>
                        <div class="spot-meta-value">3-4月</div>
                    </div>
                </div>
            </div>
        </div>

        <div class="spot-card">
            <div class="spot-img-wrap">
                <img src="https://kimi-web-img.moonshot.cn/img/inews.gtimg.com/33ab9e13f3c667cdeb3a6fc0cc8cd9579bb86b82" alt="武汉大学">
                <div class="spot-img-title">武汉大学</div>
            </div>
            <div class="spot-body">
                <div class="spot-tags">
                    <span class="spot-tag">百年名校</span>
                    <span class="spot-tag">樱花大道</span>
                    <span class="spot-tag">民国建筑</span>
                </div>
                <p class="spot-text">
                    中国最美大学之一，坐拥珞珈山，环绕东湖水。每年3月下旬至4月初，樱花大道上千株樱花盛开，粉色花海与古典建筑交相辉映，吸引全国游客慕名而来。
                </p>
                <div class="spot-meta">
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">门票</div>
                        <div class="spot-meta-value">免费预约</div>
                    </div>
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">建议时长</div>
                        <div class="spot-meta-value">2小时</div>
                    </div>
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">最佳时间</div>
                        <div class="spot-meta-value">3月下旬</div>
                    </div>
                </div>
            </div>
        </div>

        <div class="spot-card">
            <div class="spot-img-wrap">
                <img src="https://kimi-web-img.moonshot.cn/img/pic.people.com.cn/0d538458ee5dab318e3fc12517736d6ede580c5f.jpg" alt="户部巷与江滩">
                <div class="spot-img-title">户部巷 & 汉口江滩</div>
            </div>
            <div class="spot-body">
                <div class="spot-tags">
                    <span class="spot-tag">美食街</span>
                    <span class="spot-tag">汉味早点</span>
                    <span class="spot-tag">百年老巷</span>
                </div>
                <p class="spot-text">
                    "汉味早点第一巷"，长150米的百年老巷，汇聚了热干面、豆皮、糊汤粉、面窝等所有武汉经典小吃。夜晚可步行至江滩，看知音号演绎民国风情。
                </p>
                <div class="spot-meta">
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">门票</div>
                        <div class="spot-meta-value">免费</div>
                    </div>
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">建议时长</div>
                        <div class="spot-meta-value">1-2小时</div>
                    </div>
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">最佳时间</div>
                        <div class="spot-meta-value">早晨/夜晚</div>
                    </div>
                </div>
            </div>
        </div>

        <div class="spot-card">
            <div class="spot-img-wrap">
                <img src="https://kimi-web-img.moonshot.cn/img/www.idwuhan.com/6317df21779c9d19bd5f9e9f6066220fa21439d1.jpg" alt="江汉路步行街">
                <div class="spot-img-title">江汉路步行街</div>
            </div>
            <div class="spot-body">
                <div class="spot-tags">
                    <span class="spot-tag">商业步行街</span>
                    <span class="spot-tag">民国建筑</span>
                    <span class="spot-tag">夜景</span>
                </div>
                <p class="spot-text">
                    中国最长的步行街，全长1600米。两侧矗立着众多民国时期的欧式建筑，被誉为"武汉二十世纪建筑博物馆"。夜晚霓虹璀璨，是感受武汉繁华的最佳去处。
                </p>
                <div class="spot-meta">
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">门票</div>
                        <div class="spot-meta-value">免费</div>
                    </div>
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">建议时长</div>
                        <div class="spot-meta-value">2-3小时</div>
                    </div>
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">最佳时间</div>
                        <div class="spot-meta-value">夜晚</div>
                    </div>
                </div>
            </div>
        </div>

        <div class="spot-card">
            <div class="spot-img-wrap">
                <img src="https://kimi-web-img.moonshot.cn/img/www.wuhan.gov.cn/ea69ffd89b67765ef76d87e8bba8e7e76c7c25b8.jpg" alt="古琴台">
                <div class="spot-img-title">古琴台</div>
            </div>
            <div class="spot-body">
                <div class="spot-tags">
                    <span class="spot-tag">人文古迹</span>
                    <span class="spot-tag">知音文化</span>
                    <span class="spot-tag">伯牙子期</span>
                </div>
                <p class="spot-text">
                    "高山流水遇知音"的发源地，纪念俞伯牙与钟子期的千古友谊。古琴台与黄鹤楼、晴川阁并称武汉三大名胜，环境清幽，是感受中国传统文化的好去处。
                </p>
                <div class="spot-meta">
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">门票</div>
                        <div class="spot-meta-value">¥15</div>
                    </div>
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">建议时长</div>
                        <div class="spot-meta-value">1小时</div>
                    </div>
                    <div class="spot-meta-item">
                        <div class="spot-meta-label">最佳时间</div>
                        <div class="spot-meta-value">午后</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 轮播推荐 -->
    <section class="section carousel-section">
        <div class="section-header">
            <div class="section-tag">SEASONS</div>
            <h2 class="section-title">四季武汉</h2>
            <p class="section-desc">不同季节，不同的美</p>
        </div>
        <div class="carousel" id="carousel">
            <div class="carousel-track" id="carouselTrack">
                <div class="carousel-slide">
                    <img src="https://kimi-web-img.moonshot.cn/img/inews.gtimg.com/33ab9e13f3c667cdeb3a6fc0cc8cd9579bb86b82" alt="春季樱花">
                    <div class="carousel-slide-overlay">
                        <div class="carousel-slide-title">🌸 春季 · 樱花烂漫</div>
                        <div class="carousel-slide-sub">武大樱花 · 东湖樱园</div>
                    </div>
                </div>
                <div class="carousel-slide">
                    <img src="https://kimi-web-img.moonshot.cn/img/news.cjn.cn/a9c1179122d20b7a4911e31d0a93c3f8eae2fad4.jpeg" alt="夏季绿道">
                    <div class="carousel-slide-overlay">
                        <div class="carousel-slide-title">🌿 夏季 · 荷塘月色</div>
                        <div class="carousel-slide-sub">东湖绿道 · 江滩纳凉</div>
                    </div>
                </div>
                <div class="carousel-slide">
                    <img src="https://kimi-web-img.moonshot.cn/img/img.daimg.com/42d9a5dac2495e70de95624811db18f95155cae5.jpg" alt="秋季黄鹤楼">
                    <div class="carousel-slide-overlay">
                        <div class="carousel-slide-title">🍁 秋季 · 层林尽染</div>
                        <div class="carousel-slide-sub">黄鹤秋色 · 龟山红叶</div>
                    </div>
                </div>
                <div class="carousel-slide">
                    <img src="https://kimi-web-img.moonshot.cn/img/www.wbu.edu.cn/ab1c0756d2b29fffdb352b58644fbae79d483de6.jpg" alt="冬季江滩">
                    <div class="carousel-slide-overlay">
                        <div class="carousel-slide-title">❄️ 冬季 · 江城夜色</div>
                        <div class="carousel-slide-sub">江滩夜景 · 灯火阑珊</div>
                    </div>
                </div>
            </div>
        </div>
        <div class="carousel-dots" id="carouselDots">
            <div class="carousel-dot active"></div>
            <div class="carousel-dot"></div>
            <div class="carousel-dot"></div>
            <div class="carousel-dot"></div>
        </div>
    </section>

    <!-- 美食 -->
    <section class="section" id="food">
        <div class="section-header">
            <div class="section-tag">CUISINE</div>
            <h2 class="section-title">汉味美食</h2>
            <p class="section-desc">过早一个月不重样，不是传说</p>
        </div>

        <div class="food-grid">
            <div class="food-card">
                <div class="food-img-wrap">
                    <img src="https://kimi-web-img.moonshot.cn/img/assets.699pic.com/c7b3d45bcc672f4814166ac8120d81f1425ac3d1.v1" alt="热干面">
                </div>
                <div class="food-body">
                    <div class="food-name">热干面</div>
                    <div class="food-desc">武汉城市名片<br>芝麻酱浓香四溢</div>
                </div>
            </div>
            <div class="food-card">
                <div class="food-img-wrap">
                    <img src="https://kimi-web-img.moonshot.cn/img/imgcache.dealmoon.com/32629406f83fcc730fe7df8c6b656d5e7e5102b1.jpg" alt="三鲜豆皮">
                </div>
                <div class="food-body">
                    <div class="food-name">三鲜豆皮</div>
                    <div class="food-desc">金黄酥脆外皮<br>糯米肉丁馅料</div>
                </div>
            </div>
            <div class="food-card">
                <div class="food-img-wrap">
                    <img src="https://kimi-web-img.moonshot.cn/img/img.alicdn.com/2d194308d41e488e23fd6b8aa7cb3f1de9c7fb62.webp" alt="周黑鸭">
                </div>
                <div class="food-body">
                    <div class="food-name">周黑鸭</div>
                    <div class="food-desc">甜辣鲜香<br>全国闻名的卤味</div>
                </div>
            </div>
            <div class="food-card">
                <div class="food-img-wrap">
                    <img src="https://kimi-web-img.moonshot.cn/img/imagepphcloud.thepaper.cn/bd6f28f3ac06890dad98bc7be1914ebbba910099.jpg" alt="糊汤粉">
                </div>
                <div class="food-body">
                    <div class="food-name">糊汤粉</div>
                    <div class="food-desc">鲜鱼熬汤<br>配油条绝佳</div>
                </div>
            </div>
            <div class="food-card">
                <div class="food-img-wrap">
                    <img src="https://kimi-web-img.moonshot.cn/img/www.wuhan.gov.cn/619b0a442eb9d16fd762c8c6388ebd06215a543c.jpg" alt="面窝">
                </div>
                <div class="food-body">
                    <div class="food-name">面窝</div>
                    <div class="food-desc">米浆炸制<br>外酥内软中空</div>
                </div>
            </div>
            <div class="food-card">
                <div class="food-img-wrap">
                    <img src="https://kimi-web-img.moonshot.cn/img/sw.wuhan.gov.cn/00eb25d1e187fe68a4761a04f39eaed59997d262.jpg" alt="汤包">
                </div>
                <div class="food-body">
                    <div class="food-name">汤包/烧梅</div>
                    <div class="food-desc">四季美汤包<br>重油烧梅</div>
                </div>
            </div>
        </div>

        <!-- 招牌老店 -->
        <div class="shop-section">
            <div class="section-header" style="margin-bottom: 24px;">
                <div class="section-tag">LEGENDARY SHOPS</div>
                <h3 style="font-size: 22px; font-weight: 900; color: var(--dark); letter-spacing: 2px;">必吃老字号</h3>
                <p class="section-desc">本地人排队也要吃的招牌门店</p>
            </div>
            
            <div class="shop-card">
                <div class="shop-img-wrap">
                    <img src="https://kimi-web-img.moonshot.cn/img/dynamic-media-cdn.tripadvisor.com/428f1680dfe1535390b53159839c4259a180a0aa.jpg" alt="蔡林记门店">
                </div>
                <div class="shop-body">
                    <div class="shop-name">蔡林记（户部巷店）</div>
                    <div class="shop-address">📍 武昌区户部巷28号 · 人均 ¥15</div>
                    <div class="shop-tags">
                        <span class="shop-tag">全料热干面</span>
                        <span class="shop-tag">湖北老字号</span>
                        <span class="shop-tag">始创于1928年</span>
                    </div>
                    <div class="shop-note">
                        武汉热干面的代名词，黑芝麻酱是灵魂。推荐全料热干面+蛋酒组合。户部巷店最老牌，但排队较长；江汉路步行街也有分店。
                    </div>
                </div>
            </div>
            
            <div class="shop-card">
                <div class="shop-img-wrap">
                    <img src="https://kimi-web-img.moonshot.cn/img/resources.zhayieye.com/e75626eb1acbc9fed7c0caae6f51b70a5b75ba54.jpg" alt="严老幺门店">
                </div>
                <div class="shop-body">
                    <div class="shop-name">严老幺烧麦（前进四路店）</div>
                    <div class="shop-address">📍 江汉区前进四路219号 · 人均 ¥25</div>
                    <div class="shop-tags">
                        <span class="shop-tag">重油烧麦</span>
                        <span class="shop-tag">三鲜豆皮</span>
                        <span class="shop-tag">天天排队</span>
                    </div>
                    <div class="shop-note">
                        武汉"过早界"的顶流，重油烧麦胡椒味浓、糯米油润，三鲜豆皮现做现卖。建议早上7点前到，避开高峰排队。
                    </div>
                </div>
            </div>
        </div>

        <!-- 美食地图 -->
        <div class="map-wrap" id="foodMap">
            <img src="https://kimi-web-img.moonshot.cn/img/www.wuhan.gov.cn/65eda09f72d3945a2e61da6db7c7757eaaa386a6.jpg" alt="武汉美食地图">
            <div class="map-caption">武汉美食分布手绘地图 · 过早集中在汉口兰陵路、山海关路及武昌户部巷</div>
        </div>
        
        <div class="map-wrap">
            <img src="https://kimi-web-img.moonshot.cn/img/sw.wuhan.gov.cn/b3e882334e839ae3ecef84bcf79344e01d6e315b.jpg" alt="武汉美食详细地图">
            <div class="map-caption">武汉名菜名点美食地图 · 覆盖吉庆街、万松园、粮道街等美食街区</div>
        </div>
    </section>

    <!-- 行程攻略 -->
    <section class="section" id="guide">
        <div class="section-header">
            <div class="section-tag">ITINERARY</div>
            <h2 class="section-title">推荐行程</h2>
            <p class="section-desc">三天两夜，玩转武汉精华</p>
        </div>

        <!-- 总览地图 -->
        <div class="map-wrap" id="guideMap">
            <img src="https://kimi-web-img.moonshot.cn/img/pica.zhimg.com/37ad9a7af0e4eac0a25eeec29328947d8ec4ca12.jpg" alt="武汉旅游景点地图">
            <div class="map-caption">武汉旅游景点分布总览 · 长江将城市分为武昌、汉口、汉阳三镇</div>
        </div>

        <div class="timeline">
            <div class="timeline-item">
                <div class="timeline-dot"></div>
                <div class="timeline-content">
                    <div class="timeline-day">DAY 1</div>
                    <div class="timeline-title">武昌人文线</div>
                    <div class="timeline-text">
                        上午：户部巷过早（蔡林记热干面+老通城豆皮）→ 步行至黄鹤楼登高望远<br>
                        下午：辛亥革命博物馆 → 昙华林文艺漫步（百年老建筑+文创小店）<<br>
                        晚上：长江大桥看夜景 → 中华路码头坐轮渡到汉口（1.5元）
                    </div>
                    <div class="timeline-map">
                        <img src="https://kimi-web-img.moonshot.cn/img/pica.zhimg.com/37ad9a7af0e4eac0a25eeec29328947d8ec4ca12.jpg" alt="武昌景点地图">
                        <div class="timeline-map-caption">武昌核心景点分布 · 户部巷、黄鹤楼、昙华林步行可达</div>
                    </div>
                </div>
            </div>
            <div class="timeline-item">
                <div class="timeline-dot"></div>
                <div class="timeline-content">
                    <div class="timeline-day">DAY 2</div>
                    <div class="timeline-title">东湖自然线</div>
                    <div class="timeline-text">
                        上午：武汉大学（樱花季需预约/平时看老建筑）→ 凌波门看东湖<br>
                        下午：东湖绿道骑行（湖中道6公里人气最高）→ 磨山景区/东湖樱花园<br>
                        晚上：湖北省博物馆（越王勾践剑、曾侯乙编钟）→ 楚河汉街吃饭
                    </div>
                    <div class="timeline-map">
                        <img src="https://kimi-web-img.moonshot.cn/img/imgbdb3.bendibao.com/ebf1309bb34b84742aecd1240f093094213dea76.png" alt="东湖绿道地图">
                        <div class="timeline-map-caption">东湖绿道骑行路线图 · 湖中道6公里为精华段，沿途可赏湖光山色</div>
                    </div>
                </div>
            </div>
            <div class="timeline-item">
                <div class="timeline-dot"></div>
                <div class="timeline-content">
                    <div class="timeline-day">DAY 3</div>
                    <div class="timeline-title">汉口风情线</div>
                    <div class="timeline-text">
                        上午：古琴台 → 晴川阁（隔江相望黄鹤楼，"晴川历历汉阳树"）<<br>
                        下午：江汉路步行街（民国建筑博物馆） → 黎黄陂路喝咖啡（俄租界风情）<<br>
                        晚上：汉口江滩散步 → 知音号游船（沉浸式民国实景演出，强烈推荐）
                    </div>
                    <div class="timeline-map">
                        <img src="https://kimi-web-img.moonshot.cn/img/sw.wuhan.gov.cn/b3e882334e839ae3ecef84bcf79344e01d6e315b.jpg" alt="汉口美食地图">
                        <div class="timeline-map-caption">汉口风情区与美食分布 · 江汉路、黎黄陂路、江滩一线串联</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 交通 -->
    <section class="section">
        <div class="section-header">
            <div class="section-tag">TRANSPORT</div>
            <h2 class="section-title">交通指南</h2>
            <p class="section-desc">大武汉出行，看这一篇就够了</p>
        </div>

        <div class="trans-card">
            <div class="trans-icon">✈️</div>
            <div class="trans-info">
                <h4>天河机场</h4>
                <p>地铁2号线直达市区，约45分钟到江汉路</p>
            </div>
        </div>
        <div class="trans-card">
            <div class="trans-icon">🚄</div>
            <div class="trans-info">
                <h4>三大火车站</h4>
                <p>汉口站（市中心）、武汉站（高铁）、武昌站（普速）</p>
            </div>
        </div>
        <div class="trans-card">
            <div class="trans-icon">🚇</div>
            <div class="trans-info">
                <h4>地铁网络</h4>
                <p>11条线路覆盖全城，支付宝/微信扫码乘车</p>
            </div>
        </div>
        <div class="trans-card">
            <div class="trans-icon">🚢</div>
            <div class="trans-info">
                <h4>过江轮渡</h4>
                <p>中华路↔武汉关，1.5元体验最地道的江城风情</p>
            </div>
        </div>

        <!-- 地铁线路图 -->
        <div class="map-wrap" style="margin-top: 24px;">
            <img src="https://kimi-web-img.moonshot.cn/img/imgbdb4.bendibao.com/2af95e04a171a4c5f7a10e171efc2fd1940351f2.png" alt="武汉地铁线路图">
            <div class="map-caption">武汉轨道交通线网图 · 11条线路覆盖三镇，景点基本都可地铁直达</div>
        </div>

        <!-- 轮渡码头实景 -->
        <div class="map-wrap">
            <img src="https://kimi-web-img.moonshot.cn/img/m.cnhubei.com/fc449b579d8f714d92793d27d8155b97cde6a785.jpeg" alt="中华路码头">
            <div class="map-caption">中华路码头夜景 · 1.5元过江，甲板上可赏长江大桥与两岸灯光秀</div>
        </div>
    </section>

    <!-- 页脚 -->
    <footer class="footer">
        <div class="footer-logo">武汉</div>
        <div class="footer-divider"></div>
        <p class="footer-text">
            大江大湖大武汉<br>
            愿你在这里遇见最美的风景<br><br>
            设计制作 · 2025
        </p>
    </footer>

    <!-- 返回顶部 -->
    <div class="back-top" id="backTop">↑</div>

    <script>
        // 加载动画
        window.addEventListener('load', () => {
            setTimeout(() => {
                document.getElementById('loader').classList.add('hidden');
            }, 1800);
        });

        // 导航栏滚动效果
        const nav = document.getElementById('nav');
        const backTop = document.getElementById('backTop');
        window.addEventListener('scroll', () => {
            if (window.scrollY > 60) {
                nav.classList.add('scrolled');
                backTop.classList.add('show');
            } else {
                nav.classList.remove('scrolled');
                backTop.classList.remove('show');
            }
        });

        // 返回顶部
        backTop.addEventListener('click', () => {
            window.scrollTo({ top: 0, behavior: 'smooth' });
        });

        // 平滑滚动
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({ behavior: 'smooth', block: 'start' });
                }
            });
        });

        // 滚动显示动画
        const observerOptions = {
            threshold: 0.08,
            rootMargin: '0px 0px -40px 0px'
        };
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('visible');
                }
            });
        }, observerOptions);
        document.querySelectorAll('.spot-card, .food-card, .timeline-item, .shop-card, .map-wrap').forEach(el => {
            observer.observe(el);
        });

        // 轮播图
        let currentSlide = 0;
        const track = document.getElementById('carouselTrack');
        const dots = document.querySelectorAll('.carousel-dot');
        const totalSlides = 4;

        function goToSlide(index) {
            currentSlide = index;
            track.style.transform = `translateX(-${index * 100}%)`;
            dots.forEach((dot, i) => dot.classList.toggle('active', i === index));
        }
        setInterval(() => goToSlide((currentSlide + 1) % totalSlides), 5000);
        dots.forEach((dot, index) => dot.addEventListener('click', () => goToSlide(index)));

        // 触摸滑动
        let startX = 0;
        let isDragging = false;
        track.addEventListener('touchstart', (e) => { startX = e.touches[0].clientX; isDragging = true; });
        track.addEventListener('touchend', (e) => {
            if (!isDragging) return;
            const diff = startX - e.changedTouches[0].clientX;
            if (Math.abs(diff) > 50) {
                if (diff > 0 && currentSlide < totalSlides - 1) goToSlide(currentSlide + 1);
                else if (diff < 0 && currentSlide > 0) goToSlide(currentSlide - 1);
            }
            isDragging = false;
        });
    </script>
</body>
</html>
