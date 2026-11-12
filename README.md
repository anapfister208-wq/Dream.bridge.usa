# Dream.Bridge.U.S.A
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dream Bridge USA | Plataforma de Inglês</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&family=Playfair+Display:ital,wght@0,700;1,400&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Montserrat', sans-serif; }
        body { background-color: #f1f5f9; color: #0f172a; line-height: 1.6; padding-bottom: 60px; }
        
        header { background: #0b1329; color: white; padding: 15px 5%; display: flex; justify-content: space-between; align-items: center; border-bottom: 3px solid #f59e0b; position: sticky; top: 0; z-index: 100; }
        .header-left { display: flex; align-items: center; gap: 15px; }
        
        .menu-toggle { background: #1e293b; border: 2px solid #f59e0b; border-radius: 6px; cursor: pointer; display: flex; flex-direction: column; gap: 4px; padding: 8px; }
        .menu-toggle span { display: block; width: 22px; height: 3px; background-color: #f59e0b; border-radius: 2px; }
        
        .logo { font-size: 1.4rem; font-weight: 700; color: #ffffff; }
        .logo span { color: #f59e0b; }
        
        .btn-acao { background-color: #f59e0b; color: #0b1329; padding: 14px 28px; font-weight: 700; font-size: 1rem; border-radius: 8px; border: none; cursor: pointer; text-align: center; display: inline-block; width: 100%; box-shadow: 0 4px 10px rgba(245, 158, 11, 0.3); margin-top: 15px; }
        .btn-acao:hover { background-color: #d97706; }
        
        .btn-secundario { background-color: #ffffff; color: #0b1329; border: 2px solid #0b1329; padding: 12px 20px; font-weight: 700; font-size: 0.9rem; border-radius: 8px; cursor: pointer; text-align: center; display: inline-block; width: 100%; margin-top: 10px; }
        .btn-secundario:hover { background-color: #f8fafc; }

        /* MENU LATERAL */
        .sidebar { position: fixed; top: 0; left: -300px; width: 300px; height: 100%; background: #0b1329; color: white; z-index: 3000; transition: left 0.3s ease; box-shadow: 5px 0 15px rgba(0,0,0,0.3); display: flex; flex-direction: column; }
        .sidebar.open { left: 0; }
        .sidebar-header { padding: 20px; background: #070c1b; display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #f59e0b; }
        .sidebar-close { background: none; border: none; color: white; font-size: 1.8rem; cursor: pointer; }
        .sidebar-menu { list-style: none; padding: 20px 0; flex-grow: 1; }
        .sidebar-menu li { padding: 15px 25px; border-bottom: 1px solid rgba(255,255,255,0.05); cursor: pointer; font-weight: 600; font-size: 1rem; }
        .sidebar-menu li:hover { background: #1e293b; color: #f59e0b; }
        .sidebar-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 2500; display: none; }
        .sidebar-overlay.open { display: block; }

        /* PAINÉIS DE TELA */
        .painel { display: none; background: white; padding: 25px; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.08); margin: 20px auto; max-width: 850px; }
        .painel.ativo { display: block; }
        
        .hero { background: #0b1329; color: white; text-align: center; padding: 40px 20px; border-bottom: 4px solid #f59e0b; border-radius: 8px; margin-bottom: 20px; }
        .hero h1 { font-size: 2rem; margin-bottom: 10px; }
        .hero p { font-size: 1rem; color: #f59e0b; font-weight: 600; max-width: 650px; margin: 0 auto; }

        .container { max-width: 850px; margin: 20px auto; padding: 0 15px; }
        
        .login-box input, .login-box select { width: 100%; padding: 12px; margin: 8px 0 16px 0; border: 1px solid #cbd5e1; border-radius: 6px; font-size: 1rem; }
        .login-box label { font-weight: 600; font-size: 0.9rem; color: #0b1329; }

        .blocks-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(90px, 1fr)); gap: 10px; margin-bottom: 20px; }
        .block-btn { background: white; border: 2px solid #cbd5e1; border-radius: 8px; padding: 12px 8px; text-align: center; font-weight: 700; color: #0b1329; cursor: pointer; }
        .block-btn.unlocked { border-color: #10b981; background: #ecfdf5; }
        .block-btn.locked { background: #e2e8f0; color: #94a3b8; cursor: not-allowed; }

        .quiz-option { display: block; width: 100%; text-align: left; padding: 12px; margin: 8px 0; background: #f8fafc; color: #0b1329; border: 1px solid #cbd5e1; border-radius: 6px; cursor: pointer; font-size: 1rem; }
        .quiz-option:hover { background: #e2e8f0; }

        .explanation-box { background: #fef3c7; border-left: 4px solid #f59e0b; padding: 15px; border-radius: 6px; margin-bottom: 15px; font-size: 0.95rem; color: #92400e; }

        .progress-bar-container { background: #e2e8f0; border-radius: 8px; height: 12px; width: 100%; overflow: hidden; margin: 5px 0 15px 0; }
        .progress-bar-fill { background: #10b981; height: 100%; width: 0%; transition: width 0.3s; }

        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); display: none; justify-content: center; align-items: center; z-index: 4000; padding: 15px; }
        .modal-card { background: white; padding: 25px; border-radius: 12px; max-width: 700px; width: 100%; text-align: center; box-shadow: 0 10px 25px rgba(0,0,0,0.3); max-height: 95vh; overflow-y: auto; }
        
        .certificado-diploma { border: 8px double #0b1329; padding: 35px; background: #fffdf9; text-align: center; margin-bottom: 20px; }
        .certificado-diploma h3 { font-family: 'Playfair Display', serif; color: #0b1329; font-size: 1.8rem; letter-spacing: 2px; margin-bottom: 10px; }
        .certificado-diploma h4 { font-family: 'Playfair Display', serif; color: #f59e0b; font-size: 2rem; margin: 15px 0; border-bottom: 2px solid #e2e8f0; display: inline-block; padding-bottom: 5px; }

        footer { background: #0b1329; color: white; text-align: center; padding: 25px 20px; margin-top: 50px; }
        footer a { color: #f59e0b; text-decoration: none; font-weight: 600; }
    </style>
</head>
<body>

    <header>
        <div class="header-left">
            <button type="button" class="menu-toggle" onclick="toggleSidebar()">
                <span></span>
                <span></span>
                <span></span>
            </button>
            <div class="logo">Dream Bridge <span>USA</span></div>
        </div>
        <span id="user-greeting" style="font-size: 0.9rem; color: #f59e0b; font-weight: 600;">Visitante</span>
    </header>

    <!-- MENU LATERAL (3 RISCOS) -->
    <div class="sidebar-overlay" id="sidebar-overlay" onclick="toggleSidebar()"></div>
    <div class="sidebar" id="sidebar">
        <div class="sidebar-header">
            <h3 style="font-size: 1.1rem; color: #f59e0b;">Menu da Plataforma</h3>
            <button type="button" class="sidebar-close" onclick="toggleSidebar()">×</button>
        </div>
        <ul class="sidebar-menu">
            <li onclick="mudarPainel('painel-aula')">📚 Sala de Aula (Blocos)</li>
            <li onclick="mudarPainel('painel-perfil')">👤 Meu Perfil e Gráficos</li>
            <li onclick="abrirModalCompartilhar()">💡 Indicar Curso para Amigos</li>
            <li onclick="sairDaPlataforma()" style="color: #ef4444;">🚪 Sair / Limpar Conta</li>
        </ul>
    </div>

    <div class="container">

        <!-- TELA 1: INICIAL COM BOAS-VINDAS E EXPLICAÇÃO -->
        <div id="painel-home" class="painel ativo">
            <div class="hero">
                <h1>Dream Bridge USA 🇺🇸</h1>
                <p>Seja muito bem-vindo(a)! Conectando brasileiros e transformando vidas através da educação internacional.</p>
            </div>
            
            <div style="text-align: left;">
                <h2 style="color: #0b1329; font-size: 1.4rem; margin-bottom: 12px;">Sobre o Nosso Objetivo</h2>
                <p style="color: #475569; margin-bottom: 20px;">
                    A <strong>Dream Bridge USA</strong> foi desenvolvida para eliminar barreiras idiomáticas. Aqui você aprende inglês com base exata nos currículos oficiais ensinados nas escolas públicas e universidades americanas (High School e College Core Curriculums), abrangendo História, Gramática, Verbos, Literatura, Oratória e muito mais.
                </p>

                <h2 style="color: #0b1329; font-size: 1.4rem; margin-bottom: 12px;">Como Funciona a Plataforma</h2>
                <p style="color: #475569; margin-bottom: 20px;">
                    O curso é dividido em <strong>9 blocos progressivos</strong>. Cada bloco possui <strong>20 perguntas baseadas em provas escolares dos EUA</strong>. Antes de cada pergunta, você terá uma explicação detalhada da matéria. Para desbloquear o próximo bloco e avançar na sua jornada rumo ao certificado oficial, é necessário acertar todas as 20 questões da etapa atual!
                </p>

                <button type="button" class="btn-acao" onclick="mudarPainel('painel-login')">🚀 Iniciar o Curso</button>
                <button type="button" class="btn-secundario" onclick="abrirModalCompartilhar()">💡 Indicar Curso para Amigos</button>
            </div>
        </div>

        <!-- TELA 2: LOGIN (APELIDO, EMAIL E NÍVEL) -->
        <div id="painel-login" class="painel">
            <div class="login-box">
                <h2 style="color: #0b1329; margin-bottom: 15px; text-align: center;">Identificação do Aluno</h2>
                <p style="color: #64748b; font-size: 0.9rem; text-align: center; margin-bottom: 20px;">Configure o seu perfil para salvar o seu progresso nas aulas.</p>
                <div>
                    <label>Seu Nome Completo</label>
                    <input type="text" id="aluno-nome" placeholder="Digite seu nome completo">
                    
                    <label>Apelido (Como quer ser chamado no site)</label>
                    <input type="text" id="aluno-apelido" placeholder="Ex: Mari, João...">
                    
                    <label>E-mail do Usuário</label>
                    <input type="email" id="aluno-email" placeholder="seu@email.com">
                    
                    <label>Escolha o seu Nível de Inglês</label>
                    <select id="aluno-nivel">
                        <option value="basico">Nível 1: Básico</option>
                        <option value="intermediario">Nível 2: Intermediário</option>
                        <option value="avancado">Nível 3: Avançado / Médio</option>
                    </select>

                    <button type="button" class="btn-acao" onclick="iniciarCursoDoAluno()">Acessar Aulas e Conteúdos</button>
                    <button type="button" class="btn-secundario" onclick="mudarPainel('painel-home')">Voltar</button>
                </div>
            </div>
        </div>

        <!-- TELA 3: SALA DE AULA / BLOCOS -->
        <div id="painel-aula" class="painel">
            <div style="background: #f8fafc; padding: 15px; border-radius: 8px; margin-bottom: 20px; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 10px; border: 1px solid #e2e8f0;">
                <div>
                    <h3 id="display-nivel-titulo" style="color: #0b1329;">Nível Básico</h3>
                    <p style="font-size: 0.85rem; color: #64748b;">Trilha de 9 Blocos do Ensino Americano</p>
                </div>
                <button type="button" class="btn-secundario" style="margin: 0; width: auto; padding: 8px 15px;" onclick="mudarPainel('painel-perfil')">👤 Meu Perfil / Gráficos</button>
            </div>

            <h4 style="margin-bottom: 15px; color: #0b1329;">Selecione um Bloco Liberado (Necessário 20 acertos para avançar):</h4>
            <div class="blocks-grid" id="grid-blocos"></div>

            <!-- QUIZ / AULAS -->
            <div class="quiz-container" id="quiz-container" style="display: none; margin-top: 20px; background: #f8fafc; padding: 20px; border-radius: 8px; border: 1px solid #e2e8f0;">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px;">
                    <h3 id="quiz-titulo" style="color: #0b1329;">Bloco 1</h3>
                    <span id="quiz-materia-tag" style="background: #fef3c7; color: #d97706; padding: 4px 10px; border-radius: 20px; font-size: 0.8rem; font-weight: 700;">História</span>
                </div>
                
                <!-- Explicação estilo prova antes da pergunta -->
                <div class="explanation-box" id="quiz-explicacao"></div>

                <p id="quiz-pergunta" style="font-size: 1.05rem; margin-bottom: 20px; font-weight: 600;"></p>
                <div id="quiz-opcoes"></div>
                <div id="quiz-feedback" style="margin-top: 15px; font-weight: 700;"></div>
            </div>
        </div>

        <!-- TELA 4: PERFIL E GRÁFICOS DE EVOLUÇÃO -->
        <div id="painel-perfil" class="painel">
            <h2 style="color: #0b1329; margin-bottom: 20px;">👤 Meu Perfil e Gráficos de Evolução</h2>
            
            <div style="background: #f8fafc; padding: 20px; border-radius: 10px; border: 1px solid #e2e8f0; margin-bottom: 20px;">
                <div style="display: flex; align-items: center; gap: 20px; margin-bottom: 15px;">
                    <div id="profile-initials" style="width: 60px; height: 60px; border-radius: 50%; background: #0b1329; color: #f59e0b; display: flex; align-items: center; justify-content: center; font-size: 1.5rem; font-weight: 700;">DB</div>
                    <div>
                        <h3 id="pf-nome" style="color: #0b1329;">Aluno</h3>
                        <p style="color: #64748b; font-size: 0.9rem;">E-mail: <span id="pf-email">email@email.com</span></p>
                    </div>
                </div>

                <!-- Formulário para alterar nome e nível a qualquer momento -->
                <div style="border-top: 1px solid #e2e8f0; padding-top: 15px; margin-top: 10px;">
                    <h4 style="font-size: 1rem; color: #0b1329; margin-bottom: 10px;">Alterar Dados Cadastrais:</h4>
                    <label style="font-size: 0.85rem; font-weight: 600;">Novo Apelido:</label>
                    <input type="text" id="edit-apelido" style="width: 100%; padding: 8px; margin: 5px 0 10px 0; border: 1px solid #cbd5e1; border-radius: 6px;">
                    
                    <label style="font-size: 0.85rem; font-weight: 600;">Novo Nível de Inglês:</label>
                    <select id="edit-nivel" style="width: 100%; padding: 8px; margin: 5px 0 15px 0; border: 1px solid #cbd5e1; border-radius: 6px;">
                        <option value="basico">Nível 1: Básico</option>
                        <option value="intermediario">Nível 2: Intermediário</option>
                        <option value="avancado">Nível 3: Avançado / Médio</option>
                    </select>
                    <button type="button" class="btn-secundario" style="margin-top: 0;" onclick="salvarAlteracoesPerfil()">Atualizar Dados</button>
                </div>
            </div>

            <h3 style="color: #0b1329; margin-bottom: 15px;">📊 Progresso Exato por Bloco (%)</h3>
            <div id="graficos-blocos-container"></div>

            <button type="button" class="btn-acao" style="margin-top: 20px;" onclick="mudarPainel('painel-aula')">Voltar às Aulas</button>
        </div>

    </div>

    <!-- MODAL DE COMPARTILHAMENTO -->
    <div class="modal-overlay" id="modal-compartilhar">
        <div class="modal-card">
            <h2 style="color: #0b1329; margin-bottom: 10px;">💡 Indique a Dream Bridge USA</h2>
            <p style="color: #475569; font-size: 0.95rem; margin-bottom: 15px;">Compartilhe a plataforma com os seus amigos:</p>
            <div style="display: flex; flex-direction: column; gap: 12px;">
                <button type="button" class="btn-acao" style="background-color: #25d366; color: white;" onclick="compartilharWhatsApp()">💬 Compartilhar no WhatsApp</button>
                <button type="button" class="btn-secundario" onclick="copiarLinkGeral()" style="width: 100%; margin: 0;">🔗 Copiar Link da Plataforma</button>
                <button type="button" onclick="fecharModalCompartilhar()" style="background: #f1f5f9; border: 1px solid #cbd5e1; padding: 10px; border-radius: 6px; font-weight: 600; cursor: pointer; margin-top: 5px;">Fechar</button>
            </div>
        </div>
    </div>

    <!-- MODAL BLOCO CONCLUÍDO -->
    <div class="modal-overlay" id="modal-bloco-concluido">
        <div class="modal-card">
            <h2 style="color: #10b981; margin-bottom: 10px;">🎉 Bloco Concluído com Sucesso!</h2>
            <p id="mensagem-bloco-concluido" style="color: #475569; margin-bottom: 20px;"></p>
            <button type="button" class="btn-acao" onclick="avancarParaProximoBloco()">Liberar Próximo Bloco</button>
        </div>
    </div>

    <!-- MODAL CERTIFICADO COMPLETO -->
    <div class="modal-overlay" id="modal-certificado">
        <div class="modal-card">
            <div class="certificado-diploma" id="area-certificado-pdf">
                <p style="font-size: 0.8rem; color: #64748b; letter-spacing: 2px;">DREAM BRIDGE USA 🇺🇸</p>
                <h3>CERTIFICADO DE CONCLUSÃO DE CURSO</h3>
                <p style="font-size: 0.9rem; font-style: italic; color: #475569; margin: 10px 0;">Parabéns por concluir todos os blocos acadêmicos!</p>
                <p style="font-size: 0.9rem; color: #0b1329;">Certificamos com muito orgulho que o(a) aluno(a)</p>
                <h4 id="cert-nome">Nome do Aluno</h4>
                <p style="font-size: 0.9rem; color: #0b1329; line-height: 1.6;">
                    completou com aproveitamento total a trilha de 9 blocos baseada no currículo americano na <strong style="color: #0b1329;">Dream Bridge USA</strong>.
                </p>
            </div>
            <div style="display: flex; gap: 10px; flex-direction: column; margin-top: 15px;">
                <button type="button" class="btn-acao" onclick="window.print()">📥 Baixar Certificado em PDF</button>
                <button type="button" class="btn-secundario" onclick="salvarCertificadoGaleria()" style="width: 100%; margin: 0;">🖼️ Salvar Certificado na Galeria</button>
                <button type="button" onclick="fecharModalCertificado()" style="background: #f1f5f9; border: 1px solid #cbd5e1; padding: 10px; border-radius: 6px; font-weight: 600; cursor: pointer;">Fechar</button>
            </div>
        </div>
    </div>

    <!-- RODAPÉ COM E-MAIL E INSTAGRAM -->
    <footer>
        <p>&copy; 2026 Dream Bridge USA. Todos os direitos reservados.</p>
        <p style="margin-top: 8px; font-size: 0.95rem; font-weight: 600;">
            Siga-nos No Instagram <a href="https://instagram.com/dreambridgeusa" target="_blank" style="color: #f59e0b;">@dreambridgeusa</a>
        </p>
        <p style="margin-top: 6px; font-size: 0.85rem;">Fale Conosco: <a href="mailto:anapfister208@gmail.com">anapfister208@gmail.com</a></p>
    </footer>

    <script>
        // GERADOR DE SONS WEB AUDIO API (Sem arquivos externos, 100% confiável)
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        function tocarSom(tipo) {
            if (audioCtx.state === 'suspended') { audioCtx.resume(); }
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.connect(gain);
            gain.connect(audioCtx.destination);
            
            if (tipo === 'acerto') {
                osc.type = 'sine';
                osc.frequency.setValueAtTime(587.33, aud
