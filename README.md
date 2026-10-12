<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Peruvallur Grama Panchayat - Spatial GIS Atlas</title>

  <!-- Modern Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Space+Grotesk:wght@500;700&display=swap" rel="stylesheet">

  <style>
    :root {
      --bg-main: #0b0f19;
      --bg-surface: #121826;
      --bg-card: #182234;
      --border-color: #233047;
      --primary: #22c55e;
      --primary-glow: rgba(34, 197, 94, 0.25);
      --accent: #38bdf8;
      --text-main: #f8fafc;
      --text-muted: #94a3b8;
      --radius: 14px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Plus Jakarta Sans', sans-serif;
      background-color: var(--bg-main);
      color: var(--text-main);
      line-height: 1.6;
      scroll-behavior: smooth;
    }

    /* Top Navigation Header */
    header {
      position: sticky;
      top: 0;
      z-index: 100;
      backdrop-filter: blur(14px);
      background: rgba(11, 15, 25, 0.88);
      border-bottom: 1px solid var(--border-color);
      padding: 1rem 2.5rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .brand {
      font-family: 'Space Grotesk', sans-serif;
      font-weight: 700;
      font-size: 1.25rem;
      letter-spacing: -0.5px;
      color: var(--text-main);
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .brand span {
      background: linear-gradient(135deg, var(--primary), var(--accent));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }

    .nav-meta {
      font-size: 0.85rem;
      color: var(--text-muted);
      font-weight: 600;
    }

    /* Hero Section */
    .hero {
      padding: 4.5rem 2rem 2.5rem;
      max-width: 1200px;
      margin: 0 auto;
      text-align: center;
    }

    .badge {
      display: inline-block;
      padding: 0.35rem 1rem;
      font-size: 0.75rem;
      text-transform: uppercase;
      letter-spacing: 1px;
      font-weight: 700;
      color: var(--primary);
      background: rgba(34, 197, 94, 0.1);
      border: 1px solid rgba(34, 197, 94, 0.25);
      border-radius: 9999px;
      margin-bottom: 1.2rem;
    }

    .hero h1 {
      font-family: 'Space Grotesk', sans-serif;
      font-size: 2.85rem;
      line-height: 1.2;
      font-weight: 800;
      margin-bottom: 1rem;
      letter-spacing: -0.03em;
    }

    .hero p {
      font-size: 1.125rem;
      color: var(--text-muted);
      max-width: 820px;
      margin: 0 auto 2.5rem;
    }

    /* Stats Overview Cards */
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 1.25rem;
      max-width: 1200px;
      margin: 0 auto 3.5rem;
      padding: 0 1.5rem;
    }

    .stat-card {
      background: var(--bg-surface);
      border: 1px solid var(--border-color);
      border-radius: var(--radius);
      padding: 1.5rem;
      text-align: center;
      transition: transform 0.2s ease, border-color 0.2s ease;
    }

    .stat-card:hover {
      transform: translateY(-4px);
      border-color: var(--primary);
    }

    .stat-card h3 {
      font-family: 'Space Grotesk', sans-serif;
      font-size: 1.75rem;
      color: var(--accent);
      margin-bottom: 0.25rem;
    }

    .stat-card p {
      font-size: 0.8rem;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: 0.5px;
      font-weight: 600;
    }

    /* Filter Bar (Without 'All Maps') */
    .controls {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 0.75rem;
      margin-bottom: 3.5rem;
      padding: 0 1.5rem;
    }

    .filter-btn {
      background: var(--bg-surface);
      border: 1px solid var(--border-color);
      color: var(--text-muted);
      padding: 0.65rem 1.4rem;
      border-radius: 9999px;
      font-size: 0.875rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .filter-btn:hover, .filter-btn.active {
      background: var(--primary);
      color: #05140b;
      border-color: var(--primary);
      box-shadow: 0 0 16px var(--primary-glow);
    }

    /* Gallery Grid Layout */
    .gallery-container {
      max-width: 1380px;
      margin: 0 auto;
      padding: 0 2rem 5rem;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(360px, 1fr));
      gap: 2rem;
    }

    .map-card {
      background: var(--bg-surface);
      border: 1px solid var(--border-color);
      border-radius: var(--radius);
      overflow: hidden;
      display: none; /* Controlled by category filter script */
      flex-direction: column;
      transition: all 0.3s ease;
    }

    .map-card:hover {
      transform: translateY(-6px);
      border-color: rgba(56, 189, 248, 0.45);
      box-shadow: 0 12px 30px rgba(0,0,0,0.5);
    }

    .map-card .img-wrapper {
      position: relative;
      background: #000;
      width: 100%;
      height: 330px;
      overflow: hidden;
      cursor: pointer;
    }

    .map-card img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      background-color: #0b111c;
      transition: transform 0.4s ease;
    }

    .map-card:hover img {
      transform: scale(1.035);
    }

    .map-card .overlay {
      position: absolute;
      inset: 0;
      background: rgba(0, 0, 0, 0.45);
      opacity: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 600;
      color: #fff;
      font-size: 0.95rem;
      backdrop-filter: blur(2px);
      transition: opacity 0.2s ease;
    }

    .map-card .img-wrapper:hover .overlay {
      opacity: 1;
    }

    .map-content {
      padding: 1.5rem;
      display: flex;
      flex-direction: column;
      flex-grow: 1;
    }

    .layer-tag {
      font-size: 0.72rem;
      text-transform: uppercase;
      font-weight: 700;
      letter-spacing: 0.8px;
      color: var(--accent);
      margin-bottom: 0.45rem;
    }

    .map-content h2 {
      font-size: 1.25rem;
      font-weight: 700;
      margin-bottom: 0.6rem;
      letter-spacing: -0.01em;
    }

    .map-content p {
      font-size: 0.875rem;
      color: var(--text-muted);
      line-height: 1.5;
      margin-bottom: 1.2rem;
      flex-grow: 1;
    }

    .tech-specs {
      border-top: 1px solid var(--border-color);
      padding-top: 0.8rem;
      display: flex;
      justify-content: space-between;
      font-size: 0.75rem;
      color: #64748b;
    }

       /* WebGIS Interactive Map Launch Section */
    .interactive-launch-section {
      text-align: center;
      padding: 2.5rem 1.5rem 4.5rem;
      max-width: 900px;
      margin: 0 auto;
    }

    .webgis-launch-btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 12px;
      background: linear-gradient(135deg, #22c55e, #0ea5e9);
      color: #041017;
      font-family: 'Space Grotesk', sans-serif;
      font-weight: 700;
      font-size: 1.1rem;
      padding: 1.1rem 2.4rem;
      border-radius: 9999px;
      text-decoration: none;
      box-shadow: 0 10px 25px rgba(34, 197, 94, 0.35);
      border: 1px solid rgba(255, 255, 255, 0.2);
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      cursor: pointer;
    }

    .webgis-launch-btn:hover {
      transform: translateY(-4px) scale(1.02);
      box-shadow: 0 16px 35px rgba(56, 189, 248, 0.45);
      color: #000;
    }

    .webgis-launch-btn svg {
      transition: transform 0.3s ease;
    }

    .webgis-launch-btn:hover svg {
      transform: scale(1.15) rotate(5deg);
    }

    .launch-subtext {
      margin-top: 0.85rem;
      font-size: 0.85rem;
      color: var(--text-muted);
    }


    /* Modal / Lightbox */
    .modal {
      position: fixed;
      inset: 0;
      background: rgba(4, 7, 13, 0.94);
      backdrop-filter: blur(8px);
      z-index: 999;
      display: none;
      align-items: center;
      justify-content: center;
      padding: 2rem;
    }

    .modal.active {
      display: flex;
    }

    .modal-content {
      position: relative;
      max-width: 90vw;
      max-height: 90vh;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .modal img {
      max-width: 100%;
      max-height: 82vh;
      object-fit: contain;
      border-radius: 8px;
      border: 1px solid var(--border-color);
    }

    .modal-caption {
      margin-top: 1rem;
      font-size: 1.05rem;
      color: var(--text-main);
      font-weight: 600;
      text-align: center;
    }

    .close-btn {
      position: absolute;
      top: -2.7rem;
      right: 0;
      background: none;
      border: none;
      color: #fff;
      font-size: 2.2rem;
      cursor: pointer;
      line-height: 1;
    }

    /* Official Footer Section */
    footer {
      border-top: 1px solid var(--border-color);
      background: var(--bg-surface);
      padding: 4rem 2rem 2rem;
    }

    .footer-container {
      max-width: 1200px;
      margin: 0 auto;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 2.5rem;
      margin-bottom: 3.5rem;
    }

    .footer-col h3 {
      font-family: 'Space Grotesk', sans-serif;
      font-size: 1.2rem;
      color: var(--text-main);
      margin-bottom: 1.2rem;
      position: relative;
    }

    .footer-col h3::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: -6px;
      width: 32px;
      height: 2px;
      background: var(--primary);
    }

    .footer-col p {
      font-size: 0.9rem;
      color: var(--text-muted);
      line-height: 1.6;
      margin-bottom: 0.8rem;
    }

    .contact-item {
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 0.92rem;
      color: var(--text-muted);
      margin-bottom: 0.9rem;
    }

    .contact-item a {
      color: var(--accent);
      text-decoration: none;
      transition: color 0.2s ease;
    }

    .contact-item a:hover {
      color: var(--primary);
      text-decoration: underline;
    }

    .contact-badge {
      display: inline-block;
      padding: 0.35rem 0.8rem;
      background: rgba(56, 189, 248, 0.1);
      border: 1px solid rgba(56, 189, 248, 0.25);
      border-radius: 6px;
      color: var(--accent);
      font-size: 0.8rem;
      font-weight: 600;
      margin-top: 0.5rem;
    }

    .bottom-bar {
      border-top: 1px solid var(--border-color);
      padding-top: 1.8rem;
      text-align: center;
      font-size: 0.82rem;
      color: var(--text-muted);
      max-width: 1200px;
      margin: 0 auto;
    }
  </style>
</head>
<body>

  <!-- Top Navbar -->
  <header>
    <div class="brand">
      <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" style="color:var(--primary)"><polygon points="1 6 1 22 8 18 16 22 23 18 23 2 16 6 8 2 1 6"></polygon><line x1="8" y1="2" x2="8" y2="18"></line><line x1="16" y1="6" x2="16" y2="22"></line></svg>
      PERUVALLUR
    </div>
    <div class="nav-meta">
      Tirurangadi Taluk | Malappuram District, Kerala
    </div>
  </header>

  <!-- Hero Section -->
  <section class="hero">
    <div class="badge">Spatial Analysis & Regional Planning Portal</div>
    <h1>PERUVALLUR GRAMA PANCHAYAT</h1>
    <p style="text-align: justify;">Peruvallur is a census town in Tirurangadi Taluk, Malappuram district in the state of Kerala, India.
Calicut International Airport is near Peruvallur, and Kondotty and Chemmad and Chelari are the nearest towns. Parambil peedika and Kadappdi are quickly emerging market centres with multistorey buildings and shopping complexes. Many villagers are gulf migrants. As per the current census data, Peruvallur Panchaythu is a census town, and categorised under special Panchaythu. Peruvallur panchayathu was formed in October 2000. K. Kuttyali Haji was first president K Koya Kutti Haji was vice-president of the panchayathu. IUML is the major dominant political party of the panchyathu.</p>
    <p style="text-align: justify;">
      Comprehensive Geographic Information System (GIS) thematic inventory cataloging administrative delineation, satellite remote sensing, altimetric terrain, geomorphology, drainage network, and micro-ward satellite atlases.
    </p>

    <!-- Geographic & Demographic Stats -->
    <div class="stats-grid">
      <div class="stat-card">
        <h3>Malappuram</h3>
        <p>Taluk: Tirurangadi</p>
      </div>
      <div class="stat-card">
        <h3>34,941</h3>
        <p>Census Population (2011)</p>
      </div>
      <div class="stat-card">
        <h3>46.78 meters (153.48 feet) above sea level</h3>
        <p>Located at an elevation</p>
      </div>
      <div class="stat-card">
        <h3>21 Wards</h3>
        <p>Micro-Level Satellite Atlases</p>
      </div>
    </div>
  </section>

  <!-- Filter Buttons: Pure Thematic Categories (No "All Maps") -->
  <div class="controls">
    <button class="filter-btn active" onclick="filterCategory('admin', event)">Administrative & Satellite</button>
    <button class="filter-btn" onclick="filterCategory('terrain', event)">Topography & Relief</button>
    <button class="filter-btn" onclick="filterCategory('hydro-geo', event)">Hydrology & Geomorphology</button>
    <button class="filter-btn" onclick="filterCategory('settlement', event)">Built-Up Environment</button>
    <button class="filter-btn" onclick="filterCategory('ward-atlas', event)">Ward Satellite Atlas (21 Wards)</button>
  </div>

  <!-- Thematic Map Grid -->
  <main class="gallery-container">
    <div class="grid">

      <!-- ================= 1. ADMINISTRATIVE & SATELLITE ================= -->

      <!-- Map 1: Ward & Key Map -->
      <article class="map-card" data-category="admin">
        <div class="img-wrapper" onclick="openModal('KEY MAP PP WARD.png', 'Administrative Key Map & Ward Delineation')">
          <img src="KEY MAP PP WARD.png" alt="Location Map and Ward Boundaries of Peruvallur" onerror="this.src='https://placehold.co/600x400/182234/fff?text=KEY+MAP+PP+WARD.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Administrative Boundary</span>
          <h2>Ward Division Master Map</h2>
          <p style="text-align: justify;">Delineates all 21 ward zones of Peruvallur Grama Panchayat with national (India), state (Kerala), and district (Malappuram) geographic location insets.</p>
          <div class="tech-specs">
            <span>Projection: Geographic WGS84</span>
            <span>Type: Vector Polygon</span>
          </div>
        </div>

      </article>
      <!-- Map: Survey of India Historical Toposheet -->
      <article class="map-card" data-category="admin">
        <div class="img-wrapper" onclick="openModal('TOPO PERS.png', 'Historical Survey of India Toposheet Map')">
          <img src="TOPO PERS.png" alt="Historical Survey of India Toposheet Map" onerror="this.src='https://placehold.co/600x400/182234/fff?text=OLD+TOPOSHEET+PERUVALLUR'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Historical Cartography</span>
          <h2>Survey of India Toposheet</h2>
          <p style="text-align: justify;">Historical Open Series Map (OSM / SOI Toposheet at 1:50,000 scale) capturing early settlement footprints, historical cart tracks, relief benchmark contours, and traditional land use prior to modern urbanization.</p>
          <div class="tech-specs">
            <span>Scale: 1:50,000 Open Series</span>
            <span>Source: Survey of India (SOI)</span>
          </div>
        </div>
      </article>

      <!-- Map 2: General Satellite Atlas -->
      <article class="map-card" data-category="admin">
        <div class="img-wrapper" onclick="openModal('PEERUVALUR PANCHAYAT ATLAS.png', 'High-Resolution Satellite Atlas Composite')">
          <img src="PEERUVALUR PANCHAYAT ATLAS.png" alt="Peruvallur Satellite Imagery Atlas" onerror="this.src='https://placehold.co/600x400/182234/fff?text=PEERUVALUR+PANCHAYAT+ATLAS.png'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Remote Sensing</span>
          <h2>Panchayat Satellite Atlas</h2>
          <p style="text-align: justify;">Orthorectified true-color surface imagery highlighting dense canopy belts, vegetative agrarian lowlands, and ribbon transportation corridors.</p>
          <div class="tech-specs">
            <span>Extent: 11.07°N - 11.13°N</span>
            <span>Source: Satellite Imagery</span>
          </div>
        </div>
      </article>


      <!-- ================= 2. TOPOGRAPHY & RELIEF ================= -->

      <!-- Map 3: DEM Continuous -->
      <article class="map-card" data-category="terrain">
        <div class="img-wrapper" onclick="openModal('DEM PERUVALLUR.png', 'Digital Elevation Model (DEM)')">
          <img src="DEM PERUVALLUR.png" alt="Digital Elevation Map" onerror="this.src='https://placehold.co/600x400/182234/fff?text=DEM+PERUVALLUR.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Elevation Analysis</span>
          <h2>Digital Elevation Model (DEM)</h2>
          <p style="text-align: justify;">Grayscale topographic raster displaying the continuous elevation model of Peruvallur, rising from 3 meters in drainage lowlands to 101 meters on northern crests.</p>
          <div class="tech-specs">
            <span>Datum: OpenTopography DEM</span>
            <span>Range: 3m - 101m</span>
          </div>
        </div>
      </article>

      <!-- Map 4: Classified Elevation -->
      <article class="map-card" data-category="terrain">
        <div class="img-wrapper" onclick="openModal('ELEVATION.png', 'Classified Hypsometric Elevation Intervals')">
          <img src="ELEVATION.png" alt="Classified Elevation Map" onerror="this.src='https://placehold.co/600x400/182234/fff?text=ELEVATION.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Hypsometry</span>
          <h2>Classified Elevation Model</h2>
          <p style="text-align: justify;">Stratified into 5 hypsometric bands (&le;23m, 23-42m, 42-62m, 62-81m, and &gt;81m) distinguishing northern residual hills from low agricultural terraces.</p>
          <div class="tech-specs">
            <span>Classes: 5 Elevation Zones</span>
            <span>Unit: Meters (m)</span>
          </div>
        </div>
      </article>

      <!-- Map 5: Hillshade Relief -->
      <article class="map-card" data-category="terrain">
        <div class="img-wrapper" onclick="openModal('HILL SHADE ELEVEATION.png', 'Hillshade Surface Relief Map')">
          <img src="HILL SHADE ELEVEATION.png" alt="Hillshade Relief Map" onerror="this.src='https://placehold.co/600x400/182234/fff?text=HILL+SHADE+ELEVEATION.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Morphometry</span>
          <h2>Hillshade Terrain Model</h2>
          <p style="text-align: justify;">Multi-directional illuminated shaded relief rendering terrain textures, slope breaklines, structural ridges, and valley incision across the landscape.</p>
          <div class="tech-specs">
            <span>Method: Shaded Relief</span>
            <span>Band: Band 1 Hypsometric</span>
          </div>
        </div>
      </article>

      <!-- Map 6: Contours -->
      <article class="map-card" data-category="terrain">
        <div class="img-wrapper" onclick="openModal('CONTOUR MAP.png', 'Topographic Contour Lines')">
          <img src="CONTOUR MAP.png" alt="Topographic Contour Map" onerror="this.src='https://placehold.co/600x400/182234/fff?text=CONTOUR+PERUVLR.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Topography</span>
          <h2>Topographic Contours</h2>
          <p style="text-align: justify;">Vector contour isolines illustrating slope gradient, escarpments, and gentle foothill zones, serving as a primary baseline for watershed and civil planning.</p>
          <div class="tech-specs">
            <span>Type: Isolines</span>
            <span>Scale: 1:25,000 Reference</span>
          </div>
        </div>
      </article>

       <!-- Map 7: Slope analysis -->
      <article class="map-card" data-category="terrain">
        <div class="img-wrapper" onclick="openModal('SLOPE PERU.png', 'Slope Map')">
          <img src="SLOPE PERU.png" alt="Slope Map of Peruvallur Grama Panchayat" onerror="this.src='https://placehold.co/600x400/182234/fff?text=CONTOUR+PERUVLR.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Slope</span>
          <h2>Slope Analysis</h2>
          <p style="text-align: justify;">Morphometric slope gradient raster classified into terrain inclination classes (nearly level valley terraces to steep ridge scarps), critical for soil conservation and runoff mapping.</p>
          <div class="tech-specs">
          <span>Unit: Degrees ° /%</span>
            <span>Derivation: DEM Surface Raster</span>
          </div>
        </div>
      </article>

             <!-- Map 8: Elevation Profile / Topographic Cross-Section -->
      <article class="map-card" data-category="terrain">
        <div class="img-wrapper" onclick="openModal('profile peruvallur.png', 'Topographic Elevation Profile & Cross-Section Graph')">
          <img src="profile peruvallur.png" alt="Slope Map of Peruvallur Grama Panchayat" onerror="this.src='https://placehold.co/600x400/182234/fff?text=CONTOUR+PERUVLR.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
       <div class="map-content">
          <span class="layer-tag">Topographic Relief</span>
          <h2>Elevation Profile & Transect Line</h2>
          <p style="text-align: justify;">Two-dimensional cross-sectional elevation profile transecting Peruvallur Grama Panchayat, depicting continuous hypsometric variation, slope gradient transitions, and crest-to-valley terrain relief across the terrain.</p>
          <div class="tech-specs">
            <span>Type: 2D Topographic Transect</span>
            <span>Elevation: 3m – 101m Range</span>
          </div>
        </div>
      </article>

      <!-- ================= 3. HYDROLOGY & GEOMORPHOLOGY ================= -->

      <!-- Map 8: Drainage Network -->
      <article class="map-card" data-category="hydro-geo">
        <div class="img-wrapper" onclick="openModal('DRAINAGE MAP PERUVALLUR.png', 'Drainage Network and Stream Hierarchy')">
          <img src="DRAINAGE MAP PERUVALLUR.png" alt="Drainage Map" onerror="this.src='https://placehold.co/600x400/182234/fff?text=DRAINAGE+MAP+PERUVALLUR.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Hydrology</span>
          <h2>Drainage Network System</h2>
          <p style="text-align: justify;">Hierarchical dendritic drainage network tracing stream order through agricultural valley floors toward natural outlets and regional river catchments.</p>
          <div class="tech-specs">
            <span>Classes: Stream Ordering</span>
            <span>Pattern: Dendritic</span>
          </div>
        </div>
      </article>

      <!-- Map 9: Geomorphology -->
      <article class="map-card" data-category="hydro-geo">
        <div class="img-wrapper" onclick="openModal('GEOMOROLOGY PANCHAYTH.png', 'Geomorphological Landforms')">
          <img src="GEOMOROLOGY PANCHAYTH.png" alt="Geomorphology Map" onerror="this.src='https://placehold.co/600x400/182234/fff?text=GEOMOROLOGY+PANCHAYTH.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Geomorphology</span>
          <h2>Geomorphological Units</h2>
          <p style="text-align: justify;">Categorization of spatial terrain units including Piedmont Zones, Valley Fills (paddy tracts), Residual Mounts, Lower Plateaus, and exposed rock structures.</p>
          <div class="tech-specs">
            <span>Units: 5 Terrain Type</span>
            <span>Scale: Micro Regional</span>
          </div>
        </div>
      </article>

      <!-- Map 10: Geology -->
      <article class="map-card" data-category="hydro-geo">
        <div class="img-wrapper" onclick="openModal('GEOLOGY PERUVALLUR.png', 'Geological Lithology Map')">
          <img src="GEOLOGY PERUVALLUR.png" alt="Geology Map of Peruvallur" onerror="this.src='https://placehold.co/600x400/182234/fff?text=GEOLOGY+PERUVALLUR.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Geology</span>
          <h2>Geological Formations</h2>
          <p style="text-align: justify;">Lithological spatial layer showing the regional bedrock basement dominated by metamorphic rock complexes characteristic of the midland Kerala terrain.</p>
          <div class="tech-specs">
            <span>Lithology: Metamorphic Rocks</span>
            <span>Category: Crystalline Complex</span>
          </div>
        </div>
      </article>

      <!-- Map 11: Soil Classification -->
      <article class="map-card" data-category="hydro-geo">
        <div class="img-wrapper" onclick="openModal('SOIL PERUVALLUR.png', 'Soil Classification and Texture Map')">
          <img src="SOIL PERUVALLUR.png" alt="Soil Classification and Texture Map" onerror="this.src='https://placehold.co/600x400/182234/fff?text=GEOLOGY+PERUVALLUR.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
    <div class="map-content">
          <span class="layer-tag">Pedology</span>
          <h2>Soil Order & Texture Types</h2>
          <p style="text-align: justify;">Spatial distribution of local pedological series across the panchayat, dominated by midland lateritic soils (Ultisols/Inceptisols) on hillslopes and rich alluvial colluvium across drainage valley floors.</p>
          <div class="tech-specs">
            <span>Type: Vector Polygon</span>
            <span>Dominant: Lateritic & Valley Alluvium</span>
          </div>
        </div>
      </article>

        <!-- Map 12: Surface Stream Channels -->
      <article class="map-card" data-category="hydro-geo">
        <div class="img-wrapper" onclick="openModal('STREAMS_PERUVALLUR.png', 'Natural Streams and Surface Flow Channels Map')">
          <img src="STREAMS_PERUVALLUR.png" alt="Soil Classification and Texture Map" onerror="this.src='https://placehold.co/600x400/182234/fff?text=GEOLOGY+PERUVALLUR.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
      <div class="map-content">
          <span class="layer-tag">Surface Water</span>
          <h2>Stream Network</h2>
          <p style="text-align: justify;">Spatial distribution of natural perennial and seasonal streams (local chal / thodu) coursing through Peruvallur Grama Panchayat, mapping surface runoff courses through agricultural tracts and wetland depressions.</p>
          <div class="tech-specs">
            <span>Feature: Natural Streams & Rivulets</span>
            <span>Geometry: Vector Polyline</span>
          </div>
        </div>
      </article>

      <!-- ================= 4. BUILT-UP ENVIRONMENT ================= -->

            <!-- Map 11: Resource Inventory -->
      <article class="map-card" data-category="settlement">
        <div class="img-wrapper" onclick="openModal('RESOURCE PERU.png', 'Spatial Resource and Civic Infrastructure Map')">
          <img src="RESOURCE PERU.png" alt="Built-Up Distribution Map" onerror="this.src='https://placehold.co/600x400/182234/fff?text=BUILDUP+MAP.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
     <div class="map-content">
          <span class="layer-tag">Infrastructure & Assets</span>
          <h2>Resource Inventory Map</h2>
          <p style="text-align: justify;">Distribution of local institutional resources, civic amenities, community facilities, health centers, water bodies, and educational establishments across Peruvallur Grama Panchayat.</p>
          <div class="tech-specs">
            <span>Type: Point & Polygon Assets</span>
            <span>Domain: Public Amenities</span>
          </div>
        </div>
      </article>

      <!-- Map 11: Built-Up Distribution -->
      <article class="map-card" data-category="settlement">
        <div class="img-wrapper" onclick="openModal('BUILDUP MAP.PNG', 'Settlement and Built-Up Distribution')">
          <img src="BUILDUP MAP.png" alt="Built-Up Distribution Map" onerror="this.src='https://placehold.co/600x400/182234/fff?text=BUILDUP+MAP.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Urban Morphology</span>
          <h2>Built-Up & Settlement Distribution</h2>
          <p style="text-align: justify;">High-resolution structural point footprint depicting settlement clustering along major transport axes and ridge shoulders, avoiding flood-prone valley floors.</p>
          <div class="tech-specs">
            <span>Layer: Structure Footprint</span>
            <span>Pattern: Linear Semi-Clustered</span>
          </div>
        </div>
      </article>

          <!-- Map 11: Road & Transportation Network -->
      <article class="map-card" data-category="settlement">
        <div class="img-wrapper" onclick="openModal('ROAD MAP PERU.png', 'Road Network and Transportation Hierarchy Map')">
          <img src="ROAD MAP PERU.png" alt="Road Network and Transportation Hierarchy Map" onerror="this.src='https://placehold.co/600x400/182234/fff?text=BUILDUP+MAP.jpg'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
       <div class="map-content">
          <span class="layer-tag">Transportation Geography</span>
          <h2>Road Network & Connectivity</h2>
          <p style="text-align: justify;">Spatial transportation hierarchy detailing arterial corridors, Major District Roads (MDR), panchayat tarred roads, and interior access lanes connecting residential wards and markets.</p>
          <div class="tech-specs">
            <span>Geometry: Vector Polyline</span>
            <span>Hierarchy: Arterial, Local & Lanes</span>
          </div>
        </div>
      </article>

      <!-- ================= 5. WARD SATELLITE ATLAS (21 WARDS) ================= -->

            <!-- Ward 1 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('VATTAPARAMB.jpg', 'Satellite Map - Ward: Vattapparambu')">
          <img src="VATTAPARAMB.jpg" alt="Satellite Map of Vattapparambu Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=VATTAPPARAMBU+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Vattapparambu</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>
      
      <!-- Ward 2 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('CHATHRA THODI.jpg', 'Satellite Map - Ward: Chathrathodi')">
          <img src="CHATHRA THODI.jpg" alt="Satellite Map of Chathrathodi Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=CHATHRATHODI+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Chathrathodi</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

      <!-- Ward 3 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('KAKKATHADAM.jpg', 'Satellite Map - Ward: Kakkathadam')">
          <img src="KAKKATHADAM.jpg" alt="Satellite Map of Kakkathadam Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=KAKKATHADAM+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Kakkathadam</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

            <!-- Ward 4 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('KADAPPAID.jpg', 'Satellite Map - Ward: Kadappadi')">
          <img src="KADAPPAID.jpg" alt="Satellite Map of Kadappadi Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=KADAPPADI+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Kadappadi</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

        <!-- Ward 5 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('KARAVANKALLU.jpg', 'Satellite Map - Ward: Karuvankallu')">
          <img src="KARAVANKALLU.jpg" alt="Satellite Map of Karuvankallu Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=KARUVANKALLU+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Karuvankallu</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E[cite: 1]</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

            <!-- Ward 6 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('NADUKARA.jpg', 'Satellite Map - Ward: Nadukkara')">
          <img src="NADUKARA.jpg" alt="Satellite Map of Nadukkara Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=NADUKKARA+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Nadukkara</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

           <!-- Ward 7 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('ILLATHMAD.jpg', 'Satellite Map - Ward: Illathmad')">
          <img src="ILLATHMAD.jpg" alt="Satellite Map of Illathmad Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=ILLATHMAD+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Illathmad</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

        <!-- Ward 8 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('SIDIQAHBAD.jpg', 'Satellite Map - Ward: Sidhiqabad')">
          <img src="SIDIQAHBAD.jpg" alt="Satellite Map of Sidhiqabad Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=SIDHIQABAD+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Sidhiqabad</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

            <!-- Ward 9 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('PENGATTU.jpg', 'Satellite Map - Ward: Pengattkund')">
          <img src="PENGATTU.jpg" alt="Satellite Map of Pengattkund Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=PENGATTKUND+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Pengattkund</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

            <!-- Ward 10 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('POTTAMLMADU.jpg', 'Satellite Map - Ward: Pottammalmad')">
          <img src="POTTAMLMADU.jpg" alt="Satellite Map of Pottammalmad Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=POTTAMMALMAD+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Pottammalmad</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

      <!-- Ward 7 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('KOLLAMCHINA.jpg', 'Satellite Map - Ward: Kollamchina')">
          <img src="KOLLAMCHINA.jpg" alt="Satellite Map of Kollamchina Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=KOLLAMCHINA+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Kollamchina</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

            <!-- Ward 12 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('NEDUMBLYAL.jpg', 'Satellite Map - Ward: Nedumballiyal')">
          <img src="NEDUMBLYAL.jpg" alt="Satellite Map of Nedumballiyal Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=NEDUMBALLIYAL+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Nedumballiyal</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

           <!-- Ward 13 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('PAPPEEDIKA.jpg', 'Satellite Map - Ward: Parambilpeedika')">
          <img src="PAPPEEDIKA.jpg" alt="Satellite Map of Parambilpeedika Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=PARAMBILPEEDIKA+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Parambil peedika</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

            <!-- Ward 14 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('PARANCHINAPURAYA.jpg', 'Satellite Map - Ward: Parachinapuraya')">
          <img src="PARANCHINAPURAYA.jpg" alt="Satellite Map of Parachinapuraya Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=PARACHINAPURAYA+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Parachinapuraya</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

      <!-- Ward 15 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('CHENAKKAL.jpg', 'Satellite Map - Ward: Chenakkal')">
          <img src="CHENAKKAL.jpg" alt="Satellite Map of Chenakkal Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=CHENAKKAL+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Chenakkal</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>
 
      
      <!-- Ward 16 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('POOVTHAMDU.jpg', 'Satellite Map - Ward: Poovathanad')">
          <img src="POOVTHAMDU.jpg" alt="Satellite Map of Poovathanad Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=POOVATHANAD+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Poovathanad</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

      <!-- Ward 17 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('KOOMANNA.jpg', 'Satellite Map - Ward: Koomanna')">
          <img src="KOOMANNA.jpg" alt="Satellite Map of Koomanna Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=KOOMANNA+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Koomanna</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

      <!-- Ward 18 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('SUPER BAZAR.jpg', 'Satellite Map - Ward: Superbazar')">
          <img src="SUPER BAZAR.jpg" alt="Satellite Map of Superbazar Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=SUPERBAZAR+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Super Bazar</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

      <!-- Ward 19 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('VALIYA PARAMB.jpg', 'Satellite Map - Ward: Valiyaparamb')">
          <img src="VALIYA PARAMB.jpg" alt="Satellite Map of Valiyaparamb Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=VALIYAPARAMB+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Valiyaparamb</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

      <!-- Ward 20 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('VARAPPARA.jpg', 'Satellite Map - Ward: Varappara')">
          <img src="VARAPPARA.jpg" alt="Satellite Map of Varappara Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=VARAPPARA+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Varappara Ward</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

            <!-- Ward 18 -->
      <article class="map-card" data-category="ward-atlas">
        <div class="img-wrapper" onclick="openModal('VADAKEEL MADU.jpg', 'Satellite Map - Ward: Vadakkeelmad')">
          <img src="VADAKEEL MADU.jpg" alt="Satellite Map of Vadakkeelmad Ward" onerror="this.src='https://placehold.co/600x400/182234/fff?text=VADAKKEELMAD+WARD'" />
          <div class="overlay">Click to Enlarge</div>
        </div>
        <div class="map-content">
          <span class="layer-tag">Ward Satellite Atlas</span>
          <h2>Vadakkeelmad</h2>
          <div class="tech-specs">
            <span>Coordinate: 11°N | 76°E</span>
            <span>Scale Bar: 0 - 200m</span>
          </div>
        </div>
      </article>

  </main>
<!-- Interactive WebGIS Launch Button Section -->
  <section class="interactive-launch-section">
    <a href="https://arakkalsha786-dotcom.github.io/PERUVALLUR-GRAMA-PANCHAYAT/" 
       id="webgis-launch-btn" 
       class="webgis-launch-btn" 
       target="_blank" 
       rel="noopener noreferrer">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
        <circle cx="12" cy="12" r="10"></circle>
        <line x1="2" y1="12" x2="22" y2="12"></line>
        <path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"></path>
      </svg>
      Launch Interactive WebGIS Map
      <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
        <line x1="7" y1="17" x2="17" y2="7"></line>
        <polyline points="7 7 17 7 17 17"></polyline>
      </svg>
    </a>
    <p class="launch-subtext">Click to explore dynamic layers, spatial queries, and full-screen thematic overlays</p>
  </section>

  <!-- Lightbox Modal -->
  <div class="modal" id="mapModal" onclick="closeModal()">
    <div class="modal-content" onclick="event.stopPropagation()">
      <button class="close-btn" onclick="closeModal()" aria-label="Close modal">&times;</button>
      <img id="modalImg" src="" alt="Enlarged GIS Map View" />
      <div class="modal-caption" id="modalCaption"></div>
    </div>
  </div>


      <!-- Column 2: Geographic Metadata -->
      <div class="footer-col">
        <h3>Regional Administration</h3>
        <p><strong>Local Body:</strong> Peruvallur Grama Panchayat</p>
        <p><strong>Taluk:</strong> Tirurangadi</p>
        <p><strong>District:</strong> Malappuram, Kerala, India</p>
        <p><strong>Total Wards:</strong> 21 Demarcated Divisions</p>
      </div>

      <!-- Column 3: Official Contact Area -->
      <div class="footer-col">
        <h3>Contact</h3>
        
        <div class="contact-item">
          Shaima Jumana
        </div>

        <div class="contact-item">
          Dept. of Geography, SSUS, Kalady
        </div>
        
        <div class="contact-item">
          <span>Email:</span>
          <a href="mailto:arakkalsha786@gmail.com">arakkalsha786@gmail.com</a>
        </div>
      </div>

    </div>

    <!-- Copyright Bar -->
    <div class="bottom-bar">
      <p>&copy; 2026 Peruvallur Grama Panchayat Spatial Database System. All rights reserved.</p>
      <p style="margin-top: 4px; font-size: 0.76rem; color: #64748b;">Cartography, DEM Elevation Models, and Ward Atlas Remote Sensing Series &bull; Shaima Jumana</p>
    </div>
  </footer>

  <!-- Script for Strict Categorical Filtering and Modal -->
  <script>
    function filterCategory(category, evt) {
      const cards = document.querySelectorAll('.map-card');
      const buttons = document.querySelectorAll('.filter-btn');

      // Update active button state
      buttons.forEach(btn => btn.classList.remove('active'));
      if (evt && evt.target) {
        evt.target.classList.add('active');
      }

      // Display only maps belonging to the clicked category
      cards.forEach(card => {
        if (card.getAttribute('data-category') === category) {
          card.style.display = 'flex';
        } else {
          card.style.display = 'none';
        }
      });
    }

    // Initialize with first category on load
    document.addEventListener('DOMContentLoaded', () => {
      const firstActiveBtn = document.querySelector('.filter-btn.active');
      if (firstActiveBtn) {
        filterCategory('admin', { target: firstActiveBtn });
      }
    });

    function openModal(imgSrc, title) {
      const modal = document.getElementById('mapModal');
      const modalImg = document.getElementById('modalImg');
      const modalCaption = document.getElementById('modalCaption');

      modalImg.src = imgSrc;
      modalCaption.textContent = title;
      modal.classList.add('active');
      document.body.style.overflow = 'hidden';
    }

    function closeModal() {
      const modal = document.getElementById('mapModal');
      modal.classList.remove('active');
      document.body.style.overflow = '';
    }

    // Close on Escape key
    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') closeModal();
    });
  </script>

</body>
</html>
