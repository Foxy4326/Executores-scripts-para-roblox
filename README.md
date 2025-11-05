<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Executores e Scripts</title>
    <style>
        /* ... (mantenha todo o CSS igual) ... */
    </style>
</head>
<body>
    <div class="container">
        <!-- ... (mantenha todo o HTML igual) ... -->
    </div>

    <button id="logout-admin" class="logout-admin-btn btn btn-danger hidden">Sair</button>

    <script>
    // Configuração
    const SECRET_CODE = "admin123";
    let currentUploadType = 'url';
    let temporaryFileStorage = {}; // Armazena arquivos apenas durante a sessão

    // Inicialização quando o DOM estiver carregado
    document.addEventListener('DOMContentLoaded', function() {
        console.log('DOM carregado - inicializando aplicação...');
        
        // Elementos DOM
        const elements = {
            authSection: document.getElementById('auth'),
            uploadSection: document.getElementById('upload'),
            authForm: document.getElementById('auth-form'),
            uploadForm: document.getElementById('upload-form'),
            editForm: document.getElementById('edit-form'),
            accessCodeInput: document.getElementById('access-code'),
            authMessage: document.getElementById('auth-message'),
            uploadMessage: document.getElementById('upload-message'),
            logoutBtn: document.getElementById('logout-btn'),
            logoutAdminBtn: document.getElementById('logout-admin'),
            executorsGrid: document.getElementById('executors-grid'),
            scriptsGrid: document.getElementById('scripts-grid'),
            uploadFormContainer: document.getElementById('upload-form-container'),
            editFormContainer: document.getElementById('edit-form-container'),
            cancelEditBtn: document.getElementById('cancel-edit-btn'),
            addItemBtn: document.getElementById('add-item-btn'),
            fileUpload: document.getElementById('file-upload'),
            fileSelectBtn: document.getElementById('file-select-btn'),
            fileName: document.getElementById('file-name'),
            urlField: document.getElementById('url-field'),
            fileField: document.getElementById('file-field'),
            uploadTypeBtns: document.querySelectorAll('.upload-type-btn'),
            editFileUpload: document.getElementById('edit-file-upload'),
            editFileSelectBtn: document.getElementById('edit-file-select-btn'),
            editFileName: document.getElementById('edit-file-name'),
            editUrlField: document.getElementById('edit-url-field'),
            editFileField: document.getElementById('edit-file-field')
        };

        // Armazenamento
        let publishedItems = JSON.parse(localStorage.getItem('publishedItems')) || [];

        // Funções de Upload - CORREÇÕES APLICADAS AQUI
        function setUploadType(type) {
            currentUploadType = type;
            
            // Atualizar botões de tipo
            elements.uploadTypeBtns.forEach(btn => {
                btn.classList.toggle('active', btn.dataset.type === type);
            });

            const editUploadTypeBtns = document.querySelectorAll('#edit-form-container .upload-type-btn');
            editUploadTypeBtns.forEach(btn => {
                btn.classList.toggle('active', btn.dataset.type === type);
            });
            
            // Mostrar/ocultar campos apropriados
            if (type === 'url') {
                elements.urlField.classList.remove('hidden');
                elements.fileField.classList.add('hidden');
                elements.editUrlField.classList.remove('hidden');
                elements.editFileField.classList.add('hidden');
                
                // Atualizar atributos required - CORREÇÃO: Remover required do file upload
                elements.fileUpload.removeAttribute('required');
                document.getElementById('download-url').setAttribute('required', 'true');
                document.getElementById('edit-download-url').setAttribute('required', 'true');
            } else {
                elements.urlField.classList.add('hidden');
                elements.fileField.classList.remove('hidden');
                elements.editUrlField.classList.add('hidden');
                elements.editFileField.classList.remove('hidden');
                
                // Atualizar atributos required - CORREÇÃO: Remover required da URL
                document.getElementById('download-url').removeAttribute('required');
                document.getElementById('edit-download-url').removeAttribute('required');
                // CORREÇÃO: Não adicionar required ao file upload pois causa problemas com validação nativa
            }
        }

        function handleFileSelect(fileInput, fileNameElement) {
            if (fileInput.files.length > 0) {
                const file = fileInput.files[0];
                fileNameElement.textContent = `${file.name} (${formatFileSize(file.size)})`;
                
                // Validar tipo de arquivo
                const validExtensions = ['.apk', '.apks', '.zip', '.rar', '.7z'];
                const fileExtension = '.' + file.name.toLowerCase().split('.').pop();
                
                if (!validExtensions.includes(fileExtension)) {
                    showAlert('Por favor, selecione um arquivo APK, ZIP ou RAR válido.', true);
                    fileInput.value = '';
                    fileNameElement.textContent = 'Nenhum arquivo selecionado';
                    return false;
                }

                // Verificar tamanho do arquivo (máximo 50MB para demonstração)
                if (file.size > 50 * 1024 * 1024) {
                    showAlert('Arquivo muito grande. Use URLs externas para arquivos grandes.', true);
                    fileInput.value = '';
                    fileNameElement.textContent = 'Nenhum arquivo selecionado';
                    return false;
                }
                return true;
            }
            return false;
        }

        function saveFileToTemporaryStorage(file) {
            return new Promise((resolve, reject) => {
                const reader = new FileReader();
                
                reader.onload = function(e) {
                    try {
                        const fileId = 'temp_file_' + Date.now() + '_' + Math.random().toString(36).substr(2, 9);
                        temporaryFileStorage[fileId] = {
                            name: file.name,
                            type: file.type,
                            size: file.size,
                            data: e.target.result,
                            uploadDate: new Date().toISOString()
                        };
                        
                        resolve({ 
                            fileId, 
                            fileName: file.name 
                        });
                    } catch (error) {
                        reject(new Error('Erro ao processar o arquivo: ' + error.message));
                    }
                };
                
                reader.onerror = () => {
                    reject(new Error('Erro ao ler o arquivo'));
                };
                
                reader.readAsDataURL(file);
            });
        }

        function downloadTemporaryFile(fileId) {
            const fileData = temporaryFileStorage[fileId];
            if (!fileData) {
                throw new Error('Arquivo não encontrado no armazenamento temporário');
            }

            // Criar link de download usando DataURL
            const a = document.createElement('a');
            a.href = fileData.data;
            a.download = fileData.name;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
        }

        // Funções Auxiliares
        function formatFileSize(bytes) {
            if (bytes === 0) return '0 Bytes';
            const k = 1024;
            const sizes = ['Bytes', 'KB', 'MB', 'GB'];
            const i = Math.floor(Math.log(bytes) / Math.log(k));
            return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
        }

        function showAlert(message, isError = false, target = 'upload') {
            let alertElement;
            if (target === 'auth') {
                alertElement = elements.authMessage;
            } else {
                alertElement = elements.uploadMessage;
            }
            
            alertElement.textContent = message;
            alertElement.className = `alert ${isError ? 'alert-error' : 'alert-success'}`;
            alertElement.classList.remove('hidden');
            
            setTimeout(() => {
                alertElement.classList.add('hidden');
            }, 5000);
        }

        function showUploadSection() {
            elements.authSection.classList.add('hidden');
            elements.uploadSection.classList.remove('hidden');
            elements.logoutBtn.classList.remove('hidden');
            elements.logoutAdminBtn.classList.remove('hidden');
        }

        function hideUploadSection() {
            elements.authSection.classList.remove('hidden');
            elements.uploadSection.classList.add('hidden');
            elements.logoutBtn.classList.add('hidden');
            elements.logoutAdminBtn.classList.add('hidden');
        }

        function showEditForm(itemId) {
            const item = publishedItems.find(item => item.id === itemId);
            if (!item) return;

            document.getElementById('edit-id').value = item.id;
            document.getElementById('edit-title').value = item.title;
            document.getElementById('edit-description').value = item.description;
            document.getElementById('edit-type').value = item.type;
            
            if (item.fileId) {
                setUploadType('file');
                document.getElementById('edit-file-name').textContent = item.fileName || 'Arquivo carregado';
            } else {
                setUploadType('url');
                document.getElementById('edit-download-url').value = item.downloadUrl || '';
            }

            elements.uploadFormContainer.classList.add('hidden');
            elements.editFormContainer.classList.remove('hidden');
            elements.addItemBtn.classList.remove('hidden');
        }

        function hideEditForm() {
            elements.uploadFormContainer.classList.remove('hidden');
            elements.editFormContainer.classList.add('hidden');
            elements.addItemBtn.classList.remove('hidden');
            elements.uploadForm.reset();
            elements.fileName.textContent = 'Nenhum arquivo selecionado';
            setUploadType('url');
        }

        function generateId() {
            return Date.now().toString(36) + Math.random().toString(36).substr(2);
        }

        function renderItems() {
            // Limpar grids
            elements.executorsGrid.innerHTML = '';
            elements.scriptsGrid.innerHTML = '';

            // Separar itens por tipo
            const executors = publishedItems.filter(item => item.type === 'executor');
            const scripts = publishedItems.filter(item => item.type === 'script');

            // Renderizar executores
            if (executors.length === 0) {
                elements.executorsGrid.innerHTML = '<div class="empty-message">Nenhum executor disponível no momento.</div>';
            } else {
                executors.forEach(item => {
                    elements.executorsGrid.appendChild(createItemCard(item));
                });
            }

            // Renderizar scripts
            if (scripts.length === 0) {
                elements.scriptsGrid.innerHTML = '<div class="empty-message">Nenhum script disponível no momento.</div>';
            } else {
                scripts.forEach(item => {
                    elements.scriptsGrid.appendChild(createItemCard(item));
                });
            }
        }

        function createItemCard(item) {
            const card = document.createElement('div');
            card.className = 'card';
            card.innerHTML = `
                <div class="card-header">
                    <h3>${item.title}</h3>
                </div>
                <div class="card-body">
                    <p>${item.description}</p>
                    <div class="date">Publicado em: ${new Date(item.date).toLocaleDateString('pt-BR')}</div>
                </div>
                <div class="card-actions">
                    <button class="btn btn-primary download-btn" data-id="${item.id}">
                        ${item.fileId ? 'Baixar Arquivo' : 'Acessar Link'}
                    </button>
                    ${localStorage.getItem('authenticated') === 'true' ? `
                        <button class="btn btn-warning btn-small edit-btn" data-id="${item.id}">Editar</button>
                        <button class="btn btn-danger btn-small delete-btn" data-id="${item.id}">Excluir</button>
                    ` : ''}
                </div>
            `;
            return card;
        }

        // Funções Principais
        function saveItems() {
            try {
                localStorage.setItem('publishedItems', JSON.stringify(publishedItems));
                return true;
            } catch (error) {
                console.error('Erro ao salvar itens:', error);
                showAlert('Erro ao salvar os dados.', true);
                return false;
            }
        }

        function checkAuthStatus() {
            const isAuthenticated = localStorage.getItem('authenticated') === 'true';
            if (isAuthenticated) {
                showUploadSection();
            }
        }

        // Event Listeners
        function initEventListeners() {
            // Autenticação
            elements.authForm.addEventListener('submit', function(e) {
                e.preventDefault();
                const code = elements.accessCodeInput.value.trim();
                
                if (code === SECRET_CODE) {
                    localStorage.setItem('authenticated', 'true');
                    showUploadSection();
                    showAlert('Autenticado com sucesso!', false, 'auth');
                    renderItems();
                } else {
                    showAlert('Código de acesso incorreto!', true, 'auth');
                }
            });

            // Logout
            elements.logoutBtn.addEventListener('click', function() {
                localStorage.removeItem('authenticated');
                hideUploadSection();
                renderItems();
            });

            elements.logoutAdminBtn.addEventListener('click', function() {
                localStorage.removeItem('authenticated');
                hideUploadSection();
                renderItems();
            });

            // Upload de arquivos
            elements.fileSelectBtn.addEventListener('click', function() {
                elements.fileUpload.click();
            });

            elements.fileUpload.addEventListener('change', function() {
                handleFileSelect(this, elements.fileName);
            });

            elements.editFileSelectBtn.addEventListener('click', function() {
                elements.editFileUpload.click();
            });

            elements.editFileUpload.addEventListener('change', function() {
                handleFileSelect(this, elements.editFileName);
            });

            // Seletor de tipo de upload
            elements.uploadTypeBtns.forEach(btn => {
                btn.addEventListener('click', function() {
                    setUploadType(this.dataset.type);
                });
            });

            // CORREÇÃO PRINCIPAL: Formulário de upload
            elements.uploadForm.addEventListener('submit', async function(e) {
                e.preventDefault();
                
                const title = document.getElementById('title').value.trim();
                const description = document.getElementById('description').value.trim();
                const type = document.getElementById('type').value;
                
                if (!title || !description || !type) {
                    showAlert('Por favor, preencha todos os campos.', true);
                    return;
                }

                let downloadUrl = '';
                let fileId = '';
                let fileName = '';

                try {
                    if (currentUploadType === 'url') {
                        downloadUrl = document.getElementById('download-url').value.trim();
                        if (!downloadUrl) {
                            showAlert('Por favor, forneça uma URL válida.', true);
                            return;
                        }
                    } else {
                        // CORREÇÃO: Verificar se um arquivo foi selecionado
                        if (!elements.fileUpload.files.length) {
                            showAlert('Por favor, selecione um arquivo.', true);
                            return;
                        }
                        
                        // CORREÇÃO: Validar o arquivo antes de processar
                        if (!handleFileSelect(elements.fileUpload, elements.fileName)) {
                            return;
                        }
                        
                        const file = elements.fileUpload.files[0];
                        const result = await saveFileToTemporaryStorage(file);
                        fileId = result.fileId;
                        fileName = result.fileName;
                    }

                    const newItem = {
                        id: generateId(),
                        title,
                        description,
                        type,
                        downloadUrl,
                        fileId,
                        fileName,
                        date: new Date().toISOString()
                    };

                    publishedItems.push(newItem);
                    
                    if (saveItems()) {
                        showAlert('Item publicado com sucesso!', false);
                        elements.uploadForm.reset();
                        elements.fileName.textContent = 'Nenhum arquivo selecionado';
                        setUploadType('url');
                        renderItems();
                    }
                } catch (error) {
                    showAlert('Erro ao publicar item: ' + error.message, true);
                }
            });

            // CORREÇÃO: Formulário de edição
            elements.editForm.addEventListener('submit', async function(e) {
                e.preventDefault();
                
                const id = document.getElementById('edit-id').value;
                const title = document.getElementById('edit-title').value.trim();
                const description = document.getElementById('edit-description').value.trim();
                const type = document.getElementById('edit-type').value;
                
                if (!title || !description || !type) {
                    showAlert('Por favor, preencha todos os campos.', true);
                    return;
                }

                try {
                    const itemIndex = publishedItems.findIndex(item => item.id === id);
                    if (itemIndex === -1) {
                        showAlert('Item não encontrado.', true);
                        return;
                    }

                    let downloadUrl = publishedItems[itemIndex].downloadUrl;
                    let fileId = publishedItems[itemIndex].fileId;
                    let fileName = publishedItems[itemIndex].fileName;

                    if (currentUploadType === 'url') {
                        downloadUrl = document.getElementById('edit-download-url').value.trim();
                        if (!downloadUrl) {
                            showAlert('Por favor, forneça uma URL válida.', true);
                            return;
                        }
                        // Limpar dados de arquivo se estiver mudando para URL
                        fileId = '';
                        fileName = '';
                    } else {
                        // CORREÇÃO: Se estiver no modo arquivo, verificar se um novo arquivo foi selecionado
                        if (elements.editFileUpload.files.length) {
                            // Validar o novo arquivo
                            if (!handleFileSelect(elements.editFileUpload, elements.editFileName)) {
                                return;
                            }
                            const file = elements.editFileUpload.files[0];
                            const result = await saveFileToTemporaryStorage(file);
                            fileId = result.fileId;
                            fileName = result.fileName;
                        }
                        // Se não selecionou novo arquivo, mantém o existente
                        // CORREÇÃO: Se não há arquivo existente nem novo, mostrar erro
                        else if (!fileId) {
                            showAlert('Por favor, selecione um arquivo ou altere para URL.', true);
                            return;
                        }
                    }

                    publishedItems[itemIndex] = {
                        ...publishedItems[itemIndex],
                        title,
                        description,
                        type,
                        downloadUrl,
                        fileId,
                        fileName
                    };

                    if (saveItems()) {
                        showAlert('Item atualizado com sucesso!', false);
                        hideEditForm();
                        renderItems();
                    }
                } catch (error) {
                    showAlert('Erro ao atualizar item: ' + error.message, true);
                }
            });

            // Cancelar edição
            elements.cancelEditBtn.addEventListener('click', hideEditForm);
            elements.addItemBtn.addEventListener('click', hideEditForm);

            // Delegation para botões dinâmicos
            document.addEventListener('click', function(e) {
                // Download
                if (e.target.classList.contains('download-btn')) {
                    const itemId = e.target.dataset.id;
                    const item = publishedItems.find(item => item.id === itemId);
                    
                    if (item) {
                        if (item.fileId) {
                            try {
                                downloadTemporaryFile(item.fileId);
                                showAlert('Download iniciado!', false);
                            } catch (error) {
                                showAlert('Erro ao baixar arquivo: ' + error.message, true);
                            }
                        } else if (item.downloadUrl) {
                            window.open(item.downloadUrl, '_blank');
                        } else {
                            showAlert('Nenhum link ou arquivo disponível para download.', true);
                        }
                    }
                }

                // Editar
                if (e.target.classList.contains('edit-btn')) {
                    const itemId = e.target.dataset.id;
                    showEditForm(itemId);
                }

                // Excluir
                if (e.target.classList.contains('delete-btn')) {
                    const itemId = e.target.dataset.id;
                    if (confirm('Tem certeza que deseja excluir este item?')) {
                        publishedItems = publishedItems.filter(item => item.id !== itemId);
                        if (saveItems()) {
                            showAlert('Item excluído com sucesso!', false);
                            renderItems();
                        }
                    }
                }
            });
        }

        // Inicialização
        function init() {
            initEventListeners();
            checkAuthStatus();
            renderItems();
            setUploadType('url');
        }

        // Iniciar aplicação
        init();
    });
    </script>
</body>
</html>