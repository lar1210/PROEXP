<index.html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portal del Expediente Electrónico</title>
    <!-- Fuentes Tipográficas e Iconografía Profesional -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Cinzel:wght@600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --magenta-primary: #8B005B;
            --magenta-dark: #660046;
            --magenta-light: #fdf2f8;
            --magenta-border: #fbcfe8;
            --bg-body: #ffffff;
            --text-main: #0f172a;
            --text-muted: #64748b;
            --shadow-card: 0 10px 30px -5px rgba(0, 0, 0, 0.05), 0 4px 6px -2px rgba(0, 0, 0, 0.02);
            --border-color: #e2e8f0;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        body {
            background-color: var(--bg-body);
            color: var(--text-main);
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            position: relative;
        }

        /* MARCA DE AGUA FIJA DE LA DIOSA THEMIS EN EL FONDO BLANCO */
        body::before {
            content: "\f24e"; /* Icono FontAwesome de la Balanza/Themis */
            font-family: "Font Awesome 6 Free";
            font-weight: 900;
            position: fixed;
            top: 55%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 38vw;
            color: rgba(139, 0, 91, 0.025);
            z-index: -1;
            pointer-events: none;
        }

        /* -------------------------------------------------------------
           1. CARGAPANTALLA INICIAL (SPLASH SCREEN - BIENVENIDA Y THEMIS)
        ------------------------------------------------------------- */
        #splash-screen {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: var(--magenta-primary);
            color: #ffffff;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 99999;
            transition: opacity 0.6s ease, visibility 0.6s ease;
            text-align: center;
            padding: 20px;
        }

        .themis-avatar-frame {
            width: 130px;
            height: 130px;
            border: 4px solid #ffffff;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(255, 255, 255, 0.12);
            box-shadow: 0 0 30px rgba(255, 255, 255, 0.35);
            margin-bottom: 20px;
            animation: pulseGlow 2.5s infinite ease-in-out;
        }

        .themis-avatar-frame i {
            font-size: 3.8rem;
            color: #ffffff;
        }

        @keyframes pulseGlow {
            0%, 100% { transform: scale(1); box-shadow: 0 0 20px rgba(255, 255, 255, 0.3); }
            50% { transform: scale(1.05); box-shadow: 0 0 40px rgba(255, 255, 255, 0.6); }
        }

        .splash-title {
            font-family: 'Cinzel', serif;
            font-size: 2.1rem;
            font-weight: 700;
            letter-spacing: 1px;
            margin-bottom: 10px;
        }

        .splash-subtitle {
            font-size: 1rem;
            opacity: 0.9;
            margin-bottom: 25px;
            font-weight: 300;
        }

        .spinner-white {
            width: 44px;
            height: 44px;
            border: 4px solid rgba(255, 255, 255, 0.25);
            border-top: 4px solid #ffffff;
            border-radius: 50%;
            animation: spin 0.8s linear infinite;
            margin-bottom: 25px;
        }

        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        .academic-toast-splash {
            background: rgba(255, 255, 255, 0.15);
            border: 1px solid rgba(255, 255, 255, 0.3);
            backdrop-filter: blur(12px);
            padding: 16px 28px;
            border-radius: 14px;
            font-size: 0.88rem;
            max-width: 550px;
            line-height: 1.6;
        }

        /* -------------------------------------------------------------
           2. ENCABEZADO Y BARRA DE MENÚ FIJA (STICKY HEADER)
        ------------------------------------------------------------- */
        .sticky-header-container {
            position: sticky;
            top: 0;
            z-index: 10000;
            background: #ffffff;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
        }

        /* Línea Superior */
        .top-header-line {
            padding: 10px 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid #f1f5f9;
        }

        .brand-left {
            display: flex;
            align-items: center;
            gap: 12px;
            color: var(--magenta-primary);
        }

        .brand-left i { font-size: 1.8rem; }

        .brand-left-title {
            font-family: 'Cinzel', serif;
            font-size: 1.25rem;
            font-weight: 700;
            letter-spacing: -0.2px;
        }

        .controls-right-line {
            display: flex;
            align-items: center;
            gap: 18px;
        }

        .lang-selector {
            display: flex;
            background: #f1f5f9;
            padding: 3px;
            border-radius: 6px;
            gap: 2px;
        }

        .lang-btn {
            border: none;
            background: transparent;
            padding: 4px 10px;
            font-size: 0.75rem;
            font-weight: 700;
            border-radius: 4px;
            cursor: pointer;
            color: var(--text-muted);
        }

        .lang-btn.active {
            background: #ffffff;
            color: var(--magenta-primary);
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }

        .widgets-bar-compact {
            display: flex;
            align-items: center;
            gap: 12px;
            background: var(--magenta-light);
            border: 1px solid var(--magenta-border);
            padding: 5px 14px;
            border-radius: 20px;
            font-size: 0.8rem;
            color: var(--magenta-primary);
            font-weight: 600;
        }

        /* Barra de Menú Magenta Fija */
        .navbar-magenta-fixed {
            background: var(--magenta-primary);
            padding: 0 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .nav-menu-links {
            display: flex;
            list-style: none;
        }

        .nav-menu-links li a {
            display: flex;
            align-items: center;
            gap: 8px;
            padding: 15px 18px;
            color: rgba(255, 255, 255, 0.9);
            text-decoration: none;
            font-size: 0.88rem;
            font-weight: 500;
            transition: all 0.2s ease;
            cursor: pointer;
        }

        .nav-menu-links li a:hover, .nav-menu-links li a.active {
            background: var(--magenta-dark);
            color: #ffffff;
        }

        .btn-search-nav-right {
            background: #ffffff !important;
            color: var(--magenta-primary) !important;
            font-weight: 700 !important;
            border-radius: 6px;
            padding: 8px 18px !important;
            transition: transform 0.2s ease;
            box-shadow: 0 2px 8px rgba(0,0,0,0.12);
        }

        .btn-search-nav-right:hover {
            transform: scale(1.03);
            background: #fdf2f8 !important;
        }

        /* -------------------------------------------------------------
           3. CONTENEDOR PRINCIPAL
        ------------------------------------------------------------- */
        .main-container {
            max-width: 1200px;
            margin: 30px auto;
            padding: 0 20px;
            flex: 1;
            width: 100%;
        }

        .info-card-panel {
            background: var(--magenta-light);
            border-left: 4px solid var(--magenta-primary);
            padding: 16px 20px;
            margin-bottom: 25px;
            border-radius: 0 8px 8px 0;
            display: none;
        }

        .info-card-panel h4 { color: var(--magenta-primary); margin-bottom: 4px; }

        /* MÓDULO DE BÚSQUEDA DE EXPEDIENTE */
        .search-card-container {
            background: #ffffff;
            border: 1px solid var(--border-color);
            border-radius: 14px;
            padding: 30px;
            box-shadow: var(--shadow-card);
            margin-bottom: 35px;
        }

        .section-title-header {
            font-size: 1.2rem;
            font-weight: 700;
            color: var(--text-main);
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .filter-tabs-group {
            display: flex;
            gap: 8px;
            background: #f8fafc;
            padding: 5px;
            border-radius: 8px;
            width: fit-content;
            margin-bottom: 22px;
            border: 1px solid #e2e8f0;
        }

        .tab-filter-btn {
            padding: 8px 20px;
            border: none;
            background: transparent;
            cursor: pointer;
            font-weight: 600;
            border-radius: 6px;
            font-size: 0.85rem;
            color: var(--text-muted);
            transition: all 0.2s;
        }

        .tab-filter-btn.active {
            background: #ffffff;
            color: var(--magenta-primary);
            box-shadow: 0 2px 6px rgba(0,0,0,0.08);
        }

        .form-panel { display: none; }
        .form-panel.active { display: block; }

        .form-grid-layout {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }

        .form-group-item label {
            display: block;
            font-size: 0.8rem;
            font-weight: 700;
            color: #334155;
            margin-bottom: 6px;
        }

        .form-group-item input, .form-group-item select {
            width: 100%;
            padding: 11px 14px;
            border: 1px solid #cbd5e1;
            border-radius: 8px;
            font-size: 0.9rem;
            transition: border-color 0.2s;
            background: #ffffff;
        }

        .form-group-item input:focus, .form-group-item select:focus {
            outline: none;
            border-color: var(--magenta-primary);
        }

        /* BLOQUE CAPTCHA DISTORSIONADO INTERACTIVO */
        .captcha-wrapper {
            background: #f8fafc;
            border: 1px solid var(--border-color);
            padding: 14px 18px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            gap: 15px;
            flex-wrap: wrap;
            margin-bottom: 25px;
            width: fit-content;
        }

        .captcha-canvas-box {
            background: #e2e8f0;
            padding: 8px 16px;
            font-family: 'Courier New', Courier, monospace;
            font-size: 1.3rem;
            font-weight: 900;
            letter-spacing: 5px;
            color: var(--magenta-primary);
            font-style: italic;
            text-decoration: line-through;
            border-radius: 6px;
            border: 1px dashed var(--magenta-primary);
            user-select: none;
        }

        .btn-submit-search {
            background: var(--magenta-primary);
            color: white;
            border: none;
            padding: 12px 28px;
            font-size: 0.9rem;
            font-weight: 700;
            border-radius: 8px;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            transition: background 0.2s;
        }

        .btn-submit-search:hover { background: var(--magenta-dark); }

        /* -------------------------------------------------------------
           4. EL NÚCLEO DEL EXPEDIENTE (LAS 4 PARTES PRINCIPALES)
        ------------------------------------------------------------- */
        #expediente-core-view { display: none; }

        /* SECCIÓN I: REPORTE DE EXPEDIENTE */
        .core-section-box {
            background: #ffffff;
            border: 1px solid var(--border-color);
            border-radius: 14px;
            margin-bottom: 30px;
            overflow: hidden;
            box-shadow: var(--shadow-card);
        }

        .core-section-header {
            background: linear-gradient(135deg, var(--magenta-primary), var(--magenta-dark));
            color: white;
            padding: 18px 24px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .core-section-header h3 {
            font-size: 1.15rem;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .status-pill {
            background: #22c55e;
            color: white;
            font-size: 0.75rem;
            font-weight: 700;
            padding: 4px 14px;
            border-radius: 20px;
            text-transform: uppercase;
        }

        .report-grid-details {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            padding: 24px;
        }

        .report-item {
            background: #f8fafc;
            padding: 16px;
            border-radius: 10px;
            border-left: 4px solid var(--magenta-primary);
        }

        .report-label {
            font-size: 0.75rem;
            font-weight: 700;
            color: var(--text-muted);
            text-transform: uppercase;
            margin-bottom: 4px;
        }

        .report-val {
            font-size: 0.92rem;
            font-weight: 600;
            color: var(--text-main);
        }

        /* SECCIÓN II: ESTADO, PROCESO Y LÍNEA DE TIEMPO ANIMADA */
        .timeline-container-box {
            padding: 24px;
        }

        .action-buttons-toolbar {
            display: flex;
            gap: 12px;
            margin-bottom: 25px;
            justify-content: flex-end;
        }

        .btn-action-outline {
            background: #ffffff;
            border: 1px solid var(--magenta-primary);
            color: var(--magenta-primary);
            padding: 8px 16px;
            border-radius: 6px;
            font-size: 0.85rem;
            font-weight: 700;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            transition: all 0.2s;
        }

        .btn-action-outline:hover {
            background: var(--magenta-light);
        }

        .animated-timeline {
            display: flex;
            justify-content: space-between;
            position: relative;
            margin: 30px 0 10px;
            flex-wrap: wrap;
            gap: 15px;
        }

        .animated-timeline::before {
            content: '';
            position: absolute;
            top: 20px; left: 0; width: 100%; height: 4px;
            background: #e2e8f0;
            z-index: 1;
        }

        .timeline-node {
            position: relative;
            z-index: 2;
            background: #ffffff;
            padding: 0 10px;
            text-align: center;
            flex: 1;
        }

        .node-circle {
            width: 42px; height: 42px;
            border-radius: 50%;
            background: #cbd5e1;
            color: white;
            display: flex; align-items: center; justify-content: center;
            margin: 0 auto 10px;
            font-size: 0.9rem;
            font-weight: 700;
            transition: all 0.4s ease;
        }

        .timeline-node.completed .node-circle {
            background: #22c55e;
            box-shadow: 0 0 0 4px #dcfce7;
        }

        .timeline-node.active .node-circle {
            background: var(--magenta-primary);
            box-shadow: 0 0 0 6px var(--magenta-border);
            animation: pulseNode 1.8s infinite;
        }

        @keyframes pulseNode {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }

        .node-title { font-size: 0.82rem; font-weight: 700; color: var(--text-main); }
        .node-date { font-size: 0.72rem; color: var(--text-muted); }

        /* SECCIÓN III: PARTES PROCESALES E INTEROPERABILIDAD INSTITUCIONAL (PISDP) */
        .interop-grid-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
            gap: 20px;
            padding: 24px;
        }

        .interop-card {
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            background: #ffffff;
            cursor: pointer;
            transition: all 0.25s ease;
            box-shadow: 0 4px 12px rgba(0,0,0,0.03);
        }

        .interop-card:hover {
            transform: translateY(-4px);
            border-color: var(--magenta-primary);
            box-shadow: 0 10px 20px rgba(139, 0, 91, 0.12);
        }

        .interop-badge-icon {
            width: 58px; height: 58px;
            border-radius: 50%;
            background: var(--magenta-light);
            color: var(--magenta-primary);
            display: flex; align-items: center; justify-content: center;
            margin: 0 auto 12px;
            font-size: 1.5rem;
            border: 2px solid var(--magenta-border);
        }

        .interop-title { font-size: 0.95rem; font-weight: 700; color: var(--text-main); }
        .interop-subtitle { font-size: 0.75rem; color: var(--text-muted); margin-top: 4px; }

        /* SECCIÓN IV: SEGUIMIENTO DEL EXPEDIENTE (RESOLUCIONES Y NOTIFICACIONES) */
        .documents-table-view {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.88rem;
        }

        .documents-table-view th {
            background: #f8fafc;
            color: #334155;
            padding: 14px 18px;
            text-align: left;
            font-weight: 700;
            border-bottom: 1px solid var(--border-color);
        }

        .documents-table-view td {
            padding: 14px 18px;
            border-bottom: 1px solid #f1f5f9;
        }

        .btn-doc-view {
            background: var(--magenta-primary);
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 5px;
            font-size: 0.75rem;
            font-weight: 600;
            cursor: pointer;
            margin-right: 5px;
        }

        .btn-doc-download {
            background: #0284c7;
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 5px;
            font-size: 0.75rem;
            font-weight: 600;
            cursor: pointer;
        }

        /* -------------------------------------------------------------
           5. MODALES Y VENTANAS EMERGENTES
        ------------------------------------------------------------- */
        .modal-overlay-backdrop {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(15, 23, 42, 0.65);
            backdrop-filter: blur(5px);
            display: flex; justify-content: center; align-items: center;
            z-index: 999999;
            display: none;
        }

        .modal-card-dialog {
            background: #ffffff;
            border-radius: 14px;
            max-width: 550px;
            width: 90%;
            padding: 28px;
            position: relative;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.3);
        }

        .modal-close-icon {
            position: absolute; top: 16px; right: 20px;
            font-size: 1.3rem; color: var(--text-muted);
            cursor: pointer; border: none; background: none;
        }

        .profile-masked-box {
            display: flex;
            gap: 18px;
            align-items: center;
            margin-top: 15px;
            background: #f8fafc;
            padding: 16px;
            border-radius: 10px;
            border: 1px solid var(--border-color);
        }

        .photo-simulated-frame {
            width: 85px;
            height: 105px;
            background: #e2e8f0;
            border-radius: 6px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: #94a3b8;
            font-size: 0.72rem;
            border: 2px dashed #cbd5e1;
            text-align: center;
            padding: 4px;
        }

        footer {
            background: #0f172a;
            color: #94a3b8;
            text-align: center;
            padding: 18px;
            font-size: 0.8rem;
            margin-top: auto;
        }

        @media(max-width:768px){
            .top-header-line { flex-direction: column; gap: 10px; }
            .navbar-magenta-fixed { flex-direction: column; padding: 10px; }
            .nav-menu-links { flex-wrap: wrap; justify-content: center; }
            .animated-timeline::before { display: none; }
        }
    </style>
</head>
<body>

    <!-- 1. CARGAPANTALLA INICIAL (SPLASH SCREEN - THEMIS Y BIENVENIDA ACADÉMICA) -->
    <div id="splash-screen">
        <div class="themis-avatar-frame">
            <i class="fa-solid fa-scale-balanced"></i>
        </div>
        <div class="splash-title">Portal del Expediente Electrónico</div>
        <div class="splash-subtitle">Bienvenido al Sistema Digital de Consulta de Procesos Judiciales</div>
        <div class="spinner-white"></div>
        <div class="academic-toast-splash">
            <strong>PROTOTIPO ACADÉMICO DE EVALUACIÓN</strong><br>
            Asignatura: <strong>Gobierno Digital y Derecho Informático</strong><br>
            Estudiante: <em>Sonia Pilar Condori Ruelas</em> | Docente: <em>Michael Espinoza Coila</em>
        </div>
    </div>

    <!-- 2. ENCABEZADO Y BARRA MAGENTA FIJA (NO SE MUEVE AL HACER SCROLL) -->
    <div class="sticky-header-container">
        <!-- Línea Superior -->
        <div class="top-header-line">
            <div class="brand-left">
                <i class="fa-solid fa-scale-balanced"></i>
                <span class="brand-left-title">Portal del Expediente Electrónico</span>
            </div>
            
            <div class="controls-right-line">
                <!-- Idioma -->
                <div class="lang-selector">
                    <button class="lang-btn active">ES</button>
                    <button class="lang-btn">EN</button>
                </div>
                <!-- Reloj y Temporizador -->
                <div class="widgets-bar-compact">
                    <span><i class="fa-regular fa-clock"></i> <strong id="clock-display">00:00:00</strong></span>
                    <span>|</span>
                    <span><i class="fa-solid fa-hourglass-start"></i> <strong id="timer-display">07:00</strong></span>
                </div>
            </div>
        </div>

        <!-- Barra Magenta Fija -->
        <nav class="navbar-magenta-fixed">
            <ul class="nav-menu-links">
                <li><a class="active" onclick="showMenuInfo('Inicio', 'Bienvenido al Portal del Expediente Electrónico. Acceda a la información procesal mediante las opciones de búsqueda.')"><i class="fa-solid fa-house"></i> Inicio</a></li>
                <li><a onclick="showMenuInfo('Misión', 'Garantizar el acceso transparente, rápido y digital a los procesos judiciales mediante la modernización del Expediente Judicial Electrónico (EJE).')"><i class="fa-solid fa-bullseye"></i> Misión</a></li>
                <li><a onclick="showMenuInfo('Visión', 'Ser una plataforma de justicia digital eficiente, confiable e interoperable al servicio de la ciudadanía y los operadores del derecho.')"><i class="fa-solid fa-eye"></i> Visión</a></li>
                <li><a onclick="showMenuInfo('Transparencia', 'Acceso libre a resoluciones, jurisprudencia y estadísticas judiciales conforme al principio de máxima divulgación pública.')"><i class="fa-solid fa-shield-halved"></i> Transparencia</a></li>
                <li><a onclick="showMenuInfo('Contáctanos', 'Mesa de Ayuda Técnica - Atención al Ciudadano: Soporte EJE | Teléfono: (01) 410-0000 | Correo: soporte_eje@pj.gob.pe')"><i class="fa-solid fa-envelope"></i> Contáctanos</a></li>
            </ul>
            
            <!-- Botón Búsqueda a la Extrema Derecha -->
            <a class="btn-search-nav-right" onclick="scrollToSearchModule()"><i class="fa-solid fa-magnifying-glass"></i> Búsqueda de Expediente</a>
        </nav>
    </div>

    <!-- 3. CONTENEDOR PRINCIPAL -->
    <main class="main-container">

        <!-- Panel de información del Menú -->
        <div id="menu-info-card" class="info-card-panel">
            <h4 id="menu-info-title">Inicio</h4>
            <p id="menu-info-text" style="font-size: 0.88rem; color: #475569;"></p>
        </div>

        <!-- MÓDULO DE BÚSQUEDA DE EXPEDIENTE -->
        <section id="search-module" class="search-card-container">
            <div class="section-title-header">
                <i class="fa-solid fa-folder-search" style="color:var(--magenta-primary)"></i> Módulo de Consulta de Expedientes
            </div>
            
            <div class="filter-tabs-group">
                <button class="tab-filter-btn active" onclick="toggleSearchTab('numero')">Por Número de Expediente</button>
                <button class="tab-filter-btn" onclick="toggleSearchTab('partes')">Por Partes Procesales</button>
            </div>

            <!-- FILTRO 1: NÚMERO DE EXPEDIENTE (PRELLENADO CON LOS DATOS REALES) -->
            <div id="filter-panel-numero" class="form-panel active">
                <form onsubmit="handleSearchSubmit(event, 'code')">
                    <div class="form-grid-layout">
                        <div class="form-group-item">
                            <label>CÓDIGO DE EXPEDIENTE</label>
                            <input type="text" id="input-exp-code" value="00174-2019-0-2111-JR-LA-02" required>
                        </div>
                        <div class="form-group-item">
                            <label>DISTRITO JUDICIAL</label>
                            <select required><option selected>PUNO</option></select>
                        </div>
                    </div>

                    <!-- CAPTCHA DISTORSIONADO -->
                    <div class="captcha-wrapper">
                        <div class="captcha-canvas-box" id="captcha-code-display-1">9K4M2</div>
                        <i class="fa-solid fa-rotate-right" style="cursor:pointer; color:var(--text-muted);" onclick="refreshCaptcha(1)"></i>
                        <input type="text" id="captcha-input-1" placeholder="Ingrese captcha" style="padding:8px 12px; border:1px solid #cbd5e1; border-radius:6px; width:140px;" required>
                    </div>

                    <button type="submit" class="btn-submit-search"><i class="fa-solid fa-magnifying-glass"></i> Consultar Expediente</button>
                </form>
            </div>

            <!-- FILTRO 2: PARTES PROCESALES (PRELLENADO) -->
            <div id="filter-panel-partes" class="form-panel">
                <form onsubmit="handleSearchSubmit(event, 'partes')">
                    <div class="form-grid-layout">
                        <div class="form-group-item">
                            <label>NOMBRES Y APELLIDOS / RAZÓN SOCIAL</label>
                            <input type="text" value="Andrés Leonidas Supo Quispe" required>
                        </div>
                        <div class="form-group-item">
                            <label>DOCUMENTO DE IDENTIDAD (DNI / RUC)</label>
                            <input type="text" value="02167445">
                        </div>
                    </div>

                    <!-- CAPTCHA DISTORSIONADO -->
                    <div class="captcha-wrapper">
                        <div class="captcha-canvas-box" id="captcha-code-display-2">7P3L8</div>
                        <i class="fa-solid fa-rotate-right" style="cursor:pointer; color:var(--text-muted);" onclick="refreshCaptcha(2)"></i>
                        <input type="text" id="captcha-input-2" placeholder="Ingrese captcha" style="padding:8px 12px; border:1px solid #cbd5e1; border-radius:6px; width:140px;" required>
                    </div>

                    <button type="submit" class="btn-submit-search"><i class="fa-solid fa-user-check"></i> Buscar por Partes</button>
                </form>
            </div>
        </section>

        <!-- 4. EL NÚCLEO DEL EXPEDIENTE (DESPLEGADO TRAS LA BÚSQUEDA) -->
        <div id="expediente-core-view">
            
            <!-- PARTE I: REPORTE DE EXPEDIENTE -->
            <div class="core-section-box">
                <div class="core-section-header">
                    <h3><i class="fa-solid fa-file-contract"></i> I. REPORTE GENERAL DEL EXPEDIENTE: N° 00174-2019-0-2111-JR-LA-02</h3>
                    <span class="status-pill">EN TRÁMITE</span>
                </div>
                <div class="report-grid-details">
                    <div class="report-item">
                        <div class="report-label">Órgano Jurisdiccional</div>
                        <div class="report-val">Juzgado de Trabajo - Zona Norte (Juliaca)</div>
                    </div>
                    <div class="report-item">
                        <div class="report-label">Juez / Especialista</div>
                        <div class="report-val">Gonzalo V. Huamán Romero / Rosario Carlos Villán</div>
                    </div>
                    <div class="report-item">
                        <div class="report-label">Materia / Vía Procesal</div>
                        <div class="report-val">Desnaturalización de Contrato / Proceso Ordinario Laboral</div>
                    </div>
                    <div class="report-item">
                        <div class="report-label">Demandante</div>
                        <div class="report-val">Andrés Leonidas Supo Quispe (DNI: 02167445)</div>
                    </div>
                    <div class="report-item">
                        <div class="report-label">Demandado</div>
                        <div class="report-val">Seguro Social de Salud - EsSalud (Red Asistencial Juliaca)</div>
                    </div>
                    <div class="report-item">
                        <div class="report-label">Pretensión Principal</div>
                        <div class="report-val">Inclusión en planillas a plazo indeterminado como Almacenero desde el 01/12/1996.</div>
                    </div>
                </div>
            </div>

            <!-- PARTE II: ESTADO, PROCESO Y LÍNEA DE TIEMPO ANIMADA -->
            <div class="core-section-box">
                <div class="core-section-header" style="background:#2c3e50;">
                    <h3><i class="fa-solid fa-timeline"></i> II. ESTADO DEL PROCESO Y LÍNEA DE TIEMPO</h3>
                </div>
                <div class="timeline-container-box">
                    
                    <!-- Botones para Ver y Descargar PDF -->
                    <div class="action-buttons-toolbar">
                        <button class="btn-action-outline" onclick="openReportModal()"><i class="fa-solid fa-eye"></i> Ver Reporte Completo</button>
                        <button class="btn-action-outline" onclick="downloadPdfReport()"><i class="fa-solid fa-file-arrow-down"></i> Descargar PDF de Reporte</button>
                    </div>

                    <!-- Gráfico de Línea de Tiempo Animada -->
                    <div class="animated-timeline">
                        <div class="timeline-node completed">
                            <div class="node-circle"><i class="fa-solid fa-check"></i></div>
                            <div class="node-title">1. Demanda</div>
                            <div class="node-date">26/06/2019</div>
                        </div>
                        <div class="timeline-node completed">
                            <div class="node-circle"><i class="fa-solid fa-check"></i></div>
                            <div class="node-title">2. Admisibilidad</div>
                            <div class="node-date">28/08/2019</div>
                        </div>
                        <div class="timeline-node active">
                            <div class="node-circle"><i class="fa-solid fa-pen-to-square"></i></div>
                            <div class="node-title">3. Contestación</div>
                            <div class="node-date">25/09/2019</div>
                        </div>
                        <div class="timeline-node">
                            <div class="node-circle">4</div>
                            <div class="node-title">4. Audiencia</div>
                            <div class="node-date">Pendiente</div>
                        </div>
                        <div class="timeline-node">
                            <div class="node-circle">5</div>
                            <div class="node-title">5. Sentencia</div>
                            <div class="node-date">Pendiente</div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- PARTE III: PARTES PROCESALES E INTEROPERABILIDAD INSTITUCIONAL (PISDP) -->
            <div class="core-section-box">
                <div class="core-section-header" style="background:#1e293b;">
                    <h3><i class="fa-solid fa-network-wired"></i> III. PARTES PROCESALES E INTEROPERABILIDAD INSTITUCIONAL</h3>
                </div>
                <div class="interop-grid-cards">
                    <div class="interop-card" onclick="openInteropModal('RENIEC')">
                        <div class="interop-badge-icon"><i class="fa-solid fa-id-card"></i></div>
                        <div class="interop-title">RENIEC</div>
                        <div class="interop-subtitle">Consulta de Identidad y Ficha C4</div>
                    </div>
                    <div class="interop-card" onclick="openInteropModal('MIGRACIONES')">
                        <div class="interop-badge-icon"><i class="fa-solid fa-plane"></i></div>
                        <div class="interop-title">MIGRACIONES</div>
                        <div class="interop-subtitle">Alerta de Movimiento Migratorio</div>
                    </div>
                    <div class="interop-card" onclick="openInteropModal('PNP')">
                        <div class="interop-badge-icon"><i class="fa-solid fa-user-shield"></i></div>
                        <div class="interop-title">PNP</div>
                        <div class="interop-subtitle">Requisitorias Policiales</div>
                    </div>
                    <div class="interop-card" onclick="openInteropModal('INPE')">
                        <div class="interop-badge-icon"><i class="fa-solid fa-gavel"></i></div>
                        <div class="interop-title">INPE</div>
                        <div class="interop-subtitle">Antecedentes Penales</div>
                    </div>
                </div>
            </div>

            <!-- PARTE IV: SEGUIMIENTO DEL EXPEDIENTE (RESOLUCIONES Y NOTIFICACIONES) -->
            <div class="core-section-box">
                <div class="core-section-header" style="background:#334155;">
                    <h3><i class="fa-solid fa-folder-open"></i> IV. SEGUIMIENTO DEL EXPEDIENTE (RESOLUCIONES Y ACTUADOS)</h3>
                </div>
                <table class="documents-table-view">
                    <thead>
                        <tr>
                            <th>Fecha</th>
                            <th>Resolución / Acto</th>
                            <th>Descripción del Acto Procesal</th>
                            <th>Acciones</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>25/09/2019</td>
                            <td>Escrito N° 01</td>
                            <td>Contestación de la demanda por parte de EsSalud solicitando que sea declarada infundada.</td>
                            <td>
                                <button class="btn-doc-view" onclick="previewDocModal('Escrito N° 01 - Contestación de EsSalud')"><i class="fa-solid fa-eye"></i> Ver PDF</button>
                                <button class="btn-doc-download" onclick="downloadDocSimulated('Contestacion_EsSalud.pdf')"><i class="fa-solid fa-download"></i> Descargar</button>
                            </td>
                        </tr>
                        <tr>
                            <td>28/08/2019</td>
                            <td>Resolución N° 02</td>
                            <td>Admitir a trámite en la vía Ordinaria Laboral y dar traslado a la demandada por 10 días.</td>
                            <td>
                                <button class="btn-doc-view" onclick="previewDocModal('Resolución N° 02 - Admisibilidad Definitiva')"><i class="fa-solid fa-eye"></i> Ver PDF</button>
                                <button class="btn-doc-download" onclick="downloadDocSimulated('Resolucion_02.pdf')"><i class="fa-solid fa-download"></i> Descargar</button>
                            </td>
                        </tr>
                        <tr>
                            <td>13/08/2019</td>
                            <td>Resolución N° 01</td>
                            <td>Admisibilidad provisional con plazo de 3 días para aclaración de participación de partes.</td>
                            <td>
                                <button class="btn-doc-view" onclick="previewDocModal('Resolución N° 01 - Admisibilidad Provisional')"><i class="fa-solid fa-eye"></i> Ver PDF</button>
                                <button class="btn-doc-download" onclick="downloadDocSimulated('Resolucion_01.pdf')"><i class="fa-solid fa-download"></i> Descargar</button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>

        </div>

    </main>

    <!-- 5. MODAL DE CARGAPANTALLA / PROTECCIÓN DE DATOS PERSONALES (MINJUSDH) -->
    <div id="modal-data-protection" class="modal-overlay-backdrop">
        <div class="modal-card-dialog">
            <button class="modal-close-icon" onclick="closeDataModal()">&times;</button>
            <div style="color:var(--magenta-primary); font-weight:700; font-size:1.1rem; margin-bottom:12px;">
                <i class="fa-solid fa-shield-cat"></i> Medida Técnico-Protectiva de Datos Personales
            </div>
            <div style="font-size:0.86rem; color:#475569; line-height:1.6; margin-bottom:20px;">
                A partir de la fecha, se ha incluido un nuevo campo como medida técnica de protección, para que solo las partes puedan acceder a sus expedientes; a requerimiento de la Autoridad Nacional de Protección de Datos Personales y la Dirección de Fiscalización e Instrucción del Ministerio de Justicia y Derechos Humanos - MINJUSDH. Al amparo de la Ley N° 29733, Ley de Protección de Datos Personales.
            </div>
            <div style="text-align: right;">
                <button class="btn-submit-search" onclick="confirmAndShowCoreView()">Aceptar y Desplegar Expediente</button>
            </div>
        </div>
    </div>

    <!-- MODAL DE INTEROPERABILIDAD INSTITUCIONAL CON DATOS ENMASCARADOS -->
    <div id="modal-interop" class="modal-overlay-backdrop">
        <div class="modal-card-dialog">
            <button class="modal-close-icon" onclick="closeInteropModal()">&times;</button>
            <div id="interop-modal-title" style="color:var(--magenta-primary); font-weight:700; font-size:1.1rem; margin-bottom:15px;"></div>
            <div id="interop-modal-body" style="font-size:0.85rem; color:#475569;"></div>
        </div>
    </div>

    <!-- MODAL DE VISTA PREVIA DE DOCUMENTO / REPORTE -->
    <div id="modal-doc-preview" class="modal-overlay-backdrop">
        <div class="modal-card-dialog">
            <button class="modal-close-icon" onclick="closeDocPreviewModal()">&times;</button>
            <div id="doc-preview-title" style="color:var(--magenta-primary); font-weight:700; font-size:1.1rem; margin-bottom:12px;"></div>
            <div id="doc-preview-body" style="font-size:0.85rem; color:#475569; line-height:1.6; max-height:300px; overflow-y:auto; background:#f8fafc; padding:12px; border-radius:6px;"></div>
        </div>
    </div>

    <footer>
        Portal del Expediente Electrónico © 2026 | Desarrollado para la Asignatura de Gobierno Digital y Derecho Informático
    </footer>

    <!-- LÓGICA JAVASCRIPT CON INTERACTIVIDAD Y PERSISTENCIA -->
    <script>
        // Carga Inicial (Splash Screen)
        window.addEventListener('DOMContentLoaded', () => {
            setTimeout(() => {
                const splash = document.getElementById('splash-screen');
                splash.style.opacity = '0';
                splash.style.visibility = 'hidden';
            }, 2500);
            refreshCaptcha(1);
            refreshCaptcha(2);
        });

        // Reloj y Temporizador de 7 Minutos
        function updateClock() {
            const now = new Date();
            document.getElementById('clock-display').textContent = 
                `${String(now.getHours()).padStart(2, '0')}:${String(now.getMinutes()).padStart(2, '0')}:${String(now.getSeconds()).padStart(2, '0')}`;
        }
        setInterval(updateClock, 1000);
        updateClock();

        let sessionTimeLeft = 7 * 60;
        setInterval(() => {
            const minutes = Math.floor(sessionTimeLeft / 60);
            const seconds = sessionTimeLeft % 60;
            document.getElementById('timer-display').textContent = 
                `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
            if (sessionTimeLeft > 0) sessionTimeLeft--;
        }, 1000);

        // Captchas Distorsionados
        let generatedCaptchas = {};
        function refreshCaptcha(num) {
            const chars = "ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
            let code = "";
            for (let i = 0; i < 5; i++) code += chars.charAt(Math.floor(Math.random() * chars.length));
            generatedCaptchas[num] = code;
            document.getElementById(`captcha-code-display-${num}`).textContent = code;
        }

        function showMenuInfo(title, text) {
            const panel = document.getElementById('menu-info-card');
            document.getElementById('menu-info-title').textContent = title;
            document.getElementById('menu-info-text').textContent = text;
            panel.style.display = 'block';
        }

        function scrollToSearchModule() {
            document.getElementById('search-module').scrollIntoView({ behavior: 'smooth' });
        }

        function toggleSearchTab(tabType) {
            document.querySelectorAll('.tab-filter-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelectorAll('.form-panel').forEach(panel => panel.classList.remove('active'));
            if (tabType === 'numero') {
                event.target.classList.add('active');
                document.getElementById('filter-panel-numero').classList.add('active');
            } else {
                event.target.classList.add('active');
                document.getElementById('filter-panel-partes').classList.add('active');
            }
        }

        // Validación de Búsqueda
        function handleSearchSubmit(event, filterType) {
            event.preventDefault();
            const num = filterType === 'code' ? 1 : 2;
            const userInput = document.getElementById(`captcha-input-${num}`).value.trim().toUpperCase();

            if (userInput !== generatedCaptchas[num]) {
                alert("El código CAPTCHA ingresado no es correcto. Por favor verifique e intente nuevamente.");
                refreshCaptcha(num);
                document.getElementById(`captcha-input-${num}`).value = "";
                return;
            }

            // Mostrar Modal de Protección de Datos
            document.getElementById('modal-data-protection').style.display = 'flex';
        }

        function closeDataModal() {
            document.getElementById('modal-data-protection').style.display = 'none';
        }

        function confirmAndShowCoreView() {
            document.getElementById('modal-data-protection').style.display = 'none';
            document.getElementById('expediente-core-view').style.display = 'block';
            document.getElementById('expediente-core-view').scrollIntoView({ behavior: 'smooth' });
        }

        // Interoperabilidad con Datos Enmascarados (*)
        function openInteropModal(ente) {
            const title = document.getElementById('interop-modal-title');
            const body = document.getElementById('interop-modal-body');

            if (ente === 'RENIEC') {
                title.innerHTML = '<i class="fa-solid fa-id-card"></i> RENIEC - Plataforma Interoperable (PISDP)';
                body.innerHTML = `
                    <p style="margin-bottom:10px;"><strong>Estado de la Consulta:</strong> Registro Verificado</p>
                    <div class="profile-masked-box">
                        <div class="photo-simulated-frame">📷<br>FOTO RENIEC</div>
                        <div>
                            <p><strong>DNI:</strong> 02****45</p>
                            <p><strong>Nombres:</strong> A****s L******s S**o Q****e</p>
                            <p><strong>Estado Civil:</strong> Soltero</p>
                            <p><strong>Domicilio:</strong> Av. Manco Cápac N° 964, Juliaca</p>
                            <p><strong>Ficha C4:</strong> VIGENTE</p>
                        </div>
                    </div>`;
            } else if (ente === 'MIGRACIONES') {
                title.innerHTML = '<i class="fa-solid fa-plane"></i> MIGRACIONES - Control de Pasajeros';
                body.innerHTML = `
                    <p><strong>Ciudadano:</strong> A****s L******s S**o Q****e</p>
                    <p><strong>Alerta de Impedimento de Salida:</strong> NO REGISTRA IMPEDIMENTO</p>
                    <p><strong>Último Movimiento:</strong> Entrada por Aeropuerto Jorge Chávez (Verificado)</p>`;
            } else if (ente === 'PNP') {
                title.innerHTML = '<i class="fa-solid fa-user-shield"></i> PNP - Sistema ESINPOL';
                body.innerHTML = `
                    <p><strong>Sujeto:</strong> A****s L******s S**o Q****e (DNI: 02****45)</p>
                    <p><strong>Antecedentes Policiales:</strong> SIN ANTECEDENTES</p>
                    <p><strong>Órdenes de Captura:</strong> INEXISTENTE</p>`;
            } else if (ente === 'INPE') {
                title.innerHTML = '<i class="fa-solid fa-gavel"></i> INPE - Registro Penitenciario Nacional';
                body.innerHTML = `
                    <p><strong>Evaluado:</strong> A****s L******s S**o Q****e</p>
                    <p><strong>Antecedentes Penales:</strong> NO REGISTRA</p>
                    <p><strong>Condición Legal:</strong> Libre</p>`;
            }
            document.getElementById('modal-interop').style.display = 'flex';
        }

        function closeInteropModal() {
            document.getElementById('modal-interop').style.display = 'none';
        }

        // Funciones de Reporte y Vista Previa
        function openReportModal() {
            document.getElementById('doc-preview-title').innerHTML = '<i class="fa-solid fa-file-invoice"></i> Reporte Integral del Expediente N° 00174-2019-0-2111-JR-LA-02';
            document.getElementById('doc-preview-body').innerHTML = `
                <p><strong>Juzgado:</strong> Juzgado de Trabajo - Zona Norte - Juliaca</p>
                <p><strong>Demandante:</strong> Andrés Leonidas Supo Quispe</p>
                <p><strong>Demandado:</strong> EsSalud (Red Asistencial Juliaca)</p>
                <p><strong>Materia:</strong> Desnaturalización de la Intermediación Laboral con la contratista SILSA.</p>
                <p><strong>Resumen Fáctico:</strong> El trabajador labora desde el 01/12/1996 en el cargo de Almacenero de EsSalud, desnaturalizándose el contrato de limpieza.</p>`;
            document.getElementById('modal-doc-preview').style.display = 'flex';
        }

        function previewDocModal(docName) {
            document.getElementById('doc-preview-title').textContent = docName;
            document.getElementById('doc-preview-body').innerHTML = `
                <p><strong>Documento Oficial EJE</strong></p>
                <p>Se verifica el registro y firma digital del actuado procesal: <em>${docName}</em>.</p>
                <p>El documento satisface las medidas de autenticidad e integridad del sistema judicial.</p>`;
            document.getElementById('modal-doc-preview').style.display = 'flex';
        }

        function closeDocPreviewModal() {
            document.getElementById('modal-doc-preview').style.display = 'none';
        }

        function downloadPdfReport() {
            alert("Iniciando descarga simulada del Reporte Integral del Expediente en PDF...");
        }

        function downloadDocSimulated(filename) {
            alert(`Descargando documento judicial: ${filename}`);
        }
    </script>
</body>
</html>
