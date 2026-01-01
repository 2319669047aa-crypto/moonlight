// ==========================================
// 1. 全局变量与配置
// ==========================================
let transactions = [];
let memos = [];
let todos = [];
let passwords = []; 
const fixedTags = ['早餐', '午餐', '晚餐', '奶茶', '生活用品'];
let customTags = [];
let myChart = null;
let mindMapChart = null;
let isAllCollapsed = false;
let currentTheme = { color: '#007aff', gradient: true, titles: { accounting: "💰 本月支出", memo: "📝 个人动态" } };
let currentImageBase64 = null; 
let mindMapMode = 'fruit';
let datePickerMode = 'tree'; 
let currentMemoFilter = null; 
// 密码编辑状态
let editingPassId = null;

const monthFruits = ['🍊','🍓','🍍','🍒','🍈','🍑','🍉','🍇','🍐','🍎','🍌','🥝'];
const monthFlowers = ['🌺','🌸','🌷','🌹','💐','🪷','🌻','🌼','🏵️','🍁','🥀','❄️'];

function createEmojiIcon(emoji) {
  const canvas = document.createElement('canvas');
  canvas.width = 60; canvas.height = 60;
  const ctx = canvas.getContext('2d');
  ctx.font = '50px serif';
  ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
  ctx.fillText(emoji, 30, 32);
  return 'image://' + canvas.toDataURL();
}

// === 页面加载入口 ===
window.onload = function() {
  loadData();
  loadTheme();
  renderTags();
  const pill = document.querySelector('.toggle-pill');
  if(pill) switchMemoView('list', pill); 
};

// 点击空白关闭弹窗
window.onclick = function(event) {
  if (event.target.classList.contains('modal')) {
    event.target.style.setProperty('display', 'none', 'important');
  }
}

// ==========================================
// 2. 标题编辑逻辑 (带确认按钮)
// ==========================================
function editPageTitle(elementId) {
  const el = document.getElementById(elementId);
  const currentText = el.innerText.replace(' ✎', ''); 
  
  const wrapper = document.createElement('div');
  wrapper.className = 'title-edit-wrapper';
  
  const input = document.createElement('input');
  input.type = 'text';
  input.value = currentText;
  
  const confirmBtn = document.createElement('div');
  confirmBtn.className = 'title-save-btn';
  confirmBtn.innerHTML = '<i class="fas fa-check"></i>';
  
  const saveAction = () => saveNewTitle(elementId, input.value);
  
  confirmBtn.onclick = (e) => { e.stopPropagation(); saveAction(); };
  input.onkeydown = function(e) { if(e.key === 'Enter') saveAction(); };
  
  wrapper.appendChild(input);
  wrapper.appendChild(confirmBtn);
  el.parentNode.replaceChild(wrapper, el);
  input.focus();
}

function saveNewTitle(elementId, newValue) {
  if (!newValue.trim()) newValue = "我的标题"; 
  if (elementId === 'title-accounting') currentTheme.titles.accounting = newValue;
  if (elementId === 'title-memo') currentTheme.titles.memo = newValue;
  saveData();
  location.reload(); 
}

// ==========================================
// 3. 记账核心逻辑
// ==========================================
function addBill() {
  const moneyInput = document.getElementById('money-input');
  const itemInput = document.getElementById('item-input');
  const money = parseFloat(moneyInput.value);
  const item = itemInput.value.trim();

  if (!item || isNaN(money) || money === 0) { alert('金额和用途都要填哦'); return; }
  if (!fixedTags.includes(item) && !customTags.includes(item)) { customTags.push(item); renderTags(); }

  const id = Date.now(); 
  const now = new Date();
  const newBill = {
    id: id, item: item, money: money,
    dateString: `${now.getFullYear()}年${now.getMonth()+1}月${now.getDate()}日`,
    year: now.getFullYear(), month: now.getMonth() + 1, day: now.getDate(),
    timestamp: now.getTime()
  };
  
  transactions.unshift(newBill); 
  saveData(); 
  renderAllTransactions();
  moneyInput.value = ''; itemInput.value = '';
}

function renderAllTransactions() {
  const container = document.getElementById('bill-container');
  if(!container) return;
  container.innerHTML = ''; 

  if (transactions.length === 0) {
    container.innerHTML = '<div style="text-align:center; color:#ccc; padding:20px;">还没有记账哦</div>';
    return;
  }

  const groups = {};
  transactions.sort((a, b) => (b.timestamp || 0) - (a.timestamp || 0));

  transactions.forEach(t => {
    if(!t.dateString) t.dateString = `${t.year}年${t.month}月${t.day}日`;
    if (!groups[t.dateString]) groups[t.dateString] = [];
    groups[t.dateString].push(t);
  });

  Object.keys(groups).forEach(dateStr => {
    const dayTotal = groups[dateStr].reduce((sum, t) => sum + t.money, 0);
    const groupDiv = document.createElement('div');
    groupDiv.className = 'date-group'; groupDiv.style.padding = "0"; 
    
    groupDiv.innerHTML = `
      <div class="date-header" onclick="toggleThisGroup(this)">
        <span>${dateStr} <span style="font-size:12px;color:#999;margin-left:5px">¥${dayTotal}</span></span>
        <i class="fas fa-chevron-down arrow-icon"></i>
      </div>
      <div class="date-content"></div>`;
    
    const contentDiv = groupDiv.querySelector('.date-content');
    groups[dateStr].forEach(t => {
      const billDiv = document.createElement('div');
      billDiv.className = 'bill-item';
      billDiv.innerHTML = `
        <span class="bill-name">${t.item}</span>
        <div class="bill-right">
          <span class="bill-money">-${t.money}</span>
          <i class="fas fa-trash-alt delete-btn" onclick="deleteBill(${t.id})"></i>
        </div>`;
      contentDiv.appendChild(billDiv);
    });
    container.appendChild(groupDiv);
  });
}

function toggleThisGroup(header) {
  const content = header.nextElementSibling;
  const arrow = header.querySelector('.arrow-icon');
  if (content.classList.contains('hidden')) {
    content.classList.remove('hidden');
    arrow.style.transform = 'rotate(0deg)';
  } else {
    content.classList.add('hidden');
    arrow.style.transform = 'rotate(-90deg)';
  }
}

function deleteBill(id) {
  if(!confirm("删除这条账单？")) return;
  transactions = transactions.filter(t => t.id !== id); 
  saveData(); renderAllTransactions(); 
}

// 标签
function renderTags() {
  const container = document.getElementById('tags-wrapper');
  if(!container) return;
  container.innerHTML = '';
  fixedTags.forEach(tag => {
    const el = document.createElement('div'); el.className = 'tag-fixed'; el.innerText = tag;
    el.onclick = () => { document.getElementById('item-input').value = tag; };
    container.appendChild(el);
  });
  if (Array.isArray(customTags)) {
    customTags.forEach((tag, index) => {
      const el = document.createElement('div'); el.className = 'tag-custom';
      el.innerHTML = `<span onclick="fillInput('${tag}')">${tag}</span><span class="tag-del-icon" onclick="deleteCustomTag(event, ${index})">&times;</span>`;
      container.appendChild(el);
    });
  }
}
function addCategoryFromInput() {
  const input = document.getElementById('item-input'); const val = input.value.trim();
  if (!val) { alert("请先输入标签名"); return; }
  if (fixedTags.includes(val) || customTags.includes(val)) { alert("标签已存在"); input.value = ''; return; }
  customTags.push(val); saveData(); renderTags(); input.value = '';
}
function fillInput(val) { document.getElementById('item-input').value = val; }
function deleteCustomTag(e, index) { e.stopPropagation(); if(confirm(`删除标签?`)) { customTags.splice(index, 1); saveData(); renderTags(); } }

// ==========================================
// 4. 备忘录 & 动态
// ==========================================
function addTodo() {
  const input = document.getElementById('todo-input'); const text = input.value.trim();
  if(!text) return; todos.unshift({ text: text, completed: false }); saveData(); renderTodos(); input.value = '';
}
function toggleTodo(index) { todos[index].completed = !todos[index].completed; saveData(); renderTodos(); }
function deleteTodo(e, index) { e.stopPropagation(); if(confirm('删除?')) { todos.splice(index, 1); saveData(); renderTodos(); } }
function renderTodos() {
  const container = document.getElementById('todo-list'); container.innerHTML = '';
  todos.forEach((todo, index) => {
    const el = document.createElement('div'); el.className = `todo-item ${todo.completed ? 'completed' : ''}`;
    el.onclick = () => toggleTodo(index); 
    el.innerHTML = `<div class="todo-left"><div class="check-circle"><i class="fas fa-check"></i></div><span class="todo-text">${todo.text}</span></div><i class="fas fa-trash-alt todo-del-btn" onclick="deleteTodo(event, ${index})"></i>`;
    container.appendChild(el);
  });
}

function triggerFileInput() { document.getElementById('file-input').click(); }
function handleFileSelect(input) {
  if (input.files && input.files[0]) {
    const file = input.files[0]; const reader = new FileReader();
    reader.onload = function(e) {
      const img = new Image(); img.src = e.target.result;
      img.onload = function() {
        const canvas = document.createElement('canvas'); const ctx = canvas.getContext('2d');
        const maxWidth = 450; let width = img.width; let height = img.height;
        if (width > maxWidth) { height *= maxWidth / width; width = maxWidth; }
        canvas.width = width; canvas.height = height; ctx.drawImage(img, 0, 0, width, height);
        currentImageBase64 = canvas.toDataURL('image/jpeg', 0.5);
        document.getElementById('preview-img').src = currentImageBase64;
        document.getElementById('image-preview-area').style.display = 'inline-block';
      };
    }; reader.readAsDataURL(file);
  }
}
function clearImage() { currentImageBase64 = null; document.getElementById('file-input').value = ''; document.getElementById('image-preview-area').style.display = 'none'; }
function addMemo() {
  const memoInput = document.getElementById('memo-input'); const text = memoInput.value;
  if (text === '' && !currentImageBase64) { alert("写点东西吧"); return; }
  const now = new Date();
  const timeString = `${now.getMonth()+1}月${now.getDate()}日 ${now.getHours()}:${now.getMinutes()<10?'0'+now.getMinutes():now.getMinutes()}`;
  memos.unshift({ text: text, time: timeString, image: currentImageBase64, timestamp: Date.now() }); 
  try { saveData(); } catch (e) { alert("存储满！请导出备份。"); memos.shift(); return; }
  renderMemos(); memoInput.value = ''; clearImage();
}
function renderMemos() {
  const container = document.getElementById('memo-container'); container.innerHTML = '';
  let displayList = memos;
  if (currentMemoFilter) {
    const startTime = new Date(currentMemoFilter.start + " 00:00:00").getTime();
    const endTime = new Date(currentMemoFilter.end + " 23:59:59").getTime();
    displayList = memos.filter(m => {
      let mTime = m.timestamp;
      if(!mTime) { const currentYear = new Date().getFullYear(); const datePart = m.time.split(' ')[0].replace('月', '/').replace('日', ''); mTime = new Date(`${currentYear}/${datePart} 00:00:00`).getTime(); }
      return mTime >= startTime && mTime <= endTime;
    });
  }
  if(displayList.length === 0) { container.innerHTML = '<div style="text-align:center; color:#ccc; margin-top:20px;">暂无动态</div>'; return; }
  displayList.forEach((m) => {
     const realIndex = memos.indexOf(m);
     const newCard = document.createElement('div'); newCard.className = 'memo-card'; 
     let imgHtml = ''; if (m.image) { imgHtml = `<img src="${m.image}" class="memo-img-display" loading="lazy">`; }
     newCard.innerHTML = `<span class="memo-text">${m.text || ''}</span>${imgHtml}<div class="memo-footer"><span class="memo-date">${m.time}</span><span class="memo-del" onclick="deleteMemo(${realIndex})">删除</span></div>`;
     container.appendChild(newCard);
  });
}
function deleteMemo(index) { if(confirm("删除动态？")) { memos.splice(index, 1); saveData(); renderMemos(); } }

function openDayDetail(image, text, dateStr) {
  document.getElementById('detail-img').src = image;
  document.getElementById('detail-text').innerText = text || "（仅照片）";
  document.getElementById('detail-date').innerText = dateStr;
  document.getElementById('day-detail-modal').style.setProperty('display', 'flex', 'important');
}
function closeDayDetail() { document.getElementById('day-detail-modal').style.setProperty('display', 'none', 'important'); }
function renderMemoCalendar() {
  const now = new Date(); const year = now.getFullYear(); const month = now.getMonth(); 
  document.getElementById('memo-calendar-title').innerText = `${year}年${month+1}月`;
  const grid = document.getElementById('memo-calendar-grid'); grid.innerHTML = '';
  const daysInMonth = new Date(year, month + 1, 0).getDate(); const firstDayIndex = new Date(year, month, 1).getDay();
  const dailyData = {};
  memos.forEach(m => {
    let mDate; if (m.timestamp) { mDate = new Date(m.timestamp); } else { const datePart = m.time.split(' ')[0].replace('月', '/').replace('日', ''); mDate = new Date(`${year}/${datePart} 00:00:00`); }
    if (mDate.getFullYear() === year && mDate.getMonth() === month) { const day = mDate.getDate(); if (m.image) { dailyData[day] = { image: m.image, text: m.text, date: m.time }; } }
  });
  for (let i = 0; i < firstDayIndex; i++) grid.appendChild(document.createElement('div'));
  for (let d = 1; d <= daysInMonth; d++) {
    const cell = document.createElement('div'); cell.className = 'day-cell';
    if (dailyData[d]) {
      const data = dailyData[d];
      const photoDiv = document.createElement('div'); photoDiv.className = 'day-num has-photo';
      photoDiv.style.backgroundImage = `url(${data.image})`; photoDiv.innerText = d;
      photoDiv.onclick = function() { openDayDetail(data.image, data.text, data.date); };
      cell.appendChild(photoDiv);
    } else { cell.innerHTML = `<div class="day-num">${d}</div>`; }
    grid.appendChild(cell);
  }
}
function switchMemoView(view, btn) {
  document.querySelectorAll('.toggle-pill').forEach(b => b.classList.remove('active'));
  if (btn) btn.classList.add('active');
  const listView = document.getElementById('memo-view-list'); const calendarView = document.getElementById('memo-view-calendar');
  if (view === 'list') { listView.style.display = 'block'; calendarView.style.display = 'none'; } 
  else { listView.style.display = 'none'; calendarView.style.display = 'block'; renderMemoCalendar(); }
}

// ==========================================
// 5. 密码箱逻辑 (更新：支持编辑、复制)
// ==========================================
function openPasswordModal() { 
  document.getElementById('password-modal').style.setProperty('display', 'flex', 'important'); 
  resetPassInput(); // 每次打开都重置
  renderPasswordList(); 
}
function closePasswordModal() { 
  document.getElementById('password-modal').style.setProperty('display', 'none', 'important'); 
  resetPassInput(); 
}

// 保存逻辑（新增 或 修改）
function savePasswordItem() {
  const title = document.getElementById('pass-title').value.trim();
  const account = document.getElementById('pass-account').value.trim();
  const secret = document.getElementById('pass-secret').value.trim();
  const url = document.getElementById('pass-url').value.trim();

  if(!title || !account || !secret) { alert("请填写完整信息"); return; }

  if (editingPassId) {
    // 处于编辑模式，更新旧数据
    const index = passwords.findIndex(p => p.id === editingPassId);
    if (index !== -1) {
      passwords[index] = { id: editingPassId, title, account, secret, url };
      alert("✅ 修改保存成功！");
    }
  } else {
    // 处于新增模式
    passwords.push({ id: Date.now(), title, account, secret, url });
  }

  saveData();
  resetPassInput(); // 清空并恢复为新增状态
  renderPasswordList();
}

// 进入编辑模式
function editPassword(id) {
  const item = passwords.find(p => p.id === id);
  if (!item) return;

  // 填回输入框
  document.getElementById('pass-title').value = item.title;
  document.getElementById('pass-account').value = item.account;
  document.getElementById('pass-secret').value = item.secret;
  document.getElementById('pass-url').value = item.url || '';

  // 改变界面状态
  editingPassId = id;
  const btn = document.getElementById('pass-save-btn');
  btn.innerText = "✅ 确认修改";
  btn.style.background = "linear-gradient(135deg, #34c759, #30b34d)"; // 变绿
  document.getElementById('pass-cancel-btn').style.display = "block"; // 显示取消按钮
}

// 重置输入框
function resetPassInput() {
  document.getElementById('pass-title').value = '';
  document.getElementById('pass-account').value = '';
  document.getElementById('pass-secret').value = '';
  document.getElementById('pass-url').value = '';
  
  editingPassId = null;
  const btn = document.getElementById('pass-save-btn');
  btn.innerText = "添加保存";
  btn.style.background = ""; // 恢复默认
  document.getElementById('pass-cancel-btn').style.display = "none";
}

// 生成随机密码
function generateRandomPass() {
  const chars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*";
  let pass = "";
  for (let i=0; i<12; i++) pass += chars.charAt(Math.floor(Math.random() * chars.length));
  document.getElementById('pass-secret').value = pass;
}

// 渲染列表 (新按钮)
function renderPasswordList() {
  const container = document.getElementById('password-list-container');
  container.innerHTML = '';
  
  const displayList = [...passwords].reverse(); // 倒序显示

  displayList.forEach((p) => {
    const el = document.createElement('div');
    el.className = 'password-item';
    el.innerHTML = `
      <div class="pass-info">
        <span class="pass-title">${p.title}</span>
        <span class="pass-detail">👤 ${p.account}</span>
        <span class="pass-detail">🔑 <span class="masked-text">******</span></span>
        ${p.url ? `<span class="pass-detail">🔗 ${p.url}</span>` : ''}
      </div>
      <div class="pass-actions">
        <i class="fas fa-pen action-icon" onclick="editPassword(${p.id})" title="编辑修改"></i>
        <i class="far fa-user action-icon" onclick="copyText('${p.account}', '账号')" title="复制账号"></i>
        <i class="fas fa-key action-icon" onclick="copyText('${p.secret}', '密码')" title="复制密码"></i>
        <i class="fas fa-trash-alt action-icon" style="color:#ff3b30" onclick="deletePassword(${p.id})" title="删除"></i>
      </div>
    `;
    container.appendChild(el);
  });
}

// 复制功能
function copyText(text, type) {
  if (!text) return;
  const input = document.createElement('textarea');
  input.value = text;
  document.body.appendChild(input);
  input.select();
  document.execCommand('copy');
  document.body.removeChild(input);
  alert(`✅ ${type}已复制！`);
}

function deletePassword(id) {
  if(confirm("确定删除这条记录吗？")) {
    passwords = passwords.filter(p => p.id !== id);
    if (editingPassId === id) resetPassInput(); // 如果正在编辑它，重置
    saveData();
    renderPasswordList();
  }
}

function exportPasswordsToText() {
  if (passwords.length === 0) { alert("空空如也"); return; }
  let content = `=== 我的密码本 ===\n导出时间: ${new Date().toLocaleString()}\n\n`;
  passwords.forEach(p => { content += `【${p.title}】\n账号: ${p.account}\n密码: ${p.secret}\n`; if(p.url) content += `备注: ${p.url}\n`; content += "------------------------------\n"; });
  const blob = new Blob([content], { type: "text/plain" }); const url = URL.createObjectURL(blob);
  const a = document.createElement('a'); a.href = url; a.download = `我的密码本.txt`; a.click(); URL.revokeObjectURL(url);
}

// ==========================================
// 6. 数据管理 (V8.0 强制版)
// ==========================================
function loadData() {
  try {
    const savedTags = localStorage.getItem('myAppCustomTags'); if (savedTags) customTags = JSON.parse(savedTags);
    const savedBills = localStorage.getItem('myAppTransactions'); if (savedBills) transactions = JSON.parse(savedBills);
    const savedTodos = localStorage.getItem('myAppTodos'); if (savedTodos) todos = JSON.parse(savedTodos);
    const savedMemos = localStorage.getItem('myAppMemos'); if (savedMemos) memos = JSON.parse(savedMemos);
    const savedPasswords = localStorage.getItem('myAppPasswords'); if (savedPasswords) passwords = JSON.parse(savedPasswords);
  } catch (e) { console.error("数据修复中..."); }
  renderAllTransactions();
  renderTodos();
  renderMemos();
}
function saveData() {
  try {
    localStorage.setItem('myAppTransactions', JSON.stringify(transactions));
    localStorage.setItem('myAppMemos', JSON.stringify(memos));
    localStorage.setItem('myAppTodos', JSON.stringify(todos));
    localStorage.setItem('myAppPasswords', JSON.stringify(passwords));
    localStorage.setItem('myAppCustomTags', JSON.stringify(customTags));
    localStorage.setItem('myAppTheme', JSON.stringify(currentTheme));
  } catch(e) {
    alert("❌ 数据保存失败！\n原因可能是手机存储空间已满或在无痕模式下。\n请尝试删除一些带图的动态。");
  }
}

// 辅助函数：手动拆解日期
function getLocaLStart(dateStr) {
  if(!dateStr) return 0;
  const parts = dateStr.split(/[-/]/); 
  return new Date(parts[0], parts[1]-1, parts[2], 0, 0, 0, 0).getTime();
}
function getLocalEnd(dateStr) {
  if(!dateStr) return 0;
  const parts = dateStr.split(/[-/]/);
  return new Date(parts[0], parts[1]-1, parts[2], 23, 59, 59, 999).getTime();
}

function deleteByDateRange() {
  const s = document.getElementById('del-start-date').value; 
  const e = document.getElementById('del-end-date').value;
  const delT = document.getElementById('del-check-bill').checked; 
  const delM = document.getElementById('del-check-memo').checked;

  if (!s || !e) { alert("⚠️ 请选择日期范围"); return; }
  if (!delT && !delM) { alert("⚠️ 请选择要删除的内容"); return; }

  const st = getLocaLStart(s);
  const et = getLocalEnd(e);
  
  if(!confirm(`⚠️ 确定删除 ${s} 至 ${e} 期间的选中数据吗？`)) return;

  const currentYear = new Date().getFullYear();
  let countT = 0;
  let countM = 0;

  if (delT) {
    const initialLen = transactions.length;
    transactions = transactions.filter(t => {
      let itemTime = Number(t.timestamp);
      if (!itemTime) itemTime = new Date(t.year, t.month - 1, t.day).getTime();
      return !(itemTime >= st && itemTime <= et); 
    });
    countT = initialLen - transactions.length;
  }

  if (delM) {
    const initialLen = memos.length;
    memos = memos.filter(m => {
      let itemTime = Number(m.timestamp);
      if (!itemTime && m.time) { const datePart = m.time.split(' ')[0].replace('月', '/').replace('日', ''); itemTime = new Date(`${currentYear}/${datePart} 00:00:00`).getTime(); }
      if (!itemTime) return true; 
      return !(itemTime >= st && itemTime <= et);
    });
    countM = initialLen - memos.length;
  }
  
  saveData();
  renderAllTransactions();
  renderMemos();
  
  if (countT === 0 && countM === 0) {
    alert("⚠️ 未找到该范围内的数据。");
  } else {
    alert(`✅ 已立即删除：\n- 账单：${countT} 笔\n- 动态：${countM} 条`);
    closeSettingsModal();
  }
}

function clearAllData() { if(confirm("警告：将清空所有数据！确定吗？")) { localStorage.clear(); location.reload(); } }
function toggleAllGroups() {
  isAllCollapsed = !isAllCollapsed;
  document.querySelectorAll('.date-content').forEach(c => isAllCollapsed ? c.classList.add('hidden') : c.classList.remove('hidden'));
  document.querySelectorAll('.arrow-icon').forEach(a => a.style.transform = isAllCollapsed ? 'rotate(-90deg)' : 'rotate(0deg)');
}
function showReport() { document.getElementById('chart-modal').style.setProperty('display', 'flex', 'important'); switchReportTab('chart', document.querySelector('.tab-btn')); }
function closeReport() { document.getElementById('chart-modal').style.setProperty('display', 'none', 'important'); }
function switchReportTab(tab, btn) {
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active-tab')); btn.classList.add('active-tab');
  document.getElementById('view-chart').style.display = tab==='chart'?'block':'none'; document.getElementById('view-calendar').style.display = tab==='chart'?'none':'block';
  setTimeout(() => { if(tab==='chart') renderChart(); else renderCalendar(); }, 50);
}
function renderChart() {
  if(transactions.length===0) return; const stats={}; transactions.forEach(t => stats[t.item] = (stats[t.item]||0)+t.money);
  const ctx = document.getElementById('expense-chart').getContext('2d'); if(myChart) myChart.destroy();
  myChart = new Chart(ctx, { type: 'doughnut', data: { labels: Object.keys(stats), datasets: [{ data: Object.values(stats), backgroundColor: ['#FF6384','#36A2EB','#FFCE56','#4BC0C0','#9966FF','#FF9F40'] }] } });
}
function renderCalendar() {
  const now=new Date(); const y=now.getFullYear(); const m=now.getMonth();
  document.getElementById('calendar-title').innerText=`${y}年${m+1}月`;
  const g=document.getElementById('calendar-grid'); g.innerHTML='';
  const dim=new Date(y,m+1,0).getDate(); const start=new Date(y,m,1).getDay();
  const stats={}; transactions.forEach(t=>{ if(t.year===y && t.month===m+1) stats[t.day]=(stats[t.day]||0)+t.money; });
  for(let i=0;i<start;i++) g.appendChild(document.createElement('div'));
  for(let d=1;d<=dim;d++) {
    const c=document.createElement('div'); c.className='day-cell';
    let h=`<div class="day-num ${d===now.getDate()?'current-day-circle':''}">${d}</div>`;
    if(stats[d]) h+=`<span class="day-total">${stats[d]}</span>`;
    c.innerHTML=h; g.appendChild(c);
  }
}
function openThemeModal() { document.getElementById('theme-modal').style.setProperty('display', 'flex', 'important'); document.getElementById('main-theme-color').value=currentTheme.color; document.getElementById('gradient-toggle').checked=currentTheme.gradient; updateThemePreview(); }
function closeThemeModal() { document.getElementById('theme-modal').style.setProperty('display', 'none', 'important'); }
function lightenColor(col,amt) { var usePound=false; if(col[0]=="#"){col=col.slice(1);usePound=true;} var num=parseInt(col,16); var r=(num>>16)+amt; if(r>255)r=255;else if(r<0)r=0; var b=((num>>8)&0x00FF)+amt; if(b>255)b=255;else if(b<0)b=0; var g=(num&0x0000FF)+amt; if(g>255)g=255;else if(g<0)g=0; return (usePound?"#":"")+(g|(b<<8)|(r<<16)).toString(16).padStart(6,'0'); }
function hexToRgba(hex,alpha) { if(/^#([A-Fa-f0-9]{3}){1,2}$/.test(hex)){ let c=hex.substring(1).split(''); if(c.length==3)c=[c[0],c[0],c[1],c[1],c[2],c[2]]; c='0x'+c.join(''); return 'rgba('+[(c>>16)&255, (c>>8)&255, c&255].join(',')+','+alpha+')'; } return 'rgba(0,0,0,0.2)'; }
function updateThemePreview() { const c=document.getElementById('main-theme-color').value; const g=document.getElementById('gradient-toggle').checked; document.getElementById('theme-preview').style.background = g ? `linear-gradient(135deg, ${c}, ${lightenColor(c,40)})` : c; }
function applyTheme() {
  const c=document.getElementById('main-theme-color').value; const g=document.getElementById('gradient-toggle').checked;
  const r=document.documentElement; r.style.setProperty('--main-color', c);
  r.style.setProperty('--theme-gradient', g ? `linear-gradient(135deg, ${c}, ${lightenColor(c,40)})` : c);
  r.style.setProperty('--theme-shadow', `0 4px 12px ${hexToRgba(c,0.4)}`);
  currentTheme.color=c; currentTheme.gradient=g; saveData(); closeThemeModal();
}
function resetTheme() { document.getElementById('main-theme-color').value='#007aff'; document.getElementById('gradient-toggle').checked=true; applyTheme(); }
function loadTheme() {
  const t = localStorage.getItem('myAppTheme');
  if (t) {
    const p = JSON.parse(t); currentTheme = { ...currentTheme, ...p };
    document.getElementById('main-theme-color').value = currentTheme.color;
    document.getElementById('gradient-toggle').checked = currentTheme.gradient;
    applyTheme();
    if(currentTheme.titles) {
      document.getElementById('title-accounting').innerHTML = `${currentTheme.titles.accounting} <i class="fas fa-pen" style="font-size:10px; color:#ddd; margin-left:5px;"></i>`;
      document.getElementById('title-memo').innerHTML = `${currentTheme.titles.memo} <i class="fas fa-pen" style="font-size:10px; color:#ddd; margin-left:5px;"></i>`;
    }
  }
}
function switchPage(pageId, navElement) {
  document.querySelectorAll('.page').forEach(p => { p.classList.remove('active-page'); p.style.setProperty('display', 'none', 'important'); });
  const target = document.getElementById('page-' + pageId);
  if (target) { target.classList.add('active-page'); target.style.setProperty('display', 'block', 'important'); }
  document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
  if(navElement) navElement.classList.add('active');
}
function fillInput(val) { document.getElementById('item-input').value = val; }
function deleteCustomTag(e, index) {
  e.stopPropagation();
  if(confirm(`删除标签“${customTags[index]}”?`)) { customTags.splice(index, 1); saveData(); renderTags(); }
}
function addCategoryFromInput() {
  const input = document.getElementById('item-input');
  const val = input.value.trim();
  if (val && !fixedTags.includes(val) && !customTags.includes(val)) { customTags.push(val); saveData(); renderTags(); }
}
function openMemoFilter() { datePickerMode = 'filter_list'; document.getElementById('date-select-modal').style.setProperty('display', 'flex', 'important'); document.querySelector('#date-select-modal h3').innerText = "📅 筛选动态日期"; }
function clearMemoFilter() { currentMemoFilter = null; document.getElementById('filter-status-bar').style.display = 'none'; document.getElementById('clear-filter-btn').style.display = 'none'; renderMemos(); }
function confirmGenerateMindMap() { closeDateSelectModal(); document.getElementById('mindmap-modal').style.setProperty('display', 'flex', 'important'); const startStr = document.getElementById('mindmap-start-date').value; const endStr = document.getElementById('mindmap-end-date').value; generateMindMapWithDate(startStr, endStr); }
function openDateSelectModal(mode) { datePickerMode = mode; document.getElementById('date-select-modal').style.setProperty('display', 'flex', 'important'); const title = mode === 'tree' ? '🌳 生成生活果树' : '📅 筛选动态日期'; document.querySelector('#date-select-modal h3').innerText = title; const btn = document.getElementById('date-confirm-btn'); btn.innerText = mode === 'tree' ? '开始生长 🌱' : '确认筛选'; }
function closeDateSelectModal() { document.getElementById('date-select-modal').style.setProperty('display', 'none', 'important'); }
function closeMindMap() { document.getElementById('mindmap-modal').style.setProperty('display', 'none', 'important'); }
function generateMindMapWithDate(s,e) {
  let fMemos=memos; if(s&&e) { const st=new Date(s+" 00:00:00").getTime(); const et=new Date(e+" 23:59:59").getTime(); fMemos=memos.filter(m=>{ let t=m.timestamp; if(!t){const y=new Date().getFullYear(); const d=m.time.split(' ')[0].replace('月','/').replace('日',''); t=new Date(`${y}/${d} 00:00:00`).getTime();} return t>=st && t<=et; }); }
  renderMindMapWithData(fMemos);
}
function renderMindMapWithData(list) {
  const g={}; list.forEach(m=>{ const k=m.time.split('月')[0]+'月'; if(!g[k])g[k]=[]; g[k].push(m); });
  const c=Object.keys(g).map(k=>{
    const idx=parseInt(k.replace('月',''))-1; const icon=mindMapMode==='fruit'?createEmojiIcon(monthFruits[idx]||'🍎'):createEmojiIcon(monthFlowers[idx]||'🌸');
    return { name:k, symbol:icon, symbolSize:35, children:g[k].map(m=>{
      let n={ name:`${m.time.split(' ')[0]}\n${m.text?m.text.substring(0,8)+'...':''}`, value:m.text||'[图]' };
      if(m.image){ n.symbol=`image://${m.image}`; n.symbolSize=[50,50]; } else { n.symbol=icon; n.symbolSize=20; } return n;
    })};
  });
  const rootIcon=createEmojiIcon(mindMapMode==='fruit'?'🌳':'💐');
  const opt={ tooltip:{trigger:'item',formatter:p=>p.data.value||p.name}, series:[{type:'tree',data:[{name:mindMapMode==='fruit'?"生活\n果园":"生活\n花园",symbol:rootIcon,symbolSize:50,children:c}],top:'5%',bottom:'5%',left:'10%',right:'25%',lineStyle:{color:'#8B4513',width:2,curveness:0.5},label:{position:'right',fontSize:13,backgroundColor:'#fff',padding:4,borderRadius:4},leaves:{label:{position:'right'}},expandAndCollapse:true}]};
  if(mindMapChart) mindMapChart.dispose(); mindMapChart=echarts.init(document.getElementById('echarts-container')); mindMapChart.setOption(opt); window.onresize=function(){mindMapChart.resize();};
}
function switchMindMapMode(m) { mindMapMode=m; document.getElementById('btn-fruit').classList.toggle('active',m==='fruit'); document.getElementById('btn-flower').classList.toggle('active',m==='flower'); const s=document.getElementById('mindmap-start-date').value; const e=document.getElementById('mindmap-end-date').value; generateMindMapWithDate(s,e); }
