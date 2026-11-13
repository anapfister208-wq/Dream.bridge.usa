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
                   