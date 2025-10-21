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
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
            line-height: 1.6;
        }
        
        header {
            background: linear-gradient(135deg, #1a2a6c 0%, #2a3c7a 100%);
            color: white;
            padding: 1rem 0;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        
        .container {
            width: 90%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 15px;
        }
        
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            font-size: 1.8rem;
            font-weight: bold;
        }
        
        nav ul {
            display: flex;
            list-style: none;
        }
        
        nav ul li {
            margin-left: 20px;
        }
        
        nav ul li a {
            color: white;
            text-decoration: none;
            font-weight: 500;
            transition: opacity 0.3s;
        }
        
        nav ul li a:hover {
            opacity: 0.8;
        }
        
        .hero {
            background-color: #fff;
            padding: 3rem 0;
            text-align: center;
            margin-bottom: 2rem;
            border-radius: 0 0 10px 10px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
        }
        
        .hero h1 {
            font-size: 2.5rem;
            margin-bottom: 1rem;
            color: #333;
        }
        
        .hero p {
            font-size: 1.1rem;
            max-width: 700px;
            margin: 0 auto;
            color: #666;
        }
        
        .section-title {
            text-align: center;
            margin: 2rem 0;
            color: #333;
            position: relative;
        }
        
        .section-title:after {
            content: '';
            display: block;
            width: 80px;
            height: 3px;
            background: linear-gradient(135deg, #1a2a6c 0%, #2a3c7a 100%);
            margin: 10px auto;
        }
        
        .content-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 2rem;
            margin-bottom: 3rem;
        }
        
        .card {
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s, box-shadow 0.3s;
            position: relative;
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
        }
        
        .card-header {
            padding: 1.5rem;
            background: linear-gradient(135deg, #1a2a6c 0%, #2a3c7a 100%);
            color: white;
        }
        
        .card-body {
            padding: 1.5rem;
        }
        
        .card h3 {
            margin-bottom: 0.5rem;
            font-size: 1.3rem;
        }
        
        .card p {
            color: #666;
            margin-bottom: 1rem;
        }
        
        .card .date {
            font-size: 0.8rem;
            color: #888;
            margin-bottom: 1rem;
        }
        
        .card-actions {
            display: flex;
            gap: 0.5rem;
            margin-top: 1rem;
        }
        
        .btn {
            display: inline-block;
            background: linear-gradient(135deg, #1a2a6c 0%, #2a3c7a 100%);
            color: white;
            padding: 0.7rem 1.5rem;
            border-radius: 5px;
            text-decoration: none;
            font-weight: 500;
            transition: opacity 0.3s;
            border: none;
            cursor: pointer;
            text-align: center;
        }
        
        .btn:hover {
            opacity: 0.9;
        }
        
        .btn-outline {
            background: transparent;
            border: 2px solid #1a2a6c;
            color: #1a2a6c;
        }
        
        .btn-outline:hover {
            background: #1a2a6c;
            color: white;
        }
        
        .btn-danger {
            background: linear-gradient(135deg, #c31432 0%, #c7364d 100%);
        }
        
        .btn-warning {
            background: linear-gradient(135deg, #ff8c00 0%, #ffa500 100%);
        }
        
        .btn-small {
            padding: 0.4rem 0.8rem;
            font-size: 0.8rem;
        }
        
        footer {
            background-color: #333;
            color: white;
            padding: 2rem 0;
            text-align: center;
            margin-top: 3rem;
        }
        
        .footer-content {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .footer-links {
            display: flex;
            margin: 1rem 0;
        }
        
        .footer-links a {
            color: white;
            margin: 0 10px;
            text-decoration: none;
        }
        
        .footer-links a:hover {
            text-decoration: underline;
        }
        
        .copyright {
            margin-top: 1rem;
            font-size: 0.9rem;
            color: #ccc;
        }
        
        .upload-section {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            margin-bottom: 3rem;
        }
        
        .upload-form {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }
        
        .form-group {
            display: flex;
            flex-direction: column;
        }
        
        .form-group label {
            margin-bottom: 0.5rem;
            font-weight: 500;
        }
        
        .form-group input, .form-group select, .form-group textarea {
            padding: 0.7rem;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
        }
        
        .form-group textarea {
            min-height: 100px;
            resize: vertical;
        }
        
        .file-upload {
            border: 2px dashed #ddd;
            padding: 1.5rem;
            text-align: center;
            border-radius: 5px;
            cursor: pointer;
            transition: border-color 0.3s;
        }
        
        .file-upload:hover {
            border-color: #1a2a6c;
        }
        
        .file-upload p {
            color: #666;
        }
        
        .auth-section {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            margin-bottom: 3rem;
            max-width: 500px;
            margin-left: auto;
            margin-right: auto;
        }
        
        .auth-form {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }
        
        .hidden {
            display: none;
        }
        
        .admin-controls {
            display: flex;
            justify-content: space-between;
            margin-bottom: 1rem;
        }
        
        .alert {
            padding: 1rem;
            border-radius: 5px;
            margin-bottom: 1rem;
        }
        
        .alert-success {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        
        .alert-error {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
        
        .empty-message {
            text-align: center;
            padding: 2rem;
            color: #666;
            font-style: italic;
        }
        
        .edit-form {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            margin-bottom: 2rem;
        }
        
        .form-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }
        
        .download-btn {
            display: block;
            width: 100%;
            margin-bottom: 1rem;
        }
        
        .file-info {
            background: #f8f9fa;
            padding: 0.5rem;
            border-radius: 5px;
            margin-top: 0.5rem;
            font-size: 0.9rem;
        }
        
        .url-input {
            margin-top: 0.5rem;
        }
        
        @media (max-width: 768px) {
            .header-content {
                flex-direction: column;
                text-align: center;
            }
            
            nav ul {
                margin-top: 1rem;
                justify-content: center;
            }
            
            nav ul li {
                margin: 0 10px;
            }
            
            .content-grid {
                grid-template-columns: 1fr;
            }
            
            .admin-controls {
                flex-direction: column;
                gap: 1rem;
            }
            
            .card-actions {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
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
            <div class="content-grid" id="executors-grid">
                <!-- Conteúdo será carregado dinamicamente -->
            </div>
        </section>

        <section id="scripts">
            <h2 class="section-title">Scripts</h2>
            <div class="content-grid" id="scripts-grid">
                <!-- Conteúdo será carregado dinamicamente -->
            </div>
        </section>

        <!-- Área de Autenticação -->
        <section id="auth">
            <h2 class="section-title">Acesso Restrito</h2>
            <div class="auth-section">
                <div id="auth-message" class="alert alert-error hidden">
                    Código de acesso incorreto. Tente novamente.
                </div>
                <form class="auth-form" id="auth-form">
                    <div class="form-group">
                        <label for="access-code">Código de Acesso</label>
                        <input type="password" id="access-code" placeholder="Digite o código secreto" required>
                    </div>
                    <button type="submit" class="btn">Acessar Área de Publicação</button>
                </form>
            </div>
        </section>

        <!-- Área de Upload (inicialmente oculta) -->
        <section id="upload" class="hidden">
            <h2 class="section-title">Publicar Conteúdo</h2>
            
            <div class="admin-controls">
                <button id="add-item-btn" class="btn">Adicionar Novo Item</button>
                <button id="logout-admin" class="btn btn-danger">Sair da Área Admin</button>
            </div>
            
            <div id="upload-message" class="alert alert-success hidden">
                Conteúdo publicado com sucesso!
            </div>
            
            <!-- Formulário de Edição (inicialmente oculto) -->
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
                    &copy; 2023 Executores & Scripts. Área administrativa protegida.
                </div>
            </div>
        </div>
    </footer>

    <script>
        // Código secreto - Altere para o código que desejar
        const SECRET_CODE = "admin123";
        
        // Elementos da interface
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
        
        // Array para armazenar os itens publicados
        let publishedItems = JSON.parse(localStorage.getItem('publishedItems')) || [];
        
        // Verificar se o usuário já está autenticado
        function checkAuthStatus() {
            const isAuthenticated = localStorage.getItem('authenticated') === 'true';
            if (isAuthenticated) {
                showUploadSection();
            }
        }
        
        // Mostrar a seção de upload
        function showUploadSection() {
            authSection.classList.add('hidden');
            uploadSection.classList.remove('hidden');
            logoutBtn.classList.remove('hidden');
        }
        
        // Esconder a seção de upload
        function hideUploadSection() {
            authSection.classList.remove('hidden');
            uploadSection.classList.add('hidden');
            logoutBtn.classList.add('hidden');
            localStorage.removeItem('authenticated');
        }
        
        // Adicionar item publicado na lista
        function addPublishedItem(title, description, type, downloadUrl) {
            const newItem = {
                id: Date.now(),
                title,
                description,
                type,
                downloadUrl,
                date: new Date().toLocaleDateString('pt-BR'),
                lastUpdate: new Date().toLocaleDateString('pt-BR')
            };
            
            publishedItems.push(newItem);
            localStorage.setItem('publishedItems', JSON.stringify(publishedItems));
            
            // Atualizar a exibição
            displayPublishedItems();
        }
        
        // Atualizar item existente
        function updatePublishedItem(id, title, description, type, downloadUrl) {
            const itemIndex = publishedItems.findIndex(item => item.id === id);
            if (itemIndex !== -1) {
                publishedItems[itemIndex].title = title;
                publishedItems[itemIndex].description = description;
                publishedItems[itemIndex].type = type;
                publishedItems[itemIndex].downloadUrl = downloadUrl;
                publishedItems[itemIndex].lastUpdate = new Date().toLocaleDateString('pt-BR');
                
                localStorage.setItem('publishedItems', JSON.stringify(publishedItems));
                displayPublishedItems();
                return true;
            }
            return false;
        }
        
        // Exibir itens publicados
        function displayPublishedItems() {
            // Limpar grids
            executorsGrid.innerHTML = '';
            scriptsGrid.innerHTML = '';
            
            // Filtrar e exibir executores
            const executors = publishedItems.filter(item => item.type === 'executor');
            if (executors.length > 0) {
                executors.forEach(item => {
                    const card = createItemCard(item);
                    executorsGrid.appendChild(card);
                });
            } else {
                executorsGrid.innerHTML = '<div class="empty-message">Nenhum executor publicado ainda.</div>';
            }
            
            // Filtrar e exibir scripts
            const scripts = publishedItems.filter(item => item.type === 'script');
            if (scripts.length > 0) {
                scripts.forEach(item => {
                    const card = createItemCard(item);
                    scriptsGrid.appendChild(card);
                });
            } else {
                scriptsGrid.innerHTML = '<div class="empty-message">Nenhum script publicado ainda.</div>';
            }
        }
        
        // Criar card para item
        function createItemCard(item) {
            const card = document.createElement('div');
            card.className = 'card';
            
            // Verificar se é uma edição recente
            const isUpdated = item.lastUpdate !== item.date;
            const dateText = isUpdated ? 
                `Atualizado em: ${item.lastUpdate}` : 
                `Publicado em: ${item.date}`;
            
            card.innerHTML = `
                <div class="card-header">
                    <h3>${item.title}</h3>
                </div>
                <div class="card-body">
                    <p>${item.description}</p>
                    <p class="date">${dateText}</p>
                    <a href="${item.downloadUrl}" target="_blank" class="btn download-btn">
                        ${item.type === 'executor' ? 'Baixar APK' : 'Baixar Script'}
                    </a>
                    <div class="card-actions">
                        <button class="btn btn-warning btn-small edit-btn" data-id="${item.id}">Editar</button>
                    </div>
                </div>
            `;
            
            // Adicionar evento ao botão de editar
            const editBtn = card.querySelector('.edit-btn');
            
            editBtn.addEventListener('click', function() {
                showEditForm(item.id);
            });
            
            return card;
        }
        
        // Mostrar formulário de edição
        function showEditForm(itemId) {
            const item = publishedItems.find(item => item.id === itemId);
            if (item) {
                // Preencher formulário de edição
                document.getElementById('edit-id').value = item.id;
                document.getElementById('edit-title').value = item.title;
                document.getElementById('edit-description').value = item.description;
                document.getElementById('edit-type').value = item.type;
                document.getElementById('edit-download-url').value = item.downloadUrl;
                
                // Mostrar formulário de edição e ocultar o de publicação
                uploadFormContainer.classList.add('hidden');
                editFormContainer.classList.remove('hidden');
                
                // Rolar para o formulário de edição
                editFormContainer.scrollIntoView({ behavior: 'smooth' });
            }
        }
        
        // Cancelar edição
        function cancelEdit() {
            editFormContainer.classList.add('hidden');
            uploadFormContainer.classList.remove('hidden');
            editForm.reset();
        }
        
        // Processar autenticação
        authForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            const enteredCode = accessCodeInput.value.trim();
            
            if (enteredCode === SECRET_CODE) {
                // Código correto
                localStorage.setItem('authenticated', 'true');
                showUploadSection();
                authMessage.classList.add('hidden');
            } else {
                // Código incorreto
                authMessage.classList.remove('hidden');
                authMessage.textContent = 'Código de acesso incorreto. Tente novamente.';
                accessCodeInput.value = '';
            }
        });
        
        // Processar logout
        logoutBtn.addEventListener('click', function(e) {
            e.preventDefault();
            hideUploadSection();
        });
        
        logoutAdminBtn.addEventListener('click', function() {
            hideUploadSection();
        });
        
        // Processar envio do formulário de upload
        uploadForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Validar formulário
            const title = document.getElementById('title').value;
            const description = document.getElementById('description').value;
            const type = document.getElementById('type').value;
            const downloadUrl = document.getElementById('download-url').value;
            
            if (!title || !description || type === "" || !downloadUrl) {
                uploadMessage.textContent = 'Por favor, preencha todos os campos!';
                uploadMessage.classList.remove('alert-success');
                uploadMessage.classList.add('alert-error');
                uploadMessage.classList.remove('hidden');
                return;
            }
            
            // Validar URL
            try {
                new URL(downloadUrl);
            } catch (e) {
                uploadMessage.textContent = 'Por favor, insira uma URL válida!';
                uploadMessage.classList.remove('alert-success');
                uploadMessage.classList.add('alert-error');
                uploadMessage.classList.remove('hidden');
                return;
            }
            
            // Adicionar item publicado
            addPublishedItem(title, description, type, downloadUrl);
            
            // Mensagem de sucesso
            uploadMessage.textContent = 'Conteúdo publicado com sucesso!';
            uploadMessage.classList.remove('alert-error');
            uploadMessage.classList.add('alert-success');
            uploadMessage.classList.remove('hidden');
            
            // Limpar formulário
            uploadForm.reset();
            
            // Ocultar mensagem após 3 segundos
            setTimeout(() => {
                uploadMessage.classList.add('hidden');
            }, 3000);
        });
        
        // Processar envio do formulário de edição
        editForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Validar formulário
            const id = parseInt(document.getElementById('edit-id').value);
            const title = document.getElementById('edit-title').value;
            const description = document.getElementById('edit-description').value;
            const type = document.getElementById('edit-type').value;
            const downloadUrl = document.getElementById('edit-download-url').value;
            
            if (!title || !description || type === "" || !downloadUrl) {
                uploadMessage.textContent = 'Por favor, preencha todos os campos!';
                uploadMessage.classList.remove('alert-success');
                uploadMessage.classList.add('alert-error');
                uploadMessage.classList.remove('hidden');
                return;
            }
            
            // Validar URL
            try {
                new URL(downloadUrl);
            } catch (e) {
                uploadMessage.textContent = 'Por favor, insira uma URL válida!';
                uploadMessage.classList.remove('alert-success');
                uploadMessage.classList.add('alert-error');
                uploadMessage.classList.remove('hidden');
                return;
            }
            
            // Atualizar item
            if (updatePublishedItem(id, title, description, type, downloadUrl)) {
                // Mensagem de sucesso
                uploadMessage.textContent = 'Conteúdo atualizado com sucesso!';
                uploadMessage.classList.remove('alert-error');
                uploadMessage.classList.add('alert-success');
                uploadMessage.classList.remove('hidden');
                
                // Voltar para o formulário de publicação
                cancelEdit();
                
                // Ocultar mensagem após 3 segundos
                setTimeout(() => {
                    uploadMessage.classList.add('hidden');
                }, 3000);
            }
        });
        
        // Adicionar novo item
        addItemBtn.addEventListener('click', function() {
            uploadForm.reset();
            uploadMessage.classList.add('hidden');
            
            // Garantir que o formulário de publicação esteja visível
            uploadFormContainer.classList.remove('hidden');
            editFormContainer.classList.add('hidden');
        });
        
        // Cancelar edição
        cancelEditBtn.addEventListener('click', function() {
            cancelEdit();
        });
        
        // Verificar status de autenticação ao carregar a página
        document.addEventListener('DOMContentLoaded', function() {
            checkAuthStatus();
            displayPublishedItems();
        });
    </script>
</body>
</html>
