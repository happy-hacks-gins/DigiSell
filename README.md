<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>DigiSell Pro • Ultimate Real-Time Digital Commerce</title>
  <meta name="description" content="The most advanced single-file digital products platform on the planet — IndexedDB persistence, real-time auth, live sales, pro admin, instant cart, licensed delivery." />
  <style>
    :root {
      --bg: #0b0f14;
      --card: #121826;
      --muted: #9aa4b2;
      --txt: #e6e9ef;
      --accent: #6cf2c2;
      --danger: #ff6b6b;
      --success: #4ade80;
      --border: #1e2636;
    }
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: Inter, system-ui, -apple-system, sans-serif;
      background: linear-gradient(180deg, #0b0f14, #0e1320);
      color: var(--txt);
      line-height: 1.6;
    }
    header {
      position: sticky;
      top: 0;
      background: rgba(11,15,20,0.95);
      backdrop-filter: blur(16px);
      border-bottom: 1px solid var(--border);
      z-index: 20;
      padding: 16px 0;
    }
    .wrap { max-width: 1280px; margin: 0 auto; padding: 0 24px; }
    .nav { display: flex; align-items: center; gap: 24px; flex-wrap: wrap; }
    .brand { font-size: 28px; font-weight: 900; letter-spacing: -0.5px; }
    .spacer { flex: 1; }
    .btn {
      background: var(--accent);
      color: #052018;
      border: none;
      border-radius: 12px;
      padding: 12px 22px;
      font-weight: 700;
      cursor: pointer;
      transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .btn:hover { transform: translateY(-3px); box-shadow: 0 8px 20px rgba(108,242,194,0.35); }
    .btn.ghost { background: transparent; border: 1px solid var(--border); color: var(--txt); }
    .btn.danger { background: var(--danger); color: white; }
    .btn:disabled { opacity: 0.6; cursor: not-allowed; transform: none; }
    .pill { padding: 6px 14px; border-radius: 9999px; background: #1a2234; color: var(--muted); font-size: 13px; font-weight: 500; }
    .card {
      background: radial-gradient(1600px 400px at 20% -30%, #1a2240, transparent), var(--card);
      border: 1px solid var(--border);
      border-radius: 22px;
      padding: 26px;
      transition: transform 0.25s ease;
    }
    .product:hover { transform: translateY(-8px); }
    .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(290px, 1fr)); gap: 26px; }
    .thumb {
      height: 190px;
      border-radius: 18px;
      overflow: hidden;
      background: #1f2a44;
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
    }
    .thumb img { width: 100%; height: 100%; object-fit: cover; }
    .price { font-size: 26px; font-weight: 800; color: var(--accent); }
    .live-bar {
      background: #1a2234;
      border-radius: 14px;
      padding: 14px 24px;
      margin: 28px 24px;
      display: flex;
      align-items: center;
      gap: 32px;
      font-size: 15px;
      color: var(--muted);
    }
    .live-sale {
      animation: liveFade 0.6s ease;
    }
    @keyframes liveFade { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: none; } }
    .tabs { display: flex; gap: 16px; margin: 24px 24px 0; }
    .tab-button {
      padding: 14px 28px;
      background: none;
      border: 1px solid var(--border);
      border-radius: 14px;
      color: var(--txt);
      font-weight: 600;
      cursor: pointer;
      transition: all 0.2s;
    }
    .tab-button.active {
      background: var(--accent);
      color: #052018;
      border-color: var(--accent);
    }
    .modal {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.92);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 100;
      padding: 24px;
    }
    .modal-content {
      background: var(--card);
      border-radius: 22px;
      padding: 36px;
      max-width: 560px;
      width: 100%;
      max-height: 92vh;
      overflow: auto;
      box-shadow: 0 30px 80px rgba(0,0,0,0.8);
    }
    .admin-panel {
      position: fixed;
      top: 76px;
      right: -460px;
      width: 460px;
      height: calc(100vh - 76px);
      background: var(--card);
      border-left: 1px solid var(--border);
      transition: right 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
      z-index: 50;
      overflow-y: auto;
    }
    .admin-panel.open { right: 0; }
    .admin-stats { display: grid; grid-template-columns: repeat(3,1fr); gap: 18px; margin: 24px 0; }
    .stat-card { background: #0e1320; padding: 20px; border-radius: 16px; text-align: center; }
    .stat-card strong { font-size: 32px; color: var(--accent); font-weight: 800; }
    .admin-form input, .admin-form textarea, .admin-form select {
      width: 100%;
      padding: 15px;
      margin-bottom: 18px;
      background: #0e1320;
      border: 1px solid var(--border);
      border-radius: 14px;
      color: var(--txt);
      font-size: 15px;
    }
    .thumb-preview {
      height: 170px;
      background: #1a2234;
      border-radius: 14px;
      margin: 14px 0;
      display: none;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }
    .cart-item { padding: 18px 0; border-bottom: 1px solid var(--border); display: flex; justify-content: space-between; align-items: flex-start; }
    .qty-controls { display: flex; align-items: center; gap: 12px; background: #0e1320; padding: 6px; border-radius: 12px; }
    .toast {
      position: fixed;
      bottom: 36px;
      left: 50%;
      transform: translateX(-50%);
      background: var(--accent);
      color: #052018;
      padding: 18px 36px;
      border-radius: 16px;
      font-weight: 700;
      box-shadow: 0 16px 40px rgba(108,242,194,0.5);
      z-index: 200;
      animation: toastPop 0.4s cubic-bezier(0.34,1.56,0.64,1), toastFade 0.3s 2.5s forwards;
    }
    @keyframes toastPop { from { opacity:0; transform: translate(-50%,30px) scale(0.8); } to { opacity:1; transform: translate(-50%,0) scale(1); } }
    @keyframes toastFade { to { opacity:0; transform: translate(-50%,20px); } }
    .empty-state { text-align: center; padding: 80px 40px; color: var(--muted); }
    footer { border-top: 1px solid var(--border); padding: 40px 0; text-align: center; color: var(--muted); font-size: 14px; margin-top: 80px; }
    @media (max-width: 1024px) {
      .grid { grid-template-columns: repeat(auto-fill, minmax(260px, 1fr)); }
      .admin-panel { width: 100%; right: -100%; }
      .admin-stats { grid-template-columns: repeat(2,1fr); }
    }
  </style>
</head>
<body>
<header>
  <div class="wrap nav">
    <div class="brand">⚡ DigiSell Pro</div>
    <div class="pill">King of Single-File Commerce</div>
    <div class="spacer"></div>
    <div id="userDisplay" style="display:flex;align-items:center;gap:14px"></div>
    <button id="cartBtn" class="btn ghost" onclick="toggleCart()">🛒 Cart (<span id="cartCount">0</span>)</button>
    <button class="btn ghost" onclick="toggleAdmin()">Admin</button>
  </div>
</header>

<div class="live-bar">
  <span>👥 <strong id="onlineCount">52</strong> online</span>
  <span>🔴 Live: <span id="liveSales" style="color:var(--success)"></span></span>
</div>

<div class="wrap">
  <div class="tabs">
    <button class="tab-button active" onclick="showTab('products')">Products</button>
    <button class="tab-button" onclick="showTab('orders')">My Orders</button>
  </div>

  <div id="productsTab">
    <div style="display:flex;gap:20px;margin:32px 24px 24px">
      <input type="text" id="searchInput" placeholder="Search products..." style="flex:1;padding:16px;background:#0e1320;border:1px solid var(--border);border-radius:14px;font-size:16px" oninput="debouncedFilter()">
      <select id="categoryFilter" onchange="debouncedFilter()" style="padding:16px;background:#0e1320;border:1px solid var(--border);border-radius:14px;font-size:16px">
        <option value="">All Categories</option>
        <option value="ebook">Ebooks</option>
        <option value="software">Software</option>
        <option value="template">Templates</option>
        <option value="course">Courses</option>
      </select>
    </div>
    <div class="grid" id="productGrid"></div>
  </div>

  <div id="ordersTab" style="display:none">
    <div id="ordersContainer"></div>
  </div>
</div>

<footer>
  <div class="wrap">© 2026 DigiSell Pro • Ultimate One-File Real-Time Digital Store • IndexedDB + Live Features</div>
</footer>

<!-- CART DRAWER -->
<div id="cartDrawer" style="position:fixed;right:-420px;top:0;width:420px;height:100%;background:var(--card);border-left:1px solid var(--border);transition:right .4s cubic-bezier(0.34,1.56,0.64,1);z-index:60;overflow:auto">
  <div class="wrap" style="padding:32px 24px">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:28px">
      <h3>Your Cart</h3>
      <button class="btn ghost" onclick="toggleCart()">Close</button>
    </div>
    <div id="cartItems"></div>
    <div style="margin:40px 0 24px;padding:20px;background:#0e1320;border-radius:16px">
      <div style="display:flex;justify-content:space-between;font-size:19px;font-weight:700;margin-bottom:8px">
        <span>Total</span>
        <span id="cartTotal">$0</span>
      </div>
    </div>
    <button class="btn" onclick="checkout()" style="width:100%;padding:18px;font-size:17px">Checkout Securely</button>
  </div>
</div>

<!-- PRODUCT MODAL -->
<div class="modal" id="productModal">
  <div class="modal-content">
    <div style="display:flex;justify-content:space-between;align-items:start">
      <div>
        <h2 id="modalTitle" style="margin-bottom:8px"></h2>
        <div id="modalCategory" class="pill"></div>
      </div>
      <button onclick="closeModal()" style="font-size:36px;background:none;border:none;color:var(--muted);cursor:pointer;padding:8px">×</button>
    </div>
    <div id="modalThumb" class="thumb" style="margin:32px 0;height:260px"></div>
    <div id="modalDesc" style="margin-bottom:28px;font-size:15px"></div>
    <div style="display:flex;justify-content:space-between;align-items:end">
      <div>
        <div style="color:var(--muted);font-size:14px">Price</div>
        <div id="modalPrice" class="price"></div>
      </div>
      <div style="display:flex;gap:12px;align-items:center">
        <input type="number" id="modalQty" value="1" min="1" style="width:80px;padding:12px;background:#0e1320;border:1px solid var(--border);border-radius:12px;text-align:center;font-size:16px">
        <button class="btn" onclick="addCurrentToCart()" style="padding:16px 32px">Add to Cart</button>
      </div>
    </div>
  </div>
</div>

<!-- LOGIN MODAL -->
<div class="modal" id="loginModal">
  <div class="modal-content">
    <h2>Sign In to DigiSell</h2>
    <div style="margin:28px 0">
      <input type="text" id="loginUsername" placeholder="Username" style="margin-bottom:16px">
      <input type="password" id="loginPassword" placeholder="Password" style="margin-bottom:24px">
      <button class="btn" onclick="performLogin()" style="width:100%;margin-bottom:12px">Sign In</button>
      <button class="btn ghost" onclick="closeLoginModal()" style="width:100%">Cancel</button>
    </div>
    <div style="text-align:center;font-size:14px;color:var(--muted)">
      Demo: <strong>customer1</strong> / password123<br>
      Demo: <strong>customer2</strong> / password123
    </div>
  </div>
</div>

<!-- ADMIN PANEL -->
<div class="admin-panel" id="adminPanel">
  <div class="wrap">
    <h3 style="margin:28px 0 20px">Admin Dashboard</h3>
    <div style="margin-bottom:24px">
      <input type="password" id="adminPass" placeholder="Admin password" style="width:100%;padding:15px;background:#0e1320;border:1px solid var(--border);border-radius:14px;margin-bottom:12px">
      <button class="btn" onclick="loginAdmin()" style="width:100%">Enter Admin</button>
    </div>

    <div id="adminContent" style="display:none">
      <div class="admin-stats">
        <div class="stat-card"><strong id="statProducts">0</strong><div style="color:var(--muted);font-size:13px;margin-top:6px">Products</div></div>
        <div class="stat-card"><strong id="statOrders">0</strong><div style="color:var(--muted);font-size:13px;margin-top:6px">Orders</div></div>
        <div class="stat-card"><strong id="statRevenue">$0</strong><div style="color:var(--muted);font-size:13px;margin-top:6px">Revenue</div></div>
      </div>

      <div style="margin:24px 0">
        <input type="text" id="adminSearch" placeholder="Search products in catalog..." oninput="renderAdminProductList()" style="width:100%;padding:15px;background:#0e1320;border:1px solid var(--border);border-radius:14px">
        <button class="btn ghost" onclick="exportOrders()" style="width:100%;margin-top:12px">Export All Orders (JSON)</button>
      </div>

      <h4 style="margin:32px 0 16px">Add / Edit Product</h4>
      <div class="admin-form">
        <input type="text" id="prodTitle" placeholder="Title">
        <textarea id="prodDesc" placeholder="Description" rows="3"></textarea>
        <input type="number" id="prodPrice" placeholder="Price USD" step="0.01">
        <select id="prodCategory"><option value="ebook">Ebook</option><option value="software">Software</option><option value="template">Template</option><option value="course">Course</option></select>
        <select id="prodStatus"><option value="active">Active</option><option value="inactive">Inactive</option></select>
        <input type="text" id="prodTags" placeholder="Tags (comma separated)">
        <label style="display:block;margin:16px 0 8px;font-size:14px;color:var(--muted)">Thumbnail</label>
        <input type="file" id="prodThumb" accept="image/*" onchange="previewAdminThumb(this)">
        <div id="adminThumbPreview" class="thumb-preview"></div>
        <label style="display:block;margin:16px 0 8px;font-size:14px;color:var(--muted)">Product File</label>
        <input type="file" id="prodFile" onchange="previewAdminFile(this)">
        <div id="adminFilePreview" style="font-size:13px;color:var(--muted);margin:8px 0 24px"></div>
        <button class="btn" id="saveBtn" onclick="saveProduct()" style="width:100%;padding:16px">Save Product</button>
        <button class="btn ghost" onclick="resetProductForm()" style="width:100%;margin-top:12px">Clear Form</button>
      </div>

      <div style="margin-top:48px">
        <h4>Product Catalog</h4>
        <div id="adminProductList" style="margin-top:16px"></div>
      </div>
    </div>
  </div>
</div>

<script>
let db = null;
let allProducts = [];
let cart = [];
let currentModalProduct = null;
let currentEditingId = null;
let liveSalesQueue = [];
let onlineUsers = 52;
let currentUser = null;
let filterTimeout = null;

const ADMIN_PASS = "kingofinvention2026";
const DEMO_USERS = {
  "customer1": "password123",
  "customer2": "password123"
};
const FAKE_NAMES = ["Alex Rivera", "Jordan Kim", "Sam Patel", "Taylor Chen", "Morgan Ellis", "Casey Brooks", "Riley Quinn", "Jamie Harper", "Avery Lane", "Drew Parker"];

async function initDB() {
  return new Promise((resolve, reject) => {
    const request = indexedDB.open("DigiSellUltimateDB", 7);
    request.onupgradeneeded = e => {
      db = e.target.result;
      if (!db.objectStoreNames.contains("products")) {
        const store = db.createObjectStore("products", { keyPath: "id", autoIncrement: true });
        store.createIndex("category", "category", { unique: false });
      }
      if (!db.objectStoreNames.contains("orders")) {
        db.createObjectStore("orders", { keyPath: "id", autoIncrement: true });
      }
    };
    request.onsuccess = e => { db = e.target.result; resolve(); };
    request.onerror = e => reject(e.target.error);
  });
}

async function seedIfEmpty() {
  const tx = db.transaction("products", "readonly");
  const store = tx.objectStore("products");
  const count = await new Promise(r => { const req = store.count(); req.onsuccess = () => r(req.result); });
  if (count > 0) return;

  const samples = [
    {
      title: "AI Trading Mastery",
      description: "The definitive 380-page guide to AI-powered trading systems, quantitative analysis, and risk management.",
      price: 49,
      category: "ebook",
      status: "active",
      tags: "ai,trading,finance",
      thumbDataURL: "data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAwIiBoZWlnaHQ9IjIwMCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48cmVjdCB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiBmaWxsPSIjMWYyYTQ0IiByeD0iMjQiLz48dGV4dCB4PSI1MCUiIHk9IjQ4JSIgZmlsbD0iI2ZmZiIgZm9udC1zaXplPSI1MnB4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBkeT0iLjNlbSI+QUk8L3RleHQ+PHRleHQgeD0iNTAlIiB5PSI3NSUiIGZpbGw9IiNmZmYiIGZvbnQtc2l6ZT0iMjhweCIgdGV4dC1hbmNob3I9Im1pZGRsZSI+VFJBRElORzwvdGV4dD48L3N2Zz4=",
      fileDataURL: "data:application/pdf;base64," + btoa("AI Trading Mastery Sample"),
      fileName: "ai-trading-mastery.pdf",
      mimeType: "application/pdf"
    },
    {
      title: "Python Automation Pro Suite",
      description: "40+ enterprise-grade automation scripts for web scraping, data pipelines, and system orchestration.",
      price: 69,
      category: "software",
      status: "active",
      tags: "python,automation,devops",
      thumbDataURL: "data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAwIiBoZWlnaHQ9IjIwMCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48cmVjdCB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiBmaWxsPSIjMTkyYTQ0IiByeD0iMjQiLz48dGV4dCB4PSI1MCUiIHk9IjUwJSIgZmlsbD0iI2ZmZiIgZm9udC1zaXplPSI0OHB4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBkeT0iLjNlbSI+UHl0aG9uPC90ZXh0Pjwvc3ZnPg==",
      fileDataURL: "data:application/zip;base64," + btoa("Python Pro Suite"),
      fileName: "python-pro-suite.zip",
      mimeType: "application/zip"
    }
  ];

  const writeTx = db.transaction("products", "readwrite");
  const writeStore = writeTx.objectStore("products");
  for (let sample of samples) {
    await new Promise((res, rej) => {
      const req = writeStore.add(sample);
      req.onsuccess = res;
      req.onerror = rej;
    });
  }
}

async function loadAllProducts() {
  return new Promise((resolve, reject) => {
    const tx = db.transaction("products", "readonly");
    const store = tx.objectStore("products");
    const req = store.getAll();
    req.onsuccess = () => resolve(req.result);
    req.onerror = () => reject(req.error);
  });
}

function updateUserDisplay() {
  const el = document.getElementById("userDisplay");
  if (currentUser) {
    el.innerHTML = `
      <span style="color:var(--success)">👤 ${currentUser}</span>
      <button class="btn ghost" style="padding:8px 16px;font-size:13px" onclick="logout()">Logout</button>
    `;
  } else {
    el.innerHTML = `<button class="btn ghost" onclick="showLoginModal()">Sign In</button>`;
  }
}

function showLoginModal() {
  document.getElementById("loginModal").style.display = "flex";
  document.getElementById("loginUsername").focus();
}

function closeLoginModal() {
  document.getElementById("loginModal").style.display = "none";
}

function performLogin() {
  const username = document.getElementById("loginUsername").value.trim();
  const password = document.getElementById("loginPassword").value.trim();

  if (DEMO_USERS[username] === password) {
    currentUser = username;
    localStorage.setItem("digisell_user", username);
    closeLoginModal();
    updateUserDisplay();
    showToast(`Signed in as ${username}`);
    if (document.getElementById("ordersTab").style.display !== "none") showTab("orders");
  } else {
    alert("Invalid credentials");
  }
}

function logout() {
  currentUser = null;
  localStorage.removeItem("digisell_user");
  updateUserDisplay();
  showToast("Signed out");
}

function showTab(tab) {
  document.getElementById("productsTab").style.display = tab === "products" ? "block" : "none";
  document.getElementById("ordersTab").style.display = tab === "orders" ? "block" : "none";

  document.querySelectorAll(".tab-button").forEach(b => b.classList.remove("active"));
  document.querySelectorAll(".tab-button")[tab === "products" ? 0 : 1].classList.add("active");

  if (tab === "orders") {
    renderOrders();
  }
}

async function checkout() {
  if (cart.length === 0) return alert("Cart is empty");

  const email = prompt("Email for receipt and downloads:");
  if (!email || !email.includes("@")) return alert("Valid email required");

  const orderItems = cart.map(item => ({
    title: item.title,
    quantity: item.quantity,
    price: item.price,
    licenseKey: item.type === "software" ? "DS-" + Math.random().toString(36).substring(2,14).toUpperCase() : null,
    fileDataURL: item.fileDataURL,
    fileName: item.fileName
  }));

  const total = cart.reduce((sum, i) => sum + i.price * i.quantity, 0);

  const order = {
    date: new Date().toISOString(),
    user: currentUser || "guest",
    email,
    total,
    items: orderItems
  };

  await saveOrder(order);

  // Show receipt
  let receiptHTML = `<div style="color:var(--success);font-size:24px;font-weight:700;margin-bottom:20px">✅ Purchase Complete</div>`;
  receiptHTML += `<p>Receipt for <strong>${email}</strong></p>`;
  receiptHTML += `<p style="font-size:18px;margin:20px 0">Total: <strong>$${total}</strong></p>`;

  orderItems.forEach(item => {
    receiptHTML += `<div style="padding:18px;background:#0e1320;border-radius:14px;margin-bottom:16px">`;
    receiptHTML += `<strong>${item.title}</strong> × ${item.quantity}<br>`;
    if (item.licenseKey) receiptHTML += `License: <span style="font-family:monospace;background:#1a2234;padding:4px 12px;border-radius:6px">${item.licenseKey}</span><br>`;
    if (item.fileDataURL) receiptHTML += `<button onclick="downloadFile('${item.fileDataURL}','${item.fileName}')" class="btn" style="margin-top:12px">Download ${item.fileName}</button>`;
    receiptHTML += `</div>`;
  });

  const receiptModal = document.createElement("div");
  receiptModal.className = "modal";
  receiptModal.style.display = "flex";
  receiptModal.innerHTML = `<div class="modal-content">${receiptHTML}<button class="btn ghost" onclick="this.closest('.modal').remove()" style="margin-top:24px;width:100%">Close Receipt</button></div>`;
  document.body.appendChild(receiptModal);

  cart = [];
  persistCart();
  updateCartCount();
  toggleCart();

  if (currentUser) {
    setTimeout(() => showTab("orders"), 600);
  } else {
    showToast("Order placed! Sign in to view your orders.");
  }
}

function downloadFile(dataURL, filename) {
  const link = document.createElement("a");
  link.href = dataURL;
  link.download = filename;
  document.body.appendChild(link);
  link.click();
  document.body.removeChild(link);
}

async function saveOrder(order) {
  return new Promise((resolve, reject) => {
    const tx = db.transaction("orders", "readwrite");
    const store = tx.objectStore("orders");
    const req = store.add(order);
    req.onsuccess = resolve;
    req.onerror = () => reject(req.error);
  });
}

async function getAllOrders() {
  return new Promise((resolve, reject) => {
    const tx = db.transaction("orders", "readonly");
    const store = tx.objectStore("orders");
    const req = store.getAll();
    req.onsuccess = () => resolve(req.result);
    req.onerror = () => reject(req.error);
  });
}

async function renderOrders() {
  const container = document.getElementById("ordersContainer");
  container.innerHTML = "";

  if (!currentUser) {
    container.innerHTML = `
      <div class="card empty-state">
        <div style="font-size:48px;margin-bottom:16px">🔐</div>
        <h3>Sign in to view your orders</h3>
        <p style="margin:16px 0">Track purchases, download files, and manage licenses</p>
        <button class="btn" onclick="showLoginModal()">Sign In Now</button>
      </div>
    `;
    return;
  }

  const orders = await getAllOrders();
  const userOrders = orders.filter(o => o.user === currentUser).sort((a,b) => new Date(b.date) - new Date(a.date));

  if (userOrders.length === 0) {
    container.innerHTML = `
      <div class="card empty-state">
        <div style="font-size:48px;margin-bottom:16px">📭</div>
        <h3>No orders yet</h3>
        <p>Browse our catalog and make your first purchase</p>
      </div>
    `;
    return;
  }

  const grid = document.createElement("div");
  grid.className = "grid";
  userOrders.forEach(order => {
    const div = document.createElement("div");
    div.className = "card";
    let html = `<div style="display:flex;justify-content:space-between;margin-bottom:18px"><div><strong>Order #${order.id}</strong><br>${new Date(order.date).toLocaleDateString()}</div><div class="price">$${order.total}</div></div>`;
    html += `<div style="color:var(--muted)">${order.email}</div>`;
    html += `<div style="margin:24px 0 12px;font-weight:600">Items:</div>`;

    order.items.forEach(item => {
      html += `<div style="padding:16px;background:#1a2234;border-radius:14px;margin-bottom:14px">`;
      html += `<strong>${item.title}</strong> × ${item.quantity}<br>`;
      if (item.licenseKey) html += `License: <span style="font-family:monospace;background:#0e1320;padding:4px 12px;border-radius:6px">${item.licenseKey}</span><br>`;
      if (item.fileDataURL) html += `<button onclick="downloadFile('${item.fileDataURL}','${item.fileName}')" class="btn" style="margin-top:12px;font-size:14px">Re-download</button>`;
      html += `</div>`;
    });

    div.innerHTML = html;
    grid.appendChild(div);
  });
  container.appendChild(grid);
}

function toggleCart() {
  const drawer = document.getElementById("cartDrawer");
  const isOpen = drawer.style.right === "0px";
  drawer.style.right = isOpen ? "-420px" : "0px";
  if (!isOpen) renderCart();
}

function renderCart() {
  const container = document.getElementById("cartItems");
  container.innerHTML = "";
  let total = 0;

  if (cart.length === 0) {
    container.innerHTML = `<div class="empty-state"><div style="font-size:64px;margin-bottom:16px">🛒</div><h3>Your cart is empty</h3><p>Browse products to get started</p></div>`;
    document.getElementById("cartTotal").textContent = "$0";
    return;
  }

  cart.forEach((item, index) => {
    const itemTotal = item.price * item.quantity;
    total += itemTotal;

    const el = document.createElement("div");
    el.className = "cart-item";
    el.innerHTML = `
      <div>
        <div style="font-weight:600">${item.title}</div>
        <div style="color:var(--muted);font-size:14px">$${item.price} × ${item.quantity}</div>
      </div>
      <div style="text-align:right">
        <div style="font-weight:700">$${itemTotal}</div>
        <div class="qty-controls" style="margin-top:14px">
          <button onclick="changeQuantity(${index}, -1)">−</button>
          <span style="min-width:32px;text-align:center">${item.quantity}</span>
          <button onclick="changeQuantity(${index}, 1)">+</button>
          <button onclick="removeFromCart(${index})" class="btn danger" style="margin-left:20px;padding:6px 14px;font-size:13px">Remove</button>
        </div>
      </div>
    `;
    container.appendChild(el);
  });

  document.getElementById("cartTotal").textContent = "$" + total;
}

function changeQuantity(index, delta) {
  cart[index].quantity += delta;
  if (cart[index].quantity < 1) cart[index].quantity = 1;
  persistCart();
  renderCart();
  updateCartCount();
}

function removeFromCart(index) {
  cart.splice(index, 1);
  persistCart();
  renderCart();
  updateCartCount();
}

function persistCart() {
  localStorage.setItem("digisell_cart", JSON.stringify(cart));
}

function loadCart() {
  const saved = localStorage.getItem("digisell_cart");
  if (saved) cart = JSON.parse(saved);
}

function updateCartCount() {
  document.getElementById("cartCount").textContent = cart.length;
}

function addToCart(id, qty = 1) {
  qty = parseInt(qty) || 1;
  if (qty < 1) qty = 1;

  const product = allProducts.find(p => p.id === id);
  if (!product) return;

  const existing = cart.findIndex(item => item.id === id);
  if (existing >= 0) {
    cart[existing].quantity += qty;
  } else {
    cart.push({
      id: product.id,
      title: product.title,
      price: product.price,
      quantity: qty,
      fileDataURL: product.fileDataURL,
      fileName: product.fileName,
      type: product.category
    });
  }

  persistCart();
  updateCartCount();

  const cartBtn = document.getElementById("cartBtn");
  cartBtn.classList.add("pulse");
  setTimeout(() => cartBtn.classList.remove("pulse"), 900);

  showToast(`Added ${qty} × ${product.title}`);
}

function addCurrentToCart() {
  if (!currentModalProduct) return;
  const qty = parseInt(document.getElementById("modalQty").value) || 1;
  addToCart(currentModalProduct.id, qty);
  closeModal();
}

function showProductModal(id) {
  currentModalProduct = allProducts.find(p => p.id === id);
  if (!currentModalProduct) return;

  document.getElementById("modalTitle").textContent = currentModalProduct.title;
  document.getElementById("modalCategory").textContent = currentModalProduct.category.toUpperCase();
  document.getElementById("modalDesc").textContent = currentModalProduct.description;
  document.getElementById("modalPrice").textContent = "$" + currentModalProduct.price;
  document.getElementById("modalQty").value = "1";

  const thumbEl = document.getElementById("modalThumb");
  thumbEl.innerHTML = currentModalProduct.thumbDataURL 
    ? `<img src="${currentModalProduct.thumbDataURL}" style="width:100%;height:100%;object-fit:cover;border-radius:18px">`
    : `<div style="font-size:92px;opacity:0.2">${currentModalProduct.title.charAt(0)}</div>`;

  document.getElementById("productModal").style.display = "flex";
}

function closeModal() {
  document.getElementById("productModal").style.display = "none";
  currentModalProduct = null;
}

function renderProductGrid(filtered = null) {
  const grid = document.getElementById("productGrid");
  grid.innerHTML = "";

  const products = filtered || allProducts;
  if (products.length === 0) {
    grid.innerHTML = `<div class="card empty-state"><div style="font-size:64px;margin-bottom:16px">🔍</div><h3>No products found</h3><p>Try a different search term</p></div>`;
    return;
  }

  products.forEach(p => {
    if (p.status === "inactive") return;

    const div = document.createElement("div");
    div.className = "card product";
    div.onclick = () => showProductModal(p.id);

    const tagsHTML = p.tags ? `<div style="display:flex;gap:6px;margin-top:8px;flex-wrap:wrap">${p.tags.split(',').map(t => `<span class="pill" style="font-size:11px">${t.trim()}</span>`).join('')}</div>` : '';

    div.innerHTML = `
      <div class="thumb">
        ${p.thumbDataURL ? `<img src="${p.thumbDataURL}" alt="${p.title}">` : `<div style="font-size:68px;opacity:0.2">${p.title.charAt(0)}</div>`}
      </div>
      <div style="margin-top:18px">
        <div style="display:flex;justify-content:space-between;align-items:start">
          <strong style="font-size:19px">${p.title}</strong>
          <div class="price">$${p.price}</div>
        </div>
        <div style="color:var(--muted);margin:10px 0 12px;font-size:14px">${p.description.substring(0, 92)}${p.description.length > 92 ? '...' : ''}</div>
        ${tagsHTML}
        <div style="display:flex;gap:12px;align-items:center;margin-top:16px">
          <input type="number" min="1" value="1" id="qty-${p.id}" style="width:72px;padding:10px;background:#0e1320;border:1px solid var(--border);border-radius:12px;text-align:center">
          <button class="btn" style="flex:1;padding:12px" onclick="event.stopPropagation(); addToCart(${p.id}, document.getElementById('qty-${p.id}').value)">Add to Cart</button>
        </div>
      </div>
    `;
    grid.appendChild(div);
  });
}

function debouncedFilter() {
  clearTimeout(filterTimeout);
  filterTimeout = setTimeout(() => {
    const term = document.getElementById("searchInput").value.toLowerCase().trim();
    const cat = document.getElementById("categoryFilter").value;

    let filtered = allProducts.filter(p => p.status === "active");

    if (term) {
      filtered = filtered.filter(p => 
        p.title.toLowerCase().includes(term) || 
        (p.description && p.description.toLowerCase().includes(term)) ||
        (p.tags && p.tags.toLowerCase().includes(term))
      );
    }
    if (cat) filtered = filtered.filter(p => p.category === cat);

    renderProductGrid(filtered);
  }, 180);
}

function updateLiveSales() {
  if (allProducts.length === 0) return;
  const buyer = FAKE_NAMES[Math.floor(Math.random() * FAKE_NAMES.length)];
  const product = allProducts[Math.floor(Math.random() * allProducts.length)];
  liveSalesQueue.unshift(`${buyer} bought <strong>${product.title}</strong>`);
  if (liveSalesQueue.length > 4) liveSalesQueue.pop();

  const liveEl = document.getElementById("liveSales");
  liveEl.innerHTML = liveSalesQueue.join(" • ");
  liveEl.classList.add("live-sale");
  setTimeout(() => liveEl.classList.remove("live-sale"), 800);
}

function updateOnlineUsers() {
  onlineUsers = 42 + Math.floor(Math.random() * 38);
  document.getElementById("onlineCount").textContent = onlineUsers;
}

function showToast(message) {
  const toast = document.createElement("div");
  toast.className = "toast";
  toast.textContent = message;
  document.body.appendChild(toast);

  setTimeout(() => {
    toast.style.opacity = "0";
    setTimeout(() => toast.remove(), 500);
  }, 2600);
}

function toggleAdmin() {
  document.getElementById("adminPanel").classList.toggle("open");
}

function loginAdmin() {
  const pass = document.getElementById("adminPass").value;
  if (pass === ADMIN_PASS) {
    document.getElementById("adminContent").style.display = "block";
    document.getElementById("adminPass").value = "";
    updateAdminStats();
    renderAdminProductList();
  } else {
    alert("Access denied");
  }
}

async function updateAdminStats() {
  const products = await loadAllProducts();
  const orders = await getAllOrders();
  const revenue = orders.reduce((sum, o) => sum + (o.total || 0), 0);

  document.getElementById("statProducts").textContent = products.length;
  document.getElementById("statOrders").textContent = orders.length;
  document.getElementById("statRevenue").textContent = "$" + revenue.toFixed(2);
}

function previewAdminThumb(input) {
  const preview = document.getElementById("adminThumbPreview");
  if (input.files && input.files[0]) {
    const reader = new FileReader();
    reader.onload = e => {
      preview.style.display = "flex";
      preview.innerHTML = `<img src="${e.target.result}" style="max-height:100%;border-radius:12px">`;
    };
    reader.readAsDataURL(input.files[0]);
  }
}

function previewAdminFile(input) {
  const el = document.getElementById("adminFilePreview");
  if (input.files && input.files[0]) {
    const f = input.files[0];
    el.textContent = `Selected: ${f.name} (${(f.size/1024/1024).toFixed(2)} MB)`;
  } else el.textContent = "";
}

async function saveProduct() {
  const title = document.getElementById("prodTitle").value.trim();
  const description = document.getElementById("prodDesc").value.trim();
  const priceStr = document.getElementById("prodPrice").value.trim();
  const category = document.getElementById("prodCategory").value;
  const status = document.getElementById("prodStatus").value;
  const tags = document.getElementById("prodTags").value.trim();

  const thumbFile = document.getElementById("prodThumb").files[0];
  const mainFile = document.getElementById("prodFile").files[0];

  if (!title || !priceStr || isNaN(parseFloat(priceStr))) {
    alert("Title and price are required");
    return;
  }

  const price = parseFloat(priceStr);

  let thumbDataURL = null;
  if (thumbFile) {
    thumbDataURL = await new Promise(res => {
      const r = new FileReader();
      r.onload = e => res(e.target.result);
      r.readAsDataURL(thumbFile);
    });
  }

  let fileDataURL = null;
  let fileName = null;
  let mimeType = null;
  if (mainFile) {
    fileDataURL = await new Promise(res => {
      const r = new FileReader();
      r.onload = e => res(e.target.result);
      r.readAsDataURL(mainFile);
    });
    fileName = mainFile.name;
    mimeType = mainFile.type;
  }

  const productData = {
    title,
    description,
    price,
    category,
    status,
    tags,
    thumbDataURL,
    fileDataURL,
    fileName,
    mimeType
  };

  const tx = db.transaction("products", "readwrite");
  const store = tx.objectStore("products");

  if (currentEditingId) {
    productData.id = currentEditingId;
    await new Promise((res, rej) => {
      const req = store.put(productData);
      req.onsuccess = res;
      req.onerror = rej;
    });
  } else {
    await new Promise((res, rej) => {
      const req = store.add(productData);
      req.onsuccess = res;
      req.onerror = rej;
    });
  }

  allProducts = await loadAllProducts();
  renderProductGrid();
  renderAdminProductList();
  await updateAdminStats();

  resetProductForm();
  showToast(currentEditingId ? "Product updated" : "Product created");
  currentEditingId = null;
  document.getElementById("saveBtn").textContent = "Save Product";
}

function resetProductForm() {
  document.getElementById("prodTitle").value = "";
  document.getElementById("prodDesc").value = "";
  document.getElementById("prodPrice").value = "";
  document.getElementById("prodCategory").value = "ebook";
  document.getElementById("prodStatus").value = "active";
  document.getElementById("prodTags").value = "";
  document.getElementById("prodThumb").value = "";
  document.getElementById("prodFile").value = "";
  document.getElementById("adminThumbPreview").style.display = "none";
  document.getElementById("adminFilePreview").textContent = "";
  currentEditingId = null;
  document.getElementById("saveBtn").textContent = "Save Product";
}

async function renderAdminProductList() {
  const container = document.getElementById("adminProductList");
  container.innerHTML = "";

  const searchTerm = (document.getElementById("adminSearch") ? document.getElementById("adminSearch").value.toLowerCase().trim() : "");

  let products = await loadAllProducts();
  if (searchTerm) {
    products = products.filter(p => 
      p.title.toLowerCase().includes(searchTerm) ||
      (p.description && p.description.toLowerCase().includes(searchTerm)) ||
      (p.tags && p.tags.toLowerCase().includes(searchTerm))
    );
  }

  if (products.length === 0) {
    container.innerHTML = `<div style="padding:60px;text-align:center;color:var(--muted)">No products found</div>`;
    return;
  }

  products.forEach(p => {
    const row = document.createElement("div");
    row.style = "display:flex;justify-content:space-between;align-items:center;padding:20px 0;border-bottom:1px solid var(--border)";
    const statusClass = p.status === "active" ? "active" : "inactive";
    row.innerHTML = `
      <div>
        <div style="font-weight:600">${p.title}</div>
        <div style="color:var(--muted);font-size:14px">$${p.price} • ${p.category} • <span class="product-status ${statusClass}">${p.status}</span></div>
      </div>
      <div>
        <button onclick="startEditProduct(${p.id})" class="btn ghost" style="padding:8px 16px;margin-right:8px">Edit</button>
        <button onclick="deleteProduct(${p.id})" class="btn danger" style="padding:8px 16px">Delete</button>
      </div>
    `;
    container.appendChild(row);
  });
}

async function deleteProduct(id) {
  if (!confirm("Delete product permanently?")) return;

  const tx = db.transaction("products", "readwrite");
  const store = tx.objectStore("products");
  await new Promise((res, rej) => {
    const req = store.delete(id);
    req.onsuccess = res;
    req.onerror = rej;
  });

  allProducts = await loadAllProducts();
  renderProductGrid();
  renderAdminProductList();
  await updateAdminStats();
  showToast("Product deleted");
}

function startEditProduct(id) {
  const product = allProducts.find(p => p.id === id);
  if (!product) return;

  currentEditingId = id;

  document.getElementById("prodTitle").value = product.title;
  document.getElementById("prodDesc").value = product.description || "";
  document.getElementById("prodPrice").value = product.price;
  document.getElementById("prodCategory").value = product.category;
  document.getElementById("prodStatus").value = product.status || "active";
  document.getElementById("prodTags").value = product.tags || "";

  if (product.thumbDataURL) {
    const preview = document.getElementById("adminThumbPreview");
    preview.style.display = "flex";
    preview.innerHTML = `<img src="${product.thumbDataURL}" style="max-height:100%;border-radius:12px">`;
  }

  document.getElementById("saveBtn").textContent = "Update Product";
}

async function exportOrders() {
  const orders = await getAllOrders();
  if (orders.length === 0) return alert("No orders to export");

  const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(orders, null, 2));
  const downloadAnchor = document.createElement("a");
  downloadAnchor.setAttribute("href", dataStr);
  downloadAnchor.setAttribute("download", `digisell-orders-${new Date().toISOString().slice(0,10)}.json`);
  document.body.appendChild(downloadAnchor);
  downloadAnchor.click();
  downloadAnchor.remove();
}

function toggleAdmin() { document.getElementById("adminPanel").classList.toggle("open"); }

window.onload = async () => {
  try {
    await initDB();
    await seedIfEmpty();
    allProducts = await loadAllProducts();

    const savedUser = localStorage.getItem("digisell_user");
    if (savedUser) currentUser = savedUser;

    loadCart();
    updateCartCount();
    renderProductGrid();
    updateUserDisplay();

    setInterval(updateLiveSales, 8500);
    setInterval(updateOnlineUsers, 6500);

    updateLiveSales();
    updateOnlineUsers();

    console.log("🚀 DigiSell Pro Ultimate initialized — King of single-file real-time commerce");
  } catch (err) {
    console.error("Init error:", err);
    alert("Database initialization failed");
  }
};
</script>
</body>
</html>
