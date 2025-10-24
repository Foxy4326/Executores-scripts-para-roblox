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
        
        .file-upload-container {
            display: flex;
            gap: 10px;
            align-items: center;
        }
        
        .file-upload-btn {
            background: #4299e1;
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 0.9rem;
        }
        
        .file-upload-btn:hover {
            background: #3182ce;
        }
        
        .file-name {
            color: #718096;
            font-size: 0.9rem;
        }
        
        .upload-type-selector {
            display: flex;
            gap: 15px;
            margin-bottom: 10px;
        }
        
        .upload-type-btn {
            flex: 1;
            padding: 12px;
            border: 2px solid #e2e8f0;
            background: white;
            border-radius: 8px;
            cursor: pointer;
            text-align: center;
            transition: all 0.3s ease;
        }
        
        .upload-type-btn.active {
            background: #667eea;
            color: white;
            border-color: #667eea;
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
        
        /* Progress Bar */
        .progress-container {
            width: 100%;
            background: #e2e8f0;
            border-radius: 10px;
            margin: 10px 0;
            display: none;
        }
        
        .progress-bar {
            height: 20px;
            background: #48bb78;
            border-radius: 10px;
            width: 0%;
            transition: width 0.3s ease;
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
            
            .upload-type-selector {
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
                    
                    <!-- Seletor de tipo de upload -->
                    <div class="upload-type-selector">
                        <button type="button" class="upload-type-btn active" data-type="url">URL/Link</button>
                        <button type="button" class="upload-type-btn" data-type="file">Arquivo APK</button>
                    </div>
                    
                    <!-- Campo para URL -->
                    <div id="url-field">
                        <input type="url" id="download-url" placeholder="https://exemplo.com/download" required>
                    </div>
                    
                    <!-- Campo para upload de arquivo -->
                    <div id="file-field" class="hidden">
                        <div class="file-upload-container">
                            <input type="file" id="file-upload" accept=".apk,.apks" class="hidden">
                            <button type="button" id="file-select-btn" class="file-upload-btn">Selecionar APK</button>
                            <span id="file-name" class="file-name">Nenhum arquivo selecionado</span>
                        </div>
                        <div id="progress-container" class="progress-container">
                            <div id="progress-bar" class="progress-bar"></div>
                        </div>
                        <small style="color: #718096; font-size: 0.8rem;">
                            ✅ Agora aceita APKs de qualquer tamanho! Os arquivos são salvos no navegador.
                        </small>
                    </div>
                    
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
                    
                    <div class="upload-type-selector">
                        <button type="button" class="upload-type-btn active" data-type="url">URL/Link</button>
                        <button type="button" class="upload-type-btn" data-type="file">Arquivo APK</button>
                    </div>
                    
                    <div id="edit-url-field">
                        <input type="url" id="edit-download-url" placeholder="URL de Download" required>
                    </div>
                    
                    <div id="edit-file-field" class="hidden">
                        <div class="file-upload-container">
                            <input type="file" id="edit-file-upload" accept=".apk,.apks" class="hidden">
                            <button type="button" id="edit-file-select-btn" class="file-upload-btn">Selecionar APK</button>
                            <span id="edit-file-name" class="file-name">Nenhum arquivo selecionado</span>
                        </div>
                        <div id="edit-progress-container" class="progress-container">
                            <div id="edit-progress-bar" class="progress-bar"></div>
                        </div>
                        <small style="color: #718096; font-size: 0.8rem;">
                            ✅ Agora aceita APKs de qualquer tamanho! Os arquivos são salvos no navegador.
                        </small>
                    </div>
                    
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
    </div>

    <!-- BOTÃO DE LOGOUT ADMIN (fixo) -->
    <button id="logout-admin" class="logout-admin-btn btn btn-danger hidden">Sair</button>

    <script>
    // ================= CONFIGURAÇÃO =================
    const SECRET_CODE = "admin123";
    let currentUploadType = 'url'; // 'url' ou 'file'

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

    // Elementos de upload de arquivo
    const fileUpload = document.getElementById('file-upload');
    const fileSelectBtn = document.getElementById('file-select-btn');
    const fileName = document.getElementById('file-name');
    const urlField = document.getElementById('url-field');
    const fileField = document.getElementById('file-field');
    const uploadTypeBtns = document.querySelectorAll('.upload-type-btn');
    const progressContainer = document.getElementById('progress-container');
    const progressBar = document.getElementById('progress-bar');

    // Elementos de edição de arquivo
    const editFileUpload = document.getElementById('edit-file-upload');
    const editFileSelectBtn = document.getElementById('edit-file-select-btn');
    const editFileName = document.getElementById('edit-file-name');
    const editUrlField = document.getElementById('edit-url-field');
    const editFileField = document.getElementById('edit-file-field');
    const editUploadTypeBtns = document.querySelectorAll('#edit-form-container .upload-type-btn');
    const editProgressContainer = document.getElementById('edit-progress-container');
    const editProgressBar = document.getElementById('edit-progress-bar');

    // ================= ARMAZENAMENTO =================
    let publishedItems = JSON.parse(localStorage.getItem('publishedItems')) || [];
    let fileStorage = JSON.parse(localStorage.getItem('fileStorage')) || {};

    // ================= FUNÇÕES DE UPLOAD =================
    function setUploadType(type) {
        currentUploadType = type;
        
        // Atualizar botões
        uploadTypeBtns.forEach(btn => {
            btn.classList.toggle('active', btn.dataset.type === type);
        });
        
        editUploadTypeBtns.forEach(btn => {
            btn.classList.toggle('active', btn.dataset.type === type);
        });
        
        // Mostrar/ocultar campos
        if (type === 'url') {
            urlField.classList.remove('hidden');
            fileField.classList.add('hidden');
            editUrlField.classList.remove('hidden');
            editFileField.classList.add('hidden');
        } else {
            urlField.classList.add('hidden');
            fileField.classList.remove('hidden');
            editUrlField.classList.add('hidden');
            editFileField.classList.remove('hidden');
        }
    }

    function handleFileSelect(fileInput, fileNameElement) {
        if (fileInput.files.length > 0) {
            const file = fileInput.files[0];
            fileNameElement.textContent = `${file.name} (${formatFileSize(file.size)})`;
            
            // Validar se é um arquivo APK
            if (!file.name.toLowerCase().endsWith('.apk') && !file.name.toLowerCase().endsWith('.apks')) {
                showAlert('Por favor, selecione um arquivo APK válido.', true);
                fileInput.value = '';
                fileNameElement.textContent = 'Nenhum arquivo selecionado';
                return false;
            }
            
            // REMOVIDA A VALIDAÇÃO DE TAMANHO - AGORA ACEITA QUALQUER TAMANHO
            console.log(`Arquivo selecionado: ${file.name} - Tamanho: ${formatFileSize(file.size)}`);
            
            return true;
        }
        return false;
    }

    function saveFileToStorage(file, progressBarElement = null, progressContainerElement = null) {
        return new Promise((resolve, reject) => {
            const reader = new FileReader();
            
            // Mostrar progresso se houver elemento de progresso
            if (progressContainerElement) {
                progressContainerElement.style.display = 'block';
            }
            
            reader.onprogress = function(e) {
                if (e.lengthComputable && progressBarElement) {
                    const percentComplete = (e.loaded / e.total) * 100;
                    progressBarElement.style.width = percentComplete + '%';
                }
            };
            
            reader.onload = function(e) {
                try {
                    const fileId = 'file_' + Date.now() + '_' + Math.random().toString(36).substr(2, 9);
                    const fileData = {
                        name: file.name,
                        type: file.type,
                        size: file.size,
                        data: e.target.result,
                        uploadDate: new Date().toISOString()
                    };
                    
                    fileStorage[fileId] = fileData;
                    localStorage.setItem('fileStorage', JSON.stringify(fileStorage));
                    
                    // Criar URL para download a partir dos dados
                    const blob = new Blob([new Uint8Array(e.target.result)], { type: file.type });
                    const downloadUrl = URL.createObjectURL(blob);
                    
                    // Esconder barra de progresso
                    if (progressContainerElement) {
                        progressContainerElement.style.display = 'none';
                        progressBarElement.style.width = '0%';
                    }
                    
                    resolve({ fileId, downloadUrl, fileName: file.name });
                } catch (error) {
                    // Esconder barra de progresso em caso de erro
                    if (progressContainerElement) {
                        progressContainerElement.style.display = 'none';
                        progressBarElement.style.width = '0%';
                    }
                    reject(error);
                }
            };
            
            reader.onerror = () => {
                // Esconder barra de progresso em caso de erro
                if (progressContainerElement) {
                    progressContainerElement.style.display = 'none';
                    progressBarElement.style.width = '0%';
                }
                reject(new Error('Erro ao ler o arquivo'));
            };
            
            reader.readAsArrayBuffer(file);
        });
    }

    function cleanupFileStorage() {
        // Limpar arquivos que não estão mais sendo usados
        const usedFileIds = new Set();
        publishedItems.forEach(item => {
            if (item.fileId) {
                usedFileIds.add(item.fileId);
            }
        });

        Object.keys(fileStorage).forEach(fileId => {
            if (!usedFileIds.has(fileId)) {
                delete fileStorage[fileId];
            }
        });

        localStorage.setItem('fileStorage', JSON.stringify(fileStorage));
    }

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
            if (executors.length) {
                executors.forEach(i => executorsGrid.appendChild(createCard(i)));
            } else {
                executorsGrid.innerHTML = '<div class="empty-message">Nenhum executor publicado ainda.</div>';
            }
        }

        if (scriptsGrid) {
            scriptsGrid.innerHTML = '';
            const scripts = publishedItems.filter(i => i.type === 'script');
            if (scripts.length) {
                scripts.forEach(i => scriptsGrid.appendChild(createCard(i)));
            } else {
                scriptsGrid.innerHTML = '<div class="empty-message">Nenhum script publicado ainda.</div>';
            }
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

        // Informações do arquivo
        const fileInfo = item.fileSize ? `
            <div style="font-size: 0.8rem; color: #718096; margin-top: 5px;">
                <div>Tamanho: ${formatFileSize(item.fileSize)}</div>
                <div>Nome: ${item.fileName}</div>
                ${item.downloadType === 'file' ? '<div>💾 Salvo localmente</div>' : ''}
            </div>
        ` : '';

        card.innerHTML = `
            <div class="card-header"><h3>${item.title}</h3></div>
            <div class="card-body">
                <p>${item.description}</p>
                <p class="date">${dateText}</p>
                ${fileInfo}
                <a href="${item.downloadUrl}" target="_blank" class="btn download-btn" download="${item.fileName || 'download'}">
                    ${item.type === 'executor' ? '📱 Baixar APK' : '📜 Baixar Script'}
                </a>
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

    function formatFileSize(bytes) {
        if (bytes === 0) return '0 Bytes';
        const k = 1024;
        const sizes = ['Bytes', 'KB', 'MB', 'GB'];
        const i = Math.floor(Math.log(bytes) / Math.log(k));
        return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
    }

    function deleteItem(id) {
        if (confirm('Tem certeza que deseja excluir este item?')) {
            const item = publishedItems.find(i => i.id === id);
            // Liberar URL do blob se for um arquivo
            if (item && item.fileId) {
                if (fileStorage[item.fileId]) {
                    delete fileStorage[item.fileId];
                }
            }
            
            publishedItems = publishedItems.filter(i => i.id !== id);
            saveItems();
            localStorage.setItem('fileStorage', JSON.stringify(fileStorage));
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

        // Definir tipo de upload baseado no item
        if (item.fileId) {
            setUploadType('file');
            editFileName.textContent = `${item.fileName} (${formatFileSize(item.fileSize)})`;
            document.getElementById('edit-download-url').value = '';
        } else {
            setUploadType('url');
            document.getElementById('edit-download-url').value = item.downloadUrl;
            editFileName.textContent = 'Nenhum arquivo selecionado';
        }

        uploadFormContainer.classList.add('hidden');
        editFormContainer.classList.remove('hidden');
        editFormContainer.scrollIntoView({ behavior: 'smooth' });
    }

    function cancelEdit() {
        editFormContainer.classList.add('hidden');
        uploadFormContainer.classList.remove('hidden');
        editForm.reset();
        setUploadType('url'); // Reset para URL por padrão
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
        // Eventos de tipo de upload
        uploadTypeBtns.forEach(btn => {
            btn.addEventListener('click', () => setUploadType(btn.dataset.type));
        });

        editUploadTypeBtns.forEach(btn => {
            btn.addEventListener('click', () => setUploadType(btn.dataset.type));
        });

        // Eventos de seleção de arquivo
        fileSelectBtn.addEventListener('click', () => fileUpload.click());
        fileUpload.addEventListener('change', () => handleFileSelect(fileUpload, fileName));

        editFileSelectBtn.addEventListener('click', () => editFileUpload.click());
        editFileUpload.addEventListener('change', () => handleFileSelect(editFileUpload, editFileName));

        // Autenticação
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

        // Logout
        if (logoutBtn) {
            logoutBtn.addEventListener('click', e => { 
                e.preventDefault(); 
                handleLogout();
            });
        }

        if (logoutAdminBtn) {
            logoutAdminBtn.addEventListener('click', handleLogout);
        }

        // Upload de conteúdo
        if (uploadForm) {
            uploadForm.addEventListener('submit', async e => {
                e.preventDefault();
                const title = document.getElementById('title').value.trim();
                const description = document.getElementById('description').value.trim();
                const type = document.getElementById('type').value;
                
                if (!title || !description || !type) { 
                    showAlert('Preencha todos os campos', true); 
                    return; 
                }

                let downloadUrl = '';
                let fileId = null;
                let fileNameText = '';
                let fileSize = 0;

                if (currentUploadType === 'url') {
                    downloadUrl = document.getElementById('download-url').value.trim();
                    if (!downloadUrl) {
                        showAlert('Informe a URL de download', true);
                        return;
                    }
                } else {
                    if (!handleFileSelect(fileUpload, fileName)) {
                        showAlert('Selecione um arquivo APK válido', true);
                        return;
                    }

                    try {
                        showAlert('Salvando arquivo... Isso pode demorar para arquivos grandes.', false);
                        const file = fileUpload.files[0];
                        const result = await saveFileToStorage(file, progressBar, progressContainer);
                        downloadUrl = result.downloadUrl;
                        fileId = result.fileId;
                        fileNameText = result.fileName;
                        fileSize = file.size;
                    } catch (error) {
                        showAlert('Erro ao salvar o arquivo: ' + error.message, true);
                        return;
                    }
                }

                const newItem = { 
                    id: Date.now(), 
                    title, 
                    description, 
                    type, 
                    downloadUrl, 
                    downloadType: currentUploadType,
                    fileId,
                    fileName: fileNameText,
                    fileSize,
                    date: new Date().toLocaleDateString('pt-BR') 
                };
                publishedItems.push(newItem);
                saveItems();
                displayPublishedItems();
                uploadForm.reset();
                fileName.textContent = 'Nenhum arquivo selecionado';
                setUploadType('url'); // Reset para URL
                showAlert('Conteúdo publicado com sucesso!');
            });
        }

        // Edição de conteúdo
        if (editForm) {
            editForm.addEventListener('submit', async e => {
                e.preventDefault();
                const id = parseInt(document.getElementById('edit-id').value);
                const item = publishedItems.find(i => i.id === id);
                if (!item) return;

                item.title = document.getElementById('edit-title').value.trim();
                item.description = document.getElementById('edit-description').value.trim();
                item.type = document.getElementById('edit-type').value;

                if (currentUploadType === 'url') {
                    // Se estava usando arquivo e mudou para URL, limpar dados do arquivo
                    if (item.fileId) {
                        delete fileStorage[item.fileId];
                        item.fileId = null;
                        item.fileName = '';
                        item.fileSize = 0;
                    }
                    item.downloadUrl = document.getElementById('edit-download-url').value.trim();
                    if (!item.downloadUrl) {
                        showAlert('Informe a URL de download', true);
                        return;
                    }
                } else {
                    if (editFileUpload.files.length > 0) {
                        try {
                            showAlert('Salvando novo arquivo... Isso pode demorar para arquivos grandes.', false);
                            const file = editFileUpload.files[0];
                            const result = await saveFileToStorage(file, editProgressBar, editProgressContainer);
                            
                            // Liberar arquivo anterior se existir
                            if (item.fileId && fileStorage[item.fileId]) {
                                delete fileStorage[item.fileId];
                            }
                            
                            item.downloadUrl = result.downloadUrl;
                            item.fileId = result.fileId;
                            item.fileName = result.fileName;
                            item.fileSize = file.size;
                        } catch (error) {
                            showAlert('Erro ao salvar o arquivo: ' + error.message, true);
                            return;
                        }
                    }
                    // Se não selecionou novo arquivo, mantém os dados atuais
                }

                item.downloadType = currentUploadType;
                item.lastUpdate = new Date().toLocaleDateString('pt-BR');

                saveItems();
                localStorage.setItem('fileStorage', JSON.stringify(fileStorage));
                displayPublishedItems();
                cancelEdit();
                showAlert('Conteúdo atualizado com sucesso!');
            });
        }

        // Botões de interface
        if (cancelEditBtn) {
            cancelEditBtn.addEventListener('click', cancelEdit);
        }

        if (addItemBtn) {
            addItemBtn.addEventListener('click', () => {
                cancelEdit();
                uploadFormContainer.scrollIntoView({ behavior: 'smooth' });
            });
        }

        // Scroll suave para âncoras
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
        // Limpar storage de arquivos não utilizados
        cleanupFileStorage();
        
        checkAuthStatus();
        displayPublishedItems();
        initializeEventListeners();
        setUploadType('url'); // Definir URL como padrão
    });
    </script>
</body>
</html>