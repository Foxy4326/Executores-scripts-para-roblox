<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Executores e Scripts - Sistema Completo</title>
<style>
/* --- CSS Completo --- */
* { margin:0; padding:0; box-sizing:border-box; font-family:'Segoe UI',Tahoma,Geneva,Verdana,sans-serif;}
body{background:#f5f5f5;color:#333;line-height:1.6;}
header{background:linear-gradient(135deg,#1a2a6c 0%,#2a3c7a 100%);color:#fff;padding:1rem 0;box-shadow:0 2px 10px rgba(0,0,0,.1);}
.container{width:90%;max-width:1200px;margin:0 auto;padding:0 15px;}
.header-content{display:flex;justify-content:space-between;align-items:center;}
.logo{font-size:1.8rem;font-weight:bold;}
nav ul{display:flex;list-style:none;}
nav ul li{margin-left:20px;}
nav ul li a{color:white;text-decoration:none;font-weight:500;transition:opacity .3s;}
nav ul li a:hover{opacity:.8;}
.hero{background:#fff;padding:3rem 0;text-align:center;margin-bottom:2rem;border-radius:0 0 10px 10px;box-shadow:0 2px 10px rgba(0,0,0,.05);}
.hero h1{font-size:2.5rem;margin-bottom:1rem;color:#333;}
.hero p{font-size:1.1rem;max-width:700px;margin:0 auto;color:#666;}
.section-title{text-align:center;margin:2rem 0;color:#333;position:relative;}
.section-title:after{content:'';display:block;width:80px;height:3px;background:linear-gradient(135deg,#1a2a6c 0%,#2a3c7a 100%);margin:10px auto;}
.content-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:2rem;margin-bottom:3rem;}
.card{background:white;border-radius:10px;overflow:hidden;box-shadow:0 5px 15px rgba(0,0,0,.1);transition:transform .3s,box-shadow .3s;position:relative;}
.card:hover{transform:translateY(-5px);box-shadow:0 10px 20px rgba(0,0,0,.15);}
.card-header{padding:1.5rem;background:linear-gradient(135deg,#1a2a6c 0%,#2a3c7a 100%);color:white;}
.card-body{padding:1.5rem;}
.card h3{margin-bottom:.5rem;font-size:1.3rem;}
.card p{color:#666;margin-bottom:1rem;}
.card .date{font-size:.8rem;color:#888;margin-bottom:1rem;}
.card-actions{display:flex;gap:.5rem;margin-top:1rem;}
.btn{display:inline-block;background:linear-gradient(135deg,#1a2a6c 0%,#2a3c7a 100%);color:white;padding:.7rem 1.5rem;border-radius:5px;text-decoration:none;font-weight:500;transition:opacity .3s;border:none;cursor:pointer;text-align:center;}
.btn:hover{opacity:.9;}
.btn-outline{background:transparent;border:2px solid #1a2a6c;color:#1a2a6c;}
.btn-outline:hover{background:#1a2a6c;color:white;}
.btn-danger{background:linear-gradient(135deg,#c31432 0%,#c7364d 100%);}
.btn-warning{background:linear-gradient(135deg,#ff8c00 0%,#ffa500 100%);}
.btn-small{padding:.4rem .8rem;font-size:.8rem;}
footer{background:#333;color:white;padding:2rem 0;text-align:center;margin-top:3rem;}
.footer-content{display:flex;flex-direction:column;align-items:center;}
.footer-links{display:flex;margin:1rem 0;}
.footer-links a{color:white;margin:0 10px;text-decoration:none;}
.footer-links a:hover{text-decoration:underline;}
.copyright{margin-top:1rem;font-size:.9rem;color:#ccc;}
.upload-section{background:white;padding:2rem;border-radius:10px;box-shadow:0 5px 15px rgba(0,0,0,.1);margin-bottom:3rem;}
.upload-form{display:flex;flex-direction:column;gap:1rem;}
.form-group{display:flex;flex-direction:column;}
.form-group label{margin-bottom:.5rem;font-weight:500;}
.form-group input,.form-group select,.form-group textarea{padding:.7rem;border:1px solid #ddd;border-radius:5px;font-size:1rem;}
.form-group textarea{min-height:100px;resize:vertical;}
.file-upload{border:2px dashed #ddd;padding:1.5rem;text-align:center;border-radius:5px;cursor:pointer;transition:border-color .3s;}
.file-upload:hover{border-color:#1a2a6c;}
.file-upload p{color:#666;}
.auth-section{background:white;padding:2rem;border-radius:10px;box-shadow:0 5px 15px rgba(0,0,0,.1);margin-bottom:3rem;max-width:500px;margin-left:auto;margin-right:auto;}
.auth-form{display:flex;flex-direction:column;gap:1rem;}
.hidden{display:none;}
.admin-controls{display:flex;justify-content:space-between;margin-bottom:1rem;}
.alert{padding:1rem;border-radius:5px;margin-bottom:1rem;}
.alert-success{background-color:#d4edda;color:#155724;border:1px solid #c3e6cb;}
.alert-error{background-color:#f8d7da;color:#721c24;border:1px solid #f5c6cb;}
.empty-message{text-align:center;padding:2rem;color:#666;font-style:italic;}
.edit-form{background:white;padding:2rem;border-radius:10px;box-shadow:0 5px 15px rgba(0,0,0,.1);margin-bottom:2rem;}
.form-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:1.5rem;}
.download-btn{display:block;width:100%;margin-bottom:1rem;}
.file-info{background:#f8f9fa;padding:.5rem;border-radius:5px;margin-top:.5rem;font-size:.9rem;}
.url-input{margin-top:.5rem;}

/* --- ESTILOS DA PÁGINA 404 --- */
.error-page {display:none;background:linear-gradient(135deg,#1a2a6c 0%,#2a3c7a 100%);color:white;min-height:100vh;flex-direction:column;justify-content:center;align-items:center;text-align:center;padding:2rem;position:fixed;top:0;left:0;width:100%;height:100%;z-index:1000;}
.error-container{max-width:600px;padding:2rem;}
.error-code{font-size:8rem;font-weight:bold;margin-bottom:1rem;text-shadow:3px 3px 0 rgba(0,0,0,.2);}
.error-title{font-size:2rem;margin-bottom:1rem;}
.error-message{font-size:1.2rem;margin-bottom:2rem;opacity:.9;}
.home-btn{display:inline-block;background:white;color:#1a2a6c;padding:1rem 2rem;text-decoration:none;border-radius:5px;font-weight:bold;transition:transform .3s,box-shadow .3s;margin-top:1rem;border:none;cursor:pointer;font-size:1rem;}
.home-btn:hover{transform:translateY(-2px);box-shadow:0 5px 15px rgba(0,0,0,.3);}
.error-logo{font-size:2rem;font-weight:bold;margin-bottom:2rem;}

@media(max-width:768px){
.header-content{flex-direction:column;text-align:center;}
nav ul{margin-top:1rem;justify-content:center;}
nav ul li{margin:0 10px;}
.content-grid{grid-template-columns:1fr;}
.admin-controls{flex-direction:column;gap:1rem;}
.card-actions{flex-direction:column;}
.error-code{font-size:5rem;}
.error-title{font-size:1.5rem;}
.error-message{font-size:1rem;}
}
</style>
</head>
<body>

<!-- Página 404 (oculta inicialmente) -->
<div id="error-page" class="error-page">
    <div class="error-logo">Executores & Scripts</div>
    <div class="error-container">
        <div class="error-code">404</div>
        <h1 class="error-title">Página Não Encontrada</h1>
        <p class="error-message">
            A página que você está procurando não existe ou foi movida.
        </p>
        <button id="home-redirect" class="home-btn">Voltar para a Página Inicial</button>
    </div>
</div>

<!-- Conteúdo Principal do Site -->
<div id="main-content">
<header>
<div class="container">
<div class="header-content">
<div class="logo">Executores & Scripts</div>
<nav>
<ul>
<li><a href="#home">Início</a></li>
<li><a href="#executores">Executores</a></li>
<li><a href="#scripts">Scripts</a></li>
<li><a href="#upload">Publicar</a></li>
<li><a href="#" id="logout-btn" class="hidden">Sair</a></li>
</ul>
</nav>
</div>
</div>
</header>

<section class="hero" id="home">
<div class="container">
<h1>Encontre os Melhores Executores e Scripts</h1>
<p>Baixe executores em formato APK e scripts para diversas finalidades. Área de publicação restrita.</p>
</div>
</section>

<div class="container">
<section id="executores">
<h2 class="section-title">Executores (APK)</h2>
<div class="content-grid" id="executors-grid"></div>
</section>

<section id="scripts">
<h2 class="section-title">Scripts</h2>
<div class="content-grid" id="scripts-grid"></div>
</section>

<!-- Área de Autenticação -->
<section id="auth">
<h2 class="section-title">Acesso Restrito</h2>
<div class="auth-section">
<div id="auth-message" class="alert alert-error hidden"></div>
<form class="auth-form" id="auth-form">
<div class="form-group">
<label for="access-code">Código de Acesso</label>
<input type="password" id="access-code" placeholder="Digite o código secreto" required>
</div>
<button type="submit" class="btn">Acessar Área de Publicação</button>
</form>
</div>
</section>

<!-- Área de Upload -->
<section id="upload" class="hidden">
<h2 class="section-title">Publicar Conteúdo</h2>
<div class="admin-controls">
<button id="add-item-btn" class="btn">Adicionar Novo Item</button>
<button id="logout-admin" class="btn btn-danger">Sair da Área Admin</button>
</div>

<div id="upload-message" class="alert alert-success hidden"></div>

<!-- Formulário de Edição -->
<div id="edit-form-container" class="edit-form hidden">
<div class="form-header">
<h3>Editar Conteúdo</h3>
<button id="cancel-edit-btn" class="btn btn-danger btn-small">Cancelar</button>
</div>
<form class="upload-form" id="edit-form">
<input type="hidden" id="edit-id">
<div class="form-group">
<label for="edit-title">Título</label>
<input type="text" id="edit-title" placeholder="Digite o título do conteúdo" required>
</div>
<div class="form-group">
<label for="edit-description">Descrição</label>
<textarea id="edit-description" placeholder="Descreva o conteúdo" required></textarea>
</div>
<div class="form-group">
<label for="edit-type">Tipo de Conteúdo</label>
<select id="edit-type" required>
<option value="">Selecione o tipo</option>
<option value="executor">Executor (APK)</option>
<option value="script">Script</option>
</select>
</div>
<div class="form-group">
<label>URL do Download</label>
<input type="url" id="edit-download-url" class="url-input" placeholder="https://exemplo.com/arquivo.apk" required>
</div>
<button type="submit" class="btn btn-warning">Salvar Alterações</button>
</form>
</div>

<!-- Formulário de Publicação -->
<div class="upload-section" id="upload-form-container">
<form class="upload-form" id="upload-form">
<div class="form-group">
<label for="title">Título</label>
<input type="text" id="title" placeholder="Digite o título do conteúdo" required>
</div>
<div class="form-group">
<label for="description">Descrição</label>
<textarea id="description" placeholder="Descreva o conteúdo" required></textarea>
</div>
<div class="form-group">
<label for="type">Tipo de Conteúdo</label>
<select id="type" required>
<option value="">Selecione o tipo</option>
<option value="executor">Executor (APK)</option>
<option value="script">Script</option>
</select>
</div>
<div class="form-group">
<label>URL do Download</label>
<input type="url" id="download-url" class="url-input" placeholder="https://exemplo.com/arquivo.apk" required>
<div class="file-info">
<small>Use serviços como Google Drive, MediaFire, ou Mega.nz para hospedar seus arquivos</small>
</div>
</div>
<button type="submit" class="btn">Publicar Conteúdo</button>
</form>
</div>
</section>
</div>

<footer>
<div class="container">
<div class="footer-content">
<div class="logo">Executores & Scripts</div>
<div class="footer-links">
<a href="#home">Início</a>
<a href="#executores">Executores</a>
<a href="#scripts">Scripts</a>
<a href="#upload">Publicar</a>
<a href="#">Contato</a>
</div>
<div class="copyright">
&copy; 2025 Executores & Scripts. Área administrativa protegida.
</div>
</div>
</div>
</footer>
</div>

<!-- ================= JAVASCRIPT ================= -->
<script>
// ================= CONFIGURAÇÃO =================
const SECRET_CODE = "admin123"; // Código secreto

// ================= ELEMENTOS =================
const authSection = document.getElementById('auth');
const uploadSection = document.getElementById('upload');
const authForm = document.getElementById('auth-form');
const uploadForm = document.getElementById('upload-form');
const editForm = document.getElementById('edit-form');
const accessCodeInput = document.getElementById('access-code');
const authMessage = document.getElementById('auth-message');
const uploadMessage = document.getElementById('upload-message');
const logoutBtn = document.getElementById('logout-btn');
const logoutAdminBtn = document.getElementById('logout-admin');
const executorsGrid = document.getElementById('executors-grid');
const scriptsGrid = document.getElementById('scripts-grid');
const uploadFormContainer = document.getElementById('upload-form-container');
const editFormContainer = document.getElementById('edit-form-container');
const cancelEditBtn = document.getElementById('cancel-edit-btn');
const addItemBtn = document.getElementById('add-item-btn');
const errorPage = document.getElementById('error-page');
const mainContent = document.getElementById('main-content');
const homeRedirect = document.getElementById('home-redirect');

// ================= ARMAZENAMENTO =================
let publishedItems = JSON.parse(localStorage.getItem('publishedItems')) || [];

// ================= FUNÇÕES PRINCIPAIS =================
function saveItems() { 
    localStorage.setItem('publishedItems', JSON.stringify(publishedItems)); 
}

function checkAuthStatus() {
    const isAuthenticated = localStorage.getItem('authenticated') === 'true';
    if (isAuthenticated) showUploadSection();
}

function showUploadSection() {
    authSection.classList.add('hidden');
    uploadSection.classList.remove('hidden');
    logoutBtn.classList.remove('hidden');
}

function hideUploadSection() {
    authSection.classList.remove('hidden');
    uploadSection.classList.add('hidden');
    logoutBtn.classList.add('hidden');
    localStorage.removeItem('authenticated');
}

function displayPublishedItems() {
    executorsGrid.innerHTML = '';
    scriptsGrid.innerHTML = '';

    const executors = publishedItems.filter(i => i.type === 'executor');
    const scripts = publishedItems.filter(i => i.type === 'script');

    if (executors.length) executors.forEach(i => executorsGrid.appendChild(createCard(i)));
    else executorsGrid.innerHTML = '<div class="empty-message">Nenhum executor publicado ainda.</div>';

    if (scripts.length) scripts.forEach(i => scriptsGrid.appendChild(createCard(i)));
    else scriptsGrid.innerHTML = '<div class="empty-message">Nenhum script publicado ainda.</div>';
}

function createCard(item) {
    const card = document.createElement('div');
    card.className = 'card';
    const dateText = item.lastUpdate ? `Atualizado em: ${item.lastUpdate}` : `Publicado em: ${item.date || new Date().toLocaleDateString('pt-BR')}`;
    card.innerHTML = `
        <div class="card-header"><h3>${item.title}</h3></div>
        <div class="card-body">
        <p>${item.description}</p>
        <p class="date">${dateText}</p>
        <a href="${item.downloadUrl}" target="_blank" class="btn download-btn">${item.type === 'executor' ? 'Baixar APK' : 'Baixar Script'}</a>
        <div class="card-actions">
            <button class="btn btn-warning btn-small edit-btn" data-id="${item.id}">Editar</button>
        </div>
        </div>
    `;
    card.querySelector('.edit-btn').addEventListener('click', () => showEditForm(item.id));
    return card;
}

function showEditForm(id) {
    const item = publishedItems.find(i => i.id === id);
    if (!item) return;
    document.getElementById('edit-id').value = id;
    document.getElementById('edit-title').value = item.title;
    document.getElementById('edit-description').value = item.description;
    document.getElementById('edit-type').value = item.type;
    document.getElementById('edit-download-url').value = item.downloadUrl;

    uploadFormContainer.classList.add('hidden');
    editFormContainer.classList.remove('hidden');
    editFormContainer.scrollIntoView({ behavior: 'smooth' });
}

function cancelEdit() {
    editFormContainer.classList.add('hidden');
    uploadFormContainer.classList.remove('hidden');
    editForm.reset();
}

function showAlert(msg, error = false) {
    uploadMessage.textContent = msg;
    uploadMessage.className = error ? 'alert alert-error' : 'alert alert-success';
    uploadMessage.classList.remove('hidden');
    setTimeout(() => uploadMessage.classList.add('hidden'), 4000);
}

// ================= TRATAMENTO DE ERRO 404 =================
function checkPageNotFound() {
    // Lista de paths válidos para o site
    const validPaths = ['/', '/index.html', ''];
    const currentPath = window.location.pathname;
    
    // Verifica se é uma página do próprio site (âncora)
    const isAnchorLink = currentPath === '/' && window.location.hash;
    
    // Se não for um path válido e não for um link âncora, mostra erro 404
    if (!validPaths.includes(currentPath) && !isAnchorLink) {
        showErrorPage();
        return true;
    }
    return false;
}

function showErrorPage() {
    mainContent.style.display = 'none';
    errorPage.style.display = 'flex';
    // Atualiza o título da página
    document.title = 'Página Não Encontrada - Executores e Scripts';
}

function hideErrorPage() {
    errorPage.style.display = 'none';
    mainContent.style.display = 'block';
    // Restaura o título original
    document.title = 'Executores e Scripts - Sistema Completo';
    // Corrige a URL na barra de endereços
    window.history.replaceState({}, document.title, window.location.origin + '/');
}

// ================= EVENTOS =================
authForm.addEventListener('submit', e => {
    e.preventDefault();
    if (accessCodeInput.value.trim() === SECRET_CODE) {
        localStorage.setItem('authenticated', 'true');
        showUploadSection();
        authMessage.classList.add('hidden');
    } else {
        authMessage.textContent = 'Código de acesso incorreto. Tente novamente.';
        authMessage.classList.remove('hidden');
        accessCodeInput.value = '';
    }
});

logoutBtn.addEventListener('click', e => { 
    e.preventDefault(); 
    hideUploadSection(); 
});

logoutAdminBtn.addEventListener('click', hideUploadSection);

uploadForm.addEventListener('submit', e => {
    e.preventDefault();
    const title = document.getElementById('title').value.trim();
    const description = document.getElementById('description').value.trim();
    const type = document.getElementById('type').value;
    const downloadUrl = document.getElementById('download-url').value.trim();
    if (!title || !description || !type || !downloadUrl) { 
        showAlert('Preencha todos os campos', true); 
        return; 
    }

    const newItem = { 
        id: Date.now(), 
        title, 
        description, 
        type, 
        downloadUrl, 
        date: new Date().toLocaleDateString('pt-BR') 
    };
    publishedItems.push(newItem);
    saveItems();
    displayPublishedItems();
    uploadForm.reset();
    showAlert('Conteúdo publicado com sucesso!');
});

editForm.addEventListener('submit', e => {
    e.preventDefault();
    const id = parseInt(document.getElementById('edit-id').value);
    const item = publishedItems.find(i => i.id === id);
    if (!item) return;

    item.title = document.getElementById('edit-title').value.trim();
    item.description = document.getElementById('edit-description').value.trim();
    item.type = document.getElementById('edit-type').value;
    item.downloadUrl = document.getElementById('edit-download-url').value.trim();
    item.lastUpdate = new Date().toLocaleDateString('pt-BR');

    saveItems();
    displayPublishedItems();
    cancelEdit();
    showAlert('Conteúdo atualizado com sucesso!');
});

cancelEditBtn.addEventListener('click', cancelEdit);

addItemBtn.addEventListener('click', () => {
    cancelEdit();
    uploadFormContainer.scrollIntoView({ behavior: 'smooth' });
});

// Evento para o botão de redirecionamento da página 404
homeRedirect.addEventListener('click', (e) => {
    e.preventDefault();
    hideErrorPage();
});

// ================= INICIALIZAÇÃO =================
document.addEventListener('DOMContentLoaded', () => {
    // Verifica se deve mostrar página 404
    const isNotFound = checkPageNotFound();
    
    // Só inicializa o app principal se não for uma página 404
    if (!isNotFound) {
        checkAuthStatus();
        displayPublishedItems();
        
        // Suaviza o scroll para links âncora
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
      
