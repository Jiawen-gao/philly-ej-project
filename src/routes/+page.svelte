<script>
	// 脚本区域：将来用于控制地图的逻辑
</script>

<svelte:head>
	<title>Philly Algorithmic Justice</title>
	<link href="https://fonts.googleapis.com/css2?family=DM+Sans:opsz,wght@9..40,400;500&family=Space+Grotesk:wght@500;700&display=swap" rel="stylesheet">
</svelte:head>

<nav class="navbar">
	<div class="nav-container">
		<div class="brand">PHI / AIR / DATA</div>
		
		<ul class="nav-links">
			<li><a href="#overview" class="nav-item">Vision</a></li>
			<li><a href="#context" class="nav-item">Context</a></li> <li><a href="#concepts" class="nav-item">Frameworks</a></li>
			<li><a href="#map" class="nav-item">The Map</a></li>
			<li><a href="#team" class="nav-item">About</a></li>
		</ul>
	</div>
</nav>

<main>
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
				We investigate the hidden logic behind environmental enforcement and propose a <strong>Harm-Reduction Model</strong> that puts community health first.
			</p>
			
			<a href="#map" class="cta-button">Launch Data Map →</a>
		</div>
	</section>

	<section id="context" class="context-section">
		<div class="content-wrapper grid-layout">
			<div class="text-col">
				<h2 class="section-title">The Invisible Problem</h2>
				<p>
					In Philadelphia, decisions about where to inspect for pollution are often driven by opaque systems. 
					When enforcement relies on complaints or outdated "compliance" metrics, silent communities suffer the most.
				</p>
			</div>
			<div class="visual-col">
				<div class="abstract-box">
					<div class="line"></div>
					<div class="line"></div>
					<div class="line"></div>
				</div>
			</div>
		</div>
	</section>

	<section id="concepts" class="concepts-section">
		<div class="content-wrapper">
			<h2 class="section-title">Critical Frameworks</h2>
			<div class="cards-grid">
				
				<div class="concept-card">
					<h3>Environmental Justice</h3>
					<div class="divider"></div>
					<p>Fair treatment and meaningful involvement for all people.</p>
				</div>
				
				<div class="concept-card">
					<h3>Distributive Justice</h3>
					<div class="divider"></div>
					<p>Outcomes: Are pollution burdens shared equally?</p>
				</div>
				
				<div class="concept-card">
					<h3>Procedural Justice</h3>
					<div class="divider"></div>
					<p>Process: Is the decision-making transparent?</p>
				</div>

			</div>
		</div>
	</section>

	<section id="map" class="map-section">
		<div class="content-wrapper">
			<h2 class="section-title">Visualizing the Shift</h2>
			<p class="section-desc">
				<strong>Left:</strong> Current Compliance Model vs. <strong>Right:</strong> Proposed Harm-Reduction Model
			</p>
			
			<div class="map-placeholder">
				<div class="loader">
					<div class="bar"></div>
					<div class="bar"></div>
					<div class="bar"></div>
				</div>
				<p>Interactive Map Module Loading...</p>
			</div>
		</div>
	</section>

	<section id="team" class="footer-section">
		<div class="content-wrapper">
			
			<div class="footer-content">
				<div class="school-info">
					<div class="logo-box">SP2 LOGO</div>
					<div class="text-group">
						<h3>University of Pennsylvania</h3>
						<p>School of Social Policy & Practice</p>
						<p class="course-name">Course: Democratizing Data (Critical Data Studies)</p>
					</div>
				</div>

				<div class="team-names">
					<p><strong>Project Team:</strong> Jiawen / Bosi Ding / Yiping Miao</p>
				</div>
			</div>

			<div class="copyright">
				Designed for Assignment 2. Fall 2024.
			</div>
		</div>
	</section>

</main>

<style>
	/* --- 1. 配色方案 (Color Palette) --- */
	:root {
		/* 主色：深海蓝绿 (Deep Teal) - 代表环境、数据、深度 */
		--primary: #0F4C5C; 
		
		/* 强调色：活力珊瑚橙 (Coral) - 代表行动、警示、高亮 */
		--accent: #E36414;
		
		/* 背景色：米白色 (Off-white) - 柔和，不刺眼 */
		--bg-main: #FBF8F3; 
		
		/* 辅助背景：淡沙色 */
		--bg-alt: #EFEBE0;

		/* 文字颜色 */
		--text-main: #1A282D;
		--text-light: #5F6C72;

		/* 字体变量 */
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

	/* --- 2. 导航栏 (Navbar) --- */
	.navbar {
		position: sticky;
		top: 0;
		background: rgba(251, 248, 243, 0.9); /* 与背景色一致的半透明 */
		backdrop-filter: blur(8px);
		border-bottom: 1px solid rgba(0,0,0,0.05);
		z-index: 1000;
		padding: 1.5rem 0;
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
		gap: 2rem;
		list-style: none;
		margin: 0;
		padding: 0;
	}

	.nav-item {
		text-decoration: none;
		color: var(--text-main);
		font-family: var(--font-head); /* 导航用标题字体，更有设计感 */
		font-weight: 500;
		font-size: 0.95rem;
		transition: color 0.3s;
	}

	.nav-item:hover {
		color: var(--accent); /* 悬浮变成橙色 */
		text-decoration: underline;
		text-decoration-thickness: 2px;
		text-underline-offset: 4px;
	}

	/* --- 3. 通用布局 --- */
	.content-wrapper {
		max-width: 1000px;
		margin: 0 auto;
		padding: 0 2rem;
	}
	
	section {
		padding: 5rem 0;
	}

	.section-title {
		font-family: var(--font-head);
		font-size: 2.5rem;
		color: var(--primary);
		margin-bottom: 2rem;
	}

	/* --- 4. Hero Section --- */
	.hero-section {
		padding-top: 6rem;
		padding-bottom: 6rem;
	}

	.main-title {
		font-family: var(--font-head);
		font-size: 4rem; /* 巨大标题 */
		line-height: 1;
		margin-bottom: 1.5rem;
		color: var(--primary);
	}

	.highlight {
		color: var(--accent); /* 橙色高亮 */
		font-style: italic; /* 斜体增加动感 */
	}

	.subtitle {
		font-size: 1.5rem;
		font-weight: 500;
		margin-bottom: 1rem;
		color: var(--text-main);
	}

	.description {
		max-width: 600px;
		font-size: 1.1rem;
		color: var(--text-light);
		margin-bottom: 2.5rem;
	}

	.cta-button {
		display: inline-block;
		background: var(--accent);
		color: white;
		padding: 1rem 2.5rem;
		text-decoration: none;
		font-family: var(--font-head);
		font-weight: 700;
		border-radius: 4px; /* 直角微圆，更硬朗 */
		transition: background 0.3s, transform 0.2s;
	}

	.cta-button:hover {
		background: #C04F0B; /* 深橙色 */
		transform: translateY(-2px);
	}

	/* --- 5. Context Section (背景) --- */
	.context-section {
		background-color: var(--bg-alt); /* 浅沙色背景区分 */
	}

	.grid-layout {
		display: grid;
		grid-template-columns: 1.5fr 1fr;
		gap: 4rem;
		align-items: center;
	}

	/* 抽象黑箱装饰 */
	.abstract-box {
		width: 100%;
		height: 200px;
		background: var(--primary);
		display: flex;
		flex-direction: column;
		justify-content: center;
		padding: 20px;
		gap: 15px;
	}
	.line {
		height: 2px;
		background: rgba(255,255,255,0.2);
		width: 100%;
	}
	.line:nth-child(2) { width: 70%; }
	.line:nth-child(3) { width: 40%; }

	/* --- 6. Frameworks Section --- */
	.cards-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
		gap: 2rem;
	}

	.concept-card {
		border: 2px solid var(--text-main); /* 粗边框，波普/布鲁塔主义风格 */
		padding: 2rem;
		background: white;
		transition: transform 0.3s;
	}

	.concept-card:hover {
		transform: translate(-5px, -5px);
		box-shadow: 5px 5px 0px var(--accent); /* 硬阴影 */
	}

	.concept-card h3 {
		font-family: var(--font-head);
		font-size: 1.4rem;
		margin-top: 0;
	}

	.divider {
		height: 4px;
		width: 30px;
		background: var(--accent);
		margin: 1rem 0;
	}

	/* --- 7. Map Section --- */
	.map-placeholder {
		width: 100%;
		height: 500px;
		background: #E0E4E6;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		font-family: var(--font-head);
		color: var(--text-light);
	}

	/* 简单的加载动画 */
	.loader {
		display: flex;
		gap: 5px;
		margin-bottom: 1rem;
	}
	.bar {
		width: 10px;
		height: 30px;
		background: var(--primary);
		animation: stretch 1s infinite ease-in-out;
	}
	.bar:nth-child(2) { animation-delay: 0.1s; }
	.bar:nth-child(3) { animation-delay: 0.2s; }

	@keyframes stretch {
		0%, 100% { height: 30px; }
		50% { height: 50px; }
	}

	/* --- 8. Footer Section --- */
	.footer-section {
		background-color: var(--text-main); /* 近乎黑色的背景 */
		color: var(--bg-main);
		padding: 4rem 0 2rem 0;
	}

	.footer-content {
		display: flex;
		flex-direction: column;
		gap: 3rem;
	}

	.school-info {
		display: flex;
		gap: 1.5rem;
		align-items: center;
	}

	.logo-box {
		width: 60px;
		height: 60px;
		background: var(--bg-main);
		color: var(--primary);
		display: flex;
		align-items: center;
		justify-content: center;
		font-weight: bold;
		font-family: var(--font-head);
		font-size: 0.8rem;
		text-align: center;
	}

	.text-group h3 {
		margin: 0;
		font-family: var(--font-head);
	}
	.text-group p {
		margin: 0;
		opacity: 0.8;
		font-size: 0.9rem;
	}
	.course-name {
		margin-top: 0.5rem !important;
		color: var(--accent);
	}

	.team-names {
		border-top: 1px solid rgba(255,255,255,0.1);
		padding-top: 1.5rem;
		font-family: var(--font-head);
	}

	.copyright {
		margin-top: 3rem;
		font-size: 0.8rem;
		opacity: 0.4;
	}

	/* 响应式适配 */
	@media (max-width: 768px) {
		.grid-layout { grid-template-columns: 1fr; }
		.main-title { font-size: 2.8rem; }
	}
</style>