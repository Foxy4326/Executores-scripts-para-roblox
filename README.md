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

// ================= ARMAZENAMENTO =================
let publishedItems = JSON.parse(localStorage.getItem('publishedItems')) || [];

// ================= FUNÇÕES =================
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

logoutBtn.addEventListener('click', e => { e.preventDefault(); hideUploadSection(); });
logoutAdminBtn.addEventListener('click', hideUploadSection);

uploadForm.addEventListener('submit', e => {
  e.preventDefault();
  const title = document.getElementById('title').value.trim();
  const description = document.getElementById('description').value.trim();
  const type = document.getElementById('type').value;
  const downloadUrl = document.getElementById('download-url').value.trim();
  if (!title || !description || !type || !downloadUrl) { showAlert('Preencha todos os campos', true); return; }

  const newItem = { id: Date.now(), title, description, type, downloadUrl, date: new Date().toLocaleDateString('pt-BR') };
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

// ================= INICIALIZAÇÃO =================
document.addEventListener('DOMContentLoaded', () => {
  checkAuthStatus();
  displayPublishedItems();
});
</script>
