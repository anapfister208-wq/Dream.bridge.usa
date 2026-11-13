```html
<!DOCTYPE html>
<html lang="pt-BR" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dream Bridge USA | Sua Ponte para a Fluência no Inglês</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <!-- Chart.js para gráficos dinâmicos no Dashboard -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        usa: {
                            navy: '#0A192F',
                            navyLight: '#112240',
                            blue: '#1E3A8A',
                            red: '#DC2626',
                            redHover: '#B91C1C',
                            ice: '#F8FAFC',
                            slate: '#64748B'
                        }
                    }
                }
            }
        }
    </script>

    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #F8FAFC;
            color: #0F172A;
            overflow-x: hidden;
        }
        .glass-nav {
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid rgba(226, 232, 240, 0.8);
        }
        .hero-gradient {
            background: radial-gradient(circle at top right, rgba(30, 58, 138, 0.08), transparent 50%),
                        radial-gradient(circle at bottom left, rgba(220, 38, 38, 0.05), transparent 50%);
        }
        .card-hover {
            transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .card-hover:hover {
            transform: translateY(-3px);
            box-shadow: 0 12px 24px -8px rgba(10, 25, 47, 0.12);
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #F1F5F9;
        }
        ::-webkit-scrollbar-thumb {
            background: #CBD5E1;
            border-radius: 9999px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94A3B8;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between selection:bg-usa-red selection:text-white">

    <!-- ==================== NOTIFICAÇÃO TOAST CUSTOMIZADA ==================== -->
    <div id="toastContainer" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

    <!-- ==================== HEADER / NAVEGAÇÃO ==================== -->
    <header class="glass-nav sticky top-0 z-40">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <!-- Logo -->
            <div onclick="navigateTo('landing')" class="flex items-center gap-2.5 cursor-pointer group">
                <div class="w-9 h-9 rounded-xl bg-usa-navy flex items-center justify-center text-white shadow-sm group-hover:bg-usa-blue transition-colors relative overflow-hidden">
                    <i data-lucide="compass" class="w-5 h-5 text-white"></i>
                    <span class="absolute bottom-0 left-0 right-0 h-1 bg-usa-red"></span>
                </div>
                <div class="flex flex-col">
                    <span class="font-extrabold text-lg tracking-tight text-usa-navy leading-none">
                        Dream Bridge <span class="text-usa-red">USA</span>
                    </span>
                    <span class="text-[10px] font-medium text-slate-500 tracking-wider uppercase mt-0.5">English Mastery</span>
                </div>
            </div>

            <!-- Navegação Pública (Landing Page) -->
            <nav id="publicNav" class="hidden md:flex items-center gap-8 text-sm font-medium text-slate-600">
                <a href="#metodologia" class="hover:text-usa-navy transition-colors">Metodologia</a>
                <a href="#jornada" class="hover:text-usa-navy transition-colors">100 Níveis</a>
                <a href="#checkpoints" class="hover:text-usa-navy transition-colors">Checkpoints</a>
                <a href="#contato" class="hover:text-usa-navy transition-colors">Contato</a>
            </nav>

            <!-- Navegação Logada (App) -->
            <nav id="privateNav" class="hidden items-center gap-2 sm:gap-4">
                <button onclick="navigateTo('dashboard')" id="navBtnDashboard" class="px-3.5 py-2 rounded-xl text-sm font-semibold transition-all flex items-center gap-2 bg-usa-navy text-white">
                    <i data-lucide="layout-dashboard" class="w-4 h-4"></i>
                    <span class="hidden sm:inline">Painel</span>
                </button>
                <button onclick="navigateTo('curriculum')" id="navBtnCurriculum" class="px-3.5 py-2 rounded-xl text-sm font-semibold transition-all flex items-center gap-2 text-slate-600 hover:bg-slate-100">
                    <i data-lucide="map" class="w-4 h-4"></i>
                    <span class="hidden sm:inline">100 Níveis</span>
                </button>
            </nav>

            <!-- Botões de Ação Direita -->
            <div class="flex items-center gap-3">
                <div id="authButtons" class="flex items-center gap-2">
                    <button onclick="openAuthModal('login')" class="px-4 py-2 text-sm font-semibold text-usa-navy hover:bg-slate-100 rounded-xl transition-colors">
                        Entrar
                    </button>
                    <button onclick="openAuthModal('register')" class="px-4 py-2 text-sm font-semibold text-white bg-usa-red hover:bg-usa-redHover rounded-xl shadow-sm transition-all">
                        Começar Agora
                    </button>
                </div>

                <div id="userProfileMenu" class="hidden items-center gap-3">
                    <div class="hidden sm:flex flex-col items-end">
                        <span id="headerUserName" class="text-xs font-bold text-usa-navy">Aluno</span>
                        <span id="headerUserLevel" class="text-[11px] font-medium text-usa-red">Nível 1 / 100</span>
                    </div>
                    <button onclick="logout()" title="Sair da conta" class="p-2 text-slate-500 hover:text-usa-red hover:bg-red-50 rounded-xl transition-colors">
                        <i data-lucide="log-out" class="w-5 h-5"></i>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- ==================== CONTEÚDO PRINCIPAL ==================== -->
    <main class="flex-grow">

        <!-- =========================================================
             VIEW 1: LANDING PAGE (PÁGINA INICIAL)
        ========================================================== -->
        <section id="view-landing" class="block">
            <!-- Hero Section -->
            <div class="hero-gradient pt-16 pb-20 sm:pt-24 sm:pb-28 border-b border-slate-200/70">
                <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
                    <div class="inline-flex items-center gap-2 px-3.5 py-1.5 rounded-full bg-white border border-slate-200 shadow-sm mb-8">
                        <span class="w-2 h-2 rounded-full bg-usa-red animate-pulse"></span>
                        <span class="text-xs font-semibold text-usa-navy tracking-wide uppercase">Método Progressivo em 100 Etapas</span>
                    </div>

                    <h1 class="text-4xl sm:text-5xl lg:text-6xl font-extrabold text-usa-navy tracking-tight max-w-4xl mx-auto leading-[1.12]">
                        Atravesse a ponte para a <span class="text-transparent bg-clip-text bg-gradient-to-r from-usa-blue to-usa-red">fluência real</span> no inglês americano.
                    </h1>

                    <p class="mt-6 text-base sm:text-lg text-slate-600 max-w-2xl mx-auto leading-relaxed">
                        Uma jornada estruturada em <strong>100 níveis progressivos</strong> e validada por <strong>checkpoints rigorosos de 20 questões</strong>. Sem atalhos confusos — apenas evolução mensurável rumo aos Estados Unidos e ao mundo.
                    </p>

                    <div class="mt-10 flex flex-col sm:flex-row items-center justify-center gap-4">
                        <button onclick="loginDemo()" class="w-full sm:w-auto px-7 py-4 rounded-2xl bg-usa-navy hover:bg-usa-blue text-white font-bold text-sm sm:text-base shadow-lg shadow-usa-navy/20 transition-all flex items-center justify-center gap-2.5">
                            <i data-lucide="play-circle" class="w-5 h-5 text-usa-red"></i>
                            Testar Acesso Rápido (Demo)
                        </button>
                        <button onclick="openAuthModal('register')" class="w-full sm:w-auto px-7 py-4 rounded-2xl bg-white hover:bg-slate-50 text-usa-navy border border-slate-200 font-bold text-sm sm:text-base shadow-sm transition-all flex items-center justify-center gap-2">
                            Criar Minha Conta Grátis
                            <i data-lucide="arrow-right" class="w-4 h-4"></i>
                        </button>
                    </div>

                    <!-- Mini métricas de confiança -->
                    <div class="mt-16 grid grid-cols-2 sm:grid-cols-4 gap-6 max-w-3xl mx-auto pt-8 border-t border-slate-200/80">
                        <div>
                            <div class="text-2xl sm:text-3xl font-extrabold text-usa-navy">100</div>
                            <div class="text-xs font-medium text-slate-500 mt-1">Níveis Estruturados</div>
                        </div>
                        <div>
                            <div class="text-2xl sm:text-3xl font-extrabold text-usa-red">10</div>
                            <div class="text-xs font-medium text-slate-500 mt-1">Blocos de Domínio</div>
                        </div>
                        <div>
                            <div class="text-2xl sm:text-3xl font-extrabold text-usa-navy">20</div>
                            <div class="text-xs font-medium text-slate-500 mt-1">Questões por Checkpoint</div>
                        </div>
                        <div>
                            <div class="text-2xl sm:text-3xl font-extrabold text-usa-blue">100%</div>
                            <div class="text-xs font-medium text-slate-500 mt-1">Foco em Fluência Prática</div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Metodologia Section -->
            <div id="metodologia" class="py-20 bg-white">
                <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                    <div class="text-center max-w-2xl mx-auto mb-16">
                        <span class="text-xs font-bold uppercase tracking-widest text-usa-red">Como Funciona</span>
                        <h2 class="text-3xl sm:text-4xl font-extrabold text-usa-navy mt-2">A Metodologia Dream Bridge</h2>
                        <p class="text-slate-600 mt-3 text-sm sm:text-base">
                            Projetada para eliminar a sensação de estagnação, dividindo o aprendizado do idioma em degraus claros e verificáveis.
                        </p>
                    </div>

                    <div class="grid md:grid-cols-3 gap-8">
                        <!-- Pilar 1 -->
                        <div class="p-8 rounded-3xl bg-usa-ice border border-slate-200/80 card-hover">
                            <div class="w-12 h-12 rounded-2xl bg-usa-navy text-white flex items-center justify-center mb-6">
                                <i data-lucide="layers" class="w-6 h-6"></i>
                            </div>
                            <h3 class="text-xl font-bold text-usa-navy mb-3">1. Micro-evolução em 100 Níveis</h3>
                            <p class="text-slate-600 text-sm leading-relaxed">
                                Cada nível trabalha vocabulário essencial, estruturas reais do inglês americano e expressões cotidianas em lições objetivas e sem enrolação.
                            </p>
                        </div>

                        <!-- Pilar 2 -->
                        <div id="checkpoints" class="p-8 rounded-3xl bg-usa-ice border border-slate-200/80 card-hover">
                            <div class="w-12 h-12 rounded-2xl bg-usa-red text-white flex items-center justify-center mb-6">
                                <i data-lucide="shield-check" class="w-6 h-6"></i>
                            </div>
                            <h3 class="text-xl font-bold text-usa-navy mb-3">2. Checkpoints de 20 Questões</h3>
                            <p class="text-slate-600 text-sm leading-relaxed">
                                Ao final de cada bloco de 10 níveis, você enfrenta uma avaliação prática de 20 questões com feedback imediato. Atingindo 70% de acerto, o próximo módulo é desbloqueado.
                            </p>
                        </div>

                        <!-- Pilar 3 -->
                        <div class="p-8 rounded-3xl bg-usa-ice border border-slate-200/80 card-hover">
                            <div class="w-12 h-12 rounded-2xl bg-usa-blue text-white flex items-center justify-center mb-6">
                                <i data-lucide="bar-chart-3" class="w-6 h-6"></i>
                            </div>
                            <h3 class="text-xl font-bold text-usa-navy mb-3">3. Consistência e Métricas Reais</h3>
                            <p class="text-slate-600 text-sm leading-relaxed">
                                Acompanhe sua porcentagem exata de conclusão, mantenha sua sequência diária de estudos ativa e configure lembretes personalizados.
                            </p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Visão Geral dos 10 Blocos (100 Níveis) -->
            <div id="jornada" class="py-20 bg-usa-ice border-t border-slate-200/80">
                <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                    <div class="flex flex-col md:flex-row md:items-end justify-between mb-12 gap-4">
                        <div>
                            <span class="text-xs font-bold uppercase tracking-widest text-usa-blue">Currículo Completo</span>
                            <h2 class="text-3xl font-extrabold text-usa-navy mt-1">Da Base à Fluência Executiva</h2>
                        </div>
                        <button onclick="loginDemo()" class="inline-flex items-center gap-2 text-sm font-bold text-usa-red hover:text-usa-redHover">
                            Explorar mapa interativo agora <i data-lucide="arrow-up-right" class="w-4 h-4"></i>
                        </button>
                    </div>

                    <div class="grid sm:grid-cols-2 lg:grid-cols-5 gap-4">
                        <div class="bg-white p-5 rounded-2xl border border-slate-200/80">
                            <span class="text-xs font-bold text-usa-red">BLOCO 01 • Níveis 1–10</span>
                            <h4 class="font-bold text-usa-navy mt-1">First Steps USA</h4>
                            <p class="text-xs text-slate-500 mt-1.5">Saudações, apresentações, números e sobrevivência básica.</p>
                        </div>
                        <div class="bg-white p-5 rounded-2xl border border-slate-200/80">
                            <span class="text-xs font-bold text-usa-red">BLOCO 02 • Níveis 11–20</span>
                            <h4 class="font-bold text-usa-navy mt-1">Daily Routine</h4>
                            <p class="text-xs text-slate-500 mt-1.5">Hábitos, horários, família, compras e restaurantes.</p>
                        </div>
                        <div class="bg-white p-5 rounded-2xl border border-slate-200/80">
                            <span class="text-xs font-bold text-usa-blue">BLOCO 03–05 • Níveis 21–50</span>
                            <h4 class="font-bold text-usa-navy mt-1">Travel & Stories</h4>
                            <p class="text-xs text-slate-500 mt-1.5">Passado, futuro, aeroportos, hotéis e conversas reais.</p>
                        </div>
                        <div class="bg-white p-5 rounded-2xl border border-slate-200/80">
                            <span class="text-xs font-bold text-usa-blue">BLOCO 06–08 • Níveis 51–80</span>
                            <h4 class="font-bold text-usa-navy mt-1">Career & Idioms</h4>
                            <p class="text-xs text-slate-500 mt-1.5">Phrasal verbs, entrevistas de emprego e inglês corporativo.</p>
                        </div>
                        <div class="bg-white p-5 rounded-2xl border border-slate-200/80">
                            <span class="text-xs font-bold text-usa-navy">BLOCO 09–10 • Níveis 81–100</span>
                            <h4 class="font-bold text-usa-navy mt-1">Native Mastery</h4>
                            <p class="text-xs text-slate-500 mt-1.5">Debates avançados, negociações e fluência cultural.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- =========================================================
             VIEW 2: DASHBOARD DO ALUNO
        ========================================================== -->
        <section id="view-dashboard" class="hidden py-8 sm:py-10">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 space-y-8">
                
                <!-- Saudação e Ação Rápida -->
                <div class="bg-usa-navy rounded-3xl p-6 sm:p-8 text-white relative overflow-hidden shadow-lg">
                    <div class="absolute right-0 top-0 bottom-0 w-1/3 bg-gradient-to-l from-usa-blue/40 to-transparent pointer-events-none"></div>
                    <div class="relative z-10 flex flex-col md:flex-row md:items-center justify-between gap-6">
                        <div>
                            <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-white/10 text-xs font-semibold text-blue-200 mb-3">
                                <i data-lucide="award" class="w-3.5 h-3.5 text-usa-red"></i>
                                <span id="dashRankBadge">Explorador Iniciante</span>
                            </div>
                            <h1 class="text-2xl sm:text-3xl font-extrabold">
                                Bem-vindo de volta, <span id="dashUserName" class="text-blue-200">Aluno</span>!
                            </h1>
                            <p class="text-slate-300 text-sm mt-1.5 max-w-xl">
                                Você já concluiu <strong id="dashPercentText" class="text-white">0%</strong> da ponte até o Nível 100. Continue seu ritmo diário para desbloquear o próximo Checkpoint.
                            </p>
                        </div>

                        <div class="flex flex-wrap items-center gap-3">
                            <button onclick="continueNextLevel()" class="px-6 py-3.5 rounded-2xl bg-usa-red hover:bg-usa-redHover text-white font-bold text-sm shadow-md transition-all flex items-center gap-2">
                                <i data-lucide="play" class="w-4 h-4 fill-current"></i>
                                <span id="dashContinueBtnText">Continuar Nível 1</span>
                            </button>
                            <button onclick="navigateTo('curriculum')" class="px-5 py-3.5 rounded-2xl bg-white/10 hover:bg-white/20 text-white font-semibold text-sm transition-all">
                                Ver Todos os 100 Níveis
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Cards de KPIs -->
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-5">
                    <!-- Progresso Geral -->
                    <div class="bg-white p-6 rounded-3xl border border-slate-200/80 shadow-sm">
                        <div class="flex items-center justify-between">
                            <span class="text-xs font-bold uppercase tracking-wider text-slate-400">Progresso Total</span>
                            <div class="w-9 h-9 rounded-xl bg-blue-50 text-usa-blue flex items-center justify-center">
                                <i data-lucide="trending-up" class="w-5 h-5"></i>
                            </div>
                        </div>
                        <div class="mt-4 flex items-baseline gap-2">
                            <span id="kpiPercent" class="text-3xl font-extrabold text-usa-navy">0%</span>
                            <span id="kpiLevelsCount" class="text-xs font-medium text-slate-500">(0/100 níveis)</span>
                        </div>
                        <div class="w-full bg-slate-100 h-2 rounded-full mt-3 overflow-hidden">
                            <div id="kpiProgressBar" class="bg-usa-blue h-full rounded-full transition-all duration-500" style="width: 0%"></div>
                        </div>
                    </div>

                    <!-- Sequência de Estudos (Streak) -->
                    <div class="bg-white p-6 rounded-3xl border border-slate-200/80 shadow-sm">
                        <div class="flex items-center justify-between">
                            <span class="text-xs font-bold uppercase tracking-wider text-slate-400">Sequência Ativa</span>
                            <div class="w-9 h-9 rounded-xl bg-red-50 text-usa-red flex items-center justify-center">
                                <i data-lucide="flame" class="w-5 h-5"></i>
                            </div>
                        </div>
                        <div class="mt-4 flex items-baseline gap-2">
                            <span id="kpiStreak" class="text-3xl font-extrabold text-usa-navy">1</span>
                            <span class="text-xs font-medium text-slate-500">dias seguidos</span>
                        </div>
                        <p class="text-xs text-emerald-600 font-medium mt-3 flex items-center gap-1">
                            <i data-lucide="check-circle-2" class="w-3.5 h-3.5"></i> Meta diária registrada hoje
                        </p>
                    </div>

                    <!-- Checkpoints Aprovados -->
                    <div class="bg-white p-6 rounded-3xl border border-slate-200/80 shadow-sm">
                        <div class="flex items-center justify-between">
                            <span class="text-xs font-bold uppercase tracking-wider text-slate-400">Checkpoints</span>
                            <div class="w-9 h-9 rounded-xl bg-slate-100 text-usa-navy flex items-center justify-center">
                                <i data-lucide="shield-check" class="w-5 h-5"></i>
                            </div>
                        </div>
                        <div class="mt-4 flex items-baseline gap-2">
                            <span id="kpiCheckpoints" class="text-3xl font-extrabold text-usa-navy">0</span>
                            <span class="text-xs font-medium text-slate-500">/ 10 blocos validados</span>
                        </div>
                        <p class="text-xs text-slate-500 mt-3">Mínimo de 70% (14/20) para avançar</p>
                    </div>

                    <!-- Próximo Checkpoint -->
                    <div class="bg-white p-6 rounded-3xl border border-slate-200/80 shadow-sm">
                        <div class="flex items-center justify-between">
                            <span class="text-xs font-bold uppercase tracking-wider text-slate-400">Próximo Desafio</span>
                            <div class="w-9 h-9 rounded-xl bg-amber-50 text-amber-600 flex items-center justify-center">
                                <i data-lucide="flag" class="w-5 h-5"></i>
                            </div>
                        </div>
                        <div class="mt-4">
                            <span id="kpiNextCheckpoint" class="text-lg font-extrabold text-usa-navy">Checkpoint Bloco 1</span>
                        </div>
                        <p id="kpiNextCheckpointSub" class="text-xs text-slate-500 mt-2">Complete até o Nível 10 para liberar</p>
                    </div>
                </div>

                <!-- Gráficos e Lembretes de Estudo -->
                <div class="grid lg:grid-cols-3 gap-6">
                    <!-- Gráfico de Desempenho por Bloco -->
                    <div class="lg:col-span-2 bg-white p-6 sm:p-7 rounded-3xl border border-slate-200/80 shadow-sm">
                        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-2 mb-6">
                            <div>
                                <h2 class="text-lg font-bold text-usa-navy">Progresso por Módulo (100 Níveis)</h2>
                                <p class="text-xs text-slate-500">Porcentagem concluída em cada um dos 10 blocos da jornada</p>
                            </div>
                            <span class="inline-flex items-center gap-1.5 text-xs font-semibold text-usa-blue bg-blue-50 px-3 py-1 rounded-full self-start">
                                <span class="w-2 h-2 rounded-full bg-usa-blue"></span> Atualizado em tempo real
                            </span>
                        </div>
                        <div class="relative h-64 w-full">
                            <canvas id="progressChart"></canvas>
                        </div>
                    </div>

                    <!-- Lembretes de Estudo Configuráveis -->
                    <div class="bg-white p-6 sm:p-7 rounded-3xl border border-slate-200/80 shadow-sm flex flex-col justify-between">
                        <div>
                            <div class="flex items-center justify-between mb-4">
                                <div class="flex items-center gap-2.5">
                                    <div class="w-9 h-9 rounded-xl bg-red-50 text-usa-red flex items-center justify-center">
                                        <i data-lucide="bell-ring" class="w-5 h-5"></i>
                                    </div>
                                    <div>
                                        <h2 class="text-base font-bold text-usa-navy">Lembretes de Estudo</h2>
                                        <p class="text-xs text-slate-500">Mantenha sua constância</p>
                                    </div>
                                </div>
                                <label class="relative inline-flex items-center cursor-pointer">
                                    <input type="checkbox" id="reminderToggle" class="sr-only peer" checked onchange="saveReminderSettings()">
                                    <div class="w-11 h-6 bg-slate-200 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-usa-red"></div>
                                </label>
                            </div>

                            <div class="space-y-4 mt-5">
                                <div>
                                    <label class="block text-xs font-semibold text-slate-600 mb-1.5">Horário Diário</label>
                                    <input type="time" id="reminderTime" value="19:30" onchange="saveReminderSettings()" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-200 text-sm font-semibold text-usa-navy focus:outline-none focus:border-usa-blue">
                                </div>

                                <div>
                                    <label class="block text-xs font-semibold text-slate-600 mb-1.5">Dias da Semana</label>
                                    <div id="reminderDaysContainer" class="grid grid-cols-7 gap-1.5">
                                        <!-- Gerado via JS -->
                                    </div>
                                </div>

                                <div>
                                    <label class="block text-xs font-semibold text-slate-600 mb-1.5">Meta Diária</label>
                                    <select id="reminderGoal" onchange="saveReminderSettings()" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-200 text-sm font-medium text-usa-navy focus:outline-none focus:border-usa-blue">
                                        <option value="1">1 Nível por dia (Ritmo Leve)</option>
                                        <option value="2" selected>2 Níveis por dia (Recomendado)</option>
                                        <option value="5">5 Níveis por dia (Intensivo USA)</option>
                                    </select>
                                </div>
                            </div>
                        </div>

                        <button onclick="triggerTestReminder()" class="mt-6 w-full py-2.5 px-4 rounded-xl bg-slate-100 hover:bg-slate-200 text-usa-navy font-semibold text-xs transition-colors flex items-center justify-center gap-2">
                            <i data-lucide="bell" class="w-3.5 h-3.5 text-usa-red"></i>
                            Testar Notificação de Lembrete
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- =========================================================
             VIEW 3: CURRÍCULO DE 100 NÍVEIS E CHECKPOINTS
        ========================================================== -->
        <section id="view-curriculum" class="hidden py-8 sm:py-10">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 space-y-8">
                
                <!-- Cabeçalho do Currículo -->
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 bg-white p-6 rounded-3xl border border-slate-200/80 shadow-sm">
                    <div>
                        <h1 class="text-2xl sm:text-3xl font-extrabold text-usa-navy">Mapa dos 100 Níveis</h1>
                        <p class="text-sm text-slate-500 mt-1">
                            Conclua os 10 níveis de cada bloco e passe no <strong>Checkpoint de 20 questões</strong> para liberar o próximo módulo.
                        </p>
                    </div>

                    <!-- Filtro rápido de blocos -->
                    <div class="flex items-center gap-2">
                        <select id="blockFilter" onchange="renderCurriculum()" class="px-4 py-2.5 rounded-xl border border-slate-200 text-sm font-semibold text-usa-navy bg-usa-ice focus:outline-none focus:border-usa-blue">
                            <option value="all">Todos os 10 Blocos (1–100)</option>
                            <option value="1">Bloco 1 (Níveis 1–10)</option>
                            <option value="2">Bloco 2 (Níveis 11–20)</option>
                            <option value="3">Bloco 3 (Níveis 21–30)</option>
                            <option value="4">Bloco 4 (Níveis 31–40)</option>
                            <option value="5">Bloco 5 (Níveis 41–50)</option>
                            <option value="6">Bloco 6 (Níveis 51–60)</option>
                            <option value="7">Bloco 7 (Níveis 61–70)</option>
                            <option value="8">Bloco 8 (Níveis 71–80)</option>
                            <option value="9">Bloco 9 (Níveis 81–90)</option>
                            <option value="10">Bloco 10 (Níveis 91–100)</option>
                        </select>
                    </div>
                </div>

                <!-- Lista de Blocos e Níveis -->
                <div id="curriculumContainer" class="space-y-8">
                    <!-- Renderizado dinamicamente via JS -->
                </div>
            </div>
        </section>

    </main>

    <!-- ==================== MODAL: AUTENTICAÇÃO (LOGIN / CADASTRO) ==================== -->
    <div id="authModal" class="fixed inset-0 z-50 hidden items-center justify-center bg-usa-navy/60 backdrop-blur-sm p-4">
        <div class="bg-white rounded-3xl max-w-md w-full p-6 sm:p-8 shadow-2xl border border-slate-100 relative animate-[fadeIn_0.2s_ease-out]">
            <button onclick="closeAuthModal()" class="absolute top-5 right-5 p-2 rounded-xl text-slate-400 hover:text-slate-700 hover:bg-slate-100 transition-colors">
                <i data-lucide="x" class="w-5 h-5"></i>
            </button>

            <div class="flex items-center gap-2 mb-6">
                <div class="w-8 h-8 rounded-lg bg-usa-navy flex items-center justify-center text-white">
                    <i data-lucide="compass" class="w-4 h-4"></i>
                </div>
                <span class="font-extrabold text-usa-navy">Dream Bridge <span class="text-usa-red">USA</span></span>
            </div>

            <!-- Tabs Login / Cadastro -->
            <div class="grid grid-cols-2 gap-1 p-1 bg-slate-100 rounded-xl mb-6">
                <button id="tabLogin" onclick="switchAuthTab('login')" class="py-2 text-sm font-bold rounded-lg bg-white text-usa-navy shadow-sm transition-all">
                    Entrar
                </button>
                <button id="tabRegister" onclick="switchAuthTab('register')" class="py-2 text-sm font-bold rounded-lg text-slate-500 hover:text-usa-navy transition-all">
                    Criar Conta
                </button>
            </div>

            <form id="authForm" onsubmit="handleAuthSubmit(event)" class="space-y-4">
                <div id="nameFieldGroup" class="hidden">
                    <label class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-1.5">Nome Completo</label>
                    <input type="text" id="authName" placeholder="Ex: Ana Pfister" class="w-full px-4 py-3 rounded-xl border border-slate-200 text-sm focus:outline-none focus:border-usa-blue">
                </div>

                <div>
                    <label class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-1.5">E-mail</label>
                    <input type="email" id="authEmail" required placeholder="seu@email.com" class="w-full px-4 py-3 rounded-xl border border-slate-200 text-sm focus:outline-none focus:border-usa-blue">
                </div>

                <div>
                    <label class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-1.5">Senha</label>
                    <input type="password" id="authPassword" required placeholder="••••••••" class="w-full px-4 py-3 rounded-xl border border-slate-200 text-sm focus:outline-none focus:border-usa-blue">
                </div>

                <button type="submit" id="authSubmitBtn" class="w-full py-3.5 rounded-xl bg-usa-navy hover:bg-usa-blue text-white font-bold text-sm shadow-md transition-all">
                    Acessar Plataforma
                </button>
            </form>

            <div class="relative my-6">
                <div class="absolute inset-0 flex items-center"><div class="w-full border-t border-slate-200"></div></div>
                <div class="relative flex justify-center text-xs uppercase"><span class="bg-white px-3 text-slate-400 font-semibold">ou acesso instantâneo</span></div>
            </div>

            <button onclick="loginDemo()" class="w-full py-3 rounded-xl border-2 border-usa-red/20 bg-red-50/50 hover:bg-red-50 text-usa-red font-bold text-sm transition-all flex items-center justify-center gap-2">
                <i data-lucide="zap" class="w-4 h-4"></i>
                Entrar no Modo Demonstração
            </button>
        </div>
    </div>

    <!-- ==================== MODAL: ESTUDO DE NÍVEL (LIÇÃO INTERATIVA) ==================== -->
    <div id="lessonModal" class="fixed inset-0 z-50 hidden items-center justify-center bg-usa-navy/70 backdrop-blur-sm p-4">
        <div class="bg-white rounded-3xl max-w-2xl w-full p-6 sm:p-8 shadow-2xl border border-slate-100 max-h-[90vh] overflow-y-auto">
            <div class="flex items-center justify-between pb-4 border-b border-slate-100">
                <div>
                    <span id="lessonModalBadge" class="text-xs font-bold uppercase tracking-wider text-usa-red">Bloco 1 • Nível 1</span>
                    <h3 id="lessonModalTitle" class="text-xl font-extrabold text-usa-navy mt-0.5">Título do Nível</h3>
                </div>
                <button onclick="closeLessonModal()" class="p-2 rounded-xl text-slate-400 hover:text-slate-700 hover:bg-slate-100">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>
            </div>

            <div class="py-6 space-y-6">
                <!-- Conteúdo Didático -->
                <div class="bg-usa-ice p-5 rounded-2xl border border-slate-200/80">
                    <h4 class="text-xs font-bold uppercase tracking-wider text-usa-blue mb-2 flex items-center gap-1.5">
                        <i data-lucide="book-open" class="w-4 h-4"></i> Conceito & Estrutura Americana
                    </h4>
                    <p id="lessonModalConcept" class="text-sm text-slate-700 leading-relaxed"></p>
                    
                    <div class="mt-4 p-3.5 bg-white rounded-xl border border-slate-200/60">
                        <div class="text-xs font-semibold text-slate-400 mb-1">Exemplo Prático (USA):</div>
                        <p id="lessonModalExampleEn" class="text-sm font-bold text-usa-navy"></p>
                        <p id="lessonModalExamplePt" class="text-xs text-slate-500 mt-0.5"></p>
                    </div>
                </div>

                <!-- Mini Prática Rápida -->
                <div>
                    <h4 class="text-xs font-bold uppercase tracking-wider text-slate-500 mb-3">Prática de Fixação:</h4>
                    <p id="lessonModalQuestion" class="text-sm font-bold text-usa-navy mb-3"></p>
                    <div id="lessonModalOptions" class="space-y-2"></div>
                    <div id="lessonFeedback" class="hidden mt-3 p-3 rounded-xl text-xs font-semibold"></div>
                </div>
            </div>

            <div class="pt-4 border-t border-slate-100 flex items-center justify-between gap-3">
                <button onclick="closeLessonModal()" class="px-5 py-2.5 rounded-xl text-sm font-semibold text-slate-500 hover:bg-slate-100">
                    Fechar
                </button>
                <button id="completeLevelBtn" onclick="markCurrentLevelCompleted()" class="px-6 py-3 rounded-xl bg-usa-navy hover:bg-usa-blue text-white font-bold text-sm shadow-md transition-all flex items-center gap-2">
                    <i data-lucide="check-circle" class="w-4 h-4"></i>
                    Concluir Nível e Avançar
                </button>
            </div>
        </div>
    </div>

    <!-- ==================== MODAL: CHECKPOINT DE 20 QUESTÕES ==================== -->
    <div id="checkpointModal" class="fixed inset-0 z-50 hidden items-center justify-center bg-usa-navy/80 backdrop-blur-sm p-3 sm:p-4">
        <div class="bg-white rounded-3xl max-w-3xl w-full p-5 sm:p-8 shadow-2xl border border-slate-100 max-h-[92vh] flex flex-col">
            <!-- Header do Checkpoint -->
            <div class="flex items-center justify-between pb-4 border-b border-slate-100 shrink-0">
                <div>
                    <div class="flex items-center gap-2">
                        <span class="px-2.5 py-0.5 rounded-md bg-usa-red text-white text-[11px] font-bold uppercase">Checkpoint Oficial</span>
                        <span id="cpBlockLabel" class="text-xs font-bold text-slate-500">Bloco 1 (Níveis 1–10)</span>
                    </div>
                    <h3 class="text-lg sm:text-xl font-extrabold text-usa-navy mt-1">Avaliação de Validação (20 Questões)</h3>
                </div>
                <button onclick="closeCheckpointModal()" class="p-2 rounded-xl text-slate-400 hover:text-slate-700 hover:bg-slate-100">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>
            </div>

            <!-- Barra de Progresso do Quiz -->
            <div id="cpProgressHeader" class="py-3 shrink-0">
                <div class="flex items-center justify-between text-xs font-bold mb-1.5">
                    <span id="cpQuestionCounter" class="text-usa-navy">Questão 1 de 20</span>
                    <span id="cpScoreLive" class="text-usa-blue">Acertos: 0</span>
                </div>
                <div class="w-full h-2 bg-slate-100 rounded-full overflow-hidden">
                    <div id="cpProgressBar" class="h-full bg-usa-red transition-all duration-300" style="width: 5%"></div>
                </div>
            </div>

            <!-- Corpo da Questão -->
            <div id="cpQuizBody" class="py-4 overflow-y-auto flex-grow space-y-5">
                <div class="p-5 rounded-2xl bg-usa-ice border border-slate-200/80">
                    <span id="cpTopicTag" class="text-[11px] font-bold uppercase tracking-wider text-usa-blue">Grammar & Vocabulary</span>
                    <h4 id="cpQuestionText" class="text-base sm:text-lg font-bold text-usa-navy mt-1.5"></h4>
                </div>

                <div id="cpOptionsContainer" class="space-y-2.5"></div>

                <!-- Feedback Imediato da Questão -->
                <div id="cpImmediateFeedback" class="hidden p-4 rounded-2xl border text-sm"></div>
            </div>

            <!-- Tela de Resultado Final do Checkpoint -->
            <div id="cpResultBody" class="hidden py-6 overflow-y-auto flex-grow text-center space-y-5">
                <div id="cpResultIcon" class="w-16 h-16 rounded-full mx-auto flex items-center justify-center"></div>
                <div>
                    <h3 id="cpResultTitle" class="text-2xl font-extrabold text-usa-navy"></h3>
                    <p id="cpResultSubtitle" class="text-sm text-slate-600 mt-1 max-w-md mx-auto"></p>
                </div>

                <div class="grid grid-cols-3 gap-3 max-w-md mx-auto pt-2">
                    <div class="p-3.5 rounded-2xl bg-usa-ice border border-slate-200">
                        <div class="text-xs text-slate-500">Pontuação</div>
                        <div id="cpFinalScore" class="text-xl font-extrabold text-usa-navy mt-0.5">0/20</div>
                    </div>
                    <div class="p-3.5 rounded-2xl bg-usa-ice border border-slate-200">
                        <div class="text-xs text-slate-500">Aproveitamento</div>
                        <div id="cpFinalPercent" class="text-xl font-extrabold text-usa-blue mt-0.5">0%</div>
                    </div>
                    <div class="p-3.5 rounded-2xl bg-usa-ice border border-slate-200">
                        <div class="text-xs text-slate-500">Status</div>
                        <div id="cpFinalStatus" class="text-sm font-extrabold mt-1.5"></div>
                    </div>
                </div>
            </div>

            <!-- Footer do Checkpoint -->
            <div class="pt-4 border-t border-slate-100 flex items-center justify-between shrink-0">
                <span class="text-xs text-slate-400">Nota mínima para aprovação: <strong>70% (14 acertos)</strong></span>
                <div class="flex items-center gap-2">
                    <button id="cpNextBtn" onclick="nextCheckpointQuestion()" disabled class="px-6 py-2.5 rounded-xl bg-usa-navy disabled:opacity-40 hover:bg-usa-blue text-white font-bold text-sm transition-all flex items-center gap-2">
                        Próxima Questão <i data-lucide="arrow-right" class="w-4 h-4"></i>
                    </button>
                    <button id="cpFinishCloseBtn" onclick="closeCheckpointModal()" class="hidden px-6 py-2.5 rounded-xl bg-usa-red hover:bg-usa-redHover text-white font-bold text-sm transition-all">
                        Concluir e Voltar ao Mapa
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- ==================== RODAPÉ OBRIGATÓRIO ==================== -->
    <footer id="contato" class="bg-usa-navy text-white border-t border-slate-800 mt-auto">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
            <div class="flex flex-col md:flex-row items-center justify-between gap-6">
                <!-- Marca -->
                <div class="flex items-center gap-3">
                    <div class="w-9 h-9 rounded-xl bg-white/10 flex items-center justify-center text-white relative overflow-hidden">
                        <i data-lucide="compass" class="w-5 h-5"></i>
                        <span class="absolute bottom-0 left-0 right-0 h-1 bg-usa-red"></span>
                    </div>
                    <div>
                        <span class="font-extrabold text-lg tracking-tight">Dream Bridge <span class="text-usa-red">USA</span></span>
                        <p class="text-xs text-slate-400">Construindo sua fluência, um nível de cada vez.</p>
                    </div>
                </div>

                <!-- Seção de Contato Exata Solicitada -->
                <div class="px-5 py-3 rounded-2xl bg-white/5 border border-white/10 flex items-center gap-3">
                    <i data-lucide="mail" class="w-4 h-4 text-usa-red shrink-0"></i>
                    <span class="text-sm font-medium text-slate-100 select-all">Fale Conosco: anapfister208@gmail.com</span>
                </div>
            </div>

            <div class="mt-8 pt-6 border-t border-white/10 flex flex-col sm:flex-row items-center justify-between text-xs text-slate-400 gap-2">
                <p>&copy; 2026 Dream Bridge USA. Todos os direitos reservados.</p>
                <p>Currículo Progressivo • 100 Níveis &amp; 10 Checkpoints</p>
            </div>
        </div>
    </footer>

    <!-- ==================== LÓGICA JAVASCRIPT DA APLICAÇÃO ==================== -->
    <script>
        // =========================================================================
        // 1. ESTADO GLOBAL E BANCO DE DADOS EM MEMÓRIA
        // =========================================================================
        const BLOCK_TITLES = [
            { id: 1, title: "First Steps in the USA", theme: "Saudações, Verbo To Be e Sobrevivência" },
            { id: 2, title: "American Daily Life", theme: "Rotina, Present Simple e Horários" },
            { id: 3, title: "Navigating Cities & Airports", theme: "Direções, Viagens e Transporte" },
            { id: 4, title: "Food, Shopping & Dining", theme: "Restaurantes, Preços e Quantidades" },
            { id: 5, title: "Memories & Past Stories", theme: "Past Simple e Experiências Passadas" },
            { id: 6, title: "Future Plans & Ambitions", theme: "Will, Going To e Planejamento" },
            { id: 7, title: "Real Conversations & Phrasal Verbs", theme: "Expressões Cotidianas Americanas" },
            { id: 8, title: "Workplace & Business English", theme: "Reuniões, E-mails e Entrevistas" },
            { id: 9, title: "Debates, Culture & Nuances", theme: "Condicionais, Opiniões e Argumentação" },
            { id: 10, title: "Mastery & Native Fluency", theme: "Inglês Avançado, Negociações e Domínio Total" }
        ];

        // Estado do Usuário
        let appState = {
            isAuthenticated: false,
            user: {
                name: "Visitante",
                email: "",
                streak: 1
            },
            completedLevels: [], // Ex: [1, 2, 3]
            passedCheckpoints: [], // Ex: [1, 2] (IDs dos blocos aprovados)
            checkpointScores: {}, // Ex: { 1: 18, 2: 16 }
            reminders: {
                enabled: true,
                time: "19:30",
                days: ["Seg", "Ter", "Qua", "Qui", "Sex"],
                goal: "2"
            }
        };

        let activeLessonLevel = null;
        let progressChartInstance = null;

        // Estado do Checkpoint Ativo
        let currentCheckpoint = {
            blockId: 1,
            questions: [],
            currentIndex: 0,
            score: 0,
            answeredCurrent: false
        };

        // =========================================================================
        // 2. GERADOR DO CURRÍCULO DE 100 NÍVEIS E BANCO DE QUESTÕES
        // =========================================================================
        const LEVEL_TOPICS = [
            { topic: "Greetings & Introductions", concept: "Nos EUA, cumprimentos variam conforme a formalidade. 'How's it going?' é muito comum no dia a dia e geralmente pede uma resposta rápida como 'Pretty good, thanks!'.", en: "Hey! How's it going? I'm excited to start my journey.", pt: "Ei! Como vão as coisas? Estou animado para começar minha jornada.", q: "Qual é a resposta mais natural nos EUA para 'How's it going?'", opts: ["Pretty good, and you?", "I am going to the store.", "Yes, it goes."], ans: 0 },
            { topic: "Verb To Be in Action", concept: "O verbo 'to be' (am, is, are) é a base para descrever estados, profissões, nacionalidades e localizações sem precisar de verbos auxiliares.", en: "She is a software engineer in Seattle.", pt: "Ela é engenheira de software em Seattle.", q: "Complete: 'They ___ ready for the checkpoint.'", opts: ["is", "are", "am"], ans: 1 },
            { topic: "Numbers, Prices & Time", concept: "Ao falar preços em dólares nos EUA, os americanos costumam omitir a palavra 'dollars' e dizer apenas os dois grupos de números (ex: $15.50 = fifteen fifty).", en: "That coffee will be four seventy-five.", pt: "Esse café vai custar quatro dólares e setenta e cinco centavos.", q: "Como se diz '$12.30' de forma natural nos EUA?", opts: ["Twelve thirty", "Twelve and three", "Ten two thirty"], ans: 0 },
            { topic: "Asking for Directions", concept: "Para pedir informações na rua com educação, comece sempre com 'Excuse me' antes de perguntar onde fica um local.", en: "Excuse me, how do I get to the nearest subway station?", pt: "Com licença, como eu chego à estação de metrô mais próxima?", q: "Qual expressão inicia um pedido educado de informação?", opts: ["Listen to me", "Excuse me", "Tell me now"], ans: 1 },
            { topic: "Ordering at a Restaurant", concept: "Em restaurantes americanos, evite dizer 'I want'. Prefira 'I'd like...' (I would like) ou 'Can I get...' para soar natural e educado.", en: "Hi, can I get a cheeseburger with fries, please?", pt: "Oi, pode me ver um cheeseburger com fritas, por favor?", q: "Qual frase é mais educada para pedir comida nos EUA?", opts: ["Give me a water.", "I want water now.", "I'd like a glass of water, please."], ans: 2 },
            { topic: "Simple Present & Routines", concept: "Usamos o Simple Present para rotinas e fatos. Lembre-se de adicionar '-s' ou '-es' ao verbo na terceira pessoa do singular (he, she, it).", en: "He studies English every evening before bed.", pt: "Ele estuda inglês todas as noites antes de dormir.", q: "Escolha a frase gramaticalmente correta:", opts: ["She work in New York.", "She works in New York.", "She working in New York."], ans: 1 },
            { topic: "Past Simple & Storytelling", concept: "Para relatar eventos concluídos no passado, usamos verbos regulares com '-ed' ou formas irregulares (go -> went, see -> saw).", en: "Last summer, we visited Boston and walked the Freedom Trail.", pt: "No verão passado, visitamos Boston e caminhamos pela Freedom Trail.", q: "Qual é o passado simples do verbo 'go'?", opts: ["Goed", "Gone", "Went"], ans: 2 },
            { topic: "Future with Going To & Will", concept: "Use 'going to' para planos já decididos e 'will' para decisões tomadas na hora ou promessas.", en: "I'm going to pass all ten checkpoints this year!", pt: "Eu vou passar em todos os dez checkpoints este ano!", q: "Qual frase expressa um plano já definido?", opts: ["I am going to travel to Miami next month.", "I travel Miami yesterday.", "I going travel Miami."], ans: 0 },
            { topic: "Essential Phrasal Verbs", concept: "Phrasal verbs combinam um verbo com uma preposição, criando um novo significado essencial para entender nativos.", en: "Never give up on your dreams, keep moving forward.", pt: "Nunca desista dos seus sonhos, continue seguindo em frente.", q: "O que significa o phrasal verb 'give up'?", opts: ["Desistir", "Subir", "Entregar um presente"], ans: 0 },
            { topic: "Workplace & Fluency Mastery", concept: "No ambiente corporativo americano, clareza e objetividade são valorizadas. Expressões como 'touch base' (fazer contato rápido) são muito usadas.", en: "Let's touch base tomorrow morning to review the project.", pt: "Vamos nos falar rapidamente amanhã de manhã para revisar o projeto.", q: "O que significa 'touch base' no inglês corporativo?", opts: ["Cancelar uma reunião", "Fazer um contato breve / atualizar-se", "Assinar um contrato"], ans: 1 }
        ];

        function getLevelData(levelNumber) {
            const blockId = Math.ceil(levelNumber / 10);
            const block = BLOCK_TITLES[blockId - 1];
            const template = LEVEL_TOPICS[(levelNumber - 1) % LEVEL_TOPICS.length];
            return {
                number: levelNumber,
                blockId: blockId,
                blockTitle: block.title,
                title: `Nível ${levelNumber}: ${template.topic}`,
                concept: template.concept,
                exampleEn: template.en,
                examplePt: template.pt,
                question: template.q,
                options: template.opts,
                correctIndex: template.ans
            };
        }

        // Banco Base de Questões para gerar 20 questões únicas e desafiadoras por Checkpoint
        const CHECKPOINT_QUESTION_BANK = [
            { topic: "Grammar • Verb To Be", q: "Complete correctly: 'My friends and I ___ ready to travel to California.'", opts: ["is", "am", "are", "be"], ans: 2, exp: "'My friends and I' equivale a 'We', que exige 'are'." },
            { topic: "Vocabulary • Daily USA", q: "What is the American English word for 'elevador'?", opts: ["Lift", "Elevator", "Escalator", "Stairs"], ans: 1, exp: "Nos EUA usa-se 'Elevator' (enquanto 'Lift' é usado no Reino Unido)." },
            { topic: "Prepositions • Time", q: "Complete: 'Our English class starts ___ 7:30 PM.'", opts: ["in", "on", "at", "to"], ans: 2, exp: "Para horários exatos, utilizamos sempre a preposição 'at'." },
            { topic: "Communication • Dining", q: "When a waiter asks 'For here or to go?', what does 'to go' mean?", opts: ["Para comer no local", "Para viagem / levar", "Conta separada", "Sem gelo"], ans: 1, exp: "'To go' é o termo padrão nos EUA para pedidos para viagem." },
            { topic: "Grammar • Simple Present", q: "Choose the correct negative sentence:", opts: ["She don't like cold weather.", "She doesn't likes cold weather.", "She doesn't like cold weather.", "She not like cold weather."], ans: 2, exp: "Na terceira pessoa do singular negativa, usa-se 'doesn't' + verbo na forma base." },
            { topic: "Vocabulary • Airport", q: "Where do you pick up your suitcases after landing?", opts: ["Boarding Gate", "Baggage Claim", "Customs Office", "Check-in Desk"], ans: 1, exp: "'Baggage Claim' é a esteira de restituição de bagagens." },
            { topic: "Grammar • Past Simple", q: "Complete: 'Yesterday, I ___ a great movie in English without subtitles.'", opts: ["watch", "watched", "watching", "watches"], ans: 1, exp: "'Yesterday' indica passado concluído, exigindo o verbo regular 'watched'." },
            { topic: "Expressions • Everyday", q: "What does 'No worries!' mean in casual American conversation?", opts: ["Estou muito preocupado", "Sem problemas / Não se preocupe", "Não tenho certeza", "Com licença"], ans: 1, exp: "'No worries' é uma forma amigável de dizer 'de nada' ou 'sem problemas'." },
            { topic: "Grammar • Comparatives", q: "Complete: 'New York is ___ than my hometown.'", opts: ["more big", "biggest", "bigger", "biger"], ans: 2, exp: "Adjetivos curtos consoante-vogal-consoante dobram a última letra: 'bigger'." },
            { topic: "Vocabulary • Numbers", q: "How do Americans usually read the year '2026'?", opts: ["Twenty twenty-six", "Two zero two six", "Twenty hundred twenty-six", "Two thousand twenty-sixth"], ans: 0, exp: "Anos modernos são lidos em dois pares: 'Twenty twenty-six'." },
            { topic: "Grammar • Present Continuous", q: "What are you doing right now? 'I ___ for my Dream Bridge checkpoint.'", opts: ["study", "am studying", "studied", "will study"], ans: 1, exp: "Ações acontecendo no momento da fala usam Present Continuous ('am studying')." },
            { topic: "Phrasal Verbs", q: "If you don't know a word, you can 'look it up' in a dictionary. What does 'look up' mean?", opts: ["Olhar para o teto", "Pesquisar / Consultar", "Jogar fora", "Esquecer"], ans: 1, exp: "'Look up' significa pesquisar uma informação ou palavra." },
            { topic: "Prepositions • Place", q: "Complete: 'The meeting room is ___ the second floor.'", opts: ["in", "at", "on", "under"], ans: 2, exp: "Para andares de um prédio, usa-se a preposição 'on' ('on the second floor')." },
            { topic: "Grammar • Modal Verbs", q: "Which sentence expresses strong advice?", opts: ["You should practice English every day.", "You can to practice English.", "You musted practice English.", "You mights practice."], ans: 0, exp: "'Should' é o verbo modal ideal para dar conselhos e recomendações." },
            { topic: "Vocabulary • Weather", q: "In the USA, temperature is measured in:", opts: ["Celsius", "Kelvin", "Fahrenheit", "Meters"], ans: 2, exp: "Os Estados Unidos utilizam a escala Fahrenheit (°F) para temperaturas." },
            { topic: "Grammar • Countable/Uncountable", q: "Complete: 'How ___ time do we have before the flight?'", opts: ["many", "much", "few", "a few"], ans: 1, exp: "'Time' (tempo no geral) é incontável, portanto usa-se 'How much'." },
            { topic: "Business English", q: "In a professional email, what does 'ASAP' stand for?", opts: ["As Soon As Possible", "Always Send A Proposal", "After Saturday Afternoon Party", "All Systems Are Prepared"], ans: 0, exp: "'ASAP' significa 'As Soon As Possible' (o mais rápido possível)." },
            { topic: "Grammar • Present Perfect", q: "Complete: 'I ___ never ___ to the United States, but I will go soon!'", opts: ["have / been", "has / be", "am / been", "had / went"], ans: 0, exp: "Para experiências de vida até o presente, usamos Present Perfect: 'have never been'." },
            { topic: "Idioms • USA Culture", q: "If an exam was 'a piece of cake', how was it?", opts: ["Muito difícil", "Muito fácil", "Muito longo", "Cancelado"], ans: 1, exp: "'A piece of cake' é uma expressão idiomática para algo extremamente fácil." },
            { topic: "Fluency • Conditionals", q: "Complete the First Conditional: 'If you study consistently, you ___ fluency.'", opts: ["achieve", "will achieve", "achieved", "would achieved"], ans: 1, exp: "Na First Conditional (If + Present), a consequência futura usa 'will + verbo'." }
        ];

        function generateCheckpointQuestions(blockId) {
            // Gera exatamente 20 questões contextualizadas para o bloco
            return CHECKPOINT_QUESTION_BANK.map((item, idx) => ({
                id: idx + 1,
                topic: `Bloco ${blockId} • ${item.topic}`,
                question: `[Bloco ${blockId}] ${item.q}`,
                options: item.opts,
                correctIndex: item.ans,
                explanation: item.exp
            }));
        }

        // =========================================================================
        // 3. NAVEGAÇÃO E AUTENTICAÇÃO
        // =========================================================================
        function navigateTo(viewName) {
            const views = ['landing', 'dashboard', 'curriculum'];
            views.forEach(v => {
                const el = document.getElementById(`view-${v}`);
                if (el) el.classList.add('hidden');
            });

            const target = document.getElementById(`view-${viewName}`);
            if (target) target.classList.remove('hidden');

            // Atualiza botões da navbar privada
            const btnDash = document.getElementById('navBtnDashboard');
            const btnCurr = document.getElementById('navBtnCurriculum');
            if (btnDash && btnCurr) {
                if (viewName === 'dashboard') {
                    btnDash.className = "px-3.5 py-2 rounded-xl text-sm font-semibold transition-all flex items-center gap-2 bg-usa-navy text-white";
                    btnCurr.className = "px-3.5 py-2 rounded-xl text-sm font-semibold transition-all flex items-center gap-2 text-slate-600 hover:bg-slate-100";
                } else if (viewName === 'curriculum') {
                    btnCurr.className = "px-3.5 py-2 rounded-xl text-sm font-semibold transition-all flex items-center gap-2 bg-usa-navy text-white";
                    btnDash.className = "px-3.5 py-2 rounded-xl text-sm font-semibold transition-all flex items-center gap-2 text-slate-600 hover:bg-slate-100";
                }
            }

            if (viewName === 'dashboard') {
                updateDashboardUI();
            } else if (viewName === 'curriculum') {
                renderCurriculum();
            }

            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function updateAuthUI() {
            const publicNav = document.getElementById('publicNav');
            const privateNav = document.getElementById('privateNav');
            const authButtons = document.getElementById('authButtons');
            const userProfileMenu = document.getElementById('userProfileMenu');

            if (appState.isAuthenticated) {
                publicNav.classList.add('hidden');
                publicNav.classList.remove('md:flex');
                privateNav.classList.remove('hidden');
                privateNav.classList.add('flex');
                authButtons.classList.add('hidden');
                userProfileMenu.classList.remove('hidden');
                userProfileMenu.classList.add('flex');

                document.getElementById('headerUserName').textContent = appState.user.name;
                const currentLvl = Math.min(100, appState.completedLevels.length + 1);
                document.getElementById('headerUserLevel').textContent = `Nível ${currentLvl} / 100`;
            } else {
                publicNav.classList.remove('hidden');
                publicNav.classList.add('md:flex');
                privateNav.classList.add('hidden');
                privateNav.classList.remove('flex');
                authButtons.classList.remove('hidden');
                userProfileMenu.classList.add('hidden');
                userProfileMenu.classList.remove('flex');
            }
        }

        function openAuthModal(mode = 'login') {
            switchAuthTab(mode);
            const modal = document.getElementById('authModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        function closeAuthModal() {
            const modal = document.getElementById('authModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function switchAuthTab(mode) {
            const tabLogin = document.getElementById('tabLogin');
            const tabRegister = document.getElementById('tabRegister');
            const nameGroup = document.getElementById('nameFieldGroup');
            const submitBtn = document.getElementById('authSubmitBtn');
            const nameInput = document.getElementById('authName');

            if (mode === 'login') {
                tabLogin.className = "py-2 text-sm font-bold rounded-lg bg-white text-usa-navy shadow-sm transition-all";
                tabRegister.className = "py-2 text-sm font-bold rounded-lg text-slate-500 hover:text-usa-navy transition-all";
                nameGroup.classList.add('hidden');
                nameInput.required = false;
                submitBtn.textContent = "Acessar Plataforma";
            } else {
                tabRegister.className = "py-2 text-sm font-bold rounded-lg bg-white text-usa-navy shadow-sm transition-all";
                tabLogin.className = "py-2 text-sm font-bold rounded-lg text-slate-500 hover:text-usa-navy transition-all";
                nameGroup.classList.remove('hidden');
                nameInput.required = true;
                submitBtn.textContent = "Criar Conta e Começar";
            }
        }

        function handleAuthSubmit(e) {
            e.preventDefault();
            const email = document.getElementById('authEmail').value.trim();
            const nameInput = document.getElementById('authName').value.trim();
            const displayName = nameInput || email.split('@')[0];

            appState.isAuthenticated = true;
            appState.user.name = displayName.charAt(0).toUpperCase() + displayName.slice(1);
            appState.user.email = email;

            closeAuthModal();
            updateAuthUI();
            navigateTo('dashboard');
            showToast(`Bem-vindo à Dream Bridge USA, ${appState.user.name}!`, 'success');
        }

        function loginDemo() {
            appState.isAuthenticated = true;
            appState.user = {
                name: "Aluno Demo USA",
                email: "demo@dreambridgeusa.com",
                streak: 7
            };
            // Popula um progresso inicial realista (Bloco 1 concluído + Checkpoint 1 pronto para testar ou níveis 1-13)
            if (appState.completedLevels.length === 0) {
                appState.completedLevels = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
            }

            closeAuthModal();
            updateAuthUI();
            navigateTo('dashboard');
            showToast("Modo Demonstração ativado! Bloco 1 pronto para o Checkpoint.", "info");
        }

        function logout() {
            appState.isAuthenticated = false;
            updateAuthUI();
            navigateTo('landing');
            showToast("Você saiu da sua conta.", "info");
        }

        // =========================================================================
        // 4. LÓGICA DO DASHBOARD, GRÁFICOS E LEMBRETES
        // =========================================================================
        function getMaxUnlockedBlock() {
            // Bloco 1 sempre desbloqueado. Bloco N desbloqueia quando Checkpoint N-1 é aprovado.
            let maxBlock = 1;
            for (let b = 1; b < 10; b++) {
                if (appState.passedCheckpoints.includes(b)) {
                    maxBlock = b + 1;
                } else {
                    break;
                }
            }
            return maxBlock;
        }

        function updateDashboardUI() {
            const totalCompleted = appState.completedLevels.length;
            const percent = Math.round((totalCompleted / 100) * 100);
            const maxBlock = getMaxUnlockedBlock();

            document.getElementById('dashUserName').textContent = appState.user.name;
            document.getElementById('dashPercentText').textContent = `${percent}%`;
            document.getElementById('kpiPercent').textContent = `${percent}%`;
            document.getElementById('kpiLevelsCount').textContent = `(${totalCompleted}/100 níveis)`;
            document.getElementById('kpiProgressBar').style.width = `${percent}%`;
            document.getElementById('kpiStreak').textContent = appState.user.streak;
            document.getElementById('kpiCheckpoints').textContent = appState.passedCheckpoints.length;
            document.getElementById('headerUserLevel').textContent = `Nível ${Math.min(100, totalCompleted + 1)} / 100`;

            // Rank Badge
            let rank = "Explorador Iniciante (Níveis 1–20)";
            if (totalCompleted >= 80) rank = "Embaixador da Fluência (Níveis 81–100)";
            else if (totalCompleted >= 50) rank = "Comunicador Avançado (Níveis 51–80)";
            else if (totalCompleted >= 20) rank = "Viajante Confiante (Níveis 21–50)";
            document.getElementById('dashRankBadge').textContent = rank;

            // Próximo nível ou checkpoint
            const nextLevel = getNextAvailableAction();
            const btnText = document.getElementById('dashContinueBtnText');
            if (nextLevel.type === 'checkpoint') {
                btnText.textContent = `Fazer Checkpoint Bloco ${nextLevel.blockId}`;
            } else if (nextLevel.type === 'level') {
                btnText.textContent = `Continuar Nível ${nextLevel.level}`;
            } else {
                btnText.textContent = "Jornada 100% Concluída!";
            }

            // Próximo Checkpoint KPI
            const nextCpBlock = Math.min(10, appState.passedCheckpoints.length + 1);
            document.getElementById('kpiNextCheckpoint').textContent = `Checkpoint Bloco ${nextCpBlock}`;
            const blockStart = (nextCpBlock - 1) * 10 + 1;
            const blockEnd = nextCpBlock * 10;
            const completedInBlock = appState.completedLevels.filter(l => l >= blockStart && l <= blockEnd).length;
            
            if (completedInBlock >= 10 && !appState.passedCheckpoints.includes(nextCpBlock)) {
                document.getElementById('kpiNextCheckpointSub').innerHTML = `<span class="text-usa-red font-bold">Liberado! Clique para fazer agora</span>`;
            } else {
                document.getElementById('kpiNextCheckpointSub').textContent = `${completedInBlock}/10 níveis do bloco concluídos`;
            }

            renderProgressChart();
            renderReminderDays();
        }

        function getNextAvailableAction() {
            const maxBlock = getMaxUnlockedBlock();
            for (let b = 1; b <= maxBlock; b++) {
                const start = (b - 1) * 10 + 1;
                const end = b * 10;
                for (let l = start; l <= end; l++) {
                    if (!appState.completedLevels.includes(l)) {
                        return { type: 'level', level: l, blockId: b };
                    }
                }
                if (!appState.passedCheckpoints.includes(b)) {
                    return { type: 'checkpoint', blockId: b };
                }
            }
            return { type: 'done' };
        }

        function continueNextLevel() {
            const next = getNextAvailableAction();
            if (next.type === 'level') {
                openLessonModal(next.level);
            } else if (next.type === 'checkpoint') {
                openCheckpointModal(next.blockId);
            } else {
                showToast("Parabéns! Você completou todos os 100 níveis da Dream Bridge USA!", "success");
            }
        }

        function renderProgressChart() {
            const ctx = document.getElementById('progressChart');
            if (!ctx) return;

            const blockPercentages = BLOCK_TITLES.map(b => {
                const start = (b.id - 1) * 10 + 1;
                const end = b.id * 10;
                const count = appState.completedLevels.filter(l => l >= start && l <= end).length;
                return count * 10; // 0 a 100%
            });

            if (progressChartInstance) {
                progressChartInstance.destroy();
            }

            progressChartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: BLOCK_TITLES.map(b => `Bloco ${b.id}`),
                    datasets: [{
                        label: '% Concluída',
                        data: blockPercentages,
                        backgroundColor: blockPercentages.map((val, i) => 
                            appState.passedCheckpoints.includes(i + 1) ? '#0A192F' : (val > 0 ? '#DC2626' : '#E2E8F0')
                        ),
                        borderRadius: 8,
                        barThickness: 22
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false },
                        tooltip: {
                            callbacks: {
                                label: (context) => ` Progresso: ${context.raw}% (${context.raw / 10}/10 níveis)`
                            }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            max: 100,
                            ticks: {
                                callback: (val) => `${val}%`,
                                font: { family: 'Inter', size: 11 }
                            },
                            grid: { color: '#F1F5F9' }
                        },
                        x: {
                            ticks: { font: { family: 'Inter', size: 11, weight: '600' } },
                            grid: { display: false }
                        }
                    }
                }
            });
        }

        // Lembretes de Estudo
        function renderReminderDays() {
            const allDays = ["Dom", "Seg", "Ter", "Qua", "Qui", "Sex", "Sáb"];
            const container = document.getElementById('reminderDaysContainer');
            if (!container) return;

            container.innerHTML = allDays.map(day => {
                const active = appState.reminders.days.includes(day);
                return `
                    <button type="button" onclick="toggleReminderDay('${day}')" 
                        class="py-1.5 rounded-lg text-[11px] font-bold transition-all ${active ? 'bg-usa-navy text-white shadow-sm' : 'bg-slate-100 text-slate-500 hover:bg-slate-200'}">
                        ${day}
                    </button>
                `;
            }).join('');
        }

        function toggleReminderDay(day) {
            const idx = appState.reminders.days.indexOf(day);
            if (idx > -1) {
                appState.reminders.days.splice(idx, 1);
            } else {
                appState.reminders.days.push(day);
            }
            renderReminderDays();
            saveReminderSettings(false);
        }

        function saveReminderSettings(notify = true) {
            appState.reminders.enabled = document.getElementById('reminderToggle').checked;
            appState.reminders.time = document.getElementById('reminderTime').value;
            appState.reminders.goal = document.getElementById('reminderGoal').value;
            if (notify) {
                showToast(`Lembrete configurado para ${appState.reminders.time} (${appState.reminders.goal} níveis/dia).`, "success");
            }
        }

        function triggerTestReminder() {
            const time = document.getElementById('reminderTime').value;
            const goal = document.getElementById('reminderGoal').value;
            showToast(`⏰ Lembrete Dream Bridge USA (${time}): Hora de completar seus ${goal} níveis de hoje!`, "info");
        }

        // =========================================================================
        // 5. CURRÍCULO INTERATIVO (100 NÍVEIS E CHECKPOINTS)
        // =========================================================================
        function renderCurriculum() {
            const container = document.getElementById('curriculumContainer');
            const filter = document.getElementById('blockFilter').value;
            const maxUnlockedBlock = getMaxUnlockedBlock();

            const blocksToRender = filter === 'all' 
                ? BLOCK_TITLES 
                : BLOCK_TITLES.filter(b => b.id === parseInt(filter));

            container.innerHTML = blocksToRender.map(block => {
                const isBlockUnlocked = block.id <= maxUnlockedBlock;
                const isCheckpointPassed = appState.passedCheckpoints.includes(block.id);
                const startLvl = (block.id - 1) * 10 + 1;
                const endLvl = block.id * 10;

                // Contagem de níveis concluídos no bloco
                let completedCount = 0;
                for (let l = startLvl; l <= endLvl; l++) {
                    if (appState.completedLevels.includes(l)) completedCount++;
                }

                const canTakeCheckpoint = isBlockUnlocked && completedCount === 10;
                const cpScore = appState.checkpointScores[block.id];

                // Gera os 10 cards de níveis do bloco
                let levelsHTML = '';
                for (let l = startLvl; l <= endLvl; l++) {
                    const isCompleted = appState.completedLevels.includes(l);
                    // Nível está acessível se o bloco estiver desbloqueado e (for o primeiro do bloco ou o anterior estiver concluído)
                    const isLevelPlayable = isBlockUnlocked && (l === startLvl || appState.completedLevels.includes(l - 1) || isCompleted);

                    let cardStyle = "bg-slate-50 border-slate-200/70 opacity-60 cursor-not-allowed";
                    let badgeHTML = `<i data-lucide="lock" class="w-3.5 h-3.5 text-slate-400"></i>`;

                    if (isCompleted) {
                        cardStyle = "bg-emerald-50/60 border-emerald-200 hover:border-emerald-400 cursor-pointer card-hover";
                        badgeHTML = `<i data-lucide="check-circle-2" class="w-4 h-4 text-emerald-600"></i>`;
                    } else if (isLevelPlayable) {
                        cardStyle = "bg-white border-usa-blue/40 ring-2 ring-usa-blue/10 hover:border-usa-red cursor-pointer card-hover";
                        badgeHTML = `<span class="w-2 h-2 rounded-full bg-usa-red animate-ping"></span>`;
                    }

                    const lvlData = getLevelData(l);
                    const clickAttr = isLevelPlayable ? `onclick="openLessonModal(${l})"` : `onclick="showToast('Conclua os níveis e checkpoints anteriores para desbloquear o Nível ${l}.', 'info')"`;

                    levelsHTML += `
                        <div ${clickAttr} class="p-4 rounded-2xl border transition-all flex flex-col justify-between ${cardStyle}">
                            <div class="flex items-center justify-between mb-2">
                                <span class="text-xs font-extrabold ${isCompleted ? 'text-emerald-700' : (isLevelPlayable ? 'text-usa-blue' : 'text-slate-400')}">
                                    NÍVEL ${l}
                                </span>
                                ${badgeHTML}
                            </div>
                            <div class="text-xs font-semibold text-usa-navy line-clamp-2 leading-snug">
                                ${lvlData.title.replace(`Nível ${l}: `, '')}
                            </div>
                        </div>
                    `;
                }

                return `
                    <div class="bg-white rounded-3xl border ${isBlockUnlocked ? 'border-slate-200/90 shadow-sm' : 'border-slate-200/60 bg-slate-50/50'} p-6 sm:p-8">
                        <!-- Cabeçalho do Bloco -->
                        <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-4 pb-6 border-b border-slate-100">
                            <div>
                                <div class="flex flex-wrap items-center gap-2.5">
                                    <span class="px-3 py-1 rounded-lg text-xs font-extrabold uppercase tracking-wider ${isCheckpointPassed ? 'bg-emerald-100 text-emerald-800' : (isBlockUnlocked ? 'bg-usa-navy text-white' : 'bg-slate-200 text-slate-600')}">
                                        Bloco ${block.id} • Níveis ${startLvl}–${endLvl}
                                    </span>
                                    ${isCheckpointPassed ? `<span class="text-xs font-bold text-emerald-600 flex items-center gap-1"><i data-lucide="award" class="w-4 h-4"></i> Checkpoint Aprovado (${cpScore}/20)</span>` : ''}
                                    ${!isBlockUnlocked ? `<span class="text-xs font-semibold text-slate-400 flex items-center gap-1"><i data-lucide="lock" class="w-3.5 h-3.5"></i> Bloqueado (Passe no Checkpoint ${block.id - 1})</span>` : ''}
                                </div>
                                <h2 class="text-xl font-extrabold text-usa-navy mt-2">${block.title}</h2>
                                <p class="text-xs sm:text-sm text-slate-500 mt-0.5">${block.theme}</p>
                            </div>

                            <!-- Botão do Checkpoint do Bloco -->
                            <div class="flex items-center gap-3 shrink-0">
                                <div class="text-right hidden sm:block">
                                    <div class="text-xs font-bold text-usa-navy">${completedCount}/10 Níveis</div>
                                    <div class="text-[11px] text-slate-400">Progresso do Bloco</div>
                                </div>
                                <button onclick="${canTakeCheckpoint ? `openCheckpointModal(${block.id})` : `showToast('Complete todos os 10 níveis deste bloco para liberar o Checkpoint de 20 questões!', 'info')`}"
                                    class="px-5 py-3 rounded-2xl font-bold text-xs sm:text-sm transition-all flex items-center gap-2 ${
                                        isCheckpointPassed 
                                            ? 'bg-emerald-600 hover:bg-emerald-700 text-white shadow-sm' 
                                            : (canTakeCheckpoint 
                                                ? 'bg-usa-red hover:bg-usa-redHover text-white shadow-md shadow-usa-red/20 animate-pulse' 
                                                : 'bg-slate-100 text-slate-400 cursor-not-allowed')
                                    }">
                                    <i data-lucide="shield-check" class="w-4 h-4"></i>
                                    ${isCheckpointPassed ? 'Refazer Checkpoint (20Q)' : 'Checkpoint (20 Questões)'}
                                </button>
                            </div>
                        </div>

                        <!-- Grid dos 10 Níveis -->
                        <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-5 gap-3.5 mt-6">
                            ${levelsHTML}
                        </div>
                    </div>
                `;
            }).join('');

            lucide.createIcons();
        }

        // =========================================================================
        // 6. MODAL DE ESTUDO DO NÍVEL
        // =========================================================================
        function openLessonModal(levelNumber) {
            activeLessonLevel = levelNumber;
            const data = getLevelData(levelNumber);

            document.getElementById('lessonModalBadge').textContent = `Bloco ${data.blockId} • ${data.blockTitle}`;
            document.getElementById('lessonModalTitle').textContent = data.title;
            document.getElementById('lessonModalConcept').textContent = data.concept;
            document.getElementById('lessonModalExampleEn').textContent = `"${data.exampleEn}"`;
            document.getElementById('lessonModalExamplePt').textContent = data.examplePt;
            document.getElementById('lessonModalQuestion').textContent = data.question;

            const feedbackEl = document.getElementById('lessonFeedback');
            feedbackEl.classList.add('hidden');

            const optsContainer = document.getElementById('lessonModalOptions');
            optsContainer.innerHTML = data.options.map((opt, idx) => `
                <button onclick="checkLessonPractice(${idx}, ${data.correctIndex})" 
                    class="w-full text-left px-4 py-3 rounded-xl border border-slate-200 hover:border-usa-blue hover:bg-blue-50/50 text-sm font-medium text-usa-navy transition-all">
                    ${opt}
                </button>
            `).join('');

            const isAlreadyCompleted = appState.completedLevels.includes(levelNumber);
            const completeBtn = document.getElementById('completeLevelBtn');
            completeBtn.innerHTML = isAlreadyCompleted 
                ? `<i data-lucide="check-circle" class="w-4 h-4"></i> Nível Já Concluído (Avançar)`
                : `<i data-lucide="check-circle" class="w-4 h-4"></i> Concluir Nível ${levelNumber}`;

            const modal = document.getElementById('lessonModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            lucide.createIcons();
        }

        function checkLessonPractice(selectedIdx, correctIdx) {
            const feedbackEl = document.getElementById('lessonFeedback');
            feedbackEl.classList.remove('hidden');
            if (selectedIdx === correctIdx) {
                feedbackEl.className = "mt-3 p-3 rounded-xl text-xs font-semibold bg-emerald-50 text-emerald-800 border border-emerald-200";
                feedbackEl.textContent = "✓ Excelente! Resposta correta. Você já pode concluir este nível.";
            } else {
                feedbackEl.className = "mt-3 p-3 rounded-xl text-xs font-semibold bg-red-50 text-red-800 border border-red-200";
                feedbackEl.textContent = "✕ Quase lá! Revise o exemplo acima e tente novamente.";
            }
        }

        function markCurrentLevelCompleted() {
            if (!activeLessonLevel) return;

            if (!appState.completedLevels.includes(activeLessonLevel)) {
                appState.completedLevels.push(activeLessonLevel);
                appState.completedLevels.sort((a, b) => a - b);
                showToast(`Nível ${activeLessonLevel} concluído com sucesso!`, "success");
            }

            const completedLvl = activeLessonLevel;
            closeLessonModal();
            updateAuthUI();
            updateDashboardUI();
            renderCurriculum();

            // Se acabou de completar o 10º nível de um bloco, sugere o Checkpoint imediatamente
            if (completedLvl % 10 === 0) {
                const blockId = completedLvl / 10;
                if (!appState.passedCheckpoints.includes(blockId)) {
                    setTimeout(() => {
                        showToast(`Bloco ${blockId} completo! O Checkpoint de 20 questões foi desbloqueado.`, "info");
                    }, 400);
                }
            }
        }

        function closeLessonModal() {
            const modal = document.getElementById('lessonModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
            activeLessonLevel = null;
        }

        // =========================================================================
        // 7. CHECKPOINT DE 20 QUESTÕES (AVALIAÇÃO E DESBLOQUEIO)
        // =========================================================================
        function openCheckpointModal(blockId) {
            currentCheckpoint = {
                blockId: blockId,
                questions: generateCheckpointQuestions(blockId),
                currentIndex: 0,
                score: 0,
                answeredCurrent: false
            };

            const startLvl = (blockId - 1) * 10 + 1;
            const endLvl = blockId * 10;
            document.getElementById('cpBlockLabel').textContent = `Bloco ${blockId} (Níveis ${startLvl}–${endLvl})`;

            // Reseta visibilidade das áreas do modal
            document.getElementById('cpProgressHeader').classList.remove('hidden');
            document.getElementById('cpQuizBody').classList.remove('hidden');
            document.getElementById('cpResultBody').classList.add('hidden');
            document.getElementById('cpNextBtn').classList.remove('hidden');
            document.getElementById('cpFinishCloseBtn').classList.add('hidden');

            renderCheckpointQuestion();

            const modal = document.getElementById('checkpointModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            lucide.createIcons();
        }

        function renderCheckpointQuestion() {
            const qObj = currentCheckpoint.questions[currentCheckpoint.currentIndex];
            const qNum = currentCheckpoint.currentIndex + 1;
            currentCheckpoint.answeredCurrent = false;

            document.getElementById('cpQuestionCounter').textContent = `Questão ${qNum} de 20`;
            document.getElementById('cpScoreLive').textContent = `Acertos: ${currentCheckpoint.score}`;
            document.getElementById('cpProgressBar').style.width = `${(qNum / 20) * 100}%`;

            document.getElementById('cpTopicTag').textContent = qObj.topic;
            document.getElementById('cpQuestionText').textContent = qObj.question;

            const feedbackEl = document.getElementById('cpImmediateFeedback');
            feedbackEl.classList.add('hidden');

            const nextBtn = document.getElementById('cpNextBtn');
            nextBtn.disabled = true;
            nextBtn.innerHTML = qNum === 20 
                ? `Finalizar Avaliação <i data-lucide="award" class="w-4 h-4"></i>` 
                : `Próxima Questão <i data-lucide="arrow-right" class="w-4 h-4"></i>`;

            const optsContainer = document.getElementById('cpOptionsContainer');
            const letters = ['A', 'B', 'C', 'D'];
            optsContainer.innerHTML = qObj.options.map((opt, idx) => `
                <button id="cpOptBtn-${idx}" onclick="selectCheckpointOption(${idx})"
                    class="w-full text-left p-4 rounded-2xl border-2 border-slate-200 hover:border-usa-blue hover:bg-blue-50/40 transition-all flex items-center gap-3.5 group">
                    <span class="w-8 h-8 rounded-xl bg-slate-100 group-hover:bg-usa-navy group-hover:text-white text-usa-navy font-bold text-xs flex items-center justify-center shrink-0 transition-colors">
                        ${letters[idx]}
                    </span>
                    <span class="text-sm font-semibold text-usa-navy">${opt}</span>
                </button>
            `).join('');

            lucide.createIcons();
        }

        function selectCheckpointOption(selectedIndex) {
            if (currentCheckpoint.answeredCurrent) return;
            currentCheckpoint.answeredCurrent = true;

            const qObj = currentCheckpoint.questions[currentCheckpoint.currentIndex];
            const isCorrect = selectedIndex === qObj.correctIndex;

            if (isCorrect) {
                currentCheckpoint.score++;
                document.getElementById('cpScoreLive').textContent = `Acertos: ${currentCheckpoint.score}`;
            }

            // Estiliza opções após resposta
            qObj.options.forEach((_, idx) => {
                const btn = document.getElementById(`cpOptBtn-${idx}`);
                btn.disabled = true;
                if (idx === qObj.correctIndex) {
                    btn.className = "w-full text-left p-4 rounded-2xl border-2 border-emerald-500 bg-emerald-50 text-emerald-950 flex items-center gap-3.5";
                } else if (idx === selectedIndex && !isCorrect) {
                    btn.className = "w-full text-left p-4 rounded-2xl border-2 border-red-500 bg-red-50 text-red-950 flex items-center gap-3.5";
                } else {
                    btn.className = "w-full text-left p-4 rounded-2xl border-2 border-slate-100 opacity-50 flex items-center gap-3.5";
                }
            });

            // Feedback imediato
            const feedbackEl = document.getElementById('cpImmediateFeedback');
            feedbackEl.classList.remove('hidden');
            if (isCorrect) {
                feedbackEl.className = "p-4 rounded-2xl border border-emerald-200 bg-emerald-50/80 text-emerald-900 text-xs sm:text-sm";
                feedbackEl.innerHTML = `<strong>✓ Resposta Correta!</strong> ${qObj.explanation}`;
            } else {
                feedbackEl.className = "p-4 rounded-2xl border border-red-200 bg-red-50/80 text-red-900 text-xs sm:text-sm";
                feedbackEl.innerHTML = `<strong>✕ Resposta Incorreta.</strong> ${qObj.explanation}`;
            }

            document.getElementById('cpNextBtn').disabled = false;
        }

        function nextCheckpointQuestion() {
            if (currentCheckpoint.currentIndex < 19) {
                currentCheckpoint.currentIndex++;
                renderCheckpointQuestion();
            } else {
                showCheckpointResult();
            }
        }

        function showCheckpointResult() {
            document.getElementById('cpProgressHeader').classList.add('hidden');
            document.getElementById('cpQuizBody').classList.add('hidden');
            document.getElementById('cpResultBody').classList.remove('hidden');
            document.getElementById('cpNextBtn').classList.add('hidden');
            document.getElementById('cpFinishCloseBtn').classList.remove('hidden');

            const score = currentCheckpoint.score;
            const percent = Math.round((score / 20) * 100);
            const passed = score >= 14; // 70% de 20 questões
            const blockId = currentCheckpoint.blockId;

            document.getElementById('cpFinalScore').textContent = `${score}/20`;
            document.getElementById('cpFinalPercent').textContent = `${percent}%`;

            const iconEl = document.getElementById('cpResultIcon');
            const titleEl = document.getElementById('cpResultTitle');
            const subEl = document.getElementById('cpResultSubtitle');
            const statusEl = document.getElementById('cpFinalStatus');

            if (passed) {
                iconEl.className = "w-16 h-16 rounded-full mx-auto flex items-center justify-center bg-emerald-100 text-emerald-600";
                iconEl.innerHTML = `<i data-lucide="trophy" class="w-8 h-8"></i>`;
                titleEl.textContent = "Checkpoint Aprovado!";
                subEl.textContent = blockId < 10 
                    ? `Parabéns! Você atingiu ${percent}% e desbloqueou o Bloco ${blockId + 1} (Níveis ${blockId * 10 + 1} a ${(blockId + 1) * 10}).`
                    : "Incrível! Você concluiu e validou o último bloco dos 100 níveis da Dream Bridge USA!";
                statusEl.className = "text-sm font-extrabold mt-1.5 text-emerald-600";
                statusEl.textContent = "APROVADO";

                if (!appState.passedCheckpoints.includes(blockId)) {
                    appState.passedCheckpoints.push(blockId);
                }
                const prevBest = appState.checkpointScores[blockId] || 0;
                appState.checkpointScores[blockId] = Math.max(prevBest, score);
            } else {
                iconEl.className = "w-16 h-16 rounded-full mx-auto flex items-center justify-center bg-red-100 text-usa-red";
                iconEl.innerHTML = `<i data-lucide="rotate-ccw" class="w-8 h-8"></i>`;
                titleEl.textContent = "Ainda não foi desta vez";
                subEl.textContent = `Você acertou ${score} de 20 questões (${percent}%). Revise os níveis do Bloco ${blockId} e tente novamente para atingir pelo menos 14 acertos (70%).`;
                statusEl.className = "text-sm font-extrabold mt-1.5 text-usa-red";
                statusEl.textContent = "REVISAR";
            }

            updateDashboardUI();
            renderCurriculum();
            lucide.createIcons();
        }

        function closeCheckpointModal() {
            const modal = document.getElementById('checkpointModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        // =========================================================================
        // 8. UTILITÁRIO DE NOTIFICAÇÃO TOAST
        // =========================================================================
        function showToast(message, type = 'info') {
            const container = document.getElementById('toastContainer');
            const toast = document.createElement('div');

            const colors = {
                success: 'bg-usa-navy text-white border-l-4 border-emerald-400',
                info: 'bg-usa-navy text-white border-l-4 border-usa-red',
                error: 'bg-usa-red text-white border-l-4 border-white'
            };

            toast.className = `pointer-events-auto max-w-sm px-4 py-3.5 rounded-2xl shadow-xl text-xs sm:text-sm font-medium flex items-center gap-3 transition-all duration-300 transform translate-y-2 opacity-0 ${colors[type] || colors.info}`;
            toast.innerHTML = `
                <i data-lucide="${type === 'success' ? 'check-circle' : 'info'}" class="w-4 h-4 shrink-0"></i>
                <span>${message}</span>
            `;

            container.appendChild(toast);
            lucide.createIcons();

            requestAnimationFrame(() => {
                toast.classList.remove('translate-y-2', 'opacity-0');
            });

            setTimeout(() => {
                toast.classList.add('opacity-0', 'translate-y-2');
                setTimeout(() => toast.remove(), 300);
            }, 3800);
        }

        // Inicialização ao carregar a página
        window.addEventListener('DOMContentLoaded', () => {
            lucide.createIcons();
            updateAuthUI();
        });
    </script>
</body>
</html>
```