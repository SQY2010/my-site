<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>极简个人主页 · 作品集</title>
    <!-- 使用柔和且现代的字体系列，提升阅读体验 -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,600;14..32,700&display=swap" rel="stylesheet">
    <style>
        /* 基础重置与全局样式 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #f5f7fb;  /* 淡雅灰蓝背景，突出卡片层次 */
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            line-height: 1.5;
            color: #1e293b;
            padding: 2rem 1rem;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* 主卡片容器 */
        .card {
            max-width: 1000px;
            width: 100%;
            background: #ffffff;
            border-radius: 2.5rem;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.15), 0 4px 12px -2px rgba(0, 0, 0, 0.05);
            overflow: hidden;
            transition: box-shadow 0.3s ease;
        }

        .card:hover {
            box-shadow: 0 30px 60px -12px rgba(0, 0, 0, 0.2);
        }

        /* 顶部装饰区域 — 波浪/几何点缀 */
        .card-header {
            background: linear-gradient(135deg, #2c3e50, #1e2a3a);
            padding: 2.5rem 2.5rem 1.8rem 2.5rem;
            position: relative;
            overflow: hidden;
        }

        /* 抽象几何图案，营造高级感 */
        .card-header::before,
        .card-header::after {
            content: '';
            position: absolute;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.03);
            pointer-events: none;
        }

        .card-header::before {
            width: 300px;
            height: 300px;
            top: -150px;
            right: -80px;
            border: 2px solid rgba(255, 255, 255, 0.08);
        }

        .card-header::after {
            width: 200px;
            height: 200px;
            bottom: -100px;
            left: -50px;
            background: rgba(255, 255, 255, 0.02);
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        /* 头像 + 名字组合 */
        .profile-row {
            display: flex;
            align-items: center;
            gap: 1.5rem;
            position: relative;
            z-index: 2;
        }

        .avatar {
            width: 90px;
            height: 90px;
            background: linear-gradient(145deg, #3b4a5e, #2a3545);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 3px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 8px 18px rgba(0, 0, 0, 0.3);
            flex-shrink: 0;
        }

        /* 头像内的首字母 */
        .avatar-initials {
            font-size: 2.4rem;
            font-weight: 600;
            color: #eef2f6;
            letter-spacing: 1px;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
            font-family: 'Inter', sans-serif;
        }

        .name-title h1 {
            font-size: 2.2rem;
            font-weight: 700;
            color: #ffffff;
            letter-spacing: -0.02em;
            line-height: 1.2;
        }

        .name-title .tagline {
            font-size: 1rem;
            font-weight: 400;
            color: #a8b8cc;
            margin-top: 0.35rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            flex-wrap: wrap;
        }

        .tagline span {
            background: rgba(255, 255, 255, 0.1);
            padding: 0.2rem 0.8rem;
            border-radius: 30px;
            font-size: 0.8rem;
            font-weight: 400;
            color: #d0ddea;
            letter-spacing: 0.2px;
            backdrop-filter: blur(4px);
        }

        /* 卡片主体 — 内容区域 */
        .card-body {
            padding: 2.5rem;
            display: grid;
            grid-template-columns: 1fr 0.9fr;
            gap: 2.5rem;
        }

        /* 左侧：简介 + 链接 */
        .intro-section h2 {
            font-size: 1.5rem;
            font-weight: 600;
            color: #0f172a;
            letter-spacing: -0.02em;
            margin-bottom: 1rem;
            display: flex;
            align-items: center;
            gap: 0.6rem;
        }

        .intro-section h2::after {
            content: '';
            flex: 1;
            height: 2px;
            background: linear-gradient(90deg, #cbd5e1, transparent);
            margin-left: 0.5rem;
        }

        .intro-text {
            font-size: 1rem;
            color: #334155;
            margin-bottom: 1.8rem;
            line-height: 1.7;
        }

        .intro-text strong {
            color: #0f172a;
            font-weight: 600;
        }

        /* 社交链接网格 */
        .links-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
            gap: 0.8rem;
            margin-top: 0.5rem;
        }

        .social-link {
            display: flex;
            align-items: center;
            gap: 0.7rem;
            padding: 0.7rem 1rem;
            background: #f8fafc;
            border-radius: 60px;
            text-decoration: none;
            color: #1e293b;
            font-weight: 500;
            font-size: 0.9rem;
            border: 1px solid #e2e8f0;
            transition: all 0.2s ease;
        }

        .social-link:hover {
            background: #ffffff;
            border-color: #94a3b8;
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.04);
            transform: translateY(-2px);
            color: #0f172a;
        }

        /* 用简单的emoji或svg占位，清爽无依赖 */
        .social-icon {
            font-size: 1.2rem;
            line-height: 1;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            width: 1.6rem;
            text-align: center;
        }

        /* 右侧面板 — 技能 / 数据 / 迷你卡片 */
        .info-panel {
            background: #f9fbfd;
            border-radius: 1.8rem;
            padding: 1.6rem 1.8rem;
            border: 1px solid #eef2f6;
            box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.02);
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }

        .panel-block h3 {
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 0.08em;
            color: #64748b;
            font-weight: 600;
            margin-bottom: 1rem;
        }

        /* 技能标签 */
        .skills {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
        }

        .skill-tag {
            background: #ffffff;
            padding: 0.35rem 0.9rem;
            border-radius: 40px;
            font-size: 0.85rem;
            font-weight: 500;
            color: #1e293b;
            border: 1px solid #d9e2ef;
            box-shadow: 0 1px 2px rgba(0, 0, 0, 0.02);
            transition: all 0.15s;
        }

        .skill-tag:hover {
            background: #eef2f6;
            border-color: #b9c8da;
        }

        /* 统计数据 */
        .stats {
            display: flex;
            justify-content: space-between;
            gap: 1rem;
            margin-top: 0.25rem;
        }

        .stat-item {
            text-align: center;
            flex: 1;
            background: #ffffff;
            border-radius: 1.2rem;
            padding: 0.8rem 0.2rem;
            border: 1px solid #e9eef5;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.02);
        }

        .stat-number {
            font-size: 1.5rem;
            font-weight: 700;
            color: #0f172a;
            letter-spacing: -0.02em;
        }

        .stat-label {
            font-size: 0.7rem;
            text-transform: uppercase;
            letter-spacing: 0.04em;
            color: #64748b;
            font-weight: 500;
            margin-top: 0.2rem;
        }

        /* 分割线 */
        .divider {
            height: 1px;
            background: linear-gradient(90deg, #e2e8f0, transparent);
            margin: 0.2rem 0;
        }

        /* 小巧的“近期项目”展示 */
        .recent-item {
            display: flex;
            align-items: center;
            gap: 0.8rem;
            padding: 0.6rem 0;
            border-bottom: 1px dashed #e2e8f0;
            font-size: 0.9rem;
        }

        .recent-item:last-child {
            border-bottom: none;
        }

        .recent-dot {
            width: 6px;
            height: 6px;
            background: #3b82f6;
            border-radius: 50%;
            flex-shrink: 0;
        }

        .recent-text {
            color: #334155;
            font-weight: 500;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .recent-date {
            margin-left: auto;
            font-size: 0.75rem;
            color: #94a3b8;
            font-weight: 400;
            background: #ffffff;
            padding: 0.15rem 0.6rem;
            border-radius: 30px;
            border: 1px solid #e9eef5;
        }

        /* 卡片底部装饰 */
        .card-footer {
            padding: 1rem 2.5rem 1.5rem 2.5rem;
            background: #ffffff;
            border-top: 1px solid #f1f5f9;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.8rem;
            color: #94a3b8;
        }

        .footer-note {
            display: flex;
            align-items: center;
            gap: 0.4rem;
        }

        .footer-note span {
            color: #64748b;
        }

        /* 响应式设计 */
        @media (max-width: 780px) {
            .card-body {
                grid-template-columns: 1fr;
                gap: 2rem;
                padding: 2rem;
            }

            .profile-row {
                flex-direction: column;
                text-align: center;
                align-items: center;
            }

            .name-title h1 {
                font-size: 1.8rem;
            }

            .tagline {
                justify-content: center;
            }

            .card-header {
                padding: 2rem 1.5rem 1.5rem 1.5rem;
            }

            .card-footer {
                flex-direction: column;
                gap: 0.5rem;
                text-align: center;
                padding: 1.2rem 1.5rem;
            }

            .intro-section h2::after {
                display: none;
            }
        }

        @media (max-width: 480px) {
            body {
                padding: 1rem 0.5rem;
            }

            .card {
                border-radius: 1.8rem;
            }

            .card-body {
                padding: 1.5rem;
            }

            .info-panel {
                padding: 1.2rem;
            }

            .links-grid {
                grid-template-columns: 1fr;
            }

            .avatar {
                width: 75px;
                height: 75px;
            }

            .avatar-initials {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="card">
        <!-- 顶部区域: 头像 + 名字/头衔 -->
        <div class="card-header">
            <div class="profile-row">
                <div class="avatar">
                    <!-- 头像使用首字母 "J" 代表 Alex.J，美观且无需图片 -->
                    <div class="avatar-initials">AJ</div>
                </div>
                <div class="name-title">
                    <h1>Alex Johnson</h1>
                    <div class="tagline">
                        创意开发者 & 设计师
                        <span>开放合作</span>
                    </div>
                </div>
            </div>
        </div>

        <!-- 主体内容: 左右两栏 -->
        <div class="card-body">
            <!-- 左侧: 自我介绍 + 社交链接 -->
            <div class="intro-section">
                <h2>你好，我是 Alex</h2>
                <p class="intro-text">
                    我是一位常驻<strong>旧金山</strong>的创意开发者，专注于构建<strong>兼具美感与功能</strong>的数字产品。
                    拥有超过6年的前端与全栈经验，善于将想法转化为流畅、响应式的用户体验。
                    热爱开源、极简设计和一杯好咖啡。
                </p>

                <!-- 社交链接采用图标+文字 -->
                <div class="links-grid">
                    <a href="#" class="social-link" aria-label="GitHub">
                        <span class="social-icon">🐙</span> GitHub
                    </a>
                    <a href="#" class="social-link" aria-label="Twitter / X">
                        <span class="social-icon">🐦</span> Twitter
                    </a>
                    <a href="#" class="social-link" aria-label="LinkedIn">
                        <span class="social-icon">💼</span> LinkedIn
                    </a>
                    <a href="#" class="social-link" aria-label="Dribbble">
                        <span class="social-icon">🎨</span> Dribbble
                    </a>
                    <a href="#" class="social-link" aria-label="个人博客">
                        <span class="social-icon">📝</span> 博客
                    </a>
                    <a href="#" class="social-link" aria-label="邮箱">
                        <span class="social-icon">✉️</span> 邮件
                    </a>
                </div>
                <!-- 额外的个人状态小提示 -->
                <p style="font-size: 0.8rem; color: #64748b; margin-top: 1.5rem; display: flex; align-items: center; gap: 0.4rem;">
                    <span style="display: inline-block; width: 8px; height: 8px; background: #22c55e; border-radius: 50%;"></span>
                    目前可接受自由项目
                </p>
            </div>

            <!-- 右侧: 技能、数据、项目摘要 -->
            <div class="info-panel">
                <!-- 技能区块 -->
                <div class="panel-block">
                    <h3>技术栈 & 工具</h3>
                    <div class="skills">
                        <span class="skill-tag">React</span>
                        <span class="skill-tag">TypeScript</span>
                        <span class="skill-tag">Next.js</span>
                        <span class="skill-tag">Node.js</span>
                        <span class="skill-tag">Tailwind</span>
                        <span class="skill-tag">Figma</span>
                        <span class="skill-tag">Python</span>
                        <span class="skill-tag">GraphQL</span>
                    </div>
                </div>

                <div class="divider"></div>

                <!-- 简单统计数据 (增加可信度与互动) -->
                <div class="panel-block">
                    <h3>近期成就</h3>
                    <div class="stats">
                        <div class="stat-item">
                            <div class="stat-number">28</div>
                            <div class="stat-label">项目</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-number">6+</div>
                            <div class="stat-label">年经验</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-number">1.2k</div>
                            <div class="stat-label">GitHub ⭐</div>
                        </div>
                    </div>
                </div>

                <div class="divider"></div>

                <!-- 近期项目 / 动态列表 -->
                <div class="panel-block">
                    <h3>最近项目</h3>
                    <div class="recent-item">
                        <span class="recent-dot"></span>
                        <span class="recent-text">设计系统 2.0</span>
                        <span class="recent-date">2025-03</span>
                    </div>
                    <div class="recent-item">
                        <span class="recent-dot"></span>
                        <span class="recent-text">天气应用 (PWA)</span>
                        <span class="recent-date">2025-02</span>
                    </div>
                    <div class="recent-item">
                        <span class="recent-dot"></span>
                        <span class="recent-text">作品集网站 v3</span>
                        <span class="recent-date">2025-01</span>
                    </div>
                </div>
            </div>
        </div>

        <!-- 页脚 (包含版权和主题) -->
        <div class="card-footer">
            <div class="footer-note">
                <span>© 2025 Alex Johnson</span>
                <span style="margin: 0 0.3rem;">·</span>
                <span>保持好奇，保持创造</span>
            </div>
            <div style="display: flex; gap: 0.8rem; color: #94a3b8;">
                <span>📍 旧金山</span>
                <span>🕒 太平洋时间</span>
            </div>
        </div>
    </div>
</body>
</html>