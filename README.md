<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.2/css/all.min.css" rel="stylesheet">
    <title>游戏页面</title>
    <style>
        /* 能量条样式 */
       .energy-bar {
            background-color: #e5e7eb;
            border-radius: 0.25rem;
            overflow: hidden;
            box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
        }

       .energy-level {
            background: linear-gradient(to right, #3b82f6, #60a5fa);
            height: 100%;
            width: 50%;
            transition: width 0.3s ease;
            border-radius: 0.25rem;
            position: relative;
            animation: shine 2s infinite;
        }

        @keyframes shine {
            0% {
                box-shadow: 0 0 5px #3b82f6;
            }
            50% {
                box-shadow: 0 0 20px #3b82f6;
            }
            100% {
                box-shadow: 0 0 5px #3b82f6;
            }
        }

       .energy-level::after {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 20%;
            height: 100%;
            background: rgba(255, 255, 255, 0.3);
            transform: skewX(-20deg);
            animation: moveShine 2s infinite;
        }

        @keyframes moveShine {
            0% {
                left: -20%;
            }
            100% {
                left: 100%;
            }
        }

        /* 人物形象样式 */
       .character-image {
            width: 200px;
            height: auto;
            margin: 20px auto;
            display: block;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
        }

        /* 任务栏样式 */
       .task-bar {
            background-color: #f3f4f6;
            border-radius: 10px;
            padding: 20px;
            margin: 20px auto;
            width: 90%; /* 增大宽度 */
            max-width: 800px; /* 增大最大宽度 */
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

       .task {
            background-color: white;
            border-radius: 5px;
            padding: 10px;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
        }

       .task-name {
            font-weight: bold;
        }

       .task-status {
            color: #3b82f6;
        }

       .task-uncompleted {
            background-color: #f8d7da;
            color: #721c24;
        }

       .task-in-progress {
            background-color: #fff3cd;
            color: #856404;
        }

       .task-completed {
            background-color: #d4edda;
            color: #155724;
            text-decoration: line-through;
        }

        /* 激活状态的导航链接样式 */
       .active {
            background-color: #1e40af;
            font-weight: 900;
        }

        /* 新的布局样式 */
       .flex-container {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
        }

       .left-content {
            width: 60%;
        }

       .right-content {
            width: 40%;
        }

        /* 右上角首页链接样式 */
       .home-link {
            position: fixed;
            top: 20px;
            right: 20px;
            background-color: rgba(0, 0, 0, 0.3);
            color: white;
            padding: 10px 15px;
            border-radius: 5px;
            display: flex;
            align-items: center;
            gap: 5px;
            opacity: 0.8;
            transition: opacity 0.3s ease;
        }

       .home-link:hover {
            opacity: 1;
        }
    </style>
    <script>
        window.onload = function () {
            if (!localStorage.getItem('isLoggedIn')) {
                window.location.href = 'login.html';
            }
            const currentPage = window.location.pathname.split('/').pop();
            const navLinks = document.querySelectorAll('.nav-link');
            navLinks.forEach(link => {
                if (link.getAttribute('href') === currentPage) {
                    link.classList.add('active');
                }
            });
        };
    </script>
</head>

<body class="bg-gray-100 font-sans">
    <!-- 左上角玩家信息 -->
    <div class="fixed top-4 left-4 flex items-center space-x-2">
        <img src="https://picsum.photos/50/50" alt="玩家头像" class="rounded-full">
        <div class="energy-bar h-4 w-24">
            <div class="energy-level"></div>
        </div>
    </div>

    <!-- 右上角首页链接 -->
    <a href="index.html" class="home-link">
        <i class="fa-solid fa-house"></i> 首页
    </a>

    <!-- 导航模块 -->
    <div class="flex justify-center space-x-4 py-8">
        <a href="index.html" class="bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded transition duration-300 nav-link active">首页</a>
        <a href="map.html" class="bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded transition duration-300 nav-link">地图</a>
        <a href="ranking.html" class="bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded transition duration-300 nav-link">排行榜</a>
    </div>

    <!-- 页面内容 -->
    <div class="container mx-auto px-4 py-8 flex-container">
        <div class="left-content">
            <h1 class="text-3xl font-bold text-center text-gray-800">欢迎来到游戏世界</h1>
            <p class="text-center text-gray-600 mt-4">在这里你可以尽情探索和挑战！</p>
            <!-- 无性别人物形象（SVG 小人） -->
            <img src="https://p0.ssl.qhimgs1.com/sdr/400__/t03704801711883cfd4.jpg" alt="游戏人物形象" class="character-image">
        </div>
        <div class="right-content">
            <!-- 任务栏 -->
            <div class="task-bar">
                <h2 class="text-xl font-bold mb-4">任务栏</h2>
                <div class="task task-uncompleted">
                    <span class="task-name">完成新手教程</span>
                    <span class="task-status">未完成</span>
                </div>
                <div class="task task-in-progress">
                    <span class="task-name">击败 10 个怪物</span>
                    <span class="task-status">进行中</span>
                </div>
                <div class="task task-completed">
                    <span class="task-name">探索神秘地图</span>
                    <span class="task-status">已完成</span>
                </div>
            </div>
        </div>
    </div>
</body>

</html>
    
