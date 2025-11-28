<script>
  import { onMount, onDestroy } from 'svelte';
  import { base } from '$app/paths'; // <--- 新增这一行

  // --- 1. 内置数据 (保持不变) ---
  const complianceData = [
    { rank: 1, lat: 39.9425, lng: -75.1886, id: "110000744990", score: 0.99 },
    { rank: 2, lat: 39.9147, lng: -75.2005, id: "110000336994", score: 0.99 },
    { rank: 3, lat: 39.947892, lng: -75.192753, id: "110071498954", score: 0.98 },
    { rank: 4, lat: 39.949037, lng: -75.155787, id: "110001224648", score: 0.93 },
    { rank: 5, lat: 39.979354, lng: -75.151017, id: "110001223104", score: 0.92 },
    { rank: 6, lat: 39.952619, lng: -75.192879, id: "110000880547", score: 0.84 },
    { rank: 7, lat: 39.98236, lng: -75.08861, id: "110037149495", score: 0.82 },
    { rank: 8, lat: 39.99225, lng: -75.11894, id: "110000336903", score: 0.77 },
    { rank: 9, lat: 39.90444, lng: -75.16333, id: "110000336789", score: 0.77 },
    { rank: 10, lat: 40.01083, lng: -75.04239, id: "110000337092", score: 0.75 },
    { rank: 11, lat: 39.956793, lng: -75.16568, id: "110006509170", score: 0.74 },
    { rank: 12, lat: 39.9928, lng: -75.0784, id: "110001224167", score: 0.69 },
    { rank: 13, lat: 40.0816, lng: -75.0232, id: "110000611593", score: 0.68 },
    { rank: 14, lat: 40.007567, lng: -75.093411, id: "110041933829", score: 0.65 },
    { rank: 15, lat: 39.99143, lng: -75.08499, id: "110071095301", score: 0.64 },
    { rank: 16, lat: 39.954045, lng: -75.151756, id: "110055490729", score: 0.63 },
    { rank: 17, lat: 39.92348, lng: -75.23073, id: "110000336823", score: 0.61 },
    { rank: 18, lat: 39.93282, lng: -75.19149, id: "110000336645", score: 0.59 },
    { rank: 19, lat: 39.95764, lng: -75.228511, id: "110012574034", score: 0.58 },
    { rank: 20, lat: 39.92723, lng: -75.22236, id: "110000336958", score: 0.58 },
    { rank: 21, lat: 39.99583, lng: -75.11261, id: "110000336912", score: 0.55 },
    { rank: 22, lat: 40.03158, lng: -75.02231, id: "110000767137", score: 0.53 },
    { rank: 23, lat: 40.02107, lng: -75.06822, id: "110000337038", score: 0.51 },
    { rank: 24, lat: 39.943069, lng: -75.190723, id: "110000337029", score: 0.48 },
    { rank: 25, lat: 40.031275, lng: -75.021765, id: "110041235865", score: 0.469 },
    { rank: 26, lat: 39.95276, lng: -75.14993, id: "110023737134", score: 0.455 },
    { rank: 27, lat: 39.9671, lng: -75.1269, id: "110000336716", score: 0.448 },
    { rank: 28, lat: 40.03795, lng: -75.1119, id: "110000336636", score: 0.435 },
    { rank: 29, lat: 39.98361, lng: -75.088364, id: "110000878756", score: 0.420 },
    { rank: 30, lat: 39.95246, lng: -75.20984, id: "110001214347", score: 0.418 }
  ];

  const harmData = [
    { rank: 1, lat: 39.9425, lng: -75.1886, id: "110000744990", score: 15448990690 },
    { rank: 2, lat: 39.9147, lng: -75.2005, id: "110000336994", score: 32837300 },
    { rank: 3, lat: 39.89307, lng: -75.178223, id: "110017421654", score: 9065118 },
    { rank: 4, lat: 39.99143, lng: -75.08499, id: "110071095301", score: 6727436 },
    { rank: 5, lat: 39.875624, lng: -75.245164, id: "110007027289", score: 4986972 },
    { rank: 6, lat: 39.947892, lng: -75.192753, id: "110071498954", score: 4314127 },
    { rank: 7, lat: 39.96111, lng: -75.219447, id: "110004856184", score: 4192938 },
    { rank: 8, lat: 40.007567, lng: -75.093411, id: "110041933829", score: 3928167 },
    { rank: 9, lat: 40.0816, lng: -75.0232, id: "110000611593", score: 3926861 },
    { rank: 10, lat: 39.98236, lng: -75.08861, id: "110037149495", score: 3672076 },
    { rank: 11, lat: 39.949037, lng: -75.155787, id: "110001224648", score: 3656113 },
    { rank: 12, lat: 39.952619, lng: -75.192879, id: "110000880547", score: 3514081 },
    { rank: 13, lat: 40.0062, lng: -75.0682, id: "110000336770", score: 3487002 },
    { rank: 14, lat: 39.99225, lng: -75.11894, id: "110000336903", score: 3424177 },
    { rank: 15, lat: 39.93282, lng: -75.19149, id: "110000336645", score: 3409419 },
    { rank: 16, lat: 40.03816, lng: -75.03328, id: "110045580665", score: 3379020 },
    { rank: 17, lat: 39.92348, lng: -75.23073, id: "110000336823", score: 3375836 },
    { rank: 18, lat: 39.979354, lng: -75.151017, id: "110001223104", score: 3121528 },
    { rank: 19, lat: 40.03158, lng: -75.02231, id: "110000767137", score: 3108154 },
    { rank: 20, lat: 39.90444, lng: -75.16333, id: "110000336789", score: 2984534 },
    { rank: 21, lat: 40.01083, lng: -75.04239, id: "110000337092", score: 2883492 },
    { rank: 22, lat: 39.956793, lng: -75.16568, id: "110006509170", score: 2838327 },
    { rank: 23, lat: 40.040236, lng: -75.006155, id: "110002102496", score: 2823106 },
    { rank: 24, lat: 40.242057, lng: -75.283204, id: "110054889625", score: 2642844 },
    { rank: 25, lat: 39.96111, lng: -75.219447, id: "110004856040", score: 2621939 },
    { rank: 26, lat: 39.832588, lng: -75.424143, id: "110043797585", score: 2582410 },
    { rank: 27, lat: 39.88613, lng: -75.21825, id: "110040863768", score: 2482618 },
    { rank: 28, lat: 40.11356, lng: -74.99651, id: "110070492404", score: 2333742 },
    { rank: 29, lat: 40.10972, lng: -75.034785, id: "110000336609", score: 2330336 },
    { rank: 30, lat: 40.01353, lng: -75.03369, id: "110000336814", score: 2307185 }
  ];

  const metrics = [
    { value: 'percent_black_nh', label: 'Black (Non-Hispanic)', desc: 'Concentrated in North & West Philadelphia' },
    { value: 'percent_white_nh', label: 'White (Non-Hispanic)', desc: 'Concentrated in Center City & Northeast' },
    { value: 'percent_asian_pi_nh', label: 'Asian / Pacific Islander', desc: 'Clusters in South Philly & Chinatown' },
    { value: 'percent_hispanic', label: 'Hispanic', desc: 'Concentrated in North Philadelphia (East)' },
    { value: 'percent_multiracial_nh', label: 'Multiracial', desc: 'Distributed throughout the city' }
  ];

  let selectedMetric = 'percent_black_nh';
  
  // --- 控制状态 ---
  let showModelA = false;
  let showModelB = false;
  let rankFilterA = 'all'; // 'all', '1-10', '11-20', '21-30'
  let rankFilterB = 'all'; 

  let map;
  let L;
  let geoJsonLayer;
  let facilityLayerGroup;
  let mapContainer;

  // --- 2. 颜色逻辑 ---
  function getColor(d) {
    return d > 80 ? '#4a1486' : // Deep Purple
           d > 60 ? '#6a51a3' :
           d > 40 ? '#807dba' :
           d > 20 ? '#9e9ac8' :
           d > 10 ? '#bcbddc' :
           d > 5  ? '#dadaeb' :
           d > 0  ? '#f2f0f7' : 
                    '#ffffff';
  }

  function style(feature) {
    const props = feature.properties;
    const val = props[selectedMetric] ?? props[selectedMetric.toUpperCase()] ?? 0;
    return {
      fillColor: getColor(val),
      weight: 1, opacity: 1, color: 'white', fillOpacity: 0.75
    };
  }

  function getRankColor(rank, type) {
      const lightness = 40 + ((rank - 1) / 30) * 45; 
      if (type === 'compliance') return `hsl(210, 90%, ${lightness}%)`;
      else return `hsl(0, 85%, ${lightness}%)`;
  }

  // --- 3. 新增：重置视角函数 ---
  function resetView() {
      if (map) {
          map.setView([40.0, -75.1652], 11);
      }
  }

  // --- 4. 更新工厂点位 ---
  function updateFacilities() {
    if (!map || !L || !facilityLayerGroup) return;
    
    facilityLayerGroup.clearLayers();

    const addPoints = (data, type, rankFilter) => {
        let filteredData = data;
        
        if (rankFilter === '1-10') filteredData = data.filter(d => d.rank <= 10);
        else if (rankFilter === '11-20') filteredData = data.filter(d => d.rank >= 11 && d.rank <= 20);
        else if (rankFilter === '21-30') filteredData = data.filter(d => d.rank >= 21 && d.rank <= 30);

        filteredData.forEach(d => {
            const pointColor = getRankColor(d.rank, type);
            const iconHtml = `
              <div class="facility-marker-container">
                  <div class="dot" style="background-color: ${pointColor};"></div>
                  <div class="label" style="color: ${pointColor};">${d.rank}</div>
              </div>
            `;

            const icon = L.divIcon({
              className: 'custom-div-icon',
              html: iconHtml,
              iconSize: [20, 20],
              iconAnchor: [6, 6] 
            });

            const marker = L.marker([d.lat, d.lng], { 
                icon: icon, 
                zIndexOffset: (10000 - d.rank) + (type === 'harm' ? 50 : 0)
            });

            const scoreDisplay = Math.round(d.score).toLocaleString();
            const typeLabel = type === 'compliance' ? 'Compliance Model' : 'Harm Model';
            
            marker.bindPopup(`
              <div class="popup-content">
                  <div class="popup-header" style="color:${pointColor}">
                    ${typeLabel} #${d.rank}
                  </div>
                  <div><strong>ID:</strong> ${d.id}</div>
                  <div><strong>Score:</strong> ${scoreDisplay}</div>
              </div>
            `);
            facilityLayerGroup.addLayer(marker);
        });
    };

    if (showModelA) addPoints(complianceData, 'compliance', rankFilterA);
    if (showModelB) addPoints(harmData, 'harm', rankFilterB);
  }

  // --- 5. 响应式监听 ---
  $: if (geoJsonLayer && selectedMetric) geoJsonLayer.setStyle(style);
  
  $: if (map && facilityLayerGroup && (showModelA || !showModelA || showModelB || !showModelB || rankFilterA || rankFilterB)) {
      updateFacilities();
  }

  onMount(async () => {
    if (typeof window !== 'undefined') {
      try {
        const module = await import('leaflet');
        L = module.default;

        map = L.map(mapContainer, { zoomControl: false }).setView([40.0, -75.1652], 11);
        L.control.zoom({ position: 'topleft' }).addTo(map);

        L.tileLayer('https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png', {
          attribution: 'CARTO', subdomains: 'abcd', maxZoom: 19
        }).addTo(map);

        facilityLayerGroup = L.layerGroup().addTo(map);

        const res = await fetch(`${base}/Vital_Population_CT.geojson`);
        if (res.ok) {
            const data = await res.json();
            geoJsonLayer = L.geoJson(data, { 
                style: style,
                onEachFeature: (feature, layer) => {
                    const name = feature.properties.geography_name || 'Tract';
                    layer.bindPopup(`<strong>Census Tract:</strong> ${name}`);
                    layer.on('mouseover', e => { 
                        e.target.setStyle({ weight: 2, color: '#333' }); 
                        e.target.bringToFront(); 
                        if(facilityLayerGroup) facilityLayerGroup.bringToFront(); 
                    });
                    layer.on('mouseout', e => geoJsonLayer.resetStyle(e.target));
                }
            }).addTo(map);
            map.fitBounds(geoJsonLayer.getBounds());
        }
        
        addLegend();
      } catch (e) { console.error("Map init error:", e); }
    }
  });

  function addLegend() {
      if(!L || !map) return;
      const legend = L.control({position: 'bottomleft'});
      legend.onAdd = () => {
          const div = L.DomUtil.create('div', 'info legend');
          const grades = [0, 10, 20, 40, 60, 80];
          div.innerHTML = '<h6>Population %</h6>';
          for (let i = 0; i < grades.length; i++) {
              div.innerHTML += `<div class="legend-item"><i style="background:${getColor(grades[i] + 1)}"></i> ${grades[i]}${grades[i+1]?'&ndash;'+grades[i+1]:'+'}%</div>`;
          }
          return div;
      };
      legend.addTo(map);
  }

  onDestroy(() => { if (map) map.remove(); });
</script>

<svelte:head>
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
</svelte:head>

<div class="dashboard">
    <!-- 左侧地图：改为 wrapper 结构以容纳 Reset 按钮 -->
    <div class="map-panel">
        <div class="leaflet-map" bind:this={mapContainer}></div>
        
        <!-- Reset 按钮：绝对定位在左上角 (Zoom 控件下方) -->
        <button class="reset-btn" on:click={resetView} title="Reset View">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <circle cx="12" cy="12" r="10"></circle>
                <circle cx="12" cy="12" r="3"></circle>
                <line x1="12" y1="2" x2="12" y2="22"></line>
                <line x1="2" y1="12" x2="22" y2="12"></line>
            </svg>
        </button>
    </div>

    <!-- 右侧控制栏 -->
    <div class="sidebar">
        <div class="sidebar-header">
            <h3>Philly EJ Dashboard</h3>
            <p>Compare algorithmic enforcement strategies.</p>
        </div>

        <!-- 1. 人口 (背景) -->
        <div class="control-group">
            <div class="group-label">1. Demographic Layer (Purple)</div>
            <div class="radio-list">
                {#each metrics as metric}
                    <label class="radio-item" class:selected={selectedMetric === metric.value}>
                        <input type="radio" bind:group={selectedMetric} value={metric.value} />
                        <div class="radio-text">
                            <span class="label">{metric.label}</span>
                            <span class="desc">{metric.desc}</span>
                        </div>
                    </label>
                {/each}
            </div>
        </div>

        <!-- 2. 模型与过滤 (点位) -->
        <div class="control-group">
            <div class="group-label">2. Inspection Models & Rank</div>
            
            <!-- Model A Card -->
            <div class="model-card-container">
                <button class="model-btn compliance" class:active={showModelA} on:click={() => showModelA = !showModelA}>
                    <div class="btn-icon blue">A</div>
                    <div class="btn-text">
                        <span class="btn-title">Model A: Compliance</span>
                        <span class="btn-desc">Targets frequent violators (Blue)</span>
                    </div>
                    <div class="checkbox-indicator">{showModelA ? 'ON' : 'OFF'}</div>
                </button>
                <div class="rank-row" class:disabled={!showModelA}>
                    <button class="rank-chip" class:active={rankFilterA === 'all'} on:click={() => rankFilterA = 'all'}>All</button>
                    <button class="rank-chip" class:active={rankFilterA === '1-10'} on:click={() => rankFilterA = '1-10'}>1-10</button>
                    <button class="rank-chip" class:active={rankFilterA === '11-20'} on:click={() => rankFilterA = '11-20'}>11-20</button>
                    <button class="rank-chip" class:active={rankFilterA === '21-30'} on:click={() => rankFilterA = '21-30'}>21-30</button>
                </div>
            </div>

            <!-- Model B Card -->
            <div class="model-card-container">
                <button class="model-btn harm" class:active={showModelB} on:click={() => showModelB = !showModelB}>
                    <div class="btn-icon red">B</div>
                    <div class="btn-text">
                        <span class="btn-title">Model B: Harm Reduction</span>
                        <span class="btn-desc">Targets major polluters (Red)</span>
                    </div>
                    <div class="checkbox-indicator">{showModelB ? 'ON' : 'OFF'}</div>
                </button>
                <div class="rank-row" class:disabled={!showModelB}>
                    <button class="rank-chip" class:active={rankFilterB === 'all'} on:click={() => rankFilterB = 'all'}>All</button>
                    <button class="rank-chip" class:active={rankFilterB === '1-10'} on:click={() => rankFilterB = '1-10'}>1-10</button>
                    <button class="rank-chip" class:active={rankFilterB === '11-20'} on:click={() => rankFilterB = '11-20'}>11-20</button>
                    <button class="rank-chip" class:active={rankFilterB === '21-30'} on:click={() => rankFilterB = '21-30'}>21-30</button>
                </div>
            </div>

        </div>
    </div>
</div>

<style>
    .dashboard { display: flex; width: 100%; height: 750px; background: white; border-radius: 12px; overflow: hidden; box-shadow: 0 4px 20px rgba(0,0,0,0.08); border: 1px solid #e5e7eb; }
    
    /* 左侧地图容器，设为相对定位 */
    .map-panel { flex: 1; height: 100%; position: relative; background: #f3f4f6; }
    .leaflet-map { width: 100%; height: 100%; z-index: 1; }

    /* Reset 按钮样式 - 仿 Leaflet 原生风格 */
    .reset-btn {
        position: absolute;
        top: 80px; /* 位于缩放控件下方 */
        left: 10px;
        z-index: 1000;
        background: white;
        border: 2px solid rgba(0,0,0,0.2);
        border-radius: 4px;
        width: 30px; height: 30px;
        padding: 5px;
        cursor: pointer;
        display: flex; align-items: center; justify-content: center;
        background-clip: padding-box;
    }
    .reset-btn:hover { background: #f4f4f4; }
    .reset-btn svg { width: 18px; height: 18px; stroke: #444; }

    /* Sidebar Styles */
    .sidebar { width: 340px; background: #fff; border-left: 1px solid #e5e7eb; display: flex; flex-direction: column; overflow-y: auto; }
    .sidebar-header { padding: 20px; background: #f9fafb; border-bottom: 1px solid #eee; }
    .sidebar-header h3 { margin: 0; font-size: 1.25rem; color: #111; }
    .sidebar-header p { margin: 5px 0 0; color: #666; font-size: 0.9rem; }
    .control-group { padding: 20px; border-bottom: 1px solid #eee; }
    .group-label { font-size: 0.75rem; text-transform: uppercase; font-weight: 700; color: #9ca3af; margin-bottom: 12px; }
    
    .radio-list { display: flex; flex-direction: column; gap: 8px; }
    .radio-item { display: flex; align-items: flex-start; gap: 10px; padding: 10px; border-radius: 8px; border: 1px solid #e5e7eb; cursor: pointer; transition: all 0.2s; }
    .radio-item:hover { background: #f9fafb; }
    .radio-item.selected { background: #f3e8ff; border-color: #7e22ce; box-shadow: 0 0 0 1px #7e22ce; }
    .radio-item input { margin-top: 4px; accent-color: #7e22ce; }
    .radio-text { display: flex; flex-direction: column; }
    .label { font-weight: 600; font-size: 0.9rem; color: #374151; }
    .desc { font-size: 0.75rem; color: #6b7280; }

    .model-card-container { margin-bottom: 15px; border: 1px solid #e5e7eb; border-radius: 8px; padding: 8px; background: #fafafa; }
    .model-btn { display: flex; align-items: center; gap: 10px; width: 100%; text-align: left; padding: 8px; background: white; border: 1px solid #e5e7eb; border-radius: 6px; cursor: pointer; transition: all 0.2s; margin-bottom: 8px; }
    .model-btn:hover { background: #f9fafb; }
    .btn-icon { width: 28px; height: 28px; border-radius: 5px; display: flex; align-items: center; justify-content: center; font-weight: bold; color: white; font-size: 0.9rem; flex-shrink: 0; }
    .btn-icon.blue { background: #3b82f6; }
    .btn-icon.red { background: #ef4444; }
    .btn-text { flex: 1; display: flex; flex-direction: column; }
    .btn-title { font-weight: 700; font-size: 0.85rem; color: #111; }
    .btn-desc { font-size: 0.7rem; color: #666; }
    .checkbox-indicator { font-size: 0.7rem; font-weight: 700; color: #ccc; }

    .model-btn.compliance.active { background: #eff6ff; border-color: #3b82f6; }
    .model-btn.compliance.active .checkbox-indicator { color: #3b82f6; }
    .model-btn.harm.active { background: #fef2f2; border-color: #ef4444; }
    .model-btn.harm.active .checkbox-indicator { color: #ef4444; }

    .rank-row { display: flex; gap: 6px; }
    .rank-row.disabled { opacity: 0.4; pointer-events: none; }
    .rank-chip { flex: 1; padding: 4px 0; font-size: 0.75rem; text-align: center; border: 1px solid #e5e7eb; background: white; border-radius: 4px; cursor: pointer; color: #666; transition: all 0.1s; }
    .rank-chip:hover { background: #f3f4f6; }
    .rank-chip.active { background: #374151; color: white; border-color: #374151; font-weight: 600; }

    :global(.dot) { width: 12px; height: 12px; border-radius: 50%; border: 2px solid white; box-shadow: 0 2px 4px rgba(0,0,0,0.3); position: absolute; top: 0; left: 0; }
    :global(.facility-marker-container .label) { position: absolute; left: 12px; top: -6px; font-size: 11px; font-weight: 900; text-shadow: -1px -1px 0 #fff, 1px -1px 0 #fff, -1px 1px 0 #fff, 1px 1px 0 #fff; pointer-events: none; }
    :global(.popup-header) { font-weight: bold; padding-bottom: 4px; margin-bottom: 4px; border-bottom: 1px solid #eee; }
    :global(.info.legend) { background: white; padding: 8px; border-radius: 6px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); font-size: 12px; }
    :global(.info.legend h6) { margin: 0 0 5px; color: #555; font-size: 11px; text-transform: uppercase; font-weight: bold; }
    :global(.legend-item) { display: flex; align-items: center; margin-bottom: 3px; }
    :global(.legend-item i) { width: 14px; height: 14px; margin-right: 6px; opacity: 0.8; }
</style>