<script>
    import { onMount } from 'svelte';
    import { browser } from '$app/environment';
    import { base } from '$app/paths'; // 引入 base 路径

    // 动态加载地图组件
    let MapComponent;

    onMount(async () => {
        if (browser) {
            try {
                const module = await import('../components/InteractiveMap.svelte');
                MapComponent = module.default;
            } catch (error) {
                console.error("Error loading map:", error);
            }
        }
    });
</script>

<svelte:head>
    <title>Philly Air Justice</title>
    <!-- 引入更现代的字体：Space Grotesk (科技/标题) + DM Sans (易读正文) -->
    <link href="https://fonts.googleapis.com/css2?family=DM+Sans:opsz,wght@9..40,400;500;700&family=Space+Grotesk:wght@500;700&display=swap" rel="stylesheet">
</svelte:head>

<!-- ================= 顶部导航栏 ================= -->
<nav class="navbar">
    <div class="nav-container">
        <div class="brand">PHI / AIR / DATA</div>
        <ul class="nav-links">
            <li><a href="#overview" class="nav-item">Vision</a></li>
            <li><a href="#context" class="nav-item">Context</a></li>
            <li><a href="#concepts" class="nav-item">Frameworks</a></li>
            <li><a href="#map" class="nav-item">The Map</a></li>
            <li><a href="#methodology" class="nav-item">Methodology</a></li>
			<li><a href="#podcast" class="nav-item">Podcast</a></li>
            <li><a href="#team" class="nav-item">About</a></li>
        </ul>
    </div>
</nav>

<main>
    <!-- ================= 1. Hero: 核心愿景 ================= -->
    <section id="overview" class="hero-section">
        <div class="container hero-container">
            <div class="hero-text">
                <span class="pill">Civic Data Simulation</span>
                <h1>Is an Algorithm Deciding Your Neighborhood's Air Quality?</h1>
                <h2 class="sub-heading">Research Question: Can we re-engineer enforcement algorithms to prioritize public health over paperwork?</h2>
                <p class="hero-desc">
                    Philadelphia is using new tech to target pollution inspections. 
                    We built a simulation to uncover the hidden question: 
                    <strong>Are we prioritizing compliance paperwork, or your lungs?</strong>
                </p>
                <div class="hero-actions">
                    <a href="#map" class="btn-primary">Explore the Map</a>
                    <a href="#concepts" class="btn-secondary">How It Works</a>
                </div>
            </div>
            <!-- 装饰性元素 -->
            <div class="hero-graphic">
                <div class="stat-card float-1">
                    <span class="stat-num">30%</span>
                    <span class="stat-label">Inspections Shifted</span>
                </div>
                <div class="stat-card float-2">
                    <span class="stat-num">EJ</span>
                    <span class="stat-label">Focus Areas</span>
                </div>
            </div>
        </div>
    </section>

    <!-- ================= 2. Context: 为什么这很重要 ================= -->
    <section id="context" class="context-section">
        <div class="container">
            <div class="section-header-group">
                <span class="section-tag">Context</span>
                <h2 class="section-heading">Why This Matters</h2>
                <p class="section-abstract">
                    <strong>Abstract:</strong> Environmental justice isn't just about where factories are built—it's about where inspectors go. 
                    This project investigates the intersection of algorithmic bias, historical redlining, and modern regulatory enforcement in Philadelphia.
                </p>
            </div>
            
            <div class="grid-3">
                <div class="feature-card">
                    <div class="icon-box">🏭</div>
                    <h3>Historic Burden</h3>
                    <p>Maps of today's asthma rates look suspiciously like redlining maps from the 1930s. Pollution in Philly isn't random; it's structural.</p>
                </div>
                <div class="feature-card">
                    <div class="icon-box">🤖</div>
                    <h3>The New "Black Box"</h3>
                    <p>Agencies are adopting AI to decide where to inspect. But who writes the rules? An algorithm optimized for "efficiency" might ignore "equity."</p>
                </div>
                <div class="feature-card">
                    <div class="icon-box">⚖️</div>
                    <h3>The Trade-off</h3>
                    <p>We face a choice: Do we catch the <em>most</em> violators (even tiny ones), or do we stop the <em>biggest</em> polluters?</p>
                </div>
            </div>
        </div>
    </section>

    <!-- ================= 3. Concepts: 两种模型对比 ================= -->
    <section id="concepts" class="framework-section">
        <div class="container">
            <div class="section-header-group centered">
                <span class="section-tag">Framework</span>
                <h2 class="section-heading">Two Ways to Guard the City</h2>
                <p class="section-sub">We simulated two different enforcement strategies. Which one would you choose?</p>
            </div>
            
            <div class="comparison-grid">
                <!-- Model A -->
                <div class="model-box model-a">
                    <div class="model-badge blue">Current Strategy</div>
                    <h3>Model A: "The Compliance Hawk"</h3>
                    <div class="divider"></div>
                    <p class="goal"><strong>Goal:</strong> Catch as many rule-breakers as possible.</p>
                    <p class="outcome">
                        It targets small, frequent violators like auto shops. 
                        While efficient on paper, it often patrols suburbs and misses the heavy smoke.
                    </p>
                </div>

                <!-- Model B -->
                <div class="model-box model-b">
                    <div class="model-badge red">Our Proposal</div>
                    <h3>Model B: "The Harm Reducer"</h3>
                    <div class="divider"></div>
                    <p class="goal"><strong>Goal:</strong> Stop the largest volume of pollution.</p>
                    <p class="outcome">
                        It ignores small paperwork errors to focus on massive refineries and factories. 
                        It shifts protection to the neighborhoods that breathe the dirtiest air.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- ================= 4. Map: 核心交互 (改为浅色背景) ================= -->
    <section id="map" class="map-section-light">
        <div class="container-fluid">
            <div class="map-header">
                <span class="section-tag">Simulation</span>
                <h2>Explore the Data</h2>
                <p>Toggle the models to see how enforcement priorities shift across racial lines.</p>
            </div>
            
            <div class="map-display">
                {#if MapComponent}
                    <svelte:component this={MapComponent} />
                {:else}
                    <div class="loading-state">
                        <div class="spinner"></div>
                        <p>Loading Simulation Engine...</p>
                    </div>
                {/if}
            </div>
        </div>
    </section>

    <!-- ================= 5. Methodology (透明度板块) ================= -->
    <section id="methodology" class="method-section">
        <div class="container">
            <div class="section-header-group">
                <span class="section-tag">Transparency</span>
                <h2 class="section-title">Behind the Scenes</h2>
                <p class="section-desc">Democratizing data means being transparent about our tools and limitations.</p>
            </div>
            
            <div class="method-grid">
                <div class="method-col">
                    <h3>Data Sources</h3>
                    <p>We combined facility compliance history from the <strong>EPA ECHO Database</strong> with demographic baselines from the <strong>U.S. Census Bureau (ACS 2010-2020)</strong>. We specifically filtered for Clean Air Act (CAA) violations in the Philadelphia area.</p>
                </div>
                <div class="method-col">
                    <h3>The Algorithm</h3>
                    <p>We trained <strong>Random Forest</strong> models to simulate inspection prioritization. Model A treats "Significant Non-Compliance" as a binary target (Yes/No). Model B predicts the continuous volume of pollutant discharge to estimate potential harm.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- ================= 6. Podcast Section (新增) ================= -->
    <section id="podcast" class="podcast-section">
        <div class="container">
            <div class="section-header-group">
                <span class="section-tag">Listen</span>
                <h2 class="section-title">Beyond the Data: The Podcast</h2>
                <p class="section-desc">
                    Section description
                </p>
            </div>

            <div class="podcast-grid">
                <!-- 左侧：播放器与单集介绍 -->
                <div class="episode-card">
                    <div class="episode-tag">Episode 1</div>
                    <h3>Title of Episode 1</h3>
                    <p class="episode-meta">Nov 28, 2025 • 24 mins • Environmental Justice</p>
                    
                    <div class="audio-player-wrapper">
                        <!-- 占位音频文件，替换为真实路径 -->
                        <audio controls class="custom-audio">
                            <source src="{base}/podcast-sample.mp3" type="audio/mpeg">
                            Your browser does not support the audio element.
                        </audio>
                    </div>

                    <div class="episode-summary">
                        <p>
                            <strong>episode abstract</strong>
                        </p>
                        <ul class="topics-list">
                            <li>✨ Algorithmic Bias 101</li>
                            <li>🏙️ Redlining vs. Machine Learning</li>
                            <li>✊ Community-Led Solutions</li>
                        </ul>
                    </div>
                </div>

                <!-- 右侧：主持人介绍 -->
                <div class="host-card">
                    <div class="host-image-placeholder">
                        <!-- 这里的 src 可以替换为主持人照片 -->
                        <span>🎙️</span>
                    </div>
                    <div class="host-info">
                        <h4>Hosted by Trapetas C. McGill</h4>
                        <p class="host-role">Role</p>
                        <p class="host-bio">
                            host-bio
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </section>
</main>

<!-- ================= 7. Footer: 团队与学院 (改为浅色背景) ================= -->
<footer id="team" class="footer-section">
    <div class="container footer-content">
        
        <!-- 左侧：学院 Logo (无需白底容器了，因为背景是浅色) -->
        <div class="footer-col school-info">
            <div class="logo-box-transparent">
                <!-- 引用 static 文件夹中的 logo -->
                <img src="{base}/sp2-logo.png" alt="Penn SP2 Logo" class="sp2-logo">
            </div>
            <div class="school-details">
                <h4>University of Pennsylvania</h4>
                <h5>School of Social Policy & Practice</h5>
                <p>Master of Science in Social Policy (MSSP)</p>
            </div>
        </div>

        <!-- 中间：课程 -->
        <div class="footer-col course-info">
            <p class="label">Course</p>
            <p class="highlight">MSSP 7100: Democratizing Data?</p>
            <p>Critical Data Studies in Algorithmic Governance</p>
            <p class="sub">Fall 2025 | Prof. Elizabeth DeYoung</p>
        </div>

        <!-- 右侧：团队 -->
        <div class="footer-col team-info">
            <p class="label">Project Team</p>
            <div class="team-names">
                <span>Bosi Ding</span>
                <span>Tingyu Zhao</span>
                <span>Minxing He</span>
                <span>Yiping Miao</span>
                <span>Jiawen Gao</span>
                <span>Trapetas C. McGill</span>
            </div>
        </div>

    </div>
    <div class="footer-bottom">
        &copy; 2025 UPenn SP2 MSSP7100 Group 2. Designed for Educational Purposes.
    </div>
</footer>

<style>
    /* --- Modern Variables (Light & Fresh Theme) --- */
    :root {
        --bg-main: #ffffff;
        --bg-alt: #f0fdfa; /* 极浅的薄荷绿 */
        --bg-light-gray: #f8fafc;
        
        --text-primary: #0f172a;
        --text-secondary: #475569;
        
        --accent: #0d9488; /* Teal - 核心色调 */
        --accent-light: #ccfbf1;
        --accent-hover: #115e59;
        
        --blue-model: #2563eb;
        --red-model: #dc2626;

        --font-head: 'Space Grotesk', sans-serif;
        --font-body: 'DM Sans', sans-serif;
    }

    :global(html) { scroll-behavior: smooth; }
    :global(body) {
        margin: 0; font-family: var(--font-body);
        color: var(--text-primary); line-height: 1.6;
        background-color: var(--bg-main);
    }

    .container { max-width: 1100px; margin: 0 auto; padding: 0 24px; }
    .container-fluid { max-width: 1400px; margin: 0 auto; padding: 0 24px; }

    /* --- Navbar (Increased Interactivity) --- */
    .navbar {
        position: sticky; top: 0; z-index: 1000;
        background: rgba(255,255,255,0.95); backdrop-filter: blur(12px);
        border-bottom: 1px solid #e2e8f0; padding: 1.2rem 0;
        transition: all 0.3s ease;
    }
    .nav-container {
        display: flex; justify-content: space-between; align-items: center;
        max-width: 1200px; margin: 0 auto; padding: 0 24px;
    }
    .brand { 
        font-family: var(--font-head); font-weight: 700; font-size: 1.2rem; 
        letter-spacing: 1px; color: var(--accent); 
    }
    .nav-links { list-style: none; display: flex; gap: 2.5rem; margin: 0; padding: 0; }
    
    /* 导航项动画 */
    .nav-item { 
        text-decoration: none; color: var(--text-secondary); 
        font-weight: 500; font-size: 0.95rem; 
        position: relative; padding-bottom: 4px;
        transition: color 0.3s ease;
    }
    .nav-item::after {
        content: ''; position: absolute; width: 0; height: 2px;
        bottom: 0; left: 0; background-color: var(--accent);
        transition: width 0.3s ease;
    }
    .nav-item:hover { color: var(--text-primary); }
    .nav-item:hover::after { width: 100%; }

    /* --- Hero Section (Light & Airy) --- */
    .hero-section {
        padding: 8rem 0 6rem 0;
        /* 柔和的渐变背景 */
        background: radial-gradient(circle at 10% 20%, #f0fdfa 0%, #ffffff 80%);
        position: relative; overflow: hidden;
    }
    .hero-container { display: flex; align-items: center; justify-content: space-between; gap: 4rem; }
    
    .hero-text { max-width: 650px; z-index: 2; }
    .pill { 
        display: inline-block; background: var(--accent-light); color: var(--accent);
        padding: 6px 14px; border-radius: 50px; font-size: 0.8rem; font-weight: 700; 
        text-transform: uppercase; margin-bottom: 1.5rem; letter-spacing: 1px;
    }
    h1 {
        font-family: var(--font-head); font-size: 3.8rem; line-height: 1.1;
        margin: 0 0 1.5rem 0; color: var(--text-primary);
        letter-spacing: -1px;
    }
    .sub-heading {
        font-family: var(--font-body); font-size: 1.3rem; font-weight: 500;
        color: var(--accent); margin-bottom: 1.5rem; line-height: 1.4;
    }
    .hero-desc { font-size: 1.1rem; color: var(--text-secondary); margin-bottom: 2.5rem; max-width: 90%; }
    
    .hero-actions { display: flex; gap: 1rem; }
    .btn-primary {
        background: var(--accent); color: white; padding: 14px 32px;
        border-radius: 50px; text-decoration: none; font-weight: 700;
        box-shadow: 0 4px 12px rgba(13, 148, 136, 0.3);
        transition: all 0.3s ease;
    }
    .btn-secondary {
        background: white; color: var(--text-primary); padding: 14px 32px;
        border-radius: 50px; text-decoration: none; font-weight: 700;
        border: 1px solid #e2e8f0; transition: all 0.3s ease;
    }
    .btn-primary:hover { transform: translateY(-3px); background: var(--accent-hover); box-shadow: 0 6px 15px rgba(13, 148, 136, 0.4); }
    .btn-secondary:hover { background: #f8fafc; border-color: #cbd5e1; transform: translateY(-3px); }

    /* Hero Graphic (Decorative) */
    .hero-graphic { position: relative; width: 400px; height: 350px; display: none; }
    @media(min-width: 900px) { .hero-graphic { display: block; } }
    .stat-card {
        position: absolute; background: white; padding: 2rem;
        border-radius: 16px; box-shadow: 0 20px 40px rgba(0,0,0,0.06);
        border: 1px solid rgba(0,0,0,0.03); display: flex; flex-direction: column;
        transition: transform 0.5s ease;
    }
    .hero-section:hover .float-1 { transform: translateY(-10px) rotate(3deg); }
    .hero-section:hover .float-2 { transform: translateY(10px) rotate(-3deg); }
    
    .float-1 { top: 20px; right: 20px; transform: rotate(3deg); }
    .float-2 { bottom: 60px; left: 0; transform: rotate(-3deg); }
    .stat-num { font-family: var(--font-head); font-size: 3rem; font-weight: 700; color: var(--accent); line-height: 1; }
    .stat-label { font-size: 0.9rem; color: var(--text-secondary); font-weight: 700; text-transform: uppercase; margin-top: 5px; }

    /* --- Section Tag & Headers --- */
    .section-header-group { margin-bottom: 3rem; }
    .section-header-group.centered { text-align: center; }
    .section-tag {
        font-family: var(--font-head); font-size: 0.85rem; font-weight: 700; 
        color: var(--accent); text-transform: uppercase; letter-spacing: 1px;
        display: block; margin-bottom: 10px;
    }
    .section-heading { font-family: var(--font-head); font-size: 2.8rem; margin-bottom: 1rem; color: var(--text-primary); }
    .section-abstract { 
        font-size: 1.1rem; color: var(--text-secondary); max-width: 800px; 
        border-left: 4px solid var(--accent-light); padding-left: 1.5rem;
    }
    .section-sub { font-size: 1.2rem; color: var(--text-secondary); max-width: 600px; margin: 0 auto; }

    /* --- Context --- */
    .context-section { padding: 6rem 0; background: white; }
    
    .grid-3 { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 2.5rem; }
    .feature-card { 
        padding: 2.5rem; background: var(--bg-light-gray); border-radius: 20px; 
        transition: all 0.3s ease; border: 1px solid transparent;
    }
    .feature-card:hover { 
        transform: translateY(-5px); 
        background: white; 
        box-shadow: 0 10px 30px rgba(0,0,0,0.05);
        border-color: #e2e8f0;
    }
    .icon-box { font-size: 3rem; margin-bottom: 1.5rem; }
    .feature-card h3 { font-family: var(--font-head); font-size: 1.4rem; margin: 0 0 0.8rem 0; }
    .feature-card p { font-size: 1rem; color: var(--text-secondary); margin: 0; line-height: 1.7; }

    /* --- Concepts (Framework) --- */
    .framework-section { padding: 6rem 0; background: var(--bg-alt); }
    
    .comparison-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 3rem; margin-top: 3rem; }
    .model-box {
        padding: 3rem; border-radius: 24px; border: 1px solid transparent;
        background: white; box-shadow: 0 10px 25px -5px rgba(0,0,0,0.03);
        position: relative; overflow: hidden; transition: transform 0.3s ease;
    }
    .model-box:hover { transform: translateY(-5px); box-shadow: 0 20px 40px -10px rgba(0,0,0,0.08); }
    
    .model-badge {
        position: absolute; top: 24px; right: 24px;
        font-size: 0.75rem; font-weight: 700; text-transform: uppercase;
        padding: 6px 12px; border-radius: 6px; letter-spacing: 0.5px;
    }
    .model-badge.blue { background: #eff6ff; color: var(--blue-model); }
    .model-badge.red { background: #fef2f2; color: var(--red-model); }
    
    .model-box h3 { font-family: var(--font-head); font-size: 1.8rem; margin: 0 0 1.5rem 0; color: var(--text-primary); }
    .divider { height: 1px; width: 100%; background: #e2e8f0; margin-bottom: 1.5rem; }
    .goal { font-size: 1.1rem; color: var(--text-primary); margin-bottom: 1rem; }
    .outcome { color: var(--text-secondary); font-size: 1rem; }

    /* --- Map Section (改回浅色背景，融入整体风格) --- */
    .map-section-light { 
        padding: 6rem 0; 
        background: white; 
    }
    .map-header { text-align: center; margin-bottom: 3rem; }
    .map-header h2 { font-family: var(--font-head); font-size: 3rem; margin: 0.5rem 0 1rem 0; color: var(--text-primary); }
    .map-header p { color: var(--text-secondary); font-size: 1.2rem; }
    .map-display {
        border-radius: 24px; overflow: hidden;
        box-shadow: 0 25px 50px -12px rgba(0,0,0,0.1); /* 柔和的投影 */
        border: 1px solid #e2e8f0;
        min-height: 750px; background: #f8fafc;
    }

    /* Loading */
    .loading-state { height: 750px; display: flex; flex-direction: column; align-items: center; justify-content: center; color: var(--text-secondary); }
    .spinner { width: 40px; height: 40px; border: 3px solid #e2e8f0; border-top-color: var(--accent); border-radius: 50%; animation: spin 1s infinite linear; margin-bottom: 1rem; }
    @keyframes spin { to { transform: rotate(360deg); } }

    /* --- Methodology (Behind the Scenes) --- */
    .method-section {
        padding: 6rem 0;
        background-color: var(--bg-light-gray); 
        color: var(--text-primary);
        border-top: 1px solid #e2e8f0;
    }
    .method-section .section-title { 
        font-family: var(--font-head); 
        font-size: 2.5rem; 
        color: var(--text-primary); 
        margin-bottom: 1rem;
    }
    .section-desc { margin-bottom: 3rem; color: var(--text-secondary); font-size: 1.1rem; }
    
    .method-grid {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 4rem;
        margin-top: 2rem;
    }
    .method-col h3 {
        font-family: var(--font-head);
        font-size: 1.5rem;
        color: var(--accent); 
        margin-bottom: 1rem;
        padding-bottom: 10px;
        border-bottom: 2px solid var(--accent-light);
    }
    .method-col p { font-size: 1.05rem; line-height: 1.7; color: var(--text-secondary); }

	/* --- Podcast Section --- */
    .podcast-section {
        padding: 6rem 0;
        background-color: white;
        border-top: 1px solid #e2e8f0;
    }

    .podcast-grid {
        display: grid;
        grid-template-columns: 1.5fr 1fr; /* 左宽右窄 */
        gap: 3rem;
        margin-top: 2rem;
    }

    /* Episode Card */
    .episode-card {
        background: var(--bg-alt); /* 浅薄荷绿背景 */
        padding: 3rem;
        border-radius: 24px;
        border: 1px solid #e2e8f0;
    }

    .episode-tag {
        display: inline-block;
        background: var(--accent);
        color: white;
        padding: 4px 12px;
        border-radius: 50px;
        font-size: 0.75rem;
        font-weight: 700;
        text-transform: uppercase;
        margin-bottom: 1rem;
        letter-spacing: 0.5px;
    }

    .episode-card h3 {
        font-family: var(--font-head);
        font-size: 2rem;
        margin: 0 0 0.5rem 0;
        color: var(--text-primary);
        line-height: 1.2;
    }

    .episode-meta {
        color: var(--text-secondary);
        font-size: 0.9rem;
        margin-bottom: 2rem;
        font-weight: 500;
    }

    /* Audio Player Styling */
    .audio-player-wrapper {
        margin-bottom: 2rem;
        background: white;
        padding: 10px;
        border-radius: 50px; /* 胶囊形状 */
        box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
    }
    .custom-audio {
        width: 100%;
        height: 40px;
        outline: none;
    }

    .episode-summary p {
        font-size: 1.05rem;
        color: var(--text-secondary);
        margin-bottom: 1.5rem;
    }

    .topics-list {
        list-style: none;
        padding: 0;
        margin: 0;
        display: flex;
        flex-wrap: wrap;
        gap: 10px;
    }
    .topics-list li {
        background: white;
        padding: 6px 12px;
        border-radius: 8px;
        font-size: 0.9rem;
        font-weight: 500;
        color: var(--accent-hover);
        border: 1px solid #ccfbf1;
    }

    /* Host Card */
    .host-card {
        background: white;
        padding: 2.5rem;
        border-radius: 24px;
        border: 1px solid #e2e8f0;
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        height: fit-content; /* 紧贴内容 */
    }

    .host-image-placeholder {
        width: 120px;
        height: 120px;
        background-color: #f1f5f9;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 3rem;
        margin-bottom: 1.5rem;
        border: 4px solid white;
        box-shadow: 0 0 0 2px var(--accent-light);
    }

    .host-info h4 {
        font-family: var(--font-head);
        font-size: 1.4rem;
        margin: 0 0 0.2rem 0;
        color: var(--text-primary);
    }

    .host-role {
        color: var(--accent);
        font-weight: 700;
        font-size: 0.9rem;
        text-transform: uppercase;
        margin-bottom: 1.5rem;
        letter-spacing: 0.5px;
    }

    .host-bio {
        color: var(--text-secondary);
        font-size: 0.95rem;
        line-height: 1.6;
    }

    /* 响应式调整 */
    @media (max-width: 768px) {
        .podcast-grid {
            grid-template-columns: 1fr;
        }
    }

    /* --- Footer (浅色设计) --- */
    .footer-section { background-color: white; color: var(--text-secondary); padding: 5rem 0 2rem 0; border-top: 1px solid #e2e8f0; }
    .footer-content { display: grid; grid-template-columns: 1.2fr 1fr 1fr; gap: 3rem; padding-bottom: 3rem; border-bottom: 1px solid #e2e8f0; }
    
    .school-info { display: flex; gap: 1.5rem; align-items: flex-start; }
    
    /* Logo 容器：透明背景 */
    .logo-box-transparent {
        padding-right: 15px;
        display: inline-block;
        flex-shrink: 0;
        border-right: 1px solid #e2e8f0;
    }
    .sp2-logo { width: 80px; height: auto; display: block; }
    
    .school-details h4 { color: var(--text-primary); margin: 0; font-family: var(--font-head); font-size: 1rem; line-height: 1.4; font-weight: 700; }
    .school-details h5 { color: var(--text-secondary); margin: 5px 0 0 0; font-weight: 500; font-size: 0.9rem; }
    .school-details p { font-size: 0.85rem; margin-top: 8px; color: var(--text-secondary); opacity: 0.8; }

    .footer-col .label { text-transform: uppercase; font-size: 0.75rem; letter-spacing: 1px; font-weight: 700; color: var(--accent); margin-bottom: 1.2rem; }
    .highlight { color: var(--text-primary); font-weight: 700; margin-bottom: 0.5rem; }
    .sub { font-size: 0.9rem; margin-top: 0.5rem; color: #64748b; }

    .team-names { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
    .team-names span { color: var(--text-secondary); font-size: 0.95rem; }

    .footer-bottom { text-align: center; padding-top: 2rem; font-size: 0.85rem; color: #94a3b8; }

    /* 手机端适配 */
    @media (max-width: 768px) {
        .hero h1 { font-size: 2.8rem; }
        .hero-container { flex-direction: column; text-align: center; }
        .hero-text { margin: 0 auto; }
        .hero-actions { justify-content: center; }
        .hero-graphic { display: none; } /* 移动端隐藏装饰图 */
        
        .grid-3, .comparison-grid, .method-grid, .footer-content { grid-template-columns: 1fr; gap: 2.5rem; }
        .nav-links { display: none; } /* 这里可以后续扩展汉堡菜单 */
        .school-info { flex-direction: column; align-items: center; text-align: center; }
        .logo-box-transparent { border-right: none; padding-right: 0; padding-bottom: 15px; border-bottom: 1px solid #e2e8f0; }
    }
</style>