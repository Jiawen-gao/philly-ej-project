<script>
  import { onMount, onDestroy } from 'svelte';

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
    { rank: 25, lat: 40.031275, lng: -75.021765, id: "110041235865", score: 0.47 },
    { rank: 26, lat: 39.95276, lng: -75.14993, id: "110023737134", score: 0.45 },
    { rank: 27, lat: 39.9671, lng: -75.1269, id: "110000336716", score: 0.44 },
    { rank: 28, lat: 40.03795, lng: -75.1119, id: "110000336636", score: 0.43 },
    { rank: 29, lat: 39.98361, lng: -75.088364, id: "110000878756", score: 0.42 },
    { rank: 30, lat: 39.95246, lng: -75.20984, id: "110001214347", score: 0.41 }
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
  let activeModel = null; 

  let map;
  let L;
  let geoJsonLayer;
  let facilityLayerGroup;
  let mapContainer;

  function getColor(d) {
    return d > 80 ? '#08306b' : d > 60 ? '#08519c' : d > 40 ? '#2171b5' : 
           d > 20 ? '#4292c6' : d > 10 ? '#6baed6' : d > 5  ? '#9ecae1' : 
           d > 0  ? '#c6dbef' : '#f7fbff';
  }

  function style(feature) {
    const props = feature.properties;
    const val = props[selectedMetric] ?? props[selectedMetric.toUpperCase()] ?? 0;
    return {
      fillColor: getColor(val),
      weight: 1, opacity: 1, color: 'white', fillOpacity: 0.75
    };
  }

  // --- 关键改进：根据排名生成渐变色 ---
  function getRankColor(rank, type) {
      // 颜色越深，排名越靠前 (Rank 1 = Darkest)
      // 计算亮度 (Lightness): Rank 1 -> 35%, Rank 30 -> 85%
      const lightness = 35 + ((rank - 1) / 30) * 50; 
      
      if (type === 'compliance') {
          // 蓝色系 (Hue 220)
          return `hsl(220, 90%, ${lightness}%)`;
      } else {
          // 红色系 (Hue 0)
          return `hsl(0, 85%, ${lightness}%)`;
      }
  }

  function updateFacilities() {
    if (!map || !L || !facilityLayerGroup) return;
    facilityLayerGroup.clearLayers();
    if (!activeModel) return;

    const data = activeModel === 'compliance' ? complianceData : harmData;
    const modelType = activeModel; // 'compliance' or 'harm'

    data.forEach(d => {
      const pointColor = getRankColor(d.rank, modelType);
      
      // --- 关键改进：Icon 样式 ---
      // 1. 小圆点 (dot)
      // 2. 旁注数字 (label) 绝对定位在圆点右上方
      const iconHtml = `
        <div class="facility-marker-container">
            <div class="dot" style="background-color: ${pointColor};"></div>
            <div class="label" style="color: ${pointColor};">${d.rank}</div>
        </div>
      `;

      const icon = L.divIcon({
        className: 'custom-div-icon', // 基础清除样式
        html: iconHtml,
        iconSize: [20, 20],   // 容器大小
        iconAnchor: [6, 6]    // 锚点在圆点中心 (圆点设为12px，所以大概是6)
      });

      const marker = L.marker([d.lat, d.lng], { 
          icon: icon, 
          // Rank 1 (Score高) 的 zIndex 最高，保证覆盖在其他点上面
          zIndexOffset: 10000 - d.rank 
      });

      const scoreDisplay = Math.round(d.score).toLocaleString();
      marker.bindPopup(`
        <div class="popup-content">
            <div class="popup-header" style="color:${pointColor}">Rank #${d.rank}</div>
            <div><strong>ID:</strong> ${d.id}</div>
            <div><strong>Score:</strong> ${scoreDisplay}</div>
        </div>
      `);
      facilityLayerGroup.addLayer(marker);
    });
  }

  $: if (geoJsonLayer && selectedMetric) geoJsonLayer.setStyle(style);
  $: if (map && facilityLayerGroup && (activeModel || activeModel === null)) updateFacilities();

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

        const res = await fetch('/Vital_Population_CT.geojson');
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
                        if(facilityLayerGroup) facilityLayerGroup.bringToFront(); // 保持点在最上
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
    <div class="map-panel" bind:this={mapContainer}></div>
    <div class="sidebar">
        <div class="sidebar-header">
            <h3>Philly EJ Dashboard</h3>
            <p>Compare algorithmic enforcement strategies.</p>
        </div>

        <div class="control-group">
            <div class="group-label">1. Demographic Layer</div>
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

        <div class="control-group">
            <div class="group-label">2. Inspection Models</div>
            
            <button class="model-btn compliance" class:active={activeModel === 'compliance'} on:click={() => activeModel = activeModel === 'compliance' ? null : 'compliance'}>
                <div class="btn-icon blue">A</div>
                <div class="btn-text">
                    <span class="btn-title">Model A: Compliance</span>
                    <span class="btn-desc">Targets frequent violators (Blue)</span>
                </div>
            </button>

            <button class="model-btn harm" class:active={activeModel === 'harm'} on:click={() => activeModel = activeModel === 'harm' ? null : 'harm'}>
                <div class="btn-icon red">B</div>
                <div class="btn-text">
                    <span class="btn-title">Model B: Harm Reduction</span>
                    <span class="btn-desc">Targets major polluters (Red)</span>
                </div>
            </button>
        </div>
    </div>
</div>

<style>
    /* CSS 美化 */
    .dashboard { display: flex; width: 100%; height: 750px; background: white; border-radius: 12px; overflow: hidden; box-shadow: 0 4px 20px rgba(0,0,0,0.08); border: 1px solid #e5e7eb; }
    .map-panel { flex: 1; height: 100%; z-index: 1; background: #f3f4f6; }
    .sidebar { width: 340px; background: #fff; border-left: 1px solid #e5e7eb; display: flex; flex-direction: column; overflow-y: auto; }
    .sidebar-header { padding: 20px; background: #f9fafb; border-bottom: 1px solid #eee; }
    .sidebar-header h3 { margin: 0; font-size: 1.25rem; color: #111; }
    .sidebar-header p { margin: 5px 0 0; color: #666; font-size: 0.9rem; }
    .control-group { padding: 20px; border-bottom: 1px solid #eee; }
    .group-label { font-size: 0.75rem; text-transform: uppercase; font-weight: 700; color: #9ca3af; margin-bottom: 12px; }
    
    .radio-list { display: flex; flex-direction: column; gap: 8px; }
    .radio-item { display: flex; align-items: flex-start; gap: 10px; padding: 10px; border-radius: 8px; border: 1px solid #e5e7eb; cursor: pointer; transition: all 0.2s; }
    .radio-item:hover { background: #f9fafb; }
    .radio-item.selected { background: #eff6ff; border-color: #3b82f6; box-shadow: 0 0 0 1px #3b82f6; }
    .radio-item input { margin-top: 4px; }
    .radio-text { display: flex; flex-direction: column; }
    .label { font-weight: 600; font-size: 0.9rem; color: #374151; }
    .desc { font-size: 0.75rem; color: #6b7280; }

    .model-btn { display: flex; align-items: center; gap: 12px; width: 100%; text-align: left; padding: 12px; margin-bottom: 10px; background: white; border: 1px solid #e5e7eb; border-radius: 8px; cursor: pointer; transition: all 0.2s; }
    .model-btn:hover { background: #f9fafb; transform: translateY(-1px); }
    .btn-icon { width: 32px; height: 32px; border-radius: 6px; display: flex; align-items: center; justify-content: center; font-weight: bold; color: white; flex-shrink: 0; }
    .btn-icon.blue { background: #3b82f6; }
    .btn-icon.red { background: #ef4444; }
    .btn-text { display: flex; flex-direction: column; }
    .btn-title { font-weight: 700; font-size: 0.95rem; color: #111; }
    .btn-desc { font-size: 0.8rem; color: #666; }
    .model-btn.compliance.active { background: #eff6ff; border-color: #3b82f6; box-shadow: inset 0 0 0 1px #3b82f6; }
    .model-btn.harm.active { background: #fef2f2; border-color: #ef4444; box-shadow: inset 0 0 0 1px #ef4444; }

    /* --- 新的 Marker 样式 --- */
    :global(.custom-div-icon) { background: transparent; border: none; overflow: visible; }
    
    /* 圆点 */
    :global(.dot) {
        width: 12px; height: 12px; border-radius: 50%;
        border: 2px solid white; 
        box-shadow: 0 2px 4px rgba(0,0,0,0.3);
        /* 确保点本身不偏移 */
        position: absolute; top: 0; left: 0;
    }

    /* 旁注数字 */
    :global(.facility-marker-container .label) {
        position: absolute;
        left: 12px; /* 移到点右侧 */
        top: -6px;  /* 稍微上移 */
        font-size: 11px;
        font-weight: 900;
        text-shadow: 
            -1px -1px 0 #fff,  
             1px -1px 0 #fff,
            -1px  1px 0 #fff,
             1px  1px 0 #fff; /* 白色描边增加可读性 */
        pointer-events: none; /* 让鼠标事件穿透数字直接点到圆点 */
    }

    :global(.popup-header) { font-weight: bold; padding-bottom: 4px; margin-bottom: 4px; border-bottom: 1px solid #eee; }
    :global(.info.legend) { background: white; padding: 8px; border-radius: 6px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); font-size: 12px; }
    :global(.info.legend h6) { margin: 0 0 5px; color: #555; font-size: 11px; text-transform: uppercase; font-weight: bold; }
    :global(.legend-item) { display: flex; align-items: center; margin-bottom: 3px; }
    :global(.legend-item i) { width: 14px; height: 14px; margin-right: 6px; opacity: 0.8; }
</style>