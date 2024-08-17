<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Play.Jackdwh.top | 服务端云端上传系统</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background: linear-gradient(135deg, #6e8efb, #a777e3);
            font-family: 'Arial', sans-serif;
            overflow: hidden; /* 禁用页面滚动 */
        }

        .container {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            width: 350px;
            text-align: center;
        }

        h2 {
            margin-bottom: 20px;
            color: #333;
            font-size: 24px;
        }

        input[type="password"] {
            width: calc(100% - 20px);
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin-bottom: 20px;
            box-sizing: border-box;
        }

        input[type="submit"] {
            background: #6e8efb;
            border: none;
            padding: 12px;
            color: white;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
            box-sizing: border-box;
            transition: background 0.3s;
        }

        input[type="submit"]:hover {
            background: #5a6dcb;
        }

        .links {
            margin-top: 15px;
        }

        .links a {
            color: #6e8efb;
            text-decoration: none;
            font-size: 14px;
        }

        .links a:hover {
            text-decoration: underline;
        }

        .error {
            color: red;
            margin-top: 10px;
        }

        .heart {
            position: absolute;
            width: 50px;
            height: 50px;
            background: url('https://cdn-icons-png.flaticon.com/512/833/833472.png') no-repeat center center;
            background-size: contain;
            pointer-events: none;
            animation: heartBeat 1s ease infinite;
            display: none;
        }

        @keyframes heartBeat {
            0%, 20%, 50%, 80%, 100% {
                transform: scale(1);
            }
            40% {
                transform: scale(1.2);
            }
            60% {
                transform: scale(1.3);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>请输入密码</h2>
        <form id="passwordForm">
            <input type="password" id="password" placeholder="输入密码" required>
            <input type="submit" value="确认">
        </form>
        <div class="links">
            <a href="http://jackdwh.top:32768">找回密码</a>
        </div>
        <p id="error-message" class="error"></p>
    </div>

    <div class="heart" id="heart"></div>

    <script>
        document.addEventListener('keydown', function(event) {
            if (event.key === 'F12') {
                event.preventDefault();
                return false;
            }
        });

        document.addEventListener('contextmenu', function(event) {
            event.preventDefault();
            showHeartEffect(event.pageX, event.pageY);
        });

        async function hashPassword(password) {
            const encoder = new TextEncoder();
            const data = encoder.encode(password);
            const hashBuffer = await crypto.subtle.digest('SHA-256', data);
            const hashArray = Array.from(new Uint8Array(hashBuffer));
            return hashArray.map(byte => byte.toString(16).padStart(2, '0')).join('');
        }

        document.getElementById("passwordForm").onsubmit = async function(event) {
            event.preventDefault();
            const inputPassword = document.getElementById("password").value;
            const hashedPassword = await hashPassword(inputPassword);

            // 使用正确的哈希值
            const correctHashedPassword = '5e884898da28047151d0e56f8dc6292773603d0d6a3b59f8e72f6f7a6a5f5d21';

            if (hashedPassword === correctHashedPassword) {
                window.location.href = "http://jackdwh.top:32768/DoNotOpen.mp4";
            } else {
                document.getElementById("error-message").textContent = "错误的密码？请重试？ | Powered by NetScn | 杀死你麻麻";
            }
        };

        function showHeartEffect(x, y) {
            const heart = document.getElementById('heart');
            heart.style.left = `${x - 25}px`;
            heart.style.top = `${y - 25}px`;
            heart.style.display = 'block';
            setTimeout(() => {
                heart.style.display = 'none';
            }, 1000);
        }
    </script>
</body>
</html>
