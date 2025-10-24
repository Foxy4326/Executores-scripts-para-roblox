<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Executores e Scripts - Sistema Completo</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .hidden {
            display: none !important;
        }
        
        /* Header e Navegação */
        .hero {
            text-align: center;
            padding: 60px 20px;
            color: white;
        }
        
        .hero h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .hero p {
            font-size: 1.2rem;
            margin-bottom: 2rem;
            opacity: 0.9;
        }
        
        /* Seções */
        .section {
            background: white;
            margin: 30px 0;
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }
        
        .section h2 {
            color: #4a5568;
            margin-bottom: 30px;
            font-size: 2rem;
            border-bottom: 3px solid #667eea;
            padding-bottom: 10px;
        }
        
        /* Grid de Cards */
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 25px;
            margin-top: 20px;
        }
        
        .card {
            background: #f8f9fa;
            border: 1px solid #e9ecef;
            border-radius: 12px;
            padding: 25px;
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.15);
        }
        
        .card-header h3 {
            color: #2d3748;
            margin-bottom: 15px;
            font-size: 1.3rem;
        }
        
        .card-body p {
            color: #4a5568;
            margin-bottom: 15px;
            line-height: 1.5;
        }
        
        .date {
            color: #718096 !important;
            font-size: 0.9rem;
            font-style: italic;
        }
        
        .card-actions {
            margin-top: 20px;
            display: flex;
            gap: 10px;
        }
        
        /* Formulários */
        .auth-section {
            background: white;
            margin: 50px auto;
            padding: 50px;
            border-radius: 15px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            max-width: 400px;
            text-align: center;
        }
        
        .auth-section h1 {
            color: #4a5568;
            margin-bottom: 30px;
        }
        
        .auth-form {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        
        .upload-section {
            background: white;
            margin: 30px 0;
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }
        
        .upload-form {
            display: flex;
            flex-direction: column;
            gap: 20px;
            max-width: 600px;
        }
        
        .form-actions {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }
        
        /* Inputs */
        input, textarea, select {
            padding: 15px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }
        
        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: #667eea;
        }
        
        textarea {
            min-height: 100px;
            resize: vertical;
        }
        
        /* Botões */
        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            text-decoration: none;
            display: inline-block;
            text-align: center;
        }
        
        .btn-primary {
            background: #667eea;
            color: white;
        }
        
        .btn-primary:hover {
            background: #5a6fd8;
            transform: translateY(-2px);
        }
        
        .btn-success {
            background: #48bb78;
            color: white;
        }
        
        .btn-success:hover {
            background: #3fa76c;
            transform: translateY(-2px);
        }
        
        .btn-warning {
            background: #ed8936;
            color: white;
        }
        
        .btn-warning:hover {
            background: #e37820;
        }
        
        .btn-danger {
            background: #f56565;
            color: white;
        }
        
        .btn-danger:hover {
            background: #e53e3e;
        }
        
        .btn-secondary {
            background: #a0aec0;
            color: white;
        }
        
        .btn-secondary:hover {
            background: #9099a6;
        }
        
        .btn-outline {
            background: transparent;
            color: white;
            border: 2px solid white;
        }
        
        .btn-outline:hover {
            background: white;
            color: #667eea;
        }
        
        .btn-small {
            padding: 8px 15px;
            font-size: 0.9rem;
        }
        
        .download-btn {
            background: #4299e1;
            color: white;
            width: 100%;
            margin-top: 10px;
        }
        
        .download-btn:hover {
            background: #3182ce;
        }
        
        /* Alertas */
        .alert {
            padding: 15px;
            border-radius: 8px;
            margin: 20px 0;
            font-weight: 500;
        }
        
        .alert-error {
            background: #fed7d7;
            color: #c53030;
            border: 1px solid #feb2b2;
        }
        
        .alert-success {
            background: #c6f6d5;
            color: #276749;
            border: 1px solid #9ae6b4;
        }
        
        /* Mensagens vazias */
        .empty-message {
            text-align: center;
            color: #718096;
            font-style: italic;
            padding: 40px;
            grid-column: 1 / -1;
        }
        
        /* Botão de logout admin */
        .logout-admin-btn {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 1000;
        }
        
        /* Página de erro */
        .error-page {
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            text-align: center;
            color: white;
        }
        
        .error-content h1 {
            font-size: 4rem;
            margin-bottom: 1rem;
        }
        
        .error-content p {
            font-size: 1.2rem;
            margin-bottom: 2rem;
            opacity: 0.9;
        }
        
        /* Responsivo */
        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .hero h1 {
                font-size: 2rem;
            }
            
            .section {
                padding: 25px;
                margin: 20px 0;
            }
            
            .grid {
                grid-template-columns: 1fr;
            }
            
            .auth-section {
                margin: 20px;
                padding: 30px;
            }
            
            .upload-section {
                padding: 25px;
            }
            
            .form-actions {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Seção de Autenticação -->
        <section id="auth" class="auth-section">
            <div class="auth-container">
                <h1>Acesso Administrativo</h1>
                <form id="auth-form" class="auth-form">
                    <input type="password" id="access-code" placeholder="Digite o código de acesso" required>
                    <button type="submit" class="btn btn-primary">Acessar</button>
                </form>
                <div id="auth-message" class="alert alert-error hidden"></div>
            </div>
        </section>

        <!-- Seção de Upload (inicialmente hidden) -->
        <section id="upload" class="upload-section hidden">
            <h2>Publicar Novo Conteúdo</h2>
            <div id="upload-form-container">
                <form id="upload-form" class="upload-form">
                    <input type="text" id="title" placeholder="Título" required>
                    <textarea id="description" placeholder="Descrição" required></textarea>
                    <select id="type" required>
                        <option value="">Selecione o tipo</option>
                        <option value="executor">Executor</option>
                        <option value="script">Script</option>
                    </select>
                    <input type="url" id="download-url" placeholder="URL de Download" required>
                    <button type="submit" class="btn btn-success">Publicar</button>
                </form>
            </div>
            
            <div id="edit-form-container" class="hidden">
                <form id="edit-form" class="upload-form">
                    <input type="hidden" id="edit-id">
                    <input type="text" id="edit-title" placeholder="Título" required>
                    <textarea id="edit-description" placeholder="Descrição" required></textarea>
                    <select id="edit-type" required>
                        <option value="executor">Executor</option>
                        <option value="script">Script</option>
                    </select>
                    <input type="url" id="edit-download-url" placeholder="URL de Download" required>
                    <div class="form-actions">
                        <button type="submit" class="btn btn-success">Atualizar</button>
                        <button type="button" id="cancel-edit-btn" class="btn btn-secondary">Cancelar</button>
                    </div>
                </form>
            </div>
            
            <div id="upload-message" class="alert hidden"></div>
            <button id="add-item-btn" class="btn btn-primary">Adicionar Novo Item</button>
        </section>

        <!-- Conteúdo Principal -->
        <main id="main-content">
            <header class="hero">
                <h1>Executores e Scripts</h1>
                <p>Encontre os melhores executores e scripts em um só lugar</p>
                <button id="logout-btn" class="btn btn-outline hidden">Sair do Admin</button>
            </header>

            <!-- Seção de Executores -->
            <section id="executors" class="section">
                <h2>Executores Disponíveis</h2>
                <div id="executors-grid" class="grid"></div>
            </section>

            <!-- Seção de Scripts -->
            <section id="scripts" class="section">
                <h2>Scripts Disponíveis</h2>
                <div id="scripts-grid" class="grid"></div>
            </section>
        </main>

        <!-- Página de Erro 404 -->
        <div id="error-page" class="error-page hidden">
            <div class="error-content">
                <h1>404 - Página Não Encontrada</h1>
                <p>A página que você está procurando não existe.</p>
                <a href="#" id="home-redirect" class="btn btn-primary">Voltar para Home</a>
            </div>
        </div>
    </div>

    <!-- BOTÃO DE LOGOUT ADMIN (fixo) -->
    <button id="logout-admin" class="logout-admin-btn btn btn-danger hidden">Sair</button>

    <script>
    // ================= CONFIGURAÇÃO =================
    const SECRET_CODE = "admin123";

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
        if (authSection) authSection.classList.add('hidden');
        if (uploadSection) uploadSection.classList.remove('hidden');
        if (logoutBtn) logoutBtn.classList.remove('hidden');
        if (logoutAdminBtn) logoutAdminBtn.classList.remove('hidden');
    }

    function hideUploadSection() {
        if (authSection) authSection.classList.remove('hidden');
        if (uploadSection) uploadSection.classList.add('hidden');
        if (logoutBtn) logoutBtn.classList.add('hidden');
        if (logoutAdminBtn) logoutAdminBtn.classList.add('hidden');
        localStorage.removeItem('authenticated');
    }

    function displayPublishedItems() {
        if (executorsGrid) {
            executorsGrid.innerHTML = '';
            const executors = publishedItems.filter(i => i.type === 'executor');
            if (executors.length) executors.forEach(i => executorsGrid.appendChild(createCard(i)));
            else executorsGrid.innerHTML = '<div class="empty-message">Nenhum executor publicado ainda.</div>';
        }

        if (scriptsGrid) {
            scriptsGrid.innerHTML = '';
            const scripts = publishedItems.filter(i => i.type === 'script');
            if (scripts.length) scripts.forEach(i => scriptsGrid.appendChild(createCard(i)));
            else scriptsGrid.innerHTML = '<div class="empty-message">Nenhum script publicado ainda.</div>';
        }
    }

    function createCard(item) {
        const card = document.createElement('div');
        card.className = 'card';
        const dateText = item.lastUpdate ? `Atualizado em: ${item.lastUpdate}` : `Publicado em: ${item.date || new Date().toLocaleDateString('pt-BR')}`;
        
        const adminButtons = localStorage.getItem('authenticated') === 'true' ? `
            <div class="card-actions">
                <button class="btn btn-warning btn-small edit-btn" data-id="${item.id}">Editar</button>
                <button class="btn btn-danger btn-small delete-btn" data-id="${item.id}">Excluir</button>
            </div>
        ` : '';

        card.innerHTML = `
            <div class="card-header"><h3>${item.title}</h3></div>
            <div class="card-body">
                <p>${item.description}</p>
                <p class="date">${dateText}</p>
                <a href="${item.downloadUrl}" target="_blank" class="btn download-btn">${item.type === 'executor' ? 'Baixar APK' : 'Baixar Script'}</a>
                ${adminButtons}
            </div>
        `;

        if (localStorage.getItem('authenticated') === 'true') {
            const editBtn = card.querySelector('.edit-btn');
            const deleteBtn = card.querySelector('.delete-btn');
            if (editBtn) editBtn.addEventListener('click', () => showEditForm(item.id));
            if (deleteBtn) deleteBtn.addEventListener('click', () => deleteItem(item.id));
        }
        
        return card;
    }

    function deleteItem(id) {
        if (confirm('Tem certeza que deseja excluir este item?')) {
            publishedItems = publishedItems.filter(i => i.id !== id);
            saveItems();
            displayPublishedItems();
            showAlert('Item excluído com sucesso.');
        }
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
        if (uploadMessage) {
            uploadMessage.textContent = msg;
            uploadMessage.className = error ? 'alert alert-error' : 'alert alert-success';
            uploadMessage.classList.remove('hidden');
            setTimeout(() => uploadMessage.classList.add('hidden'), 4000);
        }
    }

    function handleLogout() {
        hideUploadSection();
        displayPublishedItems();
    }

    // ================= EVENT LISTENERS =================
    function initializeEventListeners() {
        if (authForm) {
            authForm.addEventListener('submit', e => {
                e.preventDefault();
                if (accessCodeInput.value.trim() === SECRET_CODE) {
                    localStorage.setItem('authenticated', 'true');
                    showUploadSection();
                    authMessage.classList.add('hidden');
                    displayPublishedItems();
                } else {
                    authMessage.textContent = 'Código de acesso incorreto. Tente novamente.';
                    authMessage.classList.remove('hidden');
                    accessCodeInput.value = '';
                }
            });
        }

        if (logoutBtn) {
            logoutBtn.addEventListener('click', e => { 
                e.preventDefault(); 
                handleLogout();
            });
        }

        if (logoutAdminBtn) {
            logoutAdminBtn.addEventListener('click', handleLogout);
        }

        if (uploadForm) {
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
        }

        if (editForm) {
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
        }

        if (cancelEditBtn) {
            cancelEditBtn.addEventListener('click', cancelEdit);
        }

        if (addItemBtn) {
            addItemBtn.addEventListener('click', () => {
                cancelEdit();
                uploadFormContainer.scrollIntoView({ behavior: 'smooth' });
            });
        }

        if (homeRedirect) {
            homeRedirect.addEventListener('click', (e) => {
                e.preventDefault();
                errorPage.classList.add('hidden');
                mainContent.style.display = 'block';
            });
        }

        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const targetId = this.getAttribute('href');
                const targetElement = document.querySelector(targetId);
                if (targetElement) {
                    targetElement.scrollIntoView({ behavior: 'smooth' });
                }
            });
        });
    }

    // ================= INICIALIZAÇÃO =================
    document.addEventListener('DOMContentLoaded', () => {
        checkAuthStatus();
        displayPublishedItems();
        initializeEventListeners();
    });
    </script>
</body>
</html>