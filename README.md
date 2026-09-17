# Memorando
<!DOCTYPE html>
<html lang="es" class="dark scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SpaceX Starfactory Ops | Misión ElectroAndina Solver</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;700;800;900&family=Space+Grotesk:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        spacex: {
                            black: '#000000',
                            dark: '#08080a',
                            card: '#0f1117',
                            border: 'rgba(255, 255, 255, 0.12)',
                            accent: '#00d2ff',
                            purple: '#8b5cf6',
                            green: '#10b981',
                            amber: '#f59e0b',
                            red: '#ef4444',
                            silver: '#a1a1aa'
                        }
                    },
                    fontFamily: {
                        heading: ['Orbitron', 'sans-serif'],
                        body: ['Space Grotesk', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Space Grotesk', sans-serif;
            background-color: #000000;
            color: #f4f4f5;
        }
        .font-heading {
            font-family: 'Orbitron', sans-serif;
        }
        .glass-panel {
            background: rgba(15, 17, 23, 0.88);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.12);
        }
        .glass-panel:hover {
            border-color: rgba(0, 210, 255, 0.4);
        }
        .hud-border {
            position: relative;
        }
        .hud-border::before {
            content: '';
            position: absolute;
            top: -1px; left: -1px;
            width: 8px; height: 8px;
            border-top: 2px solid #00d2ff;
            border-left: 2px solid #00d2ff;
        }
        .hud-border::after {
            content: '';
            position: absolute;
            bottom: -1px; right: -1px;
            width: 8px; height: 8px;
            border-bottom: 2px solid #00d2ff;
            border-right: 2px solid #00d2ff;
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 5px;
            height: 5px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #000;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #27272a;
            border-radius: 3px;
        }
        .step-active {
            border-color: #00d2ff !important;
            background: rgba(0, 210, 255, 0.12) !important;
            box-shadow: 0 0 15px rgba(0, 210, 255, 0.2);
        }
        @keyframes pulse-glow {
            0%, 100% { opacity: 0.3; }
            50% { opacity: 0.8; }
        }
        .glow-effect {
            animation: pulse-glow 3s infinite ease-in-out;
        }
    </style>
</head>
<body class="bg-black text-gray-100 min-h-screen custom-scrollbar flex flex-col justify-between selection:bg-spacex-accent selection:text-black">

    <!-- Navigation Header -->
    <header class="sticky top-0 z-50 bg-black/90 backdrop-blur-md border-b border-white/10 px-4 lg:px-8 py-3">
        <div class="max-w-7xl mx-auto flex items-center justify-between">
            <a href="#" class="flex items-center gap-3 group">
                <div class="w-9 h-9 rounded-lg bg-white/5 border border-white/20 flex items-center justify-center text-spacex-accent group-hover:border-spacex-accent transition-all">
                    <i class="fa-solid fa-rocket text-base"></i>
                </div>
                <div class="flex flex-col">
                    <span class="font-heading font-black tracking-widest text-base text-white group-hover:text-spacex-accent transition-colors">SPACEX STARFACTORY</span>
                    <span class="text-[9px] uppercase tracking-widest text-spacex-accent font-mono">Control de Misión ElectroAndina (12-20 Años)</span>
                </div>
            </a>

            <!-- Navigation Links -->
            <nav class="hidden lg:flex items-center gap-6 text-[11px] font-heading font-bold uppercase tracking-widest text-gray-300">
                <a href="#tutorial" onclick="scrollToSec('tutorial')" class="hover:text-spacex-accent transition-colors flex items-center gap-1.5 text-spacex-accent">
                    <i class="fa-solid fa-graduation-cap"></i> Academia
                </a>
                <a href="#plan" onclick="scrollToSec('plan')" class="hover:text-spacex-accent transition-colors flex items-center gap-1.5">
                    <i class="fa-solid fa-table-cells"></i> Telemetría Solver
                </a>
                <a href="#simulator" onclick="scrollToSec('simulator')" class="hover:text-spacex-accent transition-colors flex items-center gap-1.5 text-spacex-amber">
                    <i class="fa-solid fa-sliders"></i> Simulador
                </a>
                <a href="#costs" onclick="scrollToSec('costs')" class="hover:text-spacex-accent transition-colors flex items-center gap-1.5">
                    <i class="fa-solid fa-chart-pie"></i> Costos
                </a>
                <a href="#insights" onclick="scrollToSec('insights')" class="hover:text-spacex-accent transition-colors flex items-center gap-1.5">
                    <i class="fa-solid fa-brain"></i> Decisiones
                </a>
                <a href="#challenge" onclick="scrollToSec('challenge')" class="hover:text-spacex-accent transition-colors flex items-center gap-1.5 text-spacex-green">
                    <i class="fa-solid fa-gamepad"></i> Quiz
                </a>
            </nav>

            <!-- Header Quick Actions -->
            <div class="flex items-center gap-3">
                <button onclick="scrollToSec('simulator')" class="hidden sm:inline-flex items-center gap-2 px-3.5 py-1.5 text-xs font-heading font-bold tracking-wider text-black bg-spacex-accent hover:bg-cyan-300 rounded transition-all shadow-lg hover:shadow-cyan-500/20 uppercase">
                    <i class="fa-solid fa-play text-[10px]"></i> Probar Simulador
                </button>
                <button id="mobileMenuBtn" class="lg:hidden text-gray-300 hover:text-white p-2">
                    <i class="fa-solid fa-bars text-xl"></i>
                </button>
            </div>
        </div>

        <!-- Mobile Drawer -->
        <div id="mobileMenu" class="hidden lg:hidden pt-3 pb-2 border-t border-white/10 mt-3 flex flex-col gap-2 text-xs font-mono">
            <a href="#tutorial" onclick="scrollToSec('tutorial')" class="px-2 py-1.5 text-spacex-accent font-bold">🚀 1. Academia Interactiva (Paso a Paso)</a>
            <a href="#plan" onclick="scrollToSec('plan')" class="px-2 py-1.5 hover:text-spacex-accent">📊 2. Plan de Producción e Inventario</a>
            <a href="#simulator" onclick="scrollToSec('simulator')" class="px-2 py-1.5 text-spacex-amber font-bold">🎛️ 3. Simulador interactivo What-If</a>
            <a href="#costs" onclick="scrollToSec('costs')" class="px-2 py-1.5 hover:text-spacex-accent">💵 4. Desglose de Costos ($294,915.44)</a>
            <a href="#insights" onclick="scrollToSec('insights')" class="px-2 py-1.5 hover:text-spacex-accent">💡 5. Observaciones Gerenciales</a>
            <a href="#challenge" onclick="scrollToSec('challenge')" class="px-2 py-1.5 text-spacex-green">🎮 6. Desafío Quiz Interactivo</a>
            <a href="#export-memo" onclick="scrollToSec('export-memo')" class="px-2 py-1.5 hover:text-spacex-accent">📄 7. Generar Memorando Mariana Castillo</a>
        </div>
    </header>

    <!-- Executive Mission Hero Section -->
    <section class="relative py-12 lg:py-16 px-4 border-b border-white/10 overflow-hidden">
        <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_top,_var(--tw-gradient-stops))] from-spacex-accent/15 via-black to-black pointer-events-none"></div>

        <div class="max-w-7xl mx-auto relative z-10 space-y-8">
            <!-- Mission Status Banner -->
            <div class="glass-panel p-4 rounded-xl border border-white/15 space-y-3 hud-border">
                <div class="flex flex-wrap items-center justify-between gap-3 border-b border-white/10 pb-3">
                    <div class="flex items-center gap-3">
                        <span class="px-2.5 py-0.5 rounded bg-spacex-accent/20 border border-spacex-accent/50 text-spacex-accent font-mono text-[11px] uppercase tracking-widest font-bold">
                            ESTADO DE MISIÓN: OPTIMAL
                        </span>
                        <span class="text-xs font-mono text-gray-400">Caso: ElectroAndina S.A. | Dirigido a: Mariana Castillo (Gerente Ops)</span>
                    </div>
                    <div class="flex items-center gap-2 font-mono text-xs text-gray-300">
                        <span class="w-2 h-2 rounded-full bg-emerald-400 animate-ping"></span>
                        Costo Semestral Simplex: <strong class="text-spacex-accent font-heading">$294,915.44 USD</strong>
                    </div>
                </div>

                <!-- Product Analogy Equivalents for 12-20 year olds -->
                <div class="grid sm:grid-cols-3 gap-3 text-xs font-mono">
                    <div class="bg-black/60 p-2.5 rounded border border-white/10 flex items-center justify-between">
                        <div>
                            <span class="text-gray-400 text-[10px] block">MÓDULO 1 (Licuadora):</span>
                            <span class="text-white font-bold">Soporte Vital Base</span>
                        </div>
                        <span class="text-spacex-accent font-bold">2.0h | $40</span>
                    </div>
                    <div class="bg-black/60 p-2.5 rounded border border-white/10 flex items-center justify-between">
                        <div>
                            <span class="text-gray-400 text-[10px] block">MÓDULO 2 (Batidora):</span>
                            <span class="text-purple-400 font-bold">Propulsión Core</span>
                        </div>
                        <span class="text-purple-400 font-bold">2.5h | $55</span>
                    </div>
                    <div class="bg-black/60 p-2.5 rounded border border-white/10 flex items-center justify-between">
                        <div>
                            <span class="text-gray-400 text-[10px] block">MÓDULO 3 (Procesador):</span>
                            <span class="text-emerald-400 font-bold">Aviónica Avanzada</span>
                        </div>
                        <span class="text-emerald-400 font-bold">3.5h | $75</span>
                    </div>
                </div>
            </div>

            <!-- Headline Grid -->
            <div class="grid lg:grid-cols-12 gap-8 items-center">
                <div class="lg:col-span-8 space-y-5">
                    <div class="inline-flex items-center gap-2 px-3 py-1 bg-white/5 rounded-full border border-white/10 text-xs font-mono text-gray-300">
                        <i class="fa-solid fa-microchip text-spacex-accent"></i> Programación Lineal & Algoritmo Simplex Aplicado
                    </div>
                    <h1 class="font-heading text-3xl sm:text-5xl font-black uppercase tracking-tight text-white leading-none">
                        ¿Cómo Explicar el <br><span class="bg-clip-text text-transparent bg-gradient-to-r from-spacex-accent via-white to-emerald-400">Plan Óptimo de Solver?</span>
                    </h1>
                    <p class="text-gray-300 text-sm sm:text-base leading-relaxed">
                        Aprende a explicar por qué la planta produce <strong class="text-spacex-accent">1,114 Batidoras en Octubre</strong>, mantiene las <strong class="text-emerald-400">Horas Extra en CERO</strong> durante todo el semestre y cómo reaccionar si la demanda sube un <strong class="text-spacex-amber">+10% en Nov-Dic</strong>.
                    </p>
                    <div class="flex flex-wrap gap-3 pt-2">
                        <button onclick="scrollToSec('tutorial')" class="px-5 py-3 bg-spacex-accent hover:bg-cyan-300 text-black font-heading font-extrabold text-xs uppercase tracking-widest rounded transition-all shadow-lg flex items-center gap-2">
                            <i class="fa-solid fa-graduation-cap"></i> Iniciar Guía Didáctica
                        </button>
                        <button onclick="scrollToSec('simulator')" class="px-5 py-3 bg-white/10 hover:bg-white/20 text-white font-heading font-bold text-xs uppercase tracking-widest rounded border border-white/15 transition-all flex items-center gap-2">
                            <i class="fa-solid fa-sliders text-spacex-amber"></i> Simular Escenarios
                        </button>
                    </div>
                </div>

                <!-- Mission Control Metric Cards -->
                <div class="lg:col-span-4 space-y-3">
                    <div class="glass-panel p-5 rounded-xl border border-spacex-accent/40 space-y-3 hud-border">
                        <span class="text-[10px] font-mono text-gray-400 uppercase tracking-widest block">COSTO TOTAL ÓPTIMO</span>
                        <p class="font-heading text-3xl sm:text-4xl font-black text-white">$294,915.44 <span class="text-xs text-spacex-accent font-mono font-normal">USD</span></p>

                        <div class="space-y-2 text-xs font-mono pt-3 border-t border-white/10">
                            <div class="flex justify-between items-center text-gray-300">
                                <span><i class="fa-solid fa-industry text-spacex-accent"></i> Producción Base:</span>
                                <span class="font-bold text-white">$290,850.00</span>
                            </div>
                            <div class="flex justify-between items-center text-emerald-400">
                                <span><i class="fa-solid fa-clock text-emerald-400"></i> Horas Extra Usadas:</span>
                                <span class="font-bold">0 hrs ($0.00)</span>
                            </div>
                            <div class="flex justify-between items-center text-purple-300">
                                <span><i class="fa-solid fa-warehouse text-purple-400"></i> Almacenamiento:</span>
                                <span class="font-bold">$4,065.44</span>
                            </div>
                        </div>
                    </div>

                    <div class="bg-white/5 p-4 rounded-xl border border-white/10 flex items-center justify-between font-mono text-xs">
                        <span class="text-gray-400">Pico Inventario Octubre:</span>
                        <span class="text-spacex-accent font-bold font-heading">764 Batidoras</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- INTERACTIVE TEACHING ACADEMY (12 - 20 YEARS OLD) -->
    <section id="tutorial" class="py-16 px-4 max-w-7xl mx-auto border-b border-white/10 space-y-10">
        <div class="text-center max-w-3xl mx-auto space-y-2">
            <span class="px-3 py-1 bg-spacex-accent/20 border border-spacex-accent/40 text-spacex-accent text-xs font-mono font-bold rounded uppercase tracking-widest">
                ACADEMIA INTERACTIVA PASO A PASO
            </span>
            <h2 class="font-heading text-2xl sm:text-3xl font-black text-white uppercase">Aprende la Lógica de Solver</h2>
            <p class="text-gray-400 text-sm">Explora las 5 etapas del modelo de optimización para explicarlo con facilidad en exposiciones o informes.</p>
        </div>

        <!-- Navigation Tabs -->
        <div class="grid grid-cols-2 md:grid-cols-5 gap-2.5 font-mono text-xs">
            <button onclick="selectStep(1)" id="stepBtn1" class="step-btn step-active p-3 rounded-lg glass-panel text-left border border-white/10 transition-all flex flex-col justify-between">
                <span class="text-spacex-accent font-bold">ETAPA 01</span>
                <span class="text-white font-semibold">1. Datos e Insumos</span>
            </button>
            <button onclick="selectStep(2)" id="stepBtn2" class="step-btn p-3 rounded-lg glass-panel text-left border border-white/10 transition-all flex flex-col justify-between">
                <span class="text-gray-500 font-bold">ETAPA 02</span>
                <span class="text-gray-300 font-semibold">2. Las 42 Variables</span>
            </button>
            <button onclick="selectStep(3)" id="stepBtn3" class="step-btn p-3 rounded-lg glass-panel text-left border border-white/10 transition-all flex flex-col justify-between">
                <span class="text-gray-500 font-bold">ETAPA 03</span>
                <span class="text-gray-300 font-semibold">3. Función Objetivo</span>
            </button>
            <button onclick="selectStep(4)" id="stepBtn4" class="step-btn p-3 rounded-lg glass-panel text-left border border-white/10 transition-all flex flex-col justify-between">
                <span class="text-gray-500 font-bold">ETAPA 04</span>
                <span class="text-gray-300 font-semibold">4. Restricciones</span>
            </button>
            <button onclick="selectStep(5)" id="stepBtn5" class="step-btn p-3 rounded-lg glass-panel text-left border border-white/10 transition-all flex flex-col justify-between">
                <span class="text-gray-500 font-bold">ETAPA 05</span>
                <span class="text-gray-300 font-semibold">5. ¿Por qué 0 Horas Extra?</span>
            </button>
        </div>

        <!-- Dynamic Content Panel -->
        <div class="glass-panel p-6 sm:p-8 rounded-xl border border-spacex-accent/30 space-y-6 hud-border" id="stepContentContainer">
            <!-- Stage 1 Content -->
            <div id="stepView1" class="space-y-6">
                <div class="flex items-center gap-3 border-b border-white/10 pb-4">
                    <div class="w-10 h-10 rounded-lg bg-spacex-accent/20 border border-spacex-accent flex items-center justify-center text-spacex-accent font-bold text-lg font-heading">01</div>
                    <div>
                        <h3 class="font-heading text-lg font-bold text-white uppercase">Etapa 1: Entender los Parámetros del Problema</h3>
                        <p class="text-xs text-gray-400">Todo modelo requiere conocer costos, horas de trabajo y reglas de producción.</p>
                    </div>
                </div>

                <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-4 font-mono text-xs">
                    <div class="bg-black/60 p-4 rounded-lg border border-white/10 space-y-2">
                        <span class="text-spacex-accent font-bold block uppercase"><i class="fa-solid fa-boxes-packing"></i> Productos Base</span>
                        <ul class="space-y-1 text-gray-300 text-[11px]">
                            <li>• Licuadora: 2.0 h/u | $40 USD</li>
                            <li>• Batidora: 2.5 h/u | $55 USD</li>
                            <li>• Procesador: 3.5 h/u | $75 USD</li>
                        </ul>
                    </div>

                    <div class="bg-black/60 p-4 rounded-lg border border-white/10 space-y-2">
                        <span class="text-spacex-amber font-bold block uppercase"><i class="fa-solid fa-percent"></i> Recargo Nov-Dic (+8%)</span>
                        <p class="text-gray-300 text-[11px]">En noviembre y diciembre los insumos aumentan un +8%:</p>
                        <p class="text-spacex-amber font-bold text-[11px]">Ej. Batidora: $55 ➔ $59.40 USD</p>
                    </div>

                    <div class="bg-black/60 p-4 rounded-lg border border-white/10 space-y-2">
                        <span class="text-red-400 font-bold block uppercase"><i class="fa-solid fa-user-clock"></i> Costo Horas Extra</span>
                        <p class="text-gray-300 text-[11px]">$12.00 USD por hora adicional trabajada (máx 350 horas por mes).</p>
                    </div>

                    <div class="bg-black/60 p-4 rounded-lg border border-white/10 space-y-2">
                        <span class="text-purple-400 font-bold block uppercase"><i class="fa-solid fa-warehouse"></i> Almacenamiento</span>
                        <p class="text-gray-300 text-[11px]">Costo de guardar en bodega por unidad al mes:</p>
                        <p class="text-purple-300 text-[11px]">Lic: $1.20 | Bat: $1.50 | Proc: $2.00</p>
                    </div>
                </div>

                <div class="p-4 bg-cyan-950/20 rounded-lg border border-spacex-accent/30 text-xs font-mono space-y-1">
                    <p class="text-spacex-accent font-bold uppercase flex items-center gap-2"><i class="fa-solid fa-lightbulb"></i> Analogía Didáctica para Jóvenes:</p>
                    <p class="text-gray-300">
                        "Imagina que vas a comprar suministros para un cohete espacial. Si compras los tanques en Octubre te cuestan $55 y pagas $1.50 por guardarlos en el hangar. Si esperas a Noviembre, la fábrica sube el precio a $59.40. ¿Qué te conviene más? ¡Comprarlos en Octubre y guardarlos en el hangar!"
                    </p>
                </div>
            </div>

            <!-- Stage 2 Content -->
            <div id="stepView2" class="hidden space-y-6">
                <div class="flex items-center gap-3 border-b border-white/10 pb-4">
                    <div class="w-10 h-10 rounded-lg bg-spacex-accent/20 border border-spacex-accent flex items-center justify-center text-spacex-accent font-bold text-lg font-heading">02</div>
                    <div>
                        <h3 class="font-heading text-lg font-bold text-white uppercase">Etapa 2: Definir las Variables de Decisión</h3>
                        <p class="text-xs text-gray-400">Son las incognitas numéricas que Solver calcula para minimizar el costo.</p>
                    </div>
                </div>

                <div class="grid md:grid-cols-3 gap-4 font-mono text-xs">
                    <div class="bg-black/60 p-4 rounded-lg border border-white/10 space-y-2">
                        <span class="text-spacex-accent font-bold text-sm block">1. Unidades Producidas (X_ij)</span>
                        <p class="text-gray-300">Cantidad a fabricar de cada producto $i$ en el mes $j$ (18 variables).</p>
                    </div>
                    <div class="bg-black/60 p-4 rounded-lg border border-white/10 space-y-2">
                        <span class="text-purple-400 font-bold text-sm block">2. Inventario Final (I_ij)</span>
                        <p class="text-gray-300">Cantidad a almacenar al final de cada mes $j$ (18 variables).</p>
                    </div>
                    <div class="bg-black/60 p-4 rounded-lg border border-white/10 space-y-2">
                        <span class="text-red-400 font-bold text-sm block">3. Horas Extra (HE_j)</span>
                        <p class="text-gray-300">Horas extra autorizadas en la planta cada mes $j$ (6 variables).</p>
                    </div>
                </div>

                <div class="p-3 bg-white/5 rounded-lg border border-white/10 font-mono text-xs text-gray-300">
                    <strong class="text-spacex-accent">Total: 42 Variables</strong> calculadas simultáneamente mediante el método Simplex en Excel Solver.
                </div>
            </div>

            <!-- Stage 3 Content -->
            <div id="stepView3" class="hidden space-y-6">
                <div class="flex items-center gap-3 border-b border-white/10 pb-4">
                    <div class="w-10 h-10 rounded-lg bg-spacex-accent/20 border border-spacex-accent flex items-center justify-center text-spacex-accent font-bold text-lg font-heading">03</div>
                    <div>
                        <h3 class="font-heading text-lg font-bold text-white uppercase">Etapa 3: La Función Objetivo Financiera</h3>
                        <p class="text-xs text-gray-400">Minimizar la suma total de costos durante los 6 meses (Julio a Diciembre).</p>
                    </div>
                </div>

                <div class="p-4 bg-black/80 rounded-lg border border-spacex-accent/40 font-mono text-xs space-y-3">
                    <p class="text-spacex-accent font-bold uppercase">Fórmula de Costo Total Mínimo:</p>
                    <div class="p-3 bg-white/5 rounded text-white font-mono text-center font-bold">
                        MIN Z = ∑ (Costo Producción × Unidades) + ∑ (Costo Almacenaje × Inventario) + ∑ ($12 × Horas Extra)
                    </div>
                    <p class="text-gray-300 text-[11px]">
                        Solver evaluó miles de combinaciones posibles y determinó que el valor global más bajo es <strong class="text-emerald-400">$294,915.44 USD</strong>.
                    </p>
                </div>
            </div>

            <!-- Stage 4 Content -->
            <div id="stepView4" class="hidden space-y-6">
                <div class="flex items-center gap-3 border-b border-white/10 pb-4">
                    <div class="w-10 h-10 rounded-lg bg-spacex-accent/20 border border-spacex-accent flex items-center justify-center text-spacex-accent font-bold text-lg font-heading">04</div>
                    <div>
                        <h3 class="font-heading text-lg font-bold text-white uppercase">Etapa 4: Las Restricciones del Sistema</h3>
                        <p class="text-xs text-gray-400">Las barreras físicas que la fábrica no puede sobrepasar.</p>
                    </div>
                </div>

                <div class="grid md:grid-cols-2 gap-4 font-mono text-xs">
                    <div class="bg-black/60 p-4 rounded-lg border border-white/10 space-y-2">
                        <span class="text-spacex-accent font-bold uppercase block"><i class="fa-solid fa-scale-balanced"></i> 1. Balance de Inventario</span>
                        <p class="text-gray-300">Inv. Inicial + Producción - Demanda = Inv. Final</p>
                        <p class="text-gray-400 text-[10px]">Asegura responder al 100% de los pedidos de los clientes.</p>
                    </div>

                    <div class="bg-black/60 p-4 rounded-lg border border-white/10 space-y-2">
                        <span class="text-spacex-amber font-bold uppercase block"><i class="fa-solid fa-clock"></i> 2. Capacidad Regular de Planta</span>
                        <p class="text-gray-300">Horas Requeridas ≤ Capacidad Disponible + Horas Extra</p>
                        <p class="text-gray-400 text-[10px]">Ej. En Julio la capacidad de 1,500 horas absorbió holgadamente la demanda.</p>
                    </div>

                    <div class="bg-black/60 p-4 rounded-lg border border-white/10 space-y-2">
                        <span class="text-red-400 font-bold uppercase block"><i class="fa-solid fa-stopwatch"></i> 3. Límite de Horas Extra</span>
                        <p class="text-gray-300">Horas Extra por Mes ≤ 350 horas.</p>
                    </div>

                    <div class="bg-black/60 p-4 rounded-lg border border-white/10 space-y-2">
                        <span class="text-emerald-400 font-bold uppercase block"><i class="fa-solid fa-flag-checkered"></i> 4. Inventario Cierre Diciembre</span>
                        <p class="text-gray-300">Requerido: 80 Licuadoras, 70 Batidoras, 40 Procesadores.</p>
                    </div>
                </div>
            </div>

            <!-- Stage 5 Content -->
            <div id="stepView5" class="hidden space-y-6">
                <div class="flex items-center gap-3 border-b border-white/10 pb-4">
                    <div class="w-10 h-10 rounded-lg bg-spacex-accent/20 border border-spacex-accent flex items-center justify-center text-spacex-accent font-bold text-lg font-heading">05</div>
                    <div>
                        <h3 class="font-heading text-lg font-bold text-white uppercase">Etapa 5: Demostración Matemática (¿Por qué Horas Extra = 0?)</h3>
                        <p class="text-xs text-gray-400">El secreto clave para la presentación con la Gerente Mariana Castillo.</p>
                    </div>
                </div>

                <div class="p-5 bg-black/80 rounded-lg border border-spacex-accent/40 space-y-4 font-mono text-xs">
                    <p class="text-spacex-accent font-bold uppercase text-sm">💡 Comparativa de Costos por Unidad de Procesador:</p>

                    <div class="grid sm:grid-cols-2 gap-4">
                        <div class="bg-red-950/30 p-4 rounded border border-red-500/30 space-y-1">
                            <span class="text-red-400 font-bold block">Opción A: Fabricar con Horas Extra</span>
                            <p class="text-gray-300">3.5 horas × $12 USD/hora = <strong class="text-red-400">+$42.00 USD extra por unidad</strong></p>
                        </div>

                        <div class="bg-emerald-950/30 p-4 rounded border border-emerald-500/30 space-y-1">
                            <span class="text-emerald-400 font-bold block">Opción B: Producir Antes y Guardar</span>
                            <p class="text-gray-300">Almacenar 1 mes en bodega = <strong class="text-emerald-400">+$2.00 USD extra por unidad</strong></p>
                        </div>
                    </div>

                    <p class="text-gray-300 text-[11px] pt-2 border-t border-white/10">
                        <strong>Conclusión:</strong> Almacenar es <strong class="text-spacex-accent">21 veces más barato</strong> que contratar horas extra. Por esta razón, el Algoritmo Simplex deja la variable de horas extra en CERO absoluto para todos los meses.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- EXACT SOLVER TELEMETRY TABLES SECTION -->
    <section id="plan" class="py-16 px-4 max-w-7xl mx-auto border-b border-white/10 space-y-12">
        <div class="text-center max-w-3xl mx-auto space-y-2">
            <span class="text-xs font-mono font-bold uppercase text-spacex-accent tracking-widest">Resultados del Modelo Simplex</span>
            <h2 class="font-heading text-2xl sm:text-3xl font-black text-white uppercase">Telemetría de Producción e Inventario</h2>
            <p class="text-gray-400 text-sm">Cifras exactas extraídas de la solución óptima entregada por Solver en Excel.</p>
        </div>

        <!-- Production Table -->
        <div class="space-y-4">
            <div class="flex items-center justify-between flex-wrap gap-2">
                <h3 class="font-heading text-base sm:text-lg font-bold text-white flex items-center gap-2">
                    <i class="fa-solid fa-industry text-spacex-accent"></i> 1. Plan de Producción Mensual Recomendado (Unidades)
                </h3>
                <span class="px-3 py-1 bg-emerald-500/10 border border-emerald-500/30 text-emerald-400 font-mono text-xs rounded">
                    ⚡ Horas Extra: 0 en todos los meses
                </span>
            </div>

            <div class="glass-panel rounded-xl overflow-x-auto border border-white/10">
                <table class="w-full text-left font-mono text-xs sm:text-sm">
                    <thead>
                        <tr class="bg-white/5 text-spacex-accent font-heading border-b border-white/10 text-[11px]">
                            <th class="p-3.5">MES</th>
                            <th class="p-3.5 text-center">LICUADORA</th>
                            <th class="p-3.5 text-center">BATIDORA</th>
                            <th class="p-3.5 text-center">PROCESADOR</th>
                            <th class="p-3.5 text-center">HORAS EXTRA</th>
                            <th class="p-3.5 text-right">TOTAL UNIDADES</th>
                        </tr>
                    </thead>
                    <tbody class="divide-y divide-white/5 text-gray-200" id="prodTableBody">
                        <!-- JS Rendered -->
                    </tbody>
                </table>
            </div>
        </div>

        <!-- Inventory Table -->
        <div class="space-y-4">
            <div class="flex items-center justify-between flex-wrap gap-2">
                <h3 class="font-heading text-base sm:text-lg font-bold text-white flex items-center gap-2">
                    <i class="fa-solid fa-boxes-stacked text-purple-400"></i> 2. Inventario Final en Bodega (Unidades)
                </h3>
                <span class="px-3 py-1 bg-purple-500/10 border border-purple-500/30 text-purple-300 font-mono text-xs rounded">
                    📦 Pico Máximo: 764 Batidoras al cierre de Octubre
                </span>
            </div>

            <div class="glass-panel rounded-xl overflow-x-auto border border-white/10">
                <table class="w-full text-left font-mono text-xs sm:text-sm">
                    <thead>
                        <tr class="bg-white/5 text-purple-300 font-heading border-b border-white/10 text-[11px]">
                            <th class="p-3.5">MES</th>
                            <th class="p-3.5 text-center">LICUADORA</th>
                            <th class="p-3.5 text-center">BATIDORA</th>
                            <th class="p-3.5 text-center">PROCESADOR</th>
                            <th class="p-3.5 text-right">ACUMULADO BODEGA</th>
                        </tr>
                    </thead>
                    <tbody class="divide-y divide-white/5 text-gray-200" id="invTableBody">
                        <!-- JS Rendered -->
                    </tbody>
                </table>
            </div>
        </div>
    </section>

    <!-- INTERACTIVE WHAT-IF SIMULATOR SECTION -->
    <section id="simulator" class="py-16 px-4 max-w-7xl mx-auto border-b border-white/10 space-y-10">
        <div class="text-center max-w-3xl mx-auto space-y-2">
            <span class="px-3 py-1 bg-spacex-amber/20 border border-spacex-amber/40 text-spacex-amber text-xs font-mono font-bold rounded uppercase tracking-widest">
                HERRAMIENTA INTERACTIVA TRABAJO DE CAMPO
            </span>
            <h2 class="font-heading text-2xl sm:text-3xl font-black text-white uppercase">Simulador "What-If" de Planta</h2>
            <p class="text-gray-400 text-sm">Ajusta los parámetros para explorar cómo reacciona el costo global y las horas de capacidad.</p>
        </div>

        <div class="glass-panel p-6 sm:p-8 rounded-xl border border-spacex-amber/40 space-y-6 hud-border">
            <div class="grid lg:grid-cols-12 gap-8 items-center">
                <!-- Controls -->
                <div class="lg:col-span-5 space-y-5 font-mono text-xs">
                    <h3 class="font-heading text-base font-bold text-white uppercase border-b border-white/10 pb-2">
                        <i class="fa-solid fa-sliders text-spacex-amber"></i> Ajuste de Sensibilidad
                    </h3>

                    <div class="space-y-2">
                        <div class="flex justify-between text-gray-300">
                            <label for="demandSlider">Variación Demanda Nov-Dic:</label>
                            <span id="demandVal" class="text-spacex-amber font-bold">0% (Base Excel)</span>
                        </div>
                        <input type="range" id="demandSlider" min="0" max="25" step="5" value="0" class="w-full accent-spacex-amber bg-white/10 h-2 rounded cursor-pointer">
                    </div>

                    <div class="space-y-2">
                        <div class="flex justify-between text-gray-300">
                            <label for="overtimeCostSlider">Costo de Hora Extra ($/hr):</label>
                            <span id="overtimeVal" class="text-spacex-accent font-bold">$12.00 USD</span>
                        </div>
                        <input type="range" id="overtimeCostSlider" min="8" max="25" step="1" value="12" class="w-full accent-spacex-accent bg-white/10 h-2 rounded cursor-pointer">
                    </div>

                    <div class="p-3 bg-white/5 rounded border border-white/10 text-gray-400 text-[11px] leading-relaxed">
                        <i class="fa-solid fa-circle-info text-spacex-accent"></i> Mueve los controles para ver el impacto en tiempo real sobre el costo total y el margen de seguridad de la planta.
                    </div>
                </div>

                <!-- Simulation Output -->
                <div class="lg:col-span-7 bg-black/80 p-5 rounded-xl border border-white/15 space-y-4 font-mono text-xs">
                    <div class="flex justify-between items-center border-b border-white/10 pb-3">
                        <span class="text-gray-400 text-[10px] uppercase">Resultado de Simulación</span>
                        <span id="simStatusBadge" class="px-2.5 py-1 bg-emerald-500/20 text-emerald-400 border border-emerald-500/40 rounded text-[10px] font-bold">NOMINAL / SIN HORAS EXTRA</span>
                    </div>

                    <div class="grid grid-cols-2 gap-3">
                        <div class="bg-white/5 p-3 rounded">
                            <span class="text-gray-400 text-[10px] block uppercase">Costo Total Estimado:</span>
                            <span id="simTotalCost" class="text-xl sm:text-2xl font-bold font-heading text-white">$294,915.44</span>
                        </div>
                        <div class="bg-white/5 p-3 rounded">
                            <span class="text-gray-400 text-[10px] block uppercase">Impacto vs Plan Base:</span>
                            <span id="simCostDiff" class="text-xl sm:text-2xl font-bold font-heading text-spacex-accent">+$0.00</span>
                        </div>
                    </div>

                    <div class="p-3 bg-spacex-amber/10 rounded border border-spacex-amber/30 space-y-1">
                        <span class="text-spacex-amber font-bold block uppercase text-[11px]"><i class="fa-solid fa-triangle-exclamation"></i> Diagnóstico de Riesgo Sección 4:</span>
                        <p id="simRiskText" class="text-gray-300 text-[11px]">
                            Con la demanda base el sistema opera sin horas extra. Al +10% de demanda el costo sube a $310,614.26 USD y la capacidad regular queda al 100% copada de Sep a Dic (4 meses seguidos sin holgura).
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- FINANCIAL BREAKDOWN & CHARTS SECTION -->
    <section id="costs" class="py-16 px-4 max-w-7xl mx-auto border-b border-white/10 space-y-10">
        <div class="text-center max-w-3xl mx-auto space-y-2">
            <span class="text-xs font-mono font-bold uppercase text-spacex-accent tracking-widest">Desglose Financiero</span>
            <h2 class="font-heading text-2xl sm:text-3xl font-black text-white uppercase">Estructura Económica de la Misión</h2>
            <p class="text-gray-400 text-sm">Visualiza la distribución de la producción mensual y la composición de los $294,915.44 USD.</p>
        </div>

        <div class="grid lg:grid-cols-12 gap-8 items-center">
            <!-- Cost Summary Card -->
            <div class="lg:col-span-5 glass-panel p-6 rounded-xl border border-white/10 space-y-4">
                <h3 class="font-heading text-base font-bold text-white border-b border-white/10 pb-3">
                    Resumen Consolidado (Julio - Diciembre)
                </h3>

                <div class="space-y-3 font-mono text-xs sm:text-sm">
                    <div class="flex justify-between items-center p-3 bg-white/5 rounded border border-white/5">
                        <span class="text-gray-300 flex items-center gap-2"><i class="fa-solid fa-gears text-spacex-accent"></i> Costo Producción Regular</span>
                        <span class="font-bold text-white">USD 290,850.00</span>
                    </div>

                    <div class="flex justify-between items-center p-3 bg-emerald-950/30 rounded border border-emerald-500/30">
                        <span class="text-emerald-300 flex items-center gap-2"><i class="fa-solid fa-clock-rotate-left text-emerald-400"></i> Costo por Horas Extra</span>
                        <span class="font-bold text-emerald-400">USD 0.00</span>
                    </div>

                    <div class="flex justify-between items-center p-3 bg-white/5 rounded border border-white/5">
                        <span class="text-gray-300 flex items-center gap-2"><i class="fa-solid fa-warehouse text-purple-400"></i> Costo Almacenamiento Bodega</span>
                        <span class="font-bold text-white">USD 4,065.44</span>
                    </div>

                    <div class="flex justify-between items-center p-4 bg-spacex-accent/10 rounded border border-spacex-accent/40 font-heading font-bold text-sm text-white">
                        <span>TOTAL MÍNIMO SOLVER</span>
                        <span class="text-spacex-accent">USD 294,915.44</span>
                    </div>
                </div>
            </div>

            <!-- Chart Canvas -->
            <div class="lg:col-span-7 glass-panel p-6 rounded-xl border border-white/10 space-y-4">
                <div class="flex justify-between items-center flex-wrap gap-2 border-b border-white/10 pb-3">
                    <div>
                        <h3 class="font-heading text-sm uppercase text-spacex-accent font-black tracking-wider">PRODUCCIÓN MENSUAL POR PRODUCTO</h3>
                        <span class="text-[10px] font-mono text-gray-400">Julio a Diciembre 2026</span>
                    </div>
                    <!-- Product Filter Buttons -->
                    <div class="flex gap-1 font-mono text-[10px]">
                        <button onclick="setChartFilter('all')" id="btnChartAll" class="px-2.5 py-1 rounded bg-spacex-accent text-black font-bold transition-all">Todos</button>
                        <button onclick="setChartFilter('licuadora')" id="btnChartLic" class="px-2.5 py-1 rounded bg-white/10 text-gray-300 hover:text-white transition-all">Licuadora</button>
                        <button onclick="setChartFilter('batidora')" id="btnChartBat" class="px-2.5 py-1 rounded bg-white/10 text-gray-300 hover:text-white transition-all">Batidora</button>
                        <button onclick="setChartFilter('procesador')" id="btnChartProc" class="px-2.5 py-1 rounded bg-white/10 text-gray-300 hover:text-white transition-all">Procesador</button>
                    </div>
                </div>

                <!-- Native SVG/HTML Interactive Visual Bar Chart -->
                <div id="nativeChartContainer" class="space-y-2.5 max-h-[380px] overflow-y-auto custom-scrollbar pr-1">
                    <!-- JS Rendered Dynamic Visual Bars -->
                </div>
            </div>
        </div>
    </section>

    <!-- STRATEGIC GERENCIAL OBSERVATIONS SECTION -->
    <section id="insights" class="py-16 px-4 max-w-7xl mx-auto border-b border-white/10 space-y-10">
        <div class="text-center max-w-3xl mx-auto space-y-2">
            <span class="text-xs font-mono font-bold uppercase text-spacex-accent tracking-widest">Observaciones Clave</span>
            <h2 class="font-heading text-2xl sm:text-3xl font-black text-white uppercase">3 Secretos Estratégicos para Mariana Castillo</h2>
            <p class="text-gray-400 text-sm">Puntos indispensables para defender el informe en la reunión gerencial.</p>
        </div>

        <div class="grid md:grid-cols-3 gap-6">
            <!-- Secret 1 -->
            <div class="glass-panel p-6 rounded-xl border border-red-500/30 space-y-4 hover:border-red-500/60 transition-all">
                <div class="w-10 h-10 rounded bg-red-500/10 border border-red-500/30 flex items-center justify-center text-red-400 text-lg font-bold font-heading">
                    01
                </div>
                <h3 class="font-heading text-base font-bold text-white">Horas Extra Prohibitivas</h3>
                <p class="text-xs text-gray-300 leading-relaxed">
                    El sobrecosto de <strong class="text-red-400">$12 USD/hora</strong> equivale a añadir ~$21.60 USD por cada Procesador. Almacenar 1 mes solo cuesta $2.00 USD. Producir antes destruye la necesidad de horas extra.
                </p>
            </div>

            <!-- Secret 2 -->
            <div class="glass-panel p-6 rounded-xl border border-spacex-accent/30 space-y-4 hover:border-spacex-accent/60 transition-all">
                <div class="w-10 h-10 rounded bg-spacex-accent/10 border border-spacex-accent/30 flex items-center justify-center text-spacex-accent text-lg font-bold font-heading">
                    02
                </div>
                <h3 class="font-heading text-base font-bold text-white">Congelamiento de Costo en Octubre</h3>
                <p class="text-xs text-gray-300 leading-relaxed">
                    Octubre es el último mes con costo base normal ($55 USD por Batidora). Producir <strong class="text-spacex-accent">1,114 Batidoras en Octubre</strong> permite "congelar" el costo antes del alza del +8% de Nov-Dic.
                </p>
            </div>

            <!-- Secret 3 -->
            <div class="glass-panel p-6 rounded-xl border border-purple-500/30 space-y-4 hover:border-purple-500/60 transition-all">
                <div class="w-10 h-10 rounded bg-purple-500/10 border border-purple-500/30 flex items-center justify-center text-purple-400 text-lg font-bold font-heading">
                    03
                </div>
                <h3 class="font-heading text-base font-bold text-white">Pregunta Estratégica de Capacidad</h3>
                <p class="text-xs text-gray-300 leading-relaxed">
                    ¿Vale la pena contratar un turno fijo o maquila con terceros? La planta opera al <strong class="text-purple-300">100% de capacidad durante 4 meses seguidos (Sep-Dic)</strong> sin ningún margen ante imprevistos.
                </p>
            </div>
        </div>
    </section>

    <!-- GAMIFIED QUIZ ACADEMY SECTION -->
    <section id="challenge" class="py-16 px-4 max-w-5xl mx-auto border-b border-white/10 space-y-10">
        <div class="text-center max-w-3xl mx-auto space-y-2">
            <span class="text-xs font-mono font-bold uppercase text-emerald-400 tracking-widest">Evaluación de Conocimiento</span>
            <h2 class="font-heading text-2xl sm:text-3xl font-black text-white uppercase">Desafío Estudiantil Simplex</h2>
            <p class="text-gray-400 text-sm">Responde las 3 preguntas clave para validar si estás listo para presentar el caso.</p>
        </div>

        <div class="glass-panel rounded-xl p-6 sm:p-10 border border-white/15 relative overflow-hidden" id="quizContainer">
            <!-- JS Populated Quiz -->
        </div>
    </section>

    <!-- EXPORTABLE MEMO BUILDER FOR MARIANA CASTILLO -->
    <section id="export-memo" class="py-16 px-4 max-w-7xl mx-auto space-y-10">
        <div class="text-center max-w-3xl mx-auto space-y-2">
            <span class="text-xs font-mono font-bold uppercase text-spacex-accent tracking-widest">Entrega de Tarea / Proyecto</span>
            <h2 class="font-heading text-2xl sm:text-3xl font-black text-white uppercase">Generador de Memorando Ejecutivo</h2>
            <p class="text-gray-400 text-sm">Crea una ficha lista para copiar o imprimir para tu docente o para la Gerente Mariana Castillo.</p>
        </div>

        <div class="grid lg:grid-cols-12 gap-8">
            <!-- Inputs -->
            <div class="lg:col-span-5 glass-panel p-6 rounded-xl border border-white/10 space-y-4">
                <h3 class="font-heading text-base font-bold text-white flex items-center gap-2 border-b border-white/10 pb-2">
                    <i class="fa-solid fa-pen-to-square text-spacex-accent"></i> Datos del Estudiante
                </h3>

                <div>
                    <label class="block text-xs font-mono text-gray-300 uppercase mb-1">Nombre del Analista / Estudiante</label>
                    <input type="text" id="studentName" value="Alex Rivera" class="w-full bg-black/60 border border-white/15 rounded p-2 text-xs text-white focus:outline-none focus:border-spacex-accent font-mono">
                </div>

                <div>
                    <label class="block text-xs font-mono text-gray-300 uppercase mb-1">Asignatura / Curso</label>
                    <input type="text" id="studentCourse" value="Investigación de Operaciones / Modelos de Optimización" class="w-full bg-black/60 border border-white/15 rounded p-2 text-xs text-white focus:outline-none focus:border-spacex-accent font-mono">
                </div>

                <div>
                    <div class="flex justify-between items-center mb-1">
                        <label class="block text-xs font-mono text-spacex-accent uppercase font-bold flex items-center gap-1.5">
                            <i class="fa-solid fa-robot"></i> Conclusión Recomendada (Automática)
                        </label>
                        <span id="autoGenBadge" class="text-[10px] font-mono px-2 py-0.5 rounded bg-spacex-accent/20 text-spacex-accent border border-spacex-accent/40 font-bold">
                            Auto-Sincronizada
                        </span>
                    </div>
                    <textarea id="studentConclusion" rows="4" class="w-full bg-black/60 border border-white/15 rounded p-2 text-xs text-white focus:outline-none focus:border-spacex-accent font-mono leading-relaxed" placeholder="Generando conclusión automática..."></textarea>
                    
                    <div class="flex flex-wrap gap-1.5 pt-2">
                        <button type="button" onclick="setAutoConclusionPreset('base')" class="px-2.5 py-1 bg-white/5 hover:bg-spacex-accent/20 hover:text-spacex-accent text-gray-300 rounded border border-white/10 text-[10px] font-mono transition-all">
                            ⚡ Plan Base
                        </button>
                        <button type="button" onclick="setAutoConclusionPreset('risk')" class="px-2.5 py-1 bg-white/5 hover:bg-spacex-amber/20 hover:text-spacex-amber text-gray-300 rounded border border-white/10 text-[10px] font-mono transition-all">
                            ⚠️ Riesgo +10%
                        </button>
                        <button type="button" onclick="setAutoConclusionPreset('cap')" class="px-2.5 py-1 bg-white/5 hover:bg-purple-500/20 hover:text-purple-300 text-gray-300 rounded border border-white/10 text-[10px] font-mono transition-all">
                            🏭 Capacidad Planta
                        </button>
                    </div>
                </div>

                <button id="updateReportBtn" onclick="generateAutoConclusion()" class="w-full py-2.5 bg-spacex-accent hover:bg-cyan-300 text-black font-heading font-bold text-xs uppercase tracking-widest rounded transition-all flex items-center justify-center gap-2">
                    <i class="fa-solid fa-wand-magic-sparkles"></i> Regenerar Conclusión Automática
                </button>
            </div>

            <!-- Preview Card -->
            <div class="lg:col-span-7 glass-panel p-6 sm:p-8 rounded-xl border border-spacex-accent/40 space-y-4 bg-gradient-to-br from-spacex-card to-black hud-border" id="printableArea">
                <div class="border-b border-white/10 pb-3 flex justify-between items-center">
                    <div>
                        <span class="text-[10px] font-mono text-spacex-accent uppercase tracking-widest block">MEMORANDO EJECUTIVO DE OPTIMIZACIÓN</span>
                        <h4 class="font-heading font-bold text-white text-sm sm:text-base">Para: Mariana Castillo, Gerente de Operaciones</h4>
                    </div>
                    <span class="px-2 py-0.5 bg-emerald-500/20 text-emerald-400 font-mono text-[10px] rounded border border-emerald-500/40 font-bold">2.º SEMESTRE 2026</span>
                </div>

                <div class="grid grid-cols-2 gap-2 font-mono text-[11px]">
                    <div class="bg-white/5 p-2 rounded">
                        <span class="text-gray-400 block">De:</span>
                        <span id="prevStudentName" class="text-white font-bold">Alex Rivera (Analista de Planeación)</span>
                    </div>
                    <div class="bg-white/5 p-2 rounded">
                        <span class="text-gray-400 block">Materia:</span>
                        <span id="prevCourse" class="text-spacex-accent font-bold">Investigación de Operaciones</span>
                    </div>
                </div>

                <div class="space-y-1.5 text-xs font-mono text-gray-200">
                    <span class="text-gray-400 uppercase text-[10px] block font-bold">Resumen Métrico del Plan Óptimo:</span>
                    <ul class="list-disc list-inside space-y-0.5 text-[11px]">
                        <li>Costo Total del Plan: <strong>USD 294,915.44</strong></li>
                        <li>Costo de Horas Extra: <strong>USD 0.00</strong> (0 horas requeridas en todos los meses)</li>
                        <li>Costo de Almacenamiento: <strong>USD 4,065.44</strong></li>
                        <li>Producción Pico Batidora: <strong>1,114 unidades</strong> en Octubre</li>
                    </ul>
                </div>

                <div class="space-y-1 pt-2 border-t border-white/10 text-xs">
                    <span class="text-spacex-accent font-mono text-[10px] uppercase font-bold block">Recomendación Estratégica:</span>
                    <p id="prevConclusion" class="text-gray-300 italic text-[11px] leading-relaxed">
                        Se recomienda adoptar el plan óptimo del modelo Simplex (USD 294,915.44) manteniendo horas extra en 0. Se sugiere dejar negociado un colchón de contingencia para el riesgo de demanda +10% en nov-dic.
                    </p>
                </div>

                <div class="pt-3 flex gap-3 font-mono text-xs">
                    <button onclick="copyTaskReport()" class="flex-1 py-2.5 bg-white/10 hover:bg-white/20 text-white rounded transition-all flex items-center justify-center gap-2 font-semibold">
                        <i class="fa-solid fa-copy"></i> Copiar Texto
                    </button>
                    <button onclick="window.print()" class="py-2.5 px-4 bg-spacex-accent/20 hover:bg-spacex-accent hover:text-black border border-spacex-accent/40 text-spacex-accent rounded transition-all flex items-center justify-center gap-2 font-semibold">
                        <i class="fa-solid fa-print"></i> Imprimir / PDF
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-black border-t border-white/10 py-8 px-4 text-center text-xs text-gray-500 space-y-2 font-mono">
        <div class="max-w-7xl mx-auto flex flex-col sm:flex-row justify-between items-center gap-4">
            <div class="flex items-center gap-2">
                <i class="fa-solid fa-rocket text-spacex-accent"></i>
                <span class="font-heading font-bold text-white">SPACEX STARFACTORY OPS</span>
            </div>
            <p>Taller Didáctico de Optimización Lineal (Solver Simplex) - Caso ElectroAndina 2026</p>
            <p>Mariana Castillo, Gerente de Operaciones</p>
        </div>
    </footer>

    <!-- JavaScript Application Logic -->
    <script>
        // Exact Data from ElectroAndina Memo (Jul - Dic 2026)
        const prodData = [
            { month: 'Jul', licuadora: 200, batidora: 180, procesador: 120.0, overtime: 0 },
            { month: 'Ago', licuadora: 340, batidora: 290, procesador: 190.0, overtime: 0 },
            { month: 'Sep', licuadora: 380, batidora: 310, procesador: 404.4, overtime: 0 },
            { month: 'Oct', licuadora: 420, batidora: 1114, procesador: 45.6, overtime: 0 },
            { month: 'Nov', licuadora: 560, batidora: 0, procesador: 571.1, overtime: 0 },
            { month: 'Dic', licuadora: 760, batidora: 376, procesador: 228.9, overtime: 0 }
        ];

        const invData = [
            { month: 'Jul', licuadora: 0, batidora: 0, procesador: 0 },
            { month: 'Ago', licuadora: 0, batidora: 0, procesador: 0 },
            { month: 'Sep', licuadora: 0, batidora: 0, procesador: 194.4 },
            { month: 'Oct', licuadora: 0, batidora: 764, procesador: 0 },
            { month: 'Nov', licuadora: 0, batidora: 284, procesador: 231.1 },
            { month: 'Dic', licuadora: 80, batidora: 70, procesador: 40 }
        ];

        // Step Navigation Switcher
        function selectStep(stepNum) {
            for (let i = 1; i <= 5; i++) {
                const btn = document.getElementById(`stepBtn${i}`);
                const view = document.getElementById(`stepView${i}`);
                if (i === stepNum) {
                    btn.classList.add('step-active');
                    btn.querySelector('span:first-child').className = 'text-spacex-accent font-bold';
                    btn.querySelector('span:last-child').className = 'text-white font-semibold';
                    view.classList.remove('hidden');
                } else {
                    btn.classList.remove('step-active');
                    btn.querySelector('span:first-child').className = 'text-gray-500 font-bold';
                    btn.querySelector('span:last-child').className = 'text-gray-300 font-semibold';
                    view.classList.add('hidden');
                }
            }
        }

        // Render Telemetry Tables
        function renderTables() {
            const prodBody = document.getElementById('prodTableBody');
            prodBody.innerHTML = prodData.map(row => {
                const total = row.licuadora + row.batidora + row.procesador;
                return `
                    <tr class="hover:bg-white/5 transition-colors">
                        <td class="p-3.5 font-bold text-white font-heading">${row.month}</td>
                        <td class="p-3.5 text-center">${row.licuadora}</td>
                        <td class="p-3.5 text-center ${row.batidora > 500 ? 'text-spacex-accent font-bold' : ''}">${row.batidora}</td>
                        <td class="p-3.5 text-center">${row.procesador.toFixed(1)}</td>
                        <td class="p-3.5 text-center text-emerald-400 font-bold">${row.overtime}</td>
                        <td class="p-3.5 text-right font-bold text-white">${total.toFixed(1)}</td>
                    </tr>
                `;
            }).join('');

            const invBody = document.getElementById('invTableBody');
            invBody.innerHTML = invData.map(row => {
                const total = row.licuadora + row.batidora + row.procesador;
                return `
                    <tr class="hover:bg-white/5 transition-colors">
                        <td class="p-3.5 font-bold text-white font-heading">${row.month}</td>
                        <td class="p-3.5 text-center">${row.licuadora}</td>
                        <td class="p-3.5 text-center ${row.batidora > 500 ? 'text-purple-300 font-bold' : ''}">${row.batidora}</td>
                        <td class="p-3.5 text-center">${row.procesador.toFixed(1)}</td>
                        <td class="p-3.5 text-right font-bold text-spacex-accent">${total.toFixed(1)}</td>
                    </tr>
                `;
            }).join('');
        }

        // Native Visual Bar Chart Logic
        let currentChartFilter = 'all';

        function setChartFilter(filter) {
            currentChartFilter = filter;
            const btnMap = { 'all': 'btnChartAll', 'licuadora': 'btnChartLic', 'batidora': 'btnChartBat', 'procesador': 'btnChartProc' };
            
            Object.keys(btnMap).forEach(key => {
                const btn = document.getElementById(btnMap[key]);
                if (btn) {
                    if (key === filter) {
                        btn.className = 'px-2.5 py-1 rounded bg-spacex-accent text-black font-bold transition-all';
                    } else {
                        btn.className = 'px-2.5 py-1 rounded bg-white/10 text-gray-300 hover:text-white transition-all';
                    }
                }
            });
            renderNativeChart();
        }

        function renderNativeChart() {
            const container = document.getElementById('nativeChartContainer');
            if (!container) return;

            const maxVal = 1200; // max scale benchmark (Oct Batidora es 1114)

            container.innerHTML = prodData.map(d => {
                let barsHtml = '';

                if (currentChartFilter === 'all' || currentChartFilter === 'licuadora') {
                    const pctLic = (d.licuadora / maxVal) * 100;
                    barsHtml += `
                        <div class="flex items-center gap-2 group" title="Licuadora: ${d.licuadora} u.">
                            <span class="w-10 text-[10px] text-gray-400 font-mono">Lic.</span>
                            <div class="flex-1 bg-white/5 h-3 rounded overflow-hidden p-0.5 border border-white/10">
                                <div class="bg-gradient-to-r from-cyan-500 to-spacex-accent h-full rounded transition-all duration-500" style="width: ${Math.max(pctLic, 2)}%"></div>
                            </div>
                            <span class="w-12 text-right text-[10px] font-bold text-spacex-accent font-mono">${d.licuadora}</span>
                        </div>
                    `;
                }

                if (currentChartFilter === 'all' || currentChartFilter === 'batidora') {
                    const pctBat = (d.batidora / maxVal) * 100;
                    barsHtml += `
                        <div class="flex items-center gap-2 group" title="Batidora: ${d.batidora} u.">
                            <span class="w-10 text-[10px] text-gray-400 font-mono">Bat.</span>
                            <div class="flex-1 bg-white/5 h-3 rounded overflow-hidden p-0.5 border border-white/10">
                                <div class="bg-gradient-to-r from-purple-600 to-purple-400 h-full rounded transition-all duration-500" style="width: ${Math.max(pctBat, 2)}%"></div>
                            </div>
                            <span class="w-12 text-right text-[10px] font-bold text-purple-400 font-mono">${d.batidora}</span>
                        </div>
                    `;
                }

                if (currentChartFilter === 'all' || currentChartFilter === 'procesador') {
                    const pctProc = (d.procesador / maxVal) * 100;
                    barsHtml += `
                        <div class="flex items-center gap-2 group" title="Procesador: ${d.procesador.toFixed(1)} u.">
                            <span class="w-10 text-[10px] text-gray-400 font-mono">Proc.</span>
                            <div class="flex-1 bg-white/5 h-3 rounded overflow-hidden p-0.5 border border-white/10">
                                <div class="bg-gradient-to-r from-emerald-600 to-emerald-400 h-full rounded transition-all duration-500" style="width: ${Math.max(pctProc, 2)}%"></div>
                            </div>
                            <span class="w-12 text-right text-[10px] font-bold text-emerald-400 font-mono">${d.procesador.toFixed(1)}</span>
                        </div>
                    `;
                }

                return `
                    <div class="bg-black/60 p-2.5 rounded-lg border border-white/10 space-y-1.5 hover:border-spacex-accent/40 transition-all">
                        <div class="flex justify-between items-center border-b border-white/5 pb-1">
                            <span class="font-heading font-bold text-xs text-white uppercase">${d.month} 2026</span>
                            <span class="text-[10px] font-mono text-gray-400">Total Mes: ${(d.licuadora + d.batidora + d.procesador).toFixed(1)} u.</span>
                        </div>
                        <div class="space-y-1">
                            ${barsHtml}
                        </div>
                    </div>
                `;
            }).join('');
        }

        // What-If Simulator Logic
        function updateSimulator() {
            const demandPct = parseInt(document.getElementById('demandSlider').value);
            const overtimeRate = parseInt(document.getElementById('overtimeCostSlider').value);

            document.getElementById('demandVal').innerText = `${demandPct}% ${demandPct === 0 ? '(Base Excel)' : ''}`;
            document.getElementById('overtimeVal').innerText = `$${overtimeRate}.00 USD`;

            const baseCost = 294915.44;
            let costDiff = 0;

            if (demandPct === 10) {
                costDiff = 15698.82; // Exact from section 4 of the Memo ($310,614.26 - $294,915.44)
            } else if (demandPct > 10) {
                costDiff = 15698.82 + ((demandPct - 10) * 2200);
            } else if (demandPct > 0) {
                costDiff = (demandPct / 10) * 15698.82;
            }

            const totalCost = baseCost + costDiff;

            document.getElementById('simTotalCost').innerText = `$${totalCost.toLocaleString('en-US', { minimumFractionDigits: 2, maximumFractionDigits: 2 })}`;
            document.getElementById('simCostDiff').innerText = `+$${costDiff.toLocaleString('en-US', { minimumFractionDigits: 2, maximumFractionDigits: 2 })}`;

            const badge = document.getElementById('simStatusBadge');
            const riskText = document.getElementById('simRiskText');

            if (demandPct === 0) {
                badge.className = 'px-2.5 py-1 bg-emerald-500/20 text-emerald-400 border border-emerald-500/40 rounded text-[10px] font-bold';
                badge.innerText = 'NOMINAL / SIN HORAS EXTRA';
                riskText.innerText = 'Con la demanda base de Excel, el sistema opera óptimamente sin requerir horas extra (Costo: $294,915.44 USD).';
            } else if (demandPct === 10) {
                badge.className = 'px-2.5 py-1 bg-spacex-amber/20 text-spacex-amber border border-spacex-amber/40 rounded text-[10px] font-bold';
                badge.innerText = 'CAPACIDAD REGULAR AL 100% (4 MESES)';
                riskText.innerText = 'Con +10% de demanda en Nov-Dic, el costo sube a $310,614.26 USD (+5.3%). La planta opera al 100% de capacidad regular desde Sep hasta Dic sin ningún colchón de seguridad.';
            } else {
                badge.className = 'px-2.5 py-1 bg-red-500/20 text-red-400 border border-red-500/40 rounded text-[10px] font-bold';
                badge.innerText = 'ALTA TENSION DE CAPACIDAD';
                riskText.innerText = `Con +${demandPct}% de demanda, la capacidad regular queda sobrepasada y se requeriría negociar turnos extra o maquila externa con urgencia.`;
            }

            generateAutoConclusion();
        }

        // Automatic Conclusion Generator Logic
        function generateAutoConclusion(preset = null) {
            const demandPct = parseInt(document.getElementById('demandSlider')?.value || 0);
            const concTextarea = document.getElementById('studentConclusion');
            
            let conclusion = "";

            if (preset === 'base' || (preset === null && demandPct === 0)) {
                conclusion = "Se recomienda adoptar sin modificaciones el plan óptimo del modelo Simplex ($294,915.44 USD) manteniendo horas extra en 0. Almacenar en bodega ($1.50-$2.00/u) resulta 21 veces más económico que el sobrecosto de horas extra ($12.00/hr). Asimismo, se aprovecha el pico de producción en Octubre (1,114 Batidoras) para congelar costos antes del incremento del +8% en Nov-Dic.";
            } else if (preset === 'risk' || (preset === null && demandPct > 0)) {
                const estCost = (294915.44 + (demandPct >= 10 ? 15698.82 : (demandPct/10)*15698.82)).toLocaleString('en-US', {maximumFractionDigits:2});
                conclusion = `Ante una variación de demanda del +${demandPct}% en Nov-Dic (Costo estimado: $${estCost} USD), se sugiere a Mariana Castillo aprobar el plan base y negociar preventivamente un acuerdo de capacidad o maquila flexible de contingencia para cubrir los 4 meses seguidos al 100% de ocupación de planta.`;
            } else if (preset === 'cap') {
                conclusion = "Se evidencia un cuello de botella logístico con 4 meses seguidos (Sep-Dic) al 100% de capacidad regular. Se aconseja priorizar la gestión del inventario acumulado en Octubre (764 Batidoras en bodega) y mantener estricta disciplina operativa sin incurrir en horas extra penalizadas a $12/hr.";
            }

            if (concTextarea) {
                concTextarea.value = conclusion;
            }
            
            const prevConc = document.getElementById('prevConclusion');
            if (prevConc) {
                prevConc.innerText = conclusion;
            }
        }

        function setAutoConclusionPreset(preset) {
            generateAutoConclusion(preset);
            showToast(`Conclusión cargada: Plantilla ${preset.toUpperCase()}`);
        }

        // Memo Generator Binding
        function bindExporter() {
            const nameIn = document.getElementById('studentName');
            const courseIn = document.getElementById('studentCourse');
            const concIn = document.getElementById('studentConclusion');

            function updatePreview() {
                document.getElementById('prevStudentName').innerText = nameIn.value || 'Estudiante / Analista';
                document.getElementById('prevCourse').innerText = courseIn.value || 'Investigación de Operaciones';
                document.getElementById('prevConclusion').innerText = concIn.value || '';
            }

            // Real-time dynamic bindings
            nameIn.addEventListener('input', updatePreview);
            courseIn.addEventListener('input', updatePreview);
            concIn.addEventListener('input', updatePreview);

            generateAutoConclusion();
            updatePreview();
        }

        // Quiz System Data
        const quizQuestions = [
            {
                q: '1. ¿Por qué el modelo Simplex dejó las Horas Extra en CERO en todos los meses?',
                options: [
                    'Porque la fábrica no tenía personal capacitado',
                    'Porque el sobrecosto de $12/hr (+$42 en Procesador) es mucho mayor que producir antes y guardar en bodega ($2/mes)',
                    'Porque Solver tuvo un error en la ecuación',
                    'Porque en diciembre la demanda fue cero'
                ],
                correct: 1,
                explain: '¡Correcto! Guardar en bodega solo cuesta $1.50 - $2.00/mes, mientras que usar horas extra cuesta $12/hr (21 veces más caro).'
            },
            {
                q: '2. ¿Por qué se producen 1,114 Batidoras en Octubre?',
                options: [
                    'Para congelar el costo de $55 antes del aumento del +8% en Noviembre y Diciembre',
                    'Porque el cliente lo exigió en ese mes',
                    'Fue una cifra asignada al azar',
                    'Porque en octubre las horas de trabajo valen la mitad'
                ],
                correct: 0,
                explain: '¡Excelente! Fabricar en Octubre permite evitar el recargo de insumos de Nov-Dic ($59.40) ahorrando dinero a la empresa.'
            },
            {
                q: '3. ¿Qué ocurre si la demanda aumenta un 10% en Noviembre y Diciembre?',
                options: [
                    'El costo baja a $200,000 USD',
                    'El plan es infactible y la fábrica cierra',
                    'El costo sube a $310,614.26 USD (+5.3%) y la planta opera al 100% de capacidad durante 4 meses',
                    'Se requieren 500 horas extra de inmediato'
                ],
                correct: 2,
                explain: '¡Respuesta Perfecta! Con +10% de demanda el sistema lo absorbe con inventario previo, pero deja la planta al 100% de su límite sin margen.'
            }
        ];

        let currentQuizIdx = 0;
        let score = 0;

        function renderQuiz() {
            const container = document.getElementById('quizContainer');

            if (currentQuizIdx >= quizQuestions.length) {
                let badge = 'Analista Junior de Planeación';
                if (score === 3) badge = 'Comandante Simplex ElectroAndina 🚀';
                else if (score >= 1) badge = 'Supervisor de Operaciones Starfactory 🛰️';

                container.innerHTML = `
                    <div class="text-center py-6 space-y-4 font-mono">
                        <div class="w-14 h-14 rounded-full bg-spacex-accent/20 border border-spacex-accent flex items-center justify-center mx-auto text-spacex-accent text-2xl">
                            <i class="fa-solid fa-trophy"></i>
                        </div>
                        <h3 class="font-heading text-xl font-bold text-white uppercase">¡Evaluación de Misión Completada!</h3>
                        <p class="text-gray-300 text-sm">Puntaje Final: <strong class="text-spacex-accent text-lg">${score} / ${quizQuestions.length}</strong></p>
                        <div class="inline-block px-4 py-2 rounded bg-white/10 text-white border border-white/10 text-xs">
                            Rango Acreditado: <span class="text-spacex-accent font-bold">${badge}</span>
                        </div>
                        <div class="pt-2">
                            <button onclick="restartQuiz()" class="px-5 py-2 bg-spacex-accent hover:bg-cyan-300 text-black font-heading font-bold text-xs uppercase tracking-wider rounded transition-all">
                                Volver a Intentar
                            </button>
                        </div>
                    </div>
                `;
                return;
            }

            const q = quizQuestions[currentQuizIdx];
            container.innerHTML = `
                <div class="space-y-6 font-mono">
                    <div class="flex justify-between items-center text-xs">
                        <span class="text-spacex-accent font-bold">Pregunta ${currentQuizIdx + 1} de ${quizQuestions.length}</span>
                        <span class="text-gray-400">Puntaje: ${score}</span>
                    </div>

                    <h3 class="font-heading text-sm sm:text-base font-bold text-white">${q.q}</h3>

                    <div class="space-y-2.5">
                        ${q.options.map((opt, i) => `
                            <button onclick="answerQuiz(${i})" class="w-full text-left p-3.5 rounded glass-panel hover:bg-white/10 border border-white/10 transition-all text-xs text-gray-200 hover:text-white flex items-center gap-3">
                                <span class="w-5 h-5 rounded bg-white/10 text-[11px] flex items-center justify-center text-spacex-accent font-bold">${String.fromCharCode(65 + i)}</span>${opt}
                            </button>
                        `).join('')}
                    </div>
                </div>
            `;
        }

        function answerQuiz(idx) {
            const q = quizQuestions[currentQuizIdx];
            const container = document.getElementById('quizContainer');
            const isCorrect = idx === q.correct;

            if (isCorrect) score++;

            container.innerHTML += `
                <div class="mt-4 p-4 rounded border ${isCorrect ? 'bg-emerald-950/40 border-emerald-500/40 text-emerald-200' : 'bg-red-950/40 border-red-500/40 text-red-200'} text-xs font-mono space-y-2">
                    <p class="font-bold uppercase">${isCorrect ? '¡CORRECTO!' : 'INCORRECTO'}</p>
                    <p>${q.explain}</p>
                    <button onclick="nextQuizQuestion()" class="mt-1 px-3 py-1.5 bg-white/10 hover:bg-white/20 text-white rounded font-mono text-xs">Siguiente ➔</button>
                </div>
            `;
        }

        function nextQuizQuestion() {
            currentQuizIdx++;
            renderQuiz();
        }

        function restartQuiz() {
            currentQuizIdx = 0;
            score = 0;
            renderQuiz();
        }

        // Memo Generator Binding
        function bindExporter() {
            const nameIn = document.getElementById('studentName');
            const courseIn = document.getElementById('studentCourse');
            const concIn = document.getElementById('studentConclusion');

            function update() {
                document.getElementById('prevStudentName').innerText = nameIn.value || 'Estudiante';
                document.getElementById('prevCourse').innerText = courseIn.value || 'Investigación de Operaciones';
                document.getElementById('prevConclusion').innerText = concIn.value;
            }

            document.getElementById('updateReportBtn').addEventListener('click', update);
        }

        function copyTaskReport() {
            const name = document.getElementById('prevStudentName').innerText;
            const course = document.getElementById('prevCourse').innerText;
            const conc = document.getElementById('prevConclusion').innerText;

            const text = `MEMORANDO EJECUTIVO ELECTROANDINA (Jul-Dic 2026)\nPara: Mariana Castillo, Gerente de Operaciones\nDe: ${name}\nMateria: ${course}\n\nResumen de Métricas Solver:\n- Costo Total del Plan: USD 294,915.44\n- Horas Extra Usadas: 0 horas (USD 0.00)\n- Almacenamiento: USD 4,065.44\n- Producción Pico Batidora: 1,114 unidades en Octubre\n\nRecomendación:\n${conc}`;

            const dummy = document.createElement('textarea');
            document.body.appendChild(dummy);
            dummy.value = text;
            dummy.select();
            document.execCommand('copy');
            document.body.removeChild(dummy);

            showToast('¡Texto del memorando copiado al portapapeles!');
        }

        function showToast(msg) {
            const notification = document.createElement('div');
            notification.className = 'fixed bottom-5 right-5 z-50 glass-panel border border-spacex-accent p-3.5 rounded-lg text-white text-xs font-mono shadow-2xl flex items-center gap-2';
            notification.innerHTML = `<i class="fa-solid fa-circle-check text-spacex-accent text-base"></i> ${msg}`;
            document.body.appendChild(notification);
            setTimeout(() => notification.remove(), 3000);
        }

        function scrollToSec(id) {
            const elem = document.getElementById(id);
            if(elem) elem.scrollIntoView({ behavior: 'smooth' });
        }

        // Mobile Menu Drawer
        document.getElementById('mobileMenuBtn').addEventListener('click', () => {
            const menu = document.getElementById('mobileMenu');
            menu.classList.toggle('hidden');
        });

        // Window Load Event Initializer
        window.onload = function() {
            renderTables();
            renderNativeChart();
            renderQuiz();
            bindExporter();
            updateSimulator();

            document.getElementById('demandSlider').addEventListener('input', updateSimulator);
            document.getElementById('overtimeCostSlider').addEventListener('input', updateSimulator);
        };
    </script>
</body>
</html>
