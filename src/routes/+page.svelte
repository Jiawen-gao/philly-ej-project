<script>
    import { onMount } from 'svelte';
    import { browser } from '$app/environment';

    // 变量用于存储动态加载的组件
    let MapComponent;

    onMount(async () => {
        if (browser) {
            try {
                // 动态导入：确保路径 '../components/InteractiveMap.svelte' 是正确的
                const module = await import('../components/InteractiveMap.svelte');
                MapComponent = module.default;
                console.log("Map component loaded successfully");
            } catch (error) {
                console.error("Map loading failed:", error);
            }
        }
    });
</script>

<svelte:head>
	<title>Philly Algorithmic Justice</title>
	<link href="https://fonts.googleapis.com/css2?family=DM+Sans:opsz,wght@9..40,400;500&family=Space+Grotesk:wght@500;700&display=swap" rel="stylesheet">
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
			<!-- 新增: Methodology 入口，响应老师关于"Behind the scenes"的建议 -->
			<li><a href="#methodology" class="nav-item">Methodology</a></li>
			<li><a href="#team" class="nav-item">About</a></li>
		</ul>
	</div>
</nav>

<main>
	<!-- ================= 1. Hero: 核心愿景 ================= -->
	<section id="overview" class="hero-section">
		<div class="content-wrapper">
			<h1 class="main-title">
				Democratizing <br>
				<span class="highlight">Algorithmic Governance</span>
			</h1>
			<p class="subtitle">
				Are the algorithms protecting Philadelphia's air, or just managing it?
			</p>
			<p class="description">
				We investigate the hidden logic behind <strong>industrial pollution enforcement</strong> and propose a Harm-Reduction Model that puts community health first.
			</p>
			<a href="#map" class="cta-button">Launch Data Map →</a>
		</div>
	</section>

	<!-- ================= 2. Context: 背景与定义 (大幅修改) ================= -->
	<!-- 响应反馈: "Don't bury the lead" & "Provide background first" -->
	<section id="context" class="context-section">
		<div class="content-wrapper">
			<div class="context-grid">
				<!-- 左侧：明确定义检查对象 -->
				<div class="context-text">
					<h2 class="section-title">The Context</h2>
					
					<div class="info-block">
						<h3>🔍 What are we inspecting?</h3>
						<p>
							We focus specifically on <strong>Industrial Air Quality Inspections</strong> (factories, refineries, and major polluters), not residential housing. 
							These facilities release particulate matter that directly impacts respiratory health.
						</p>
					</div>

					<div class="info-block">
						<h3>📍 Why Philadelphia?</h3>
						<p>
							Philadelphia is an environmental justice battleground. Due to historical <strong>redlining</strong> and <strong>structural racism</strong>, hazardous industrial sites are disproportionately clustered near low-income communities of color. 
						</p>
					</div>

					<div class="info-block">
						<h3>⚠️ The Problem</h3>
						<p>
							Current enforcement relies on a <strong>"Compliance Model"</strong>—often triggered by complaints or outdated schedules—rather than prioritizing neighborhoods facing the highest cumulative health risks.
						</p>
					</div>
				</div>

				<!-- 右侧：视觉装饰 (抽象的工厂/地图网格) -->
				<div class="context-visual">
					<div class="stat-box">
						<span class="big-num">46%</span>
						<p>of high-risk sites are located in minority neighborhoods.</p>
					</div>
					<div class="stat-box accent">
						<span class="big-num">VS</span>
						<p>Compliance vs. Harm Reduction</p>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- ================= 3. Frameworks: 理论框架 ================= -->
	<section id="concepts" class="concepts-section">
		<div class="content-wrapper">
			<h2 class="section-title">Critical Frameworks</h2>
			<div class="cards-grid">
				<div class="concept-card">
					<h3>Environmental Justice</h3>
					<div class="divider"></div>
					<p>Fair treatment and meaningful involvement for all people regardless of race or income.</p>
				</div>
				<div class="concept-card">
					<h3>Distributive Justice</h3>
					<div class="divider"></div>
					<p><strong>Outcomes:</strong> Are pollution burdens shared equally, or concentrated in specific zip codes?</p>
				</div>
				<div class="concept-card">
					<h3>Procedural Justice</h3>
					<div class="divider"></div>
					<p><strong>Process:</strong> Is the algorithm transparent? Who defines the risk metrics?</p>
				</div>
			</div>
		</div>
	</section>

	<!-- ================= 4. Map: 互动地图 ================= -->
	<section id="map" class="map-section">
    <div class="content-wrapper">
        <h2 class="section-title">Visualizing the Shift</h2>
        <p class="section-desc">
            Explore how different algorithmic objectives reshape inspection priorities.
        </p>
        
        <div class="map-container-full">
            {#if MapComponent}
                <svelte:component this={MapComponent} />
            {:else}
                <!-- 如果一直在这一步，请检查 F12 控制台报错 -->
                <div class="loading-placeholder">
                    <div class="spinner"></div>
                    <p>Loading Interactive Map...</p>
                    <p style="font-size: 0.8rem; color: #999; margin-top: 10px;">(If stuck, check Console F12)</p>
                </div>
            {/if}
        </div>
    </div>
	</section>

	<!-- ================= 5. Methodology: 幕后思考 (新增) ================= -->
	<!-- 响应反馈: "Modeling transparency in research" & "Links to readings" -->
	<section id="methodology" class="method-section">
		<div class="content-wrapper">
			<h2 class="section-title">Behind the Model</h2>
			
			<div class="method-grid">
				<div class="method-col">
					<h3>Data Ethics & Limitations</h3>
					<p>
						Our model uses data from the <strong>EPA ECHO database</strong> and <strong>Census Bureau</strong>. 
						Following the critique by <em>Porter</em> on quantification, we acknowledge that these datasets are not neutral. 
						They may underreport pollution in marginalized areas due to lack of sensors or "complaint bias."
					</p>
				</div>
				<div class="method-col">
					<h3>Algorithmic Transparency</h3>
					<p>
						We aim to make the "black box" visible. Unlike the state's proprietary prioritization, our <strong>Harm-Reduction Model</strong> 
						openly weights factors like <em>Asthma Rates</em> and <em>Poverty Levels</em> (referencing <em>Gillborn's</em> work on racism in data).
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- ================= 6. Footer: 团队信息 ================= -->
	<section id="team" class="footer-section">
		<div class="content-wrapper">
			<div class="footer-content">
				<div class="school-info">
					<div class="logo-box">SP2 LOGO</div> <!-- 记得替换为 logo 图片 -->
					<div class="text-group">
						<h3>University of Pennsylvania</h3>
						<p>School of Social Policy & Practice</p>
						<p class="course-name">Course: Democratizing Data (Critical Data Studies)</p>
					</div>
				</div>

				<div class="team-names">
					<p><strong>Project Team:</strong> Jiawen / Bosi Ding / Yiping Miao / Tingyu Zhao / Minxing He</p>
				</div>
			</div>
			<div class="copyright">
				Designed for Assignment 2. Fall 2024.
			</div>
		</div>
	</section>
</main>

<!-- ================= 样式表 (CSS) ================= -->
<style>
	/* --- 配色与字体变量 --- */
	:root {
		--primary: #0F4C5C; 
		--accent: #E36414;
		--bg-main: #FBF8F3; 
		--bg-alt: #EFEBE0;
		--bg-dark: #1A282D; /* 新增深色背景用于 Methodology */
		
		--text-main: #1A282D;
		--text-light: #5F6C72;
		--text-inverse: #FBF8F3; /* 反白文字 */

		--font-head: 'Space Grotesk', sans-serif;
		--font-body: 'DM Sans', sans-serif;
	}

	:global(html) { scroll-behavior: smooth; }
	:global(body) {
		margin: 0;
		font-family: var(--font-body);
		color: var(--text-main);
		background-color: var(--bg-main);
		line-height: 1.6;
	}

	/* --- 导航栏 --- */
	.navbar {
		position: sticky;
		top: 0;
		background: rgba(251, 248, 243, 0.95);
		backdrop-filter: blur(8px);
		border-bottom: 1px solid rgba(0,0,0,0.05);
		z-index: 1000;
		padding: 1.2rem 0;
	}

	.nav-container {
		max-width: 1200px;
		margin: 0 auto;
		padding: 0 2rem;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.brand {
		font-family: var(--font-head);
		font-weight: 700;
		font-size: 1.1rem;
		letter-spacing: 1px;
		color: var(--primary);
	}

	.nav-links {
		display: flex;
		gap: 1.5rem;
		list-style: none;
		margin: 0;
		padding: 0;
	}

	.nav-item {
		text-decoration: none;
		color: var(--text-main);
		font-family: var(--font-head);
		font-weight: 500;
		font-size: 0.9rem;
		transition: color 0.3s;
	}
	.nav-item:hover { color: var(--accent); }

	/* --- 通用布局 --- */
	.content-wrapper {
		max-width: 1000px;
		margin: 0 auto;
		padding: 0 2rem;
	}
	section { padding: 5rem 0; }
	.section-title {
		font-family: var(--font-head);
		font-size: 2.5rem;
		color: var(--primary);
		margin-bottom: 2rem;
	}

	/* --- Hero --- */
	.hero-section { padding-top: 6rem; padding-bottom: 6rem; }
	.main-title {
		font-family: var(--font-head);
		font-size: 3.5rem;
		line-height: 1;
		margin-bottom: 1.5rem;
		color: var(--primary);
	}
	.highlight { color: var(--accent); font-style: italic; }
	.subtitle { font-size: 1.4rem; font-weight: 500; margin-bottom: 1rem; }
	.description { max-width: 650px; font-size: 1.1rem; color: var(--text-light); margin-bottom: 2.5rem; }
	
	.cta-button {
		display: inline-block;
		background: var(--accent);
		color: white;
		padding: 1rem 2rem;
		text-decoration: none;
		font-family: var(--font-head);
		font-weight: 700;
		border-radius: 4px;
		transition: background 0.3s;
	}
	.cta-button:hover { background: #C04F0B; }

	/* --- Context (新样式) --- */
	.context-section { background-color: var(--bg-alt); }
	.context-grid {
		display: grid;
		grid-template-columns: 1.5fr 1fr;
		gap: 4rem;
	}
	.info-block { margin-bottom: 2rem; }
	.info-block h3 {
		font-family: var(--font-head);
		color: var(--accent);
		margin-bottom: 0.5rem;
		font-size: 1.2rem;
	}
	.context-visual {
		display: flex;
		flex-direction: column;
		gap: 2rem;
		justify-content: center;
	}
	.stat-box {
		background: var(--primary);
		color: white;
		padding: 2rem;
		text-align: center;
	}
	.stat-box.accent { background: var(--accent); }
	.big-num {
		font-family: var(--font-head);
		font-size: 3rem;
		font-weight: 700;
		display: block;
		margin-bottom: 0.5rem;
	}

	/* --- Concepts --- */
	.cards-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
		gap: 2rem;
	}
	.concept-card {
		border: 2px solid var(--text-main);
		padding: 2rem;
		background: white;
		transition: transform 0.3s;
	}
	.concept-card:hover { transform: translate(-5px, -5px); box-shadow: 5px 5px 0px var(--accent); }
	.divider { height: 4px; width: 30px; background: var(--accent); margin: 1rem 0; }

	/* --- Map --- */
    .map-section { padding: 4rem 2rem; background: #f8f9fa; }
    .content-wrapper { max-width: 1400px; margin: 0 auto; text-align: center; }
    .section-title { font-size: 2.5rem; margin-bottom: 1rem; color: #111; }
    .section-desc { font-size: 1.2rem; color: #666; margin-bottom: 3rem; max-width: 800px; margin-left: auto; margin-right: auto; }
    .map-container-full { width: 100%; min-height: 750px; }
    
    .loading-placeholder {
        width: 100%; height: 750px; background: #e5e7eb;
        border-radius: 12px; display: flex; flex-direction: column;
        align-items: center; justify-content: center; color: #6b7280;
    }
    .spinner {
        width: 40px; height: 40px; border: 4px solid #d1d5db;
        border-top-color: #3b82f6; border-radius: 50%;
        animation: spin 1s linear infinite; margin-bottom: 15px;
    }
    @keyframes spin { to { transform: rotate(360deg); } }

	/* --- Methodology (新增) --- */
	.method-section {
		background-color: var(--bg-dark); /* 深色背景，体现"Deep Dive" */
		color: var(--text-inverse);
	}
	.method-section .section-title { color: var(--text-inverse); }
	.method-grid {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 3rem;
	}
	.method-col h3 {
		font-family: var(--font-head);
		color: var(--accent);
		border-left: 3px solid var(--accent);
		padding-left: 1rem;
	}
	.method-col p { opacity: 0.9; font-size: 1.05rem; }

	/* --- Footer --- */
	.footer-section { background-color: #111; color: #888; padding: 4rem 0 2rem 0; }
	.footer-content { display: flex; flex-direction: column; gap: 3rem; }
	.school-info { display: flex; gap: 1.5rem; align-items: center; }
	.logo-box {
		width: 60px; height: 60px; background: #333; color: #fff;
		display: flex; align-items: center; justify-content: center;
		font-weight: bold; font-family: var(--font-head); font-size: 0.8rem;
	}
	.text-group h3 { margin: 0; font-family: var(--font-head); color: #fff; }
	.text-group p { margin: 0; font-size: 0.9rem; }
	.course-name { margin-top: 0.5rem !important; color: var(--accent); }
	.team-names { border-top: 1px solid #333; padding-top: 1.5rem; font-family: var(--font-head); color: #fff; }
	.copyright { margin-top: 3rem; font-size: 0.8rem; opacity: 0.4; }

	@media (max-width: 768px) {
		.context-grid, .method-grid { grid-template-columns: 1fr; }
		.main-title { font-size: 2.5rem; }
	}
</style>