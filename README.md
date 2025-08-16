<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>线上易经硬币占卜</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #b21f1f);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
            color: #f5f5f5;
            min-height: 100vh;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        
        .container {
            max-width: 800px;
            width: 100%;
            background: rgba(0, 0, 0, 0.6);
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
            padding: 30px;
            position: relative;
            overflow: hidden;
        }
        
        .container::before {
            content: "";
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><path d="M0 0L100 100M100 0L0 100" stroke="rgba(255,255,255,0.03)" stroke-width="0.5"/></svg>');
            z-index: 0;
        }
        
        .content {
            position: relative;
            z-index: 1;
        }
        
        header {
            text-align: center;
            padding: 20px 0;
            margin-bottom: 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            color: #FFD700;
            text-shadow: 0 0 10px rgba(255, 215, 0, 0.5);
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.8;
            max-width: 500px;
            margin: 0 auto;
        }
        
        .process-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-bottom: 30px;
        }
        
        .coins-container {
            display: flex;
            gap: 15px;
            margin: 20px 0;
        }
        
        .coin {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            transition: transform 0.5s ease;
            background: linear-gradient(to bottom, #FFD700, #D4AF37);
            color: #8B7500;
        }
        
        .coin.yin {
            background: linear-gradient(to bottom, #C0C0C0, #A9A9A9);
        }
        
        .coin.flip {
            animation: flip 1s ease;
        }
        
        @keyframes flip {
            0% { transform: rotateY(0); }
            50% { transform: rotateY(180deg); }
            100% { transform: rotateY(360deg); }
        }
        
        .throw-btn {
            background: linear-gradient(to right, #8B4513, #A0522D);
            color: white;
            border: none;
            padding: 12px 35px;
            font-size: 1.1rem;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            margin: 15px 0;
        }
        
        .throw-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4);
        }
        
        .throw-btn:disabled {
            background: #555;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        .progress {
            width: 100%;
            margin: 20px 0;
        }
        
        .progress-bar {
            height: 8px;
            background: #333;
            border-radius: 4px;
            overflow: hidden;
            position: relative;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(to right, #FFD700, #FF9800);
            border-radius: 4px;
            transition: width 0.5s ease;
        }
        
        .progress-text {
            text-align: center;
            margin-top: 8px;
            font-size: 0.9rem;
            color: #FFD700;
        }
        
        .results-container {
            background: rgba(0, 0, 0, 0.4);
            border-radius: 10px;
            padding: 20px;
            margin-top: 20px;
        }
        
        .results-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .results-header h2 {
            color: #FFD700;
            font-size: 1.6rem;
        }
        
        .reset-btn {
            background: transparent;
            color: #FFD700;
            border: 1px solid #FFD700;
            padding: 6px 15px;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .reset-btn:hover {
            background: rgba(255, 215, 0, 0.1);
        }
        
        .throw-results {
            margin-top: 20px;
        }
        
        .throw-results h3 {
            color: #FFD700;
            margin-bottom: 10px;
            text-align: center;
        }
        
        .results-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }
        
        .result-item {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 8px;
            padding: 15px;
            font-size: 1rem;
            transition: transform 0.3s ease;
            position: relative;
            border: 1px solid rgba(255, 215, 0, 0.2);
        }
        
        .result-item:hover {
            transform: translateY(-5px);
            background: rgba(0, 0, 0, 0.4);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        .result-item .throw-num {
            color: #FFD700;
            font-weight: bold;
            margin-bottom: 10px;
            font-size: 1.2rem;
            text-align: center;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            padding-bottom: 8px;
        }
        
        .coin-results {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin: 10px 0;
        }
        
        .mini-coin {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.9rem;
            background: linear-gradient(to bottom, #FFD700, #D4AF37);
            color: #8B7500;
        }
        
        .mini-coin.yin {
            background: linear-gradient(to bottom, #C0C0C0, #A9A9A9);
        }
        
        .result-summary {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
            padding-top: 10px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .result-type {
            color: #FF9800;
            font-weight: bold;
        }
        
        .completion-message {
            text-align: center;
            margin-top: 20px;
            padding: 15px;
            background: rgba(255, 215, 0, 0.1);
            border-radius: 8px;
            color: #FFD700;
            font-size: 1.1rem;
            border: 1px solid rgba(255, 215, 0, 0.3);
        }
        
        footer {
            text-align: center;
            margin-top: 25px;
            padding-top: 15px;
            border-top: 1px solid rgba(255, 255, 255, 0.2);
            font-size: 0.85rem;
            opacity: 0.7;
        }
        
        .yin-yang {
            font-size: 3rem;
            margin: 10px 0;
            animation: rotate 10s linear infinite;
        }
        
        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
        
        /* 密码保护层样式 */
        #passwordLayer {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            backdrop-filter: blur(5px);
        }
        
        .password-container {
            background: rgba(0, 0, 0, 0.8);
            border-radius: 15px;
            padding: 40px;
            width: 90%;
            max-width: 500px;
            text-align: center;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(255, 215, 0, 0.3);
        }
        
        .password-container h2 {
            color: #FFD700;
            margin-bottom: 25px;
            font-size: 2.2rem;
            text-shadow: 0 0 10px rgba(255, 215, 0, 0.5);
        }
        
        .password-container p {
            margin-bottom: 25px;
            font-size: 1.1rem;
            opacity: 0.8;
            line-height: 1.6;
        }
        
        .password-form {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        
        .password-input {
            padding: 15px 20px;
            border-radius: 50px;
            border: 2px solid rgba(255, 215, 0, 0.3);
            background: rgba(0, 0, 0, 0.6);
            color: #FFD700;
            font-size: 1.1rem;
            outline: none;
            transition: all 0.3s ease;
        }
        
        .password-input:focus {
            border-color: #FFD700;
            box-shadow: 0 0 15px rgba(255, 215, 0, 0.3);
        }
        
        .password-btn {
            background: linear-gradient(to right, #8B4513, #A0522D);
            color: white;
            border: none;
            padding: 15px;
            font-size: 1.1rem;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        .password-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4);
            background: linear-gradient(to right, #A0522D, #8B4513);
        }
        
        .error-message {
            color: #ff6b6b;
            margin-top: 10px;
            min-height: 24px;
            font-weight: bold;
        }
        
        .password-hint {
            margin-top: 20px;
            font-size: 0.9rem;
            opacity: 0.6;
        }
        
        @media (max-width: 600px) {
            .container {
                padding: 15px;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .coin {
                width: 55px;
                height: 55px;
                font-size: 1.7rem;
            }
            
            .results-list {
                grid-template-columns: 1fr;
            }
            
            .password-container {
                padding: 25px;
            }
        }
    </style>
</head>
<body>
    <!-- 密码保护层 -->
    <div id="passwordLayer">
        <div class="password-container">
            <h2><i class="fas fa-lock"></i> 易经占卜系统</h2>
            <p>此占卜系统包含神秘力量，仅供授权用户使用。请提供访问密码以继续。</p>
            
            <div class="password-form">
                <input type="password" id="passwordInput" class="password-input" placeholder="请输入访问密码..." autocomplete="off">
                <button id="passwordBtn" class="password-btn">进入占卜系统</button>
                <div id="errorMessage" class="error-message"></div>
            </div>
            
        </div>
    </div>

    <!-- 占卜主界面 -->
    <div class="container" style="display: none;">
        <div class="content">
            <header>
                <div class="yin-yang">
                    <i class="fas fa-yin-yang"></i>
                </div>
                <h1>易经占卜投币器</h1>
                <p class="subtitle">模拟投掷三枚硬币六次，获得占卜结果</p>
            </header>
            
            <div class="process-container">
                <div class="coins-container">
                    <div class="coin" id="coin1">?</div>
                    <div class="coin" id="coin2">?</div>
                    <div class="coin" id="coin3">?</div>
                </div>
                
                <button class="throw-btn" id="throwBtn">
                    <i class="fas fa-dice"></i> 投掷硬币
                </button>
                
                <div class="progress">
                    <div class="progress-bar">
                        <div class="progress-fill" id="progressFill"></div>
                    </div>
                    <div class="progress-text">投掷进度: <span id="progressText">0/6</span></div>
                </div>
            </div>
            
            <div class="results-container">
                <div class="results-header">
                    <h2>投掷结果</h2>
                    <button class="reset-btn" id="resetBtn">
                        <i class="fas fa-redo"></i> 重新开始
                    </button>
                </div>

                <div class="throw-results">
                    <h3>投掷记录（从下至上）</h3>
                    <div class="results-list" id="resultsList">
                        <div class="result-item">
                            <div class="throw-num">准备投掷</div>
                            <p style="text-align: center; opacity: 0.8;">点击上方按钮开始投掷硬币</p>
                        </div>
                    </div>
                    <div id="completionMessage" class="completion-message" style="display: none;">
                        六爻已完成！请查看投掷结果
                    </div>
                </div>
            </div>
            
            <footer>
                <p>易经占卜系统 &copy; 2025 | 版权归属：雨汐 | <span id="accessTime"></span></p>
            </footer>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // 密码验证逻辑
            const passwordLayer = document.getElementById('passwordLayer');
            const passwordInput = document.getElementById('passwordInput');
            const passwordBtn = document.getElementById('passwordBtn');
            const errorMessage = document.getElementById('errorMessage');
            const container = document.querySelector('.container');
            const accessTime = document.getElementById('accessTime');
            
            // 设置密码（写死在代码中）
            const CORRECT_PASSWORD = "8888";
            
            passwordBtn.addEventListener('click', () => {
                const enteredPassword = passwordInput.value.trim();
                errorMessage.textContent = "";
                
                if (enteredPassword === "") {
                    errorMessage.textContent = "请输入密码";
                    passwordInput.focus();
                    return;
                }
                
                if (enteredPassword === CORRECT_PASSWORD) {
                    // 密码正确
                    passwordLayer.style.display = "none";
                    container.style.display = "block";
                    
                    // 记录访问时间
                    const now = new Date();
                    accessTime.textContent = `访问时间: ${now.toLocaleString()}`;
                } else {
                    // 密码错误
                    errorMessage.textContent = "密码错误，请重试";
                    passwordInput.value = "";
                    passwordInput.focus();
                    
                    // 添加错误动画
                    passwordInput.classList.add('error');
                    setTimeout(() => {
                        passwordInput.classList.remove('error');
                    }, 1000);
                }
            });
            
            // 按Enter键提交密码
            passwordInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    passwordBtn.click();
                }
            });
            
            // 获取DOM元素
            const throwBtn = document.getElementById('throwBtn');
            const resetBtn = document.getElementById('resetBtn');
            const coins = [
                document.getElementById('coin1'),
                document.getElementById('coin2'),
                document.getElementById('coin3')
            ];
            const progressFill = document.getElementById('progressFill');
            const progressText = document.getElementById('progressText');
            const resultsList = document.getElementById('resultsList');
            const completionMessage = document.getElementById('completionMessage');
            
            // 初始状态
            let currentThrow = 0;
            let results = [];
            
            // 硬币值
            const coinValues = { 'heads': 3, 'tails': 2 };
            
            // 投掷硬币
            throwBtn.addEventListener('click', () => {
                if (currentThrow >= 6) return;
                
                // 硬币翻转动画
                coins.forEach(coin => {
                    coin.classList.remove('flip');
                    void coin.offsetWidth; // 触发重绘
                    coin.classList.add('flip');
                });
                
                // 延迟显示结果
                setTimeout(() => {
                    // 随机生成硬币结果
                    const throwResults = [];
                    let sum = 0;
                    
                    for (let i = 0; i < 3; i++) {
                        const isHeads = Math.random() > 0.5;
                        throwResults.push(isHeads ? 'heads' : 'tails');
                        sum += isHeads ? coinValues.heads : coinValues.tails;
                        
                        // 显示硬币结果
                        coins[i].textContent = isHeads ? '阳' : '阴';
                        coins[i].className = isHeads ? 'coin' : 'coin yin';
                    }
                    
                    // 确定爻的类型
                    let yaoType;
                    switch(sum) {
                        case 6: // 老阴
                            yaoType = "老阴（变爻）";
                            break;
                        case 7: // 少阳
                            yaoType = "少阳";
                            break;
                        case 8: // 少阴
                            yaoType = "少阴";
                            break;
                        case 9: // 老阳
                            yaoType = "老阳（变爻）";
                            break;
                    }
                    
                    // 保存结果
                    results.push({
                        throw: currentThrow + 1,
                        coins: throwResults,
                        sum: sum,
                        type: yaoType
                    });
                    
                    // 更新进度
                    currentThrow++;
                    progressFill.style.width = `${(currentThrow / 6) * 100}%`;
                    progressText.textContent = `${currentThrow}/6`;
                    
                    // 更新投掷记录
                    updateThrowResults();
                    
                    // 如果已完成6次投掷
                    if (currentThrow === 6) {
                        throwBtn.disabled = true;
                        completionMessage.style.display = 'block';
                    }
                }, 800);
            });
            
            // 更新投掷记录显示
            function updateThrowResults() {
                if (results.length === 0) return;
                
                let html = '';
                // 显示最新的6条记录（从下至上的顺序）
                for (let i = results.length - 1; i >= 0; i--) {
                    const result = results[i];
                    
                    // 创建硬币图标
                    let coinIcons = '';
                    result.coins.forEach(coin => {
                        const isHeads = coin === 'heads';
                        coinIcons += `<div class="mini-coin ${isHeads ? '' : 'yin'}">${isHeads ? '阳' : '阴'}</div>`;
                    });
                    
                    html += `
                        <div class="result-item">
                            <div class="throw-num">第${result.throw}爻（${result.throw === 1 ? '初爻' : result.throw === 6 ? '上爻' : `${result.throw}爻`}）</div>
                            <div class="coin-results">
                                ${coinIcons}
                            </div>
                            <div class="result-summary">
                                <div>总和: ${result.sum}</div>
                                <div class="result-type">${result.type}</div>
                            </div>
                        </div>
                    `;
                }
                resultsList.innerHTML = html;
            }
            
            // 重置系统
            resetBtn.addEventListener('click', () => {
                currentThrow = 0;
                results = [];
                
                // 重置硬币显示
                coins.forEach(coin => {
                    coin.textContent = '?';
                    coin.className = 'coin';
                });
                
                // 重置进度
                progressFill.style.width = "0%";
                progressText.textContent = "0/6";
                throwBtn.disabled = false;
                completionMessage.style.display = 'none';
                
                // 重置结果显示
                resultsList.innerHTML = `
                    <div class="result-item">
                        <div class="throw-num">准备投掷</div>
                        <p style="text-align: center; opacity: 0.8;">点击上方按钮开始投掷硬币</p>
                    </div>
                `;
            });
        });
    </script>
</body>
</html>
