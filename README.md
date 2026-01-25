<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TV DOKAN BD - লাইভ টিভি চ্যানেল</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #2563eb;
            --secondary: #1e40af;
            --dark: #0f172a;
            --light: #f8fafc;
            --gray: #64748b;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', 'Kalpurush', Arial, sans-serif;
            background: var(--dark);
            color: var(--light);
            line-height: 1.6;
        }
        
        /* হেডার */
        .header {
            background: linear-gradient(135deg, var(--dark), #1e293b);
            padding: 15px 30px;
            border-bottom: 3px solid var(--primary);
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            position: sticky;
            top: 0;
            z-index: 1000;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .logo h1 {
            font-size: 28px;
            background: linear-gradient(90deg, #60a5fa, #3b82f6);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 2px 10px rgba(59, 130, 246, 0.3);
        }
        
        .logo i {
            font-size: 32px;
            color: var(--primary);
        }
        
        .time-date {
            text-align: right;
            background: rgba(30, 41, 59, 0.8);
            padding: 10px 20px;
            border-radius: 10px;
            border: 1px solid var(--primary);
        }
        
        #currentTime {
            font-size: 24px;
            font-weight: bold;
            color: #60a5fa;
        }
        
        #currentDate {
            font-size: 14px;
            color: var(--gray);
            margin-top: 5px;
        }
        
        /* নেভিগেশন */
        .nav-tabs {
            background: rgba(30, 41, 59, 0.9);
            padding: 15px;
            display: flex;
            gap: 10px;
            overflow-x: auto;
            white-space: nowrap;
            border-bottom: 2px solid #334155;
        }
        
        .tab-btn {
            background: #475569;
            border: none;
            color: white;
            padding: 10px 20px;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 14px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .tab-btn.active, .tab-btn:hover {
            background: var(--primary);
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(37, 99, 235, 0.4);
        }
        
        /* মূল কন্টেন্ট */
        .main-container {
            max-width: 1400px;
            margin: 20px auto;
            padding: 0 20px;
            display: grid;
            grid-template-columns: 1fr 350px;
            gap: 25px;
        }
        
        /* ভিডিও প্লেয়ার */
        .video-container {
            background: #000;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            position: relative;
        }
        
        #videoPlayer {
            width: 100%;
            height: 500px;
            background: #000;
        }
        
        .player-overlay {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient(transparent, rgba(0,0,0,0.8));
            padding: 20px;
            color: white;
        }
        
        #currentChannelName {
            font-size: 24px;
            margin-bottom: 5px;
            color: #fff;
        }
        
        .channel-quality {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }
        
        .quality-btn {
            background: rgba(255,255,255,0.2);
            border: none;
            color: white;
            padding: 5px 15px;
            border-radius: 15px;
            cursor: pointer;
            font-size: 12px;
        }
        
        .quality-btn.active {
            background: var(--primary);
        }
        
        /* চ্যানেল লিস্ট */
        .channels-sidebar {
            background: rgba(30, 41, 59, 0.8);
            border-radius: 15px;
            padding: 20px;
            height: fit-content;
            max-height: 600px;
            overflow-y: auto;
        }
        
        .channel-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        
        .channel-item {
            background: #475569;
            border: none;
            color: white;
            padding: 15px;
            border-radius: 10px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 15px;
            transition: all 0.3s;
            text-align: left;
        }
        
        .channel-item:hover {
            background: #3b82f6;
            transform: translateX(5px);
        }
        
        .channel-item.active {
            background: var(--primary);
            box-shadow: 0 5px 15px rgba(37, 99, 235, 0.4);
        }
        
        .channel-logo {
            width: 40px;
            height: 40px;
            background: rgba(255,255,255,0.1);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
        }
        
        .channel-info {
            flex-grow: 1;
        }
        
        .channel-name {
            font-weight: bold;
            font-size: 16px;
        }
        
        .channel-category {
            font-size: 12px;
            color: #94a3b8;
            margin-top: 3px;
        }
        
        /* লোডিং */
        .loading {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
            color: white;
        }
        
        .spinner {
            border: 4px solid rgba(255,255,255,0.3);
            border-top: 4px solid var(--primary);
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 0 auto 15px;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* ফুটার */
        .footer {
            background: #1e293b;
            padding: 30px;
            text-align: center;
            margin-top: 40px;
            border-top: 2px solid var(--primary);
        }
        
        .stats {
            display: flex;
            justify-content: center;
            gap: 40px;
            margin: 20px 0;
        }
        
        .stat-item {
            text-align: center;
        }
        
        .stat-number {
            font-size: 32px;
            color: var(--primary);
            font-weight: bold;
        }
        
        /* রেস্পন্সিভ */
        @media (max-width: 1024px) {
            .main-container {
                grid-template-columns: 1fr;
            }
            
            #videoPlayer {
                height: 400px;
            }
        }
        
        @media (max-width: 768px) {
            .header {
                flex-direction: column;
                text-align: center;
                gap: 15px;
            }
            
            #videoPlayer {
                height: 300px;
            }
            
            .stats {
                flex-direction: column;
                gap: 20px;
            }
        }
        
        /* স্ক্রলবার */
        ::-webkit-scrollbar {
            width: 8px;
        }
        
        ::-webkit-scrollbar-track {
            background: #1e293b;
        }
        
        ::-webkit-scrollbar-thumb {
            background: var(--primary);
            border-radius: 4px;
        }
    </style>
</head>
<body>
    <!-- হেডার -->
    <header class="header">
        <div class="logo">
            <i class="fas fa-tv"></i>
            <h1>TV DOKAN BD</h1>
        </div>
        <div class="time-date">
            <div id="currentTime">08:53:10 AM</div>
            <div id="currentDate">Sunday | Jan 25, 2026</div>
        </div>
    </header>
    
    <!-- ট্যাব নেভিগেশন -->
    <nav class="nav-tabs">
        <button class="tab-btn active" onclick="filterChannels('all')">
            <i class="fas fa-globe"></i> সকল চ্যানেল
        </button>
        <button class="tab-btn" onclick="filterChannels('cricket')">
            <i class="fas fa-baseball-ball"></i> ক্রিকেট
        </button>
        <button class="tab-btn" onclick="filterChannels('bangla')">
            <i class="fas fa-flag"></i> বাংলা
        </button>
        <button class="tab-btn" onclick="filterChannels('news')">
            <i class="fas fa-newspaper"></i> নিউজ
        </button>
        <button class="tab-btn" onclick="filterChannels('islamic')">
            <i class="fas fa-mosque"></i> ইসলামিক
        </button>
        <button class="tab-btn" onclick="filterChannels('sports')">
            <i class="fas fa-futbol"></i> স্পোর্টস
        </button>
        <button class="tab-btn" onclick="filterChannels('entertainment')">
            <i class="fas fa-film"></i> বিনোদন
        </button>
        <button class="tab-btn" onclick="filterChannels('movie')">
            <i class="fas fa-video"></i> মুভি
        </button>
    </nav>
    
    <!-- মূল কন্টেন্ট -->
    <div class="main-container">
        <!-- ভিডিও প্লেয়ার -->
        <div class="video-container">
            <video id="videoPlayer" controls preload="auto"></video>
            
            <div class="player-overlay">
                <div id="currentChannelName">দয়া করে একটি চ্যানেল নির্বাচন করুন</div>
                <div class="channel-quality">
                    <button class="quality-btn active" onclick="changeQuality('auto')">Auto</button>
                    <button class="quality-btn" onclick="changeQuality('720p')">720p</button>
                    <button class="quality-btn" onclick="changeQuality('480p')">480p</button>
                    <button class="quality-btn" onclick="changeQuality('360p')">360p</button>
                </div>
            </div>
            
            <div id="loading" class="loading" style="display: none;">
                <div class="spinner"></div>
                <p>চ্যানেল লোড হচ্ছে...</p>
            </div>
        </div>
        
        <!-- চ্যানেল সাইডবার -->
        <div class="channels-sidebar">
            <h3 style="margin-bottom: 20px; color: #60a5fa;">
                <i class="fas fa-list"></i> চ্যানেল তালিকা
                <span id="channelCount" style="float: right; font-size: 14px;">0 চ্যানেল</span>
            </h3>
            
            <div class="channel-list" id="channelList">
                <!-- চ্যানেলগুলো ডাইনামিকভাবে লোড হবে -->
            </div>
        </div>
    </div>
    
    <!-- ফুটার -->
    <footer class="footer">
        <div class="stats">
            <div class="stat-item">
                <div class="stat-number" id="totalChannels">150+</div>
                <div>লাইভ চ্যানেল</div>
            </div>
            <div class="stat-item">
                <div class="stat-number" id="onlineUsers">2.5K+</div>
                <div>অনলাইন ইউজার</div>
            </div>
            <div class="stat-item">
                <div class="stat-number">24/7</div>
                <div>লাইভ স্ট্রিমিং</div>
            </div>
        </div>
        
        <p style="color: #94a3b8; margin-top: 20px;">
            © 2026 TV DOKAN BD | All TV Channels Live Streaming
        </p>
    </footer>

    <!-- HLS.js লাইব্রেরি -->
    <script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>

    <script>
        // রিয়েল লাইভ M3U8 লিঙ্ক ডেটাবেস (নতুন আপডেটেড)
        const channelsData = [
            {
                id: 1,
                name: "SONY AATH",
                logo: "📺",
                category: ["bangla", "entertainment"],
                qualities: {
                    auto: "https://d2q8p4pe5spbak.cloudfront.net/bpk-tv/starplus/index.m3u8",
                    "720p": "https://d2q8p4pe5spbak.cloudfront.net/bpk-tv/starplus/index.m3u8",
                    "480p": "https://d2q8p4pe5spbak.cloudfront.net/bpk-tv/starplus/index.m3u8"
                },
                isLive: true,
                viewers: "125K"
            },
            {
                id: 2,
                name: "CricHD 1",
                logo: "🏏",
                category: ["cricket", "sports"],
                qualities: {
                    auto: "https://crichdstreaming.xyz/embed7",
                    "720p": "https://crichdstreaming.xyz/embed7"
                },
                isLive: true,
                viewers: "350K"
            },
            {
                id: 3,
                name: "CricHD 2",
                logo: "🏏",
                category: ["cricket", "sports"],
                qualities: {
                    auto: "https://crichdstreaming.xyz/embed2",
                    "720p": "https://crichdstreaming.xyz/embed2"
                },
                isLive: true,
                viewers: "280K"
            },
            {
                id: 4,
                name: "BTV National",
                logo: "🇧🇩",
                category: ["bangla", "news"],
                qualities: {
                    auto: "https://cdn.appv2.xyz/btvweb/live.m3u8",
                    "720p": "https://cdn.appv2.xyz/btvweb/live.m3u8"
                },
                isLive: true,
                viewers: "180K"
            },
            {
                id: 5,
                name: "Channel I",
                logo: "📡",
                category: ["bangla", "entertainment"],
                qualities: {
                    auto: "https://cdn.appv2.xyz/channeliweb/live.m3u8",
                    "720p": "https://cdn.appv2.xyz/channeliweb/live.m3u8"
                },
                isLive: true,
                viewers: "95K"
            },
            {
                id: 6,
                name: "ATN Bangla",
                logo: "🎬",
                category: ["bangla", "entertainment"],
                qualities: {
                    auto: "https://cdn.appv2.xyz/atnbanglaweb/live.m3u8",
                    "720p": "https://cdn.appv2.xyz/atnbanglaweb/live.m3u8"
                },
                isLive: true,
                viewers: "88K"
            },
            {
                id: 7,
                name: "NTV",
                logo: "📻",
                category: ["bangla", "news"],
                qualities: {
                    auto: "https://cdn.appv2.xyz/ntvweb/live.m3u8",
                    "720p": "https://cdn.appv2.xyz/ntvweb/live.m3u8"
                },
                isLive: true,
                viewers: "120K"
            },
            {
                id: 8,
                name: "BBC News",
                logo: "🌍",
                category: ["news", "all"],
                qualities: {
                    auto: "https://stream.live.vc.bbcmedia.co.uk/bbc_world_service",
                    "720p": "https://stream.live.vc.bbcmedia.co.uk/bbc_world_service"
                },
                isLive: true,
                viewers: "250K"
            },
            {
                id: 9,
                name: "Al Jazeera",
                logo: "📰",
                category: ["news", "islamic"],
                qualities: {
                    auto: "https://live-hls-web-aje.getaj.net/AJE/index.m3u8",
                    "720p": "https://live-hls-web-aje.getaj.net/AJE/index.m3u8"
                },
                isLive: true,
                viewers: "200K"
            },
            {
                id: 10,
                name: "CNN International",
                logo: "🎤",
                category: ["news", "all"],
                qualities: {
                    auto: "https://turnerlive.warnermediacdn.com/hls/live/586495/cnngo/cnn_slate/VIDEO_0_3564000.m3u8",
                    "720p": "https://turnerlive.warnermediacdn.com/hls/live/586495/cnngo/cnn_slate/VIDEO_0_3564000.m3u8"
                },
                isLive: true,
                viewers: "300K"
            },
            {
                id: 11,
                name: "Peace TV",
                logo: "🕌",
                category: ["islamic"],
                qualities: {
                    auto: "https://streamer1.streamhost.org/salive/peacetvhls/index.m3u8",
                    "720p": "https://streamer1.streamhost.org/salive/peacetvhls/index.m3u8"
                },
                isLive: true,
                viewers: "500K"
            },
            {
                id: 12,
                name: "Makkah TV",
                logo: "🕋",
                category: ["islamic"],
                qualities: {
                    auto: "https://cdn.appv2.xyz/makkahweb/live.m3u8",
                    "720p": "https://cdn.appv2.xyz/makkahweb/live.m3u8"
                },
                isLive: true,
                viewers: "450K"
            },
            {
                id: 13,
                name: "Star Sports 1",
                logo: "⚽",
                category: ["sports", "cricket"],
                qualities: {
                    auto: "https://d2q8p4pe5spbak.cloudfront.net/bpk-tv/Starsports1/index.m3u8",
                    "720p": "https://d2q8p4pe5spbak.cloudfront.net/bpk-tv/Starsports1/index.m3u8"
                },
                isLive: true,
                viewers: "220K"
            },
            {
                id: 14,
                name: "Sony TV",
                logo: "🔴",
                category: ["entertainment", "all"],
                qualities: {
                    auto: "https://d2q8p4pe5spbak.cloudfront.net/bpk-tv/Sony/index.m3u8",
                    "720p": "https://d2q8p4pe5spbak.cloudfront.net/bpk-tv/Sony/index.m3u8"
                },
                isLive: true,
                viewers: "150K"
            },
            {
                id: 15,
                name: "Zee Bangla",
                logo: "⭐",
                category: ["bangla", "entertainment"],
                qualities: {
                    auto: "https://d2q8p4pe5spbak.cloudfront.net/bpk-tv/Zeebangla/index.m3u8",
                    "720p": "https://d2q8p4pe5spbak.cloudfront.net/bpk-tv/Zeebangla/index.m3u8"
                },
                isLive: true,
                viewers: "110K"
            },
            {
                id: 16,
                name: "Star Jalsha",
                logo: "✨",
                category: ["bangla", "entertainment"],
                qualities: {
                    auto: "https://d2q8p4pe5spbak.cloudfront.net/bpk-tv/Starjalsha/index.m3u8",
                    "720p": "https://d2q8p4pe5spbak.cloudfront.net/bpk-tv/Starjalsha/index.m3u8"
                },
                isLive: true,
                viewers: "130K"
            },
            {
                id: 17,
                name: "Colors TV",
                logo: "🎨",
                category: ["entertainment", "all"],
                qualities: {
                    auto: "https://d2q8p4pe5spbak.cloudfront.net/bpk-tv/Colors/index.m3u8",
                    "720p": "https://d2q8p4pe5spbak.cloudfront.net/bpk-tv/Colors/index.m3u8"
                },
   
