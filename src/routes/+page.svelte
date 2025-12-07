<script>
    import { onMount } from 'svelte';
    import { browser } from '$app/environment';
    import { base } from '$app/paths'; // 引入 base 路径
    import { slide } from 'svelte/transition'; // 引入动画效果

    // 新增：控制 Context 区域的折叠/展开
    let isContextExpanded = false;
    const toggleContext = () => {
        isContextExpanded = !isContextExpanded;
    };
    
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
    <title>Philly Algorithmic Justice</title>
    <!-- 引入更现代的字体：Space Grotesk (科技/标题) + DM Sans (易读正文) -->
    <link href="https://fonts.googleapis.com/css2?family=DM+Sans:opsz,wght@9..40,400;500;700&family=Space+Grotesk:wght@500;700&display=swap" rel="stylesheet">
</svelte:head>

<!-- ================= Navigation Bar ================= -->
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
    <!-- 1. Hero: 沉浸式全屏背景 -->
    <section id="overview" class="hero-section" style="background-image: url('{base}/GettyImages-1151290020.jpg');">
        <!-- 黑色遮罩层，确保文字可读性 -->
        <div class="hero-overlay"></div>
        
        <div class="container hero-container">
            <div class="hero-content">
                <span class="pill">Civic Data Simulation</span>
                <h1>What's the Algorithm Deciding Your Neighborhood's Air Quality?</h1>
                <h2 class="sub-heading">The U.S. Environmental Protection Agency (EPA) has engaged labs to test the use of machine learning algorithms to reduce Clean Air Act violations. <br>
                    But is the effective choice always the fair one?
                <br><strong>We built a simulation using Philadelphia's air data as a case study to reveal the hidden risk beneath the code.</strong></h2>

                <div class="hero-actions">
                    <a href="#map" class="btn-primary">Explore the Map</a>
                    <a href="#concepts" class="btn-secondary">How It Works</a>
                </div>
            </div>
        </div>

        <!-- 图片版权说明 -->
        <div class="hero-caption">
            A view of the Philadelphia Energy Solutions refinery after a massive fire triggered several large explosions at the complex in South Philadelphia on June 21, 2019. Credit: Eduardo Munoz Alvarez/Getty Images
        </div>
    </section>

   <!-- ================= 2. Context: 垂直流式布局 ================= -->
    <section id="context" class="context-section">
        <div class="container">
            <div class="section-header-group">
                <span class="section-tag">Context</span>
                <h2 class="section-heading">Environmental Justice & Governance Algorithm</h2>
            </div>

            <div class="bento-grid">
                
                <!-- Definition 1 -->
                <div class="bento-card justice-def">
                    <div class="card-header">
                        <span class="icon">⚖️</span>
                        <h3>Distributive Justice</h3>
                    </div>
                    <p><strong>Who remains exposed?</strong> If a hit-rate goal steers attention to places where violations are easy to find, it might neglect neighborhoods with the highest burdens but complex enforcement.</p>
                </div>

                <!-- Definition 2 -->
                <div class="bento-card justice-def">
                    <div class="card-header">
                        <span class="icon">🗳️</span>
                        <h3>Procedural Justice</h3>
                    </div>
                    <p><strong>Who decides the objective?</strong> Can the choice of algorithm be transparent, explainable, and open to challenge?</p>
                </div>

                <!-- 核心叙事: 垂直流布局 (无分栏) -->
                <div class="bento-card narrative-flow">
                    
                    <!-- Part 1: The Trade-off -->
                    <div class="narrative-block top-block">
                        <h4>The Trade-off: Efficiency vs. Justice</h4>
                        <p>
                            In brief, environmental justice is about whether pollution exposure and environmental protection are distributed fairly across different communities. But in reality, governments often have to decide which cases to enforce first because of limited resources. This naturally creates a trade-off between efficiency and justice.
                        </p>
                        <p>
                            From an <span class="highlight-pill blue">efficiency standpoint</span>, targeting factories with less severe pollution can help meet policy goals faster and at lower cost. 
                            But from the perspective of <span class="highlight-pill red">environmental justice</span>, the government should instead focus on the most heavily polluted sites to ease the burden on the communities that suffer the most.
                        </p>
                    </div>

                    <div class="narrative-divider"></div>

                    <!-- Part 2: The Algorithmic Turn -->
                    <div class="narrative-block bottom-block">
                        <h4>The Algorithmic Turn</h4>
                        <p>
                            With the rise of big data, people have started asking: can we use algorithms to help make these decisions in environmental management? However, algorithms in this context are <span class="bold-text">far from neutral technical tools</span>. The data we collect and the goals we set for algorithms can lead to very different enforcement priorities.
                        </p>
                        
                        <!-- 核心高亮句 (无斜体) -->
                        <div class="highlight-quote">
                            <p>
                                “Not only can biased data produce misleading results, but governments may also use algorithms to justify decisions, 
                                <span class="mark">quietly turning policy choices into technical ones and masking their ethical implications.</span>”
                            </p>
                        </div>
                    </div>
                </div>

                <!-- Why Philly -->
                <div class="bento-card info-box accent">
                    <h4>📍 Philadelphia Case Study</h4>
                    <p>
                        Therefore, we focus on Philadelphia and look at data from industrial facilities regulated under the <strong>Clean Air Act (CAA)</strong>.
                    </p>
                    <p>
                        We built two models to simulate government decision-making to critically examine whether algorithms will reflect and reinforce existing social inequalities. By focusing on this city, we aim to:
                    </p>
                    <ul class="goal-list">
                        <li>Critically examine if algorithms reinforce social inequalities.</li>
                        <li>Make invisible biases visible.</li>
                        <li>Reframe a purely technical challenge as a <strong>fundamentally political issue</strong>.</li>
                    </ul>
                </div>

                <!-- What is CAA -->
                <div class="bento-card info-box dark">
                    <h4>📜 What is the Clean Air Act?</h4>
                    <p>
                        The United States’ core federal law for controlling air pollution. It primarily regulates fixed pollution sources such as refineries and power plants.
                    </p>
                    <p class="small-note">
                        Common violations include exceeding permitted emission limits, abnormal monitoring data, or unreported emission incidents. Once found in violation, a facility may face fines, mandatory corrective actions, or shutdown orders.
                    </p>
                    <p class="impact-note">
                        How regulators prioritize inspections directly shapes the air pollution risks faced by surrounded communities.
                    </p>
                </div>

            </div>
        </div>
    </section>

    <!-- ================= 3. Concepts: 两种模型对比 ================= -->
    <section id="concepts" class="framework-section">
        <div class="container">
            <div class="section-header-group centered">
                <span class="section-tag">Framework</span>
                <h2 class="section-heading">Two Ways to Inspect the Violations</h2>
                <p class="section-sub">We simulated two different enforcement strategies. Which one would you choose?</p>
                <!-- 新增：学术引用注脚 -->
                <div class="citation-note">
                    <span class="icon">📄</span>
                    <span>
                        Model logic inspired by Benami et al., 
                        <a href="https://law.stanford.edu/publications/the-distributive-effects-of-risk-prediction-in-environmental-compliance-algorithmic-design-environmental-justice-and-public-policy/" target="_blank" rel="noopener noreferrer">
                            "The Distributive Effects of Risk Prediction in Environmental Compliance"
                        </a> 
                        (ACM FAccT, 2021).
                    </span>
                </div>
            </div>
            
            <div class="comparison-grid">
                <!-- Model A -->
                <div class="model-box model-a">
                    <div class="model-badge blue">Current Strategy</div>
                    <h3>Model A: "The Compliance Hawk"</h3>
                    <div class="divider"></div>
                    <p class="goal"><strong>Goal:</strong> Catch as many rule-breakers as possible.</p>
                    <p class="outcome">
                        It predicts which facilities are most likely to incur a violation (HPV/Formal Action) in the future (2019–2023), which prioritizes the <strong>highest inspection hit </strong> rate.
                        While efficient on paper, it might misses the heaviest smoke.
                    </p>
                </div>

                <!-- Model B -->
                <div class="model-box model-b">
                    <div class="model-badge red">Proposal</div>
                    <h3>Model B: "The Harm Reducer"</h3>
                    <div class="divider"></div>
                    <p class="goal"><strong>Goal:</strong> Stop the largest volume of pollution.</p>
                    <p class="outcome">
                        It predicts which facilities pose the largest emission harm (RSEI value) to surrounding communities. 
                        It seeks the <strong>highest potential </strong>for harm reduction.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- ================= 4. Map: 核心交互 (改为浅色背景) ================= -->
    <!-- 4. Map Section (已更新数据来源) -->
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

            <!-- 新增：数据来源说明 -->
            <div class="data-sources-box">
                <span class="source-label">Data Sources:</span>
                <div class="source-links">
                    <a href="https://metadata.phila.gov/index.html#home/datasetdetails/61c23fb963d616001ef54695/representationdetails/61eb230b3675cd001e28a23c/" target="_blank" rel="noopener noreferrer">
                        1. Census Tract Population Metrics (OpenDataPhilly)
                    </a>
                    <span class="divider">|</span>
                    <a href="https://echo.epa.gov/facilities/facility-search" target="_blank" rel="noopener noreferrer">
                        2. EPA ECHO Facility Search (CAA Media Program)
                    </a>
                </div>
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
                    <p>When we discuss Algorithmic Government, we must realize: <strong>algorithms are only as good as the data they feed on.</strong>
                        In our analysis, we found that the 'missing data' in the EPA dataset isn't just a technical glitch; it represents a structural blind spot.</p>
                </div>
                <div class="method-col">
                    <h3>The Algorithm Ethics</h3>
                    <p>This is the very essence of the Benami model: a seemingly “rational” efficiency goal can mask or even exacerbate environmental injustice. 
                        Our research strongly demonstrates that the objective function of a regulatory algorithm is not a purely technical choice—<strong>it is a profound ethical and political choice.</strong></p>
                </div>
            </div>

            <!-- 新增：Google Slides 跳转链接 -->
            <div class="method-footer">
                <p>
                    If you want to read more about our Methodology and Critics, please see 
                    <!-- 请将 href="#" 替换为您的 Google Slide 真实网址 -->
                    <a href="https://docs.google.com/presentation/d/1ZSVW6opPhsapmlcEjHdJvMnJgoWVug47VKEHBGVf2xU/edit?usp=sharing" target="_blank" rel="noopener noreferrer" class="slide-link">
                        our detailed slides ↗
                    </a>
                </p>
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
                    <h3>Green by Algorithm</h3>
                    <p class="episode-meta">Nov 28, 2025 • 43 mins • Environmental Justice</p>
                    
                    <div class="audio-player-wrapper">
                        <!-- 占位音频文件，替换为真实路径 -->
                        <audio controls class="custom-audio">
                            <source src="{base}/Green by Algorithm.mp3" type="audio/mpeg">
                            Your browser does not support the audio element.
                        </audio>
                    </div>

                    <div class="episode-summary">
                        <p>
                            <strong>episode abstract</strong>
                        </p>
                        <ul class="topics-list">
                            <li>🔋 The AI Energy Paradox</li>
                            <li>🌍 Defining "Algorithmic Environmentalism"</li>
                            <li>📉 The "Invisible" Data Gap</li>
                            <li>🏭 Environmental Racism & Digital Redlining</li>
                            <li>🤝 Democratizing Climate Data</li>
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
                        <p class="host-role">Investment Banking & ESG Finance | Founder, 
                            <br>ICESI | Data-Driven Capital & Global Markets Strategist</p>
                        <p class="host-bio">
                            I am Trapetas Catherine McGill, a data-driven investment banker and entrepreneur advancing financial equity across the Global South and underrepresented communities in the United States. 
                            My work sits at the intersection of ESG finance, behavioral economics, and energy investment, focused on closing structural equity gaps in global capital markets.
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
                <p>Master of Science in Social Policy & Data Analytics (MSSP+DA)</p>
            </div>
        </div>

        <!-- 中间：课程 -->
        <div class="footer-col course-info">
            <p class="label">Course</p>
            <p class="highlight">MSSP 7100: Democratizing Data?</p>
            <p>Critical Data Studies in Algorithmic Governance</p>
            <p class="sub">Fall 2025 | Instructor: Dr. Elizabeth DeYoung</p>
        </div>

        <!-- 右侧：团队 -->
        <div class="footer-col team-info">
            <p class="label">Project Team</p>
            <div class="team-names">
                <span>Bosi Ding</span>
                <span>Tingyu Zhao</span>
                <span>Jiawen Gao</span>
                <span>Trapetas C. McGill</span>
                <span>Minxing He</span>
                <span>Yiping Miao</span>
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

    /* --- Navbar  --- */
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
    /* --- Hero Section (Immersive Style) --- */
    .hero-section { 
        position: relative; 
        height: 90vh; /* 占据屏幕 90% 高度，更有冲击力 */
        min-height: 600px;
        display: flex; 
        align-items: center; 
        justify-content: center;
        background-size: cover; 
        background-position: center; 
        background-repeat: no-repeat;
        color: white; /* 全局白字 */
        overflow: hidden;
    }

    /* 黑色半透明遮罩 */
    .hero-overlay {
        position: absolute;
        top: 0; left: 0; width: 100%; height: 100%;
        background: linear-gradient(to bottom, rgba(0,0,0,0.3), rgba(0,0,0,0.7)); /* 渐变遮罩 */
        z-index: 1;
    }

    .hero-container { 
        position: relative; 
        z-index: 2; /* 确保文字在遮罩之上 */
        text-align: center; /* 文字居中 */
        max-width: 900px;
    }
    
    .hero-content {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    /* 标签样式微调 */
    .pill { 
        display: inline-block; 
        background: rgba(13, 148, 136, 0.9); /* 半透明 Teal */
        color: white; 
        padding: 6px 16px; 
        border-radius: 50px; 
        font-size: 0.85rem; 
        font-weight: 700; 
        text-transform: uppercase; 
        letter-spacing: 1px;
        margin-bottom: 2rem; 
        backdrop-filter: blur(4px);
    }

    h1 { 
        font-family: var(--font-head); 
        font-size: 4rem; 
        line-height: 1.1; 
        margin: 0 0 1.5rem 0; 
        color: white; 
        letter-spacing: -1px;
        text-shadow: 0 2px 10px rgba(0,0,0,0.3); /* 增加文字阴影，防止背景过亮看不清 */
    }

    .sub-heading { 
        font-family: var(--font-body); 
        font-size: 1.4rem; 
        font-weight: 400; 
        color: rgba(255,255,255,0.9); 
        margin-bottom: 2rem; 
        line-height: 1.5;
        max-width: 800px;
    }

    .hero-desc { 
        font-size: 1.2rem; 
        color: rgba(255,255,255,0.8); 
        margin-bottom: 3rem; 
        max-width: 700px; 
        line-height: 1.7;
    }

    /* 按钮样式微调 - 适应深色背景 */
    .hero-actions { display: flex; gap: 1.5rem; }
    
    .btn-primary { 
        background: var(--accent); 
        color: white; 
        padding: 16px 36px; 
        border-radius: 50px; 
        font-weight: 700; 
        font-size: 1.1rem;
        box-shadow: 0 4px 15px rgba(0,0,0,0.3); 
        transition: all 0.3s ease; 
        border: 2px solid var(--accent);
    }
    
    .btn-secondary { 
        background: transparent; 
        color: white; 
        padding: 16px 36px; 
        border-radius: 50px; 
        font-weight: 700; 
        font-size: 1.1rem;
        border: 2px solid rgba(255,255,255,0.6); 
        transition: all 0.3s ease; 
        backdrop-filter: blur(5px);
    }

    .btn-primary:hover { 
        background: var(--accent-hover); 
        transform: translateY(-3px); 
        border-color: var(--accent-hover);
    }
    
    .btn-secondary:hover { 
        background: white; 
        color: var(--text-primary); 
        border-color: white; 
        transform: translateY(-3px); 
    }

    /* 右下角图片说明 */
    .hero-caption {
        position: absolute;
        bottom: 10px;
        right: 20px;
        z-index: 2;
        font-size: 0.7rem;
        color: rgba(255,255,255,0.5);
        max-width: 400px;
        text-align: right;
    }

    /* 移动端适配 */
    @media (max-width: 768px) {
        .hero-section { height: auto; padding: 6rem 0; }
        h1 { font-size: 2.8rem; }
        .hero-actions { flex-direction: column; width: 100%; max-width: 300px; }
        .btn-primary, .btn-secondary { width: 100%; text-align: center; }
        .hero-caption { display: none; /* 手机端隐藏长caption以免遮挡 */ }
    }

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

   /* --- Context Section (Updated) --- */
    .context-section {
        padding: 3rem 0;
        background-color: white;
    }

    /* 网格系统保持不变 */
    .bento-grid {
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-template-rows: auto auto auto;
        gap: 1.25rem;
    }

    /* 卡片基础样式 */
    .bento-card {
        background: var(--bg-light-gray);
        border-radius: 16px;
        padding: 1.8rem;
        border: 1px solid #e2e8f0;
        transition: all 0.2s ease;
    }
    .bento-card:hover {
        border-color: var(--accent);
        box-shadow: 0 4px 12px rgba(0,0,0,0.05);
    }

    /* Definitions */
    .justice-def .card-header { display: flex; align-items: center; gap: 10px; margin-bottom: 0.8rem; }
    .justice-def h3 { font-family: var(--font-head); font-size: 1.1rem; margin: 0; color: var(--text-primary); }
    .justice-def .icon { font-size: 1.2rem; }
    .justice-def p { font-size: 0.95rem; line-height: 1.6; color: var(--text-secondary); margin: 0; }

    /* --- Narrative Flow (单列垂直布局) --- */
    .narrative-flow {
        grid-column: span 2;
        background: white;
        display: flex;       /* 改为 Flex */
        flex-direction: column; /* 垂直排列 */
        gap: 0;              /* 间距由 padding 控制 */
        padding: 0;          /* 移除默认 padding，由内部块控制 */
        overflow: hidden;    /* 确保圆角 */
    }

    .narrative-block {
        padding: 1rem; /* 增加内部空间 */
    }

    .narrative-block h4 {
        font-family: var(--font-head);
        font-size: 1.25rem;
        color: var(--text-primary);
        margin: 0 0 1rem 0;
        letter-spacing: -0.5px;
    }

    .narrative-block p {
        font-size: 1.05rem; /* 稍微加大字号易读 */
        line-height: 1.7;
        color: var(--text-secondary);
        margin-bottom: 1rem;
        text-align: left;
    }
    .narrative-block p:last-child { margin-bottom: 0; }

    /* 分割线 */
    .narrative-divider {
        height: 1px;
        background: linear-gradient(to right, transparent, #e2e8f0, transparent);
        width: 100%;
    }

    /* 底部块背景微调，形成区分 */
    .bottom-block {
        background: rgba(240, 253, 250, 0.3); /* 极淡的薄荷绿背景 */
    }

    /* 样式化的高亮词 (Pills) */
    .highlight-pill {
        font-weight: 700;
        padding: 2px 6px;
        border-radius: 4px;
        font-size: 0.95em;
    }
    .highlight-pill.blue { color: var(--blue-model); background: rgba(37, 99, 235, 0.08); }
    .highlight-pill.red { color: var(--red-model); background: rgba(220, 38, 38, 0.08); }
    .bold-text { font-weight: 700; color: var(--text-primary); }

    /* 引用块 (无斜体) */
    .highlight-quote {
        margin-top: 1.5rem;
        background: white;
        padding: 1.5rem;
        border-radius: 12px;
        border-left: 4px solid var(--accent);
        box-shadow: 0 2px 8px rgba(0,0,0,0.03);
    }
    .highlight-quote p {
        font-size: 1.1rem;
        margin: 0;
        font-weight: 500; /* 半粗体代替斜体 */
        font-style: normal; /* 强制不倾斜 */
        color: var(--text-primary);
        line-height: 1.6;
    }
    .mark { 
        background: linear-gradient(120deg, rgba(13, 148, 136, 0.15) 0%, rgba(13, 148, 136, 0.15) 100%);
        background-repeat: no-repeat;
        background-size: 100% 40%;
        background-position: 0 88%; /* 下划线高亮效果 */
        color: var(--text-primary);
    }

    /* Info Boxes */
    .info-box h4 { font-family: var(--font-head); font-size: 1.1rem; margin: 0 0 0.8rem 0; }
    .info-box p { font-size: 1rem; line-height: 1.6; margin-bottom: 0.8rem; }

    /* Why Philly */
    .info-box.accent { background: var(--bg-alt); border-color: var(--accent-light); }
    .info-box.accent h4 { color: var(--accent-hover); }
    .goal-list { margin: 0; padding-left: 1.2rem; }
    .goal-list li { font-size: 0.95rem; color: var(--text-primary); margin-bottom: 6px; }

    /* CAA */
    .info-box.dark { background: var(--text-primary); color: #e2e8f0; border: none; }
    .info-box.dark h4 { color: white; border-bottom: 1px solid rgba(255,255,255,0.2); padding-bottom: 8px; display: inline-block; }
    .info-box.dark p { opacity: 0.9; }
    .small-note { font-size: 0.85rem; margin-top: 10px; color: #cbd5e1; }
    .impact-note { font-weight: 700; color: var(--accent-light); margin-top: 10px; font-size: 0.9rem; }

    /* Mobile */
    @media (max-width: 768px) {
        .bento-grid { grid-template-columns: 1fr; gap: 1.5rem; }
        .narrative-flow { grid-column: span 1; }
        .narrative-block { padding: 1.5rem; }
    }

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
    
    .model-box h3 { font-family: var(--font-head); font-size: 1.6rem; margin: 0 0 1.5rem 0; color: var(--text-primary); }
    .divider { height: 1px; width: 100%; background: #e2e8f0; margin-bottom: 1.5rem; }
    .goal { font-size: 1.1rem; color: var(--text-primary); margin-bottom: 1rem; }
    .outcome { color: var(--text-secondary); font-size: 1rem; }

    /* --- Citation Note Styles --- */
    .citation-note {
        display: inline-flex;
        align-items: center;
        gap: 8px;
        margin-top: 1rem;
        padding: 8px 16px;
        background-color: rgba(0, 0, 0, 0.03); /* 极淡的灰色背景 */
        border: 1px solid rgba(0,0,0,0.06);
        border-radius: 50px;
        font-size: 0.8rem;
        color: var(--text-secondary);
        max-width: 90%;
        line-height: 1.4;
    }

    .citation-note .icon {
        font-size: 1rem;
        opacity: 0.7;
    }

    .citation-note a {
        color: var(--text-primary);
        font-weight: 600;
        text-decoration: none;
        border-bottom: 1px solid #cbd5e1; /* 浅灰色下划线 */
        transition: all 0.2s ease;
    }

    .citation-note a:hover {
        color: var(--accent);
        border-bottom-color: var(--accent);
        background-color: rgba(13, 148, 136, 0.05);
    }

    /* 移动端适配 */
    @media (max-width: 768px) {
        .citation-note {
            flex-direction: column;
            text-align: center;
            padding: 12px;
            border-radius: 12px;
        }
        .citation-note .icon { display: none; }
    }

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

    /* 新增：数据来源样式 */
    .data-sources-box {
        margin-top: 1.5rem;
        padding: 1rem 1.5rem;
        background-color: var(--bg-light-gray);
        border-radius: 12px;
        border: 1px solid #e2e8f0;
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        gap: 10px;
        font-size: 0.85rem;
        color: var(--text-secondary);
    }
    .source-label { font-weight: 700; text-transform: uppercase; color: var(--text-primary); margin-right: 5px; }
    .source-links a { text-decoration: none; color: var(--accent); font-weight: 500; transition: color 0.2s; }
    .source-links a:hover { color: var(--accent-hover); text-decoration: underline; }
    .source-links .divider { margin: 0 8px; color: #cbd5e1; }

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

    /* --- Methodology Footer --- */
    .method-footer {
        text-align: center;
        margin-top: 1rem;
        padding-top: 1rem;
        border-top: 1px solid rgba(0,0,0,0.05); /* 顶部淡淡的分割线 */
    }

    .method-footer p {
        font-size: 1.05rem;
        color: var(--text-secondary);
    }

    .slide-link {
        display: inline-block;
        color: var(--accent);
        font-weight: 700;
        text-decoration: none;
        border-bottom: 2px solid var(--accent-light); /* 下划线装饰 */
        padding: 0 4px;
        transition: all 0.2s ease;
        margin-left: 5px;
    }

    .slide-link:hover {
        background-color: var(--accent-light); /* 鼠标悬停变色 */
        color: var(--accent-hover);
        border-bottom-color: transparent;
        border-radius: 4px;
    }

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