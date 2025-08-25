# Prototipo.ASP.NET 

Código Index: 
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Serralheria - Avaliação de Humor</title>
<style>
  /* Reset básico */
  * {
    box-sizing: border-box;
  }
  body {
    font-family: 'Inter', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(135deg, #e0eafc, #cfdef3);
    margin: 0; padding: 0;
    color: #1a1a1a;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    padding: 30px 15px;
  }
  main {
    background: #fff;
    border-radius: 15px;
    box-shadow: 0 20px 40px rgba(0,0,0,0.08);
    max-width: 500px;
    width: 100%;
    padding: 30px 35px 40px 35px;
    animation: fadeIn 0.8s ease forwards;
  }
  h1, h2 {
    text-align: center;
    color: #2c3e50;
    margin-bottom: 30px;
    font-weight: 700;
  }
  #loginSection, #avaliacaoSection, #minhasAvaliacoesSection {
    display: none;
  }
  label {
    display: block;
    margin-bottom: 8px;
    font-weight: 600;
    color: #34495e;
    font-size: 0.95rem;
  }
  input[type="email"], input[type="password"], select, textarea {
    width: 100%;
    padding: 14px 16px;
    margin-bottom: 22px;
    border: 2px solid #d1d9e6;
    border-radius: 12px;
    font-size: 1rem;
    font-weight: 500;
    color: #34495e;
    background-color: #f9fbfd;
    transition: all 0.3s ease;
    font-family: 'Inter', sans-serif;
  }
  input[type="email"]:focus, input[type="password"]:focus, select:focus, textarea:focus {
    border-color: #3f51b5;
    background-color: #fff;
    outline: none;
    box-shadow: 0 0 8px rgba(63, 81, 181, 0.3);
  }
  textarea {
    resize: vertical;
    min-height: 80px;
    font-family: 'Inter', sans-serif;
  }
  button {
    background-color: #3f51b5;
    color: white;
    border: none;
    padding: 14px 26px;
    border-radius: 14px;
    cursor: pointer;
    font-size: 1rem;
    font-weight: 600;
    margin-right: 12px;
    margin-bottom: 14px;
    transition: background-color 0.3s ease;
    font-family: 'Inter', sans-serif;
    box-shadow: 0 6px 12px rgba(63,81,181,0.25);
  }
  button:hover:not(:disabled) {
    background-color: #2c3a99;
    box-shadow: 0 8px 18px rgba(44,58,153,0.4);
  }
  button:disabled {
    background-color: #a1a9c9;
    cursor: not-allowed;
    box-shadow: none;
  }
  #btnVerAvaliacoes {
    background-color: #009688;
    box-shadow: 0 6px 12px rgba(0,150,136,0.25);
  }
  #btnVerAvaliacoes:hover {
    background-color: #00796b;
    box-shadow: 0 8px 18px rgba(0,121,107,0.4);
  }
  #mensagemFinal {
    margin-top: 22px;
    font-weight: 600;
    font-size: 1rem;
    min-height: 28px;
    text-align: center;
    color: #34495e;
  }
  .msg {
    color: #34495e;
  }
  .error {
    color: #e74c3c;
  }
  .success {
    color: #27ae60;
  }
  .avaliacao-box {
    background: #f0f4ff;
    border-radius: 14px;
    padding: 18px 22px;
    margin-bottom: 18px;
    box-shadow: 0 3px 12px rgba(0,0,0,0.07);
    font-size: 0.95rem;
    color: #34495e;
    font-weight: 500;
  }
  .avaliacao-box strong {
    color: #2c3e50;
  }
  .btnsAvaliacao button {
    margin-top: 12px;
    margin-right: 10px;
    background-color: #3f51b5;
    font-size: 0.9rem;
    padding: 8px 18px;
    border-radius: 12px;
    box-shadow: 0 4px 10px rgba(63,81,181,0.2);
  }
  .btnsAvaliacao button:hover {
    background-color: #2c3a99;
    box-shadow: 0 5px 14px rgba(44,58,153,0.35);
  }
  .btnsAvaliacao button.delete {
    background-color: #e74c3c;
    box-shadow: 0 4px 10px rgba(231,76,60,0.25);
  }
  .btnsAvaliacao button.delete:hover {
    background-color: #c0392b;
    box-shadow: 0 5px 14px rgba(192,57,43,0.4);
  }
  #perfilIcon {
    display: inline-block;
    width: 44px; height: 44px;
    line-height: 44px;
    border-radius: 50%;
    background-color: #3f51b5;
    color: white;
    font-weight: 700;
    text-align: center;
    vertical-align: middle;
    font-size: 1.5rem;
    user-select: none;
    margin-left: 14px;
    box-shadow: 0 3px 8px rgba(63,81,181,0.4);
  }
  #usuarioEmailDisplay {
    font-weight: 600;
    font-size: 1.05rem;
    color: #2c3e50;
  }
  .aviso-adm {
    background-color: #fff3cd;
    border: 1px solid #ffeeba;
    padding: 15px 20px;
    border-radius: 12px;
    color: #856404;
    font-weight: 600;
    margin-bottom: 25px;
    text-align: center;
    font-size: 1rem;
    box-shadow: 0 2px 6px rgba(255, 193, 7, 0.25);
  }
  @media (max-width: 540px) {
    main {
      padding: 25px 20px 35px 20px;
    }
    button {
      margin-right: 0;
      width: 100%;
      margin-bottom: 16px;
    }
    #btnVerAvaliacoes {
      margin-bottom: 16px;
    }
    .btnsAvaliacao button {
      width: 48%;
      margin-right: 4%;
      margin-bottom: 10px;
    }
    .btnsAvaliacao button:nth-child(2n) {
      margin-right: 0;
    }
    #perfilIcon {
      margin-left: 8px;
      width: 38px;
      height: 38px;
      line-height: 38px;
      font-size: 1.2rem;
    }
  }
  @keyframes fadeIn {
    from {opacity: 0; transform: translateY(15px);}
    to {opacity: 1; transform: translateY(0);}
  }
</style>
</head>
<body>

<main>

  <h1>Seja bem-vindo ao site da Serralheria</h1>

  <section id="loginSection" aria-label="Seção de Login">
    <label for="email">Email</label>
    <input type="email" id="email" placeholder="Digite seu email" autocomplete="username" />
    <label for="senha">Senha</label>
    <input type="password" id="senha" placeholder="Digite sua senha" autocomplete="current-password" />
    <button id="btnLogin">Entrar</button>
    <button id="btnAnonimo">Avaliar anonimamente</button>
    <div id="loginError" class="error" style="margin-top:10px; display:none;"></div>
  </section>

  <section id="avaliacaoSection" aria-label="Seção de Avaliação">
    <div class="aviso-adm">
      ⚠️ Atenção: Somente o administrador tem acesso às avaliações e dados dos funcionários.
    </div>
    <div style="text-align:center; margin-bottom: 28px; display:flex; align-items:center; justify-content:center;">
      <span>Usuário: <span id="usuarioEmailDisplay"></span></span>
      <span id="perfilIcon" title="Perfil">👤</span>
    </div>

    <label for="humor">Como você está se sentindo hoje?</label>
    <select id="humor">
      <option value="" disabled selected>Selecione seu humor</option>
      <option value="otimo">😀 Ótimo</option>
      <option value="bom">🙂 Bom</option>
      <option value="regular">😐 Regular</option>
      <option value="ruim">😞 Ruim</option>
      <option value="outro">🤔 Outro</option>
    </select>

    <label for="comentario">Comentários (opcional)</label>
    <textarea id="comentario" placeholder="Escreva aqui..."></textarea>

    <button id="btnEnviarAvaliacao">Enviar Avaliação</button>
    <button id="btnVerHistorico">Ver Histórico</button>
    <button id="btnSair">Sair</button>

    <div id="mensagemFinal"></div>
  </section>

  <section id="minhasAvaliacoesSection" aria-label="Minhas Avaliações">
    <h2>Minhas Avaliações</h2>
    <div id="listaAvaliacoes"></div>
    <button id="btnVoltar">Voltar</button>
  </section>

</main>

<script>
  const loginSection = document.getElementById('loginSection');
  const avaliacaoSection = document.getElementById('avaliacaoSection');
  const minhasAvaliacoesSection = document.getElementById('minhasAvaliacoesSection');

  const emailInput = document.getElementById('email');
  const senhaInput = document.getElementById('senha');
  const btnLogin = document.getElementById('btnLogin');
  const btnAnonimo = document.getElementById('btnAnonimo');
  const btnEnviarAvaliacao = document.getElementById('btnEnviarAvaliacao');
  const btnSair = document.getElementById('btnSair');
  const btnVerHistorico = document.getElementById('btnVerHistorico');
  const btnVoltar = document.getElementById('btnVoltar');

  const usuarioEmailDisplay = document.getElementById('usuarioEmailDisplay');
  const perfilIcon = document.getElementById('perfilIcon');
  const humorSelect = document.getElementById('humor');
  const comentarioInput = document.getElementById('comentario');
  const mensagemFinal = document.getElementById('mensagemFinal');
  const loginError = document.getElementById('loginError');
  const listaAvaliacoes = document.getElementById('listaAvaliacoes');

  let usuarioLogado = null;

  function init() {
    loginSection.style.display = 'block';
    avaliacaoSection.style.display = 'none';
    minhasAvaliacoesSection.style.display = 'none';
    emailInput.value = '';
    senhaInput.value = '';
    humorSelect.value = '';
    comentarioInput.value = '';
    mensagemFinal.textContent = '';
    loginError.style.display = 'none';
  }

  function mostrarTelaAvaliacao() {
    loginSection.style.display = 'none';
    avaliacaoSection.style.display = 'block';
    minhasAvaliacoesSection.style.display = 'none';

    if (usuarioLogado) {
      usuarioEmailDisplay.textContent = usuarioLogado.email;
    } else {
      usuarioEmailDisplay.textContent = 'Anônimo';
    }

    humorSelect.value = '';
    comentarioInput.value = '';
    mensagemFinal.textContent = '';
  }

  function mostrarHistorico() {
    if (!usuarioLogado) {
      alert('Histórico disponível apenas para usuários logados.');
      return;
    }

    const avaliacoes = JSON.parse(localStorage.getItem(`avaliacoes_${usuarioLogado.email}`)) || [];
    listaAvaliacoes.innerHTML = '';

    if (avaliacoes.length === 0) {
      listaAvaliacoes.innerHTML = '<p>Você ainda não fez nenhuma avaliação.</p>';
    } else {
      avaliacoes.forEach(av => {
        const div = document.createElement('div');
        div.className = 'avaliacao-box';
        div.innerHTML = `
          <strong>Data:</strong> ${av.data}<br>
          <strong>Humor:</strong> ${av.humor}<br>
          <strong>Comentário:</strong> ${av.comentario || 'Nenhum'}<br>
        `;
        listaAvaliacoes.appendChild(div);
      });
    }

    avaliacaoSection.style.display = 'none';
    minhasAvaliacoesSection.style.display = 'block';
  }

  // Inicializa
  init();

  btnLogin.addEventListener('click', () => {
    const email = emailInput.value.trim();
    const senha = senhaInput.value.trim();
    loginError.style.display = 'none';

    if (!email || !senha) {
      loginError.textContent = 'Por favor, preencha email e senha.';
      loginError.style.display = 'block';
      return;
    }

    usuarioLogado = { email };
    mostrarTelaAvaliacao();
  });

  btnAnonimo.addEventListener('click', () => {
    usuarioLogado = null;
    mostrarTelaAvaliacao();
  });

  btnEnviarAvaliacao.addEventListener('click', () => {
    const humor = humorSelect.value;
    const comentario = comentarioInput.value.trim();

    if (!humor) {
      mensagemFinal.textContent = 'Por favor, selecione seu humor.';
      mensagemFinal.className = 'error';
      return;
    }

    if (usuarioLogado) {
      const avaliacoes = JSON.parse(localStorage.getItem(`avaliacoes_${usuarioLogado.email}`)) || [];
      avaliacoes.push({ humor, comentario, data: new Date().toLocaleString() });
      localStorage.setItem(`avaliacoes_${usuarioLogado.email}`, JSON.stringify(avaliacoes));
    }

    mensagemFinal.textContent = (humor === 'bom' || humor === 'otimo')
      ? 'Muito obrigada pela sua avaliação!'
      : 'Podemos ajudar! Se quiser conversar, entre em contato.';
    mensagemFinal.className = (humor === 'bom' || humor === 'otimo') ? 'success' : 'error';

    humorSelect.value = '';
    comentarioInput.value = '';
  });

  btnSair.addEventListener('click', () => {
    alert(usuarioLogado ? 'Você está saindo da sua conta.' : 'Saindo do modo anônimo.');
    usuarioLogado = null;
    init();
  });

  btnVerHistorico.addEventListener('click', mostrarHistorico);
  btnVoltar.addEventListener('click', mostrarTelaAvaliacao);
</script>

</body>
</html>