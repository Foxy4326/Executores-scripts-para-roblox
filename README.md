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
    
    // Mostra os botões de admin apenas se estiver autenticado
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

    // Adiciona eventos aos botões de admin, se existirem
    if (localStorage.getItem('authenticated') === 'true') {
        card.querySelector('.edit-btn').addEventListener('click', () => showEditForm(item.id));
        card.querySelector('.delete-btn').addEventListener('click', () => deleteItem(item.id));
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
    uploadMessage.textContent = msg;
    uploadMessage.className = error ? 'alert alert-error' : 'alert alert-success';
    uploadMessage.classList.remove('hidden');
    setTimeout(() => uploadMessage.classList.add('hidden'), 4000);
}

// ================= TRATAMENTO DE ERRO 404 (OPCIONAL) =================
// Esta função agora está aqui, mas não é chamada na inicialização
// para evitar o erro ao abrir o arquivo localmente.
function checkPageNotFound() {
    const validPaths = ['/', '/index.html', ''];
    const currentPath = window.location.pathname;
    const isAnchorLink = currentPath === '/' && window.location.hash;
    
    if (!validPaths.includes(currentPath) && !isAnchorLink) {
        showErrorPage();
        return true;
    }
    return false;
}

function showErrorPage() {
    mainContent.style.display = 'none';
    errorPage.style.display = 'flex';
    document.title = 'Página Não Encontrada - Executores e Scripts';
}

function hideErrorPage() {
    errorPage.style.display = 'none';
    mainContent.style.display = 'block';
    document.title = 'Executores e Scripts - Sistema Completo';
    window.history.replaceState({}, document.title, window.location.origin + '/');
}

// ================= EVENTOS =================
authForm.addEventListener('submit', e => {
    e.preventDefault();
    if (accessCodeInput.value.trim() === SECRET_CODE) {
        localStorage.setItem('authenticated', 'true');
        showUploadSection();
        authMessage.classList.add('hidden');
        displayPublishedItems(); // Atualiza os cards para mostrar os botões de admin
    } else {
        authMessage.textContent = 'Código de acesso incorreto. Tente novamente.';
        authMessage.classList.remove('hidden');
        accessCodeInput.value = '';
    }
});

function handleLogout() {
    hideUploadSection();
    displayPublishedItems(); // Atualiza os cards para esconder os botões de admin
}

logoutBtn.addEventListener('click', e => { 
    e.preventDefault(); 
    handleLogout();
});

logoutAdminBtn.addEventListener('click', handleLogout);

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

homeRedirect.addEventListener('click', (e) => {
    e.preventDefault();
    hideErrorPage();
});

// ================= INICIALIZAÇÃO (CORRIGIDA) =================
document.addEventListener('DOMContentLoaded', () => {
    // A verificação de 404 foi desativada para funcionar localmente
    // const isNotFound = checkPageNotFound();
    // if (!isNotFound) {
    
        checkAuthStatus();
        displayPublishedItems();
        
        // Suaviza o scroll para links âncora
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                
                // Código de scroll suave que estava faltando
                const targetId = this.getAttribute('href');
                const targetElement = document.querySelector(targetId);
                if (targetElement) {
                    targetElement.scrollIntoView({
                        behavior: 'smooth'
                    });
                }
            });
        });
        
    // } // Fim do 'if' comentado
});
</script>
