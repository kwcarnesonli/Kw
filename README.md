index.html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Açougue Digital - Seu Açougue Online</title>
<style>
  /* Reset e base */
  * {
    box-sizing: border-box;
  }
  body {
    margin: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: #121212;
    color: #eee;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    transition: background-color 0.3s, color 0.3s;
  }

  /* Tema claro */
  body.light-theme {
    background-color: #f5f5f5;
    color: #222;
  }

  header {
    background: linear-gradient(90deg, #b22222, #8b0000);
    padding: 1rem 2rem;
    text-align: center;
    z-index: 1000;
    color: #eee;
    transition: background 0.3s, color 0.3s;
  }
  body.light-theme header {
    background: linear-gradient(90deg, #ef4444, #b91c1c);
    color: #fff;
  }
  header h1 {
    margin: 0;
    font-weight: 900;
    font-size: 2rem;
    letter-spacing: 2px;
  }

  main {
    flex-grow: 1;
    max-width: 900px;
    margin: 1.5rem auto 5rem;
    padding: 1rem 1.5rem;
    background-color: #1e1e1e;
    border-radius: 12px;
    box-shadow: 0 0 10px #8b0000cc;
    transition: background-color 0.3s, color 0.3s, box-shadow 0.3s;
  }

  body.light-theme main {
    background-color: #fff;
    color: #222;
    box-shadow: 0 0 12px rgba(178,34,34,0.2);
  }

  .screen {
    display: none;
  }
  .screen.active {
    display: block;
  }

  nav#bottom-nav {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    height: 56px;
    background-color: #1e1e1e;
    border-top: 1px solid #8b0000;
    display: flex;
    justify-content: space-around;
    align-items: center;
    z-index: 2000;
    transition: background-color 0.3s, border-color 0.3s;
  }

  body.light-theme nav#bottom-nav {
    background-color: #fff;
    border-top: 1px solid #b22222;
  }

  nav#bottom-nav button {
    background: none;
    border: none;
    color: #b22222;
    font-weight: 700;
    font-size: 0.95rem;
    cursor: pointer;
    flex-grow: 1;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    transition: color 0.3s;
  }
  nav#bottom-nav button svg {
    margin-bottom: 4px;
    width: 20px;
    height: 20px;
    fill: #b22222;
    transition: fill 0.3s;
  }
  nav#bottom-nav button.active,
  nav#bottom-nav button:hover {
    color: #ef4444;
  }
  nav#bottom-nav button.active svg,
  nav#bottom-nav button:hover svg {
    fill: #ef4444;
  }

  /* Telas */
  #welcome h2, #cuts h2, #home h2, #video-call h2, #tracking h2, #settings h2 {
    font-weight: 900;
    margin-bottom: 1rem;
    text-align: center;
  }

  /* Tela Welcome */
  #welcome p {
    text-align: center;
    margin-bottom: 2rem;
  }
  #welcome .btn-group {
    display: flex;
    justify-content: center;
    gap: 2rem;
  }
  #welcome button {
    background-color: #b22222;
    border: none;
    color: #fff;
    padding: 0.8rem 2rem;
    font-size: 1.2rem;
    cursor: pointer;
    border-radius: 6px;
    transition: background-color 0.3s ease;
  }
  #welcome button:hover {
    background-color: #8b0000;
  }

  /* Formulários */
  form {
    max-width: 400px;
    margin: 0 auto;
  }
  form label {
    display: block;
    margin-top: 1rem;
    font-weight: 600;
  }
  form input {
    width: 100%;
    padding: 0.6rem;
    margin-top: 0.3rem;
    border-radius: 6px;
    border: 1px solid #555;
    font-size: 1rem;
    transition: border-color 0.3s;
    background-color: #333;
    color: #eee;
  }
  body.light-theme form input {
    border: 1px solid #ccc;
    background-color: #fff;
    color: #000;
  }
  form input:focus {
    outline: none;
    box-shadow: 0 0 5px #b22222cc;
    border-color: #b22222;
  }
  form button {
    margin-top: 1.8rem;
    width: 100%;
    background-color: #b22222;
    color: #fff;
    border: none;
    padding: 0.8rem;
    font-size: 1.2rem;
    font-weight: 700;
    border-radius: 6px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  form button:hover {
    background-color: #8b0000;
  }

  /* Tela Home */
  #home .greeting {
    margin-bottom: 2rem;
    font-size: 1.2rem;
  }
  #home .menu-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit,minmax(140px,1fr));
    gap: 1rem;
  }
  #home .menu-item {
    background-color: #8b000020;
    border-radius: 10px;
    padding: 1.3rem;
    cursor: pointer;
    text-align: center;
    font-weight: 700;
    font-size: 1rem;
    transition: background-color 0.3s ease;
    border: 2px solid transparent;
    color: inherit;
  }
  #home .menu-item:hover,
  #home .menu-item:focus {
    background-color: #b222221a;
    border-color: #b22222;
    outline: none;
  }

  /* Tela Cortes (Menu de Cortes substituindo pagamento) */
  #cuts .cut-list {
    display: grid;
    grid-template-columns: repeat(auto-fit,minmax(160px,1fr));
    gap: 1rem;
  }
  #cuts .cut-item {
    background-color: #8b000020;
    padding: 1rem;
    border-radius: 12px;
    cursor: pointer;
    transition: background-color 0.3s;
    border: 2px solid transparent;
    font-weight: 700;
    color: inherit;
    text-align: center;
  }
  #cuts .cut-item:hover,
  #cuts .cut-item:focus {
    background-color: #b222221a;
    border-color: #b22222;
    outline: none;
  }

  /* Tela Pagamento */
  #payment {
    display: none;
  }
  #payment.active {
    display: block;
  }
  #payment .total {
    font-size: 1.4rem;
    margin-bottom: 2rem;
    font-weight: 700;
    color: #b22222;
    text-align: center;
  }
  #payment .pay-methods {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    max-width: 280px;
    margin: 0 auto;
  }
  #payment .pay-methods button {
    padding: 1rem;
    background-color: #8b0000;
    border: none;
    color: white;
    font-weight: 700;
    border-radius: 8px;
    cursor: pointer;
    font-size: 1.1rem;
    transition: background-color 0.3s ease;
  }
  #payment .pay-methods button:hover {
    background-color: #b22222;
  }

  /* Tela Videochamada */
  #video-call iframe {
    border: none;
    width: 100%;
    height: 480px;
    border-radius: 12px;
    box-shadow: 0 0 15px #b22222cc;
    transition: box-shadow 0.3s;
    background-color: #000;
  }
  body.light-theme #video-call iframe {
    box-shadow: 0 0 20px #ef4444cc;
    background-color: #fff;
  }

  /* Tela Acompanhamento */
  #tracking .status-list {
    max-width: 360px;
    margin: 0 auto;
    list-style: none;
    padding: 0;
  }
  #tracking .status-list li {
    background-color: #222;
    margin-bottom: 1rem;
    padding: 1rem;
    border-radius: 8px;
    font-weight: 600;
    color: #eee;
    box-shadow: 0 0 10px #b22222aa;
  }
  body.light-theme #tracking .status-list li {
    background-color: #f0f0f0;
    color: #333;
    box-shadow: 0 0 7px #ef4444aa;
  }
  #tracking .map-placeholder {
    margin-top: 2rem;
    width: 100%;
    height: 180px;
    background: url('https://maps.googleapis.com/maps/api/staticmap?center=-23.55052,-46.633308&zoom=12&size=600x180&markers=color:red%7Clabel:A%7C-23.55052,-46.633308') no-repeat center/cover;
    border-radius: 12px;
    box-shadow: 0 0 15px #b2222233;
  }

  /* Tela Configurações */
  #settings .profile-info, #settings .support, #settings .theme-toggle {
    max-width: 400px;
    margin: 1rem auto;
    background-color: #292929;
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 0 8px #b2222277;
    color: #ccc;
    transition: background-color 0.3s, color 0.3s;
  }
  body.light-theme #settings .profile-info,
  body.light-theme #settings .support,
  body.light-theme #settings .theme-toggle {
    background-color: #fafafa;
    color: #222;
    box-shadow: 0 0 12px #ef444477;
  }
  #settings .profile-info p, #settings .support p {
    margin: 0.5rem 0;
  }
  #settings .support a {
    color: #b22222;
    text-decoration: none;
    font-weight: 700;
  }
  #settings .support a:hover {
    text-decoration: underline;
  }
  #settings .theme-toggle label {
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-weight: 600;
  }
  #settings .theme-toggle input[type="checkbox"] {
    width: 20px;
    height: 20px;
    cursor: pointer;
  }

  /* Footer */
  footer {
    background-color: #000;
    color: #b22222;
    text-align: center;
    padding: 1rem;
    font-weight: 600;
    font-size: 0.9rem;
    transition: background-color 0.3s, color 0.3s;
  }
  body.light-theme footer {
    background-color: #f8f8f8;
    color: #b22222;
  }

  /* Responsividade básica */
  @media (max-width: 600px) {
    main {
      margin: 1rem;
      padding: 1rem;
    }
    #tracking .map-placeholder {
      height: 140px;
    }
    #video-call iframe {
      height: 320px;
    }
    nav#bottom-nav {
      height: 56px;
    }
  }
</style>
</head>
<body>

<header>
  Açougue Digital
</header>

<main>
  <!-- Tela 1: Boas-Vindas -->
  <section id="welcome" class="screen active" role="region" aria-label="Tela de boas-vindas">
    <h2>Bem-vindo ao Açougue Digital</h2>
    <p>Aqui você encontra os melhores cortes em tempo real com atendimento por videochamada!</p>
    <div style="text-align:center; margin-top:2rem;">
      <button onclick="showScreen('login')" class="button" style="padding:12px 24px; font-size:1.2rem; background:#b22222; border:none; border-radius:8px; color:#eee; cursor:pointer;">Entrar / Criar Conta</button>
    </div>
  </section>

  <!-- Tela 2: Cadastro / Login -->
  <section id="login" class="screen" role="region" aria-label="Tela de login e cadastro">
    <h2>Login ou Cadastro</h2>
    <form id="login-form" onsubmit="handleLogin(event)">
      <label for="name">Nome</label>
      <input type="text" id="name" required autocomplete="name" placeholder="Seu nome" />
      
      <label for="phone">Celular</label>
      <input type="tel" id="phone" required autocomplete="tel" placeholder="(99) 99999-9999" />
      
      <label for="email">E-mail (opcional)</label>
      <input type="email" id="email" autocomplete="email" placeholder="seu@email.com" />
      
      <label for="address">Endereço</label>
      <input type="text" id="address" required placeholder="Sua localização" />
      
      <button type="submit" style="margin-top: 20px; width: 100%; background:#b22222; color:#eee; font-weight: 700; padding:12px; border:none; border-radius:8px; cursor:pointer;">Entrar</button>
    </form>
  </section>

  <!-- Tela 3: Home -->
  <section id="home" class="screen" role="region" aria-label="Tela inicial home">
    <h2>Olá, <span id="user-name">Cliente</span></h2>
    <div class="greeting" tabindex="0">Bem-vindo ao Açougue Digital, onde você escolhe cortes ao vivo!</div>
    <div class="menu-grid" role="list">
      <div tabindex="0" role="listitem" class="menu-item" onclick="showScreen('video-call')" onkeypress="event.key==='Enter' && showScreen('video-call')">📞 Comprar por Videochamada</div>
      <div tabindex="0" role="listitem" class="menu-item" onclick="showScreen('cuts')" onkeypress="event.key==='Enter' && showScreen('cuts')">🥩 Corte de Carnes</div>
      <div tabindex="0" role="listitem" class="menu-item" onclick="showScreen('tracking')" onkeypress="event.key==='Enter' && showScreen('tracking')">🚚 Rastrear Entrega</div>
      <div tabindex="0" role="listitem" class="menu-item" onclick="showScreen('settings')" onkeypress="event.key==='Enter' && showScreen('settings')">⚙️ Configurações</div>
    </div>
  </section>

  <!-- Tela 4: Cortes de Carne -->
  <section id="cuts" class="screen" role="region" aria-label="Tela de cortes de carnes">
    <h2>Cortes de Carnes</h2>
    <div class="cut-list" role="list">
      <div class="cut-item" tabindex="0" role="listitem" onclick="selectCut('Picanha', 59.90)" onkeypress="event.key==='Enter' && selectCut('Picanha', 59.90)">Picanha - R$59,90/kg</div>
      <div class="cut-item" tabindex="0" role="listitem" onclick="selectCut('Alcatra', 39.90)" onkeypress="event.key==='Enter' && selectCut('Alcatra', 39.90)">Alcatra - R$39,90/kg</div>
      <div class="cut-item" tabindex="0" role="listitem" onclick="selectCut('Fraldinha', 29.90)" onkeypress="event.key==='Enter' && selectCut('Fraldinha', 29.90)">Fraldinha - R$29,90/kg</div>
      <div class="cut-item" tabindex="0" role="listitem" onclick="selectCut('Costela', 24.90)" onkeypress="event.key==='Enter' && selectCut('Costela', 24.90)">Costela - R$24,90/kg</div>
      <div class="cut-item" tabindex="0" role="listitem" onclick="selectCut('Cupim', 34.90)" onkeypress="event.key==='Enter' && selectCut('Cupim', 34.90)">Cupim - R$34,90/kg</div>
    </div>
  </section>

  <!-- Tela 5: Pagamento - aparece só após corte selecionado -->
  <section id="payment" class="screen" role="region" aria-label="Tela de pagamento" style="display:none;">
    <h2>Pagamento do Pedido</h2>
    <p class="total">Total: R$ <span id="total-value">0,00</span></p>
    <div class="pay-methods">
      <button onclick="alert('Pix selecionado')" aria-label="Selecionar pagamento por Pix">Pix (QR Code)</button>
      <button onclick="alert('Cartão selecionado')" aria-label="Selecionar pagamento por cartão">Cartão de Crédito</button>
      <button onclick="alert('Dinheiro selecionado')" aria-label="Selecionar pagamento em dinheiro">Dinheiro na Entrega</button>
    </div>
    <div style="text-align:center; margin-top: 1.2rem;">
      <button onclick="showScreen('home')" style="background:#b22222; color:#fff; border:none; padding:0.8rem 1.6rem; border-radius:6px; cursor:pointer;">Voltar ao Home</button>
    </div>
  </section>

  <!-- Tela 6: Videochamada -->
  <section id="video-call" class="screen" role="region" aria-label="Tela de videochamada">
    <h2>Videochamada com Açougueiro</h2>
    <iframe src="https://meet.jit.si/AçougueDigital2024" allow="camera; microphone; fullscreen; speaker;" title="Videochamada" aria-label="Videochamada com Açougueiro"></iframe>
  </section>

  <!-- Tela 7: Acompanhamento -->
  <section id="tracking" class="screen" role="region" aria-label="Tela de acompanhamento do pedido">
    <h2>Acompanhamento do Pedido</h2>
    <ul class="status-list" aria-live="polite">
      <li>✅ Pedido recebido</li>
      <li>⏳ Preparando corte</li>
      <li>🚚 Saiu para entrega</li>
      <li>📦 Entregue</li>
    </ul>
    <div class="map-placeholder" aria-label="Mapa de rastreamento da entrega"></div>
  </section>

  <!-- Tela 8: Configurações -->
  <section id="settings" class="screen" role="region" aria-label="Tela de configurações">
    <h2>Configurações</h2>
    <div class="profile-info">
      <h3>Perfil</h3>
      <p><strong>Nome:</strong> <span id="profile-name">Cliente</span></p>
      <p><strong>Celular:</strong> <span id="profile-phone">--</span></p>
      <p><strong>E-mail:</strong> <span id="profile-email">--</span></p>
      <p><strong>Endereço:</strong> <span id="profile-address">--</span></p>
    </div>
    <div class="support" style="max-width: 400px; margin: 1.5rem auto; color:#ccc;">
      <h3>Suporte</h3>
      <p>Precisa de ajuda? <a href="https://wa.me/5511999999999" target="_blank" rel="noopener" style="color:#b22222; font-weight:bold;">Fale conosco via WhatsApp</a></p>
    </div>
    <div class="theme-toggle" style="max-width:400px; margin:1.5rem auto; color:#ccc;">
      <h3>Tema do Aplicativo</h3>
      <label>
        <input type="checkbox" id="theme-toggle-checkbox" />
        Ativar Tema Claro
      </label>
    </div>
  </section>
</main>

<nav id="bottom-nav" aria-label="Navegação principal">
  <button data-screen="home" class="active" aria-label="Home">
    <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/></svg>
    Home
  </button>
  <button data-screen="cuts" aria-label="Menu de cortes">
    <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M5 19h14v-2H5v2zm0-7h14v-2H5v2zm0-7v2h14V5H5z"/></svg>
    Cortes
  </button>
  <button data-screen="video-call" aria-label="Vídeo chamadas">
    <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M17 10.5V6c0-1.1-.9-2-2-2H5c-1.1 0-2 .9-2 2v8c0 1.1.9 2 2 2h10c1.1 0 2-.9 2-2v-4.5l4 4v-11l-4 4z"/></svg>
    Vídeo
  </button>
  <button data-screen="tracking" aria-label="Acompanhamento">
    <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M20 13V7h-2v6h-5v2h7v-2zm-6 1v6H6v-6H4v6c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2v-6h-2zm-4-1c1.66 0 3-1.34 3-3S11.66 7 10 7 7 8.34 7 10s1.34 3 3 3z"/></svg>
    Acompanhar
  </button>
  <button data-screen="settings" aria-label="Configurações">
    <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M19.43 12.98c.04-.33.07-.66.07-1s-.03-.67-.07-1l2.11-1.65a.498.498 0 000-.79l-2-1.73a.503.503 0 00-.58-.11l-2.49 1a7.03 7.03 0 00-1.73-1l-.38-2.65A.488.488 0 0014 4h-4a.5.5 0 00-.5.42l-.38 2.65c-.61.27-1.18.63-1.73 1l-2.49-1a.5.5 0 00-.58.11l-2 1.73a.5.5 0 000 .79l2.11 1.65c-.04.33-.07.66-.07 1s.03.67.07 1l-2.11 1.65a.498.498 0 000 .79l2 1.73a.5.5 0 00.58.11l2.49-1c.55.37 1.12.7 1.73 1l.38 2.65A.5.5 0 0010 20h4a.498.498 0 00.5-.42l.38-2.65c.61-.27 1.18-.63 1.73-1l2.49 1a.5.5 0 00.58-.11l2-1.73a.5.5 0 000-.79l-2.11-1.65zM12 15.5A3.5 3.5 0 1112 8a3.5 3.5 0 010 7.5z"/></svg>
    Configurações
  </button>
</nav>

<footer>
  &copy; 2024 Açougue Digital - Todos os direitos reservados.
</footer>

<script>
  // Navegação entre telas
  const buttons = document.querySelectorAll('nav#bottom-nav button');
  const screens = document.querySelectorAll('.screen');

  function showScreen(screenId) {
    screens.forEach(screen => screen.classList.remove('active'));
    buttons.forEach(btn => btn.classList.remove('active'));
    document.getElementById(screenId).classList.add('active');
    document.querySelector(`nav#bottom-nav button[data-screen="${screenId}"]`).classList.add('active');

    // Mostra tela pagamento só se ativa; default oculto
    if(screenId === 'payment'){
      document.getElementById('payment').classList.add('active');
    } else {
      document.getElementById('payment').classList.remove('active');
    }
  }

  buttons.forEach(button => {
    button.addEventListener('click', () => {
      showScreen(button.dataset.screen);
    });
  });

  // Inicializa exibindo tela Boas-vindas
  showScreen('welcome');

  // Formulário login
  function handleLogin(event) {
    event.preventDefault();
    const name = document.getElementById('name').value.trim();
    const phone = document.getElementById('phone').value.trim();
    const email = document.getElementById('email').value.trim();
    const address = document.getElementById('address').value.trim();

    if(!name || !phone || !address){
      alert('Por favor, preencha os campos obrigatórios!');
      return;
    }

    document.getElementById('user-name').textContent = name;
    document.getElementById('profile-name').textContent = name;
    document.getElementById('profile-phone').textContent = phone;
    document.getElementById('profile-email').textContent = email || '--';
    document.getElementById('profile-address').textContent = address;

    alert('Bem-vindo, ' + name + '! Login realizado com sucesso.');
    showScreen('home');
  }

  // Tema claro/escuro
  const themeToggle = document.getElementById('theme-toggle-checkbox');
  themeToggle.addEventListener('change', () => {
    if(themeToggle.checked){
      document.body.classList.add('light-theme');
      localStorage.setItem('theme', 'light');
    } else {
      document.body.classList.remove('light-theme');
      localStorage.setItem('theme', 'dark');
    }
  });

  window.addEventListener('load', () => {
    const savedTheme = localStorage.getItem('theme') || 'dark';
    if(savedTheme === 'light'){
      document.body.classList.add('light-theme');
      themeToggle.checked = true;
    }
  });

  // Seleção de corte
  let selectedCut = null;
  let orderTotal = 0;

  function selectCut(name, price) {
    if(confirm(`Deseja adicionar o corte ${name} ao pedido por R$ ${price.toFixed(2)}?`)) {
      selectedCut = name;
      orderTotal = price;
      document.getElementById('total-value').textContent = price.toFixed(2);
      alert(`Corte ${name} selecionado! Agora vá para pagamento.`);
      showScreen('payment');
    }
  }
</script>

</body>
</html>
```
