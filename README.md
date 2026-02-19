<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FIREWORKS PREMIUM · pre-order</title>
    <!-- Fonts & Icons -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <!-- GSAP & Anime (lean) -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Space Grotesk', sans-serif;
        }
        body {
            background-color: #0c0b0e;
            color: #f0e9e1;
            overflow-x: hidden;
            position: relative;
        }
        /* fire background spark */
        body::before {
            content: '';
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: radial-gradient(circle at 30% 40%, rgba(255, 69, 0, 0.05) 0%, transparent 40%),
                        radial-gradient(circle at 80% 70%, rgba(255, 140, 0, 0.06) 0%, transparent 45%),
                        repeating-linear-gradient(45deg, rgba(255, 60, 0, 0.02) 0px, rgba(0,0,0,0) 2px);
            pointer-events: none;
            z-index: 0;
        }
        .glass-panel, .product-card, .admin-section, .modal-content, .auth-card {
            background: rgba(20, 15, 20, 0.7);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 80, 0, 0.25);
            border-radius: 32px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.8), 0 0 0 1px rgba(255, 60, 0, 0.2) inset, 0 0 20px rgba(255, 40, 0, 0.3);
        }
        .neon-glow {
            text-shadow: 0 0 8px #ff4d00, 0 0 16px #ff7700;
        }
        .btn-neon {
            background: rgba(255, 70, 0, 0.15);
            border: 1.5px solid #ff5e00;
            color: #ffb49a;
            border-radius: 60px;
            padding: 12px 28px;
            font-weight: 600;
            transition: all 0.2s ease;
            box-shadow: 0 0 12px rgba(255, 80, 0, 0.3);
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }
        .btn-neon:hover {
            background: #ff5e00;
            color: #0c0b0e;
            box-shadow: 0 0 30px #ff5e00;
            border-color: #ffaa33;
            transform: scale(1.02);
        }
        .btn-neon:active { transform: scale(0.98); }
        .ripple-effect {
            position: relative;
            overflow: hidden;
        }
        .ripple-effect:after {
            content: '';
            position: absolute;
            top: 50%; left: 50%;
            width: 5px; height: 5px;
            background: rgba(255,255,255,0.7);
            opacity: 0;
            border-radius: 100%;
            transform: scale(1) translate(-50%, -50%);
            transform-origin: 50% 50%;
        }
        .ripple-effect:focus:after {
            animation: ripple 0.5s ease-out;
        }
        @keyframes ripple {
            0% { transform: scale(0) translate(-50%, -50%); opacity: 0.7; }
            100% { transform: scale(20) translate(-50%, -50%); opacity: 0; }
        }

        /* layout */
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 1.5rem 2rem;
            position: relative;
            z-index: 5;
        }
        .flex-row {
            display: flex;
            flex-wrap: wrap;
            gap: 2rem;
            align-items: center;
            justify-content: space-between;
        }
        .grid-products {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 2rem;
            margin: 3rem 0;
        }
        /* product card */
        .product-card {
            padding: 1.8rem 1.2rem 1.5rem;
            transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
            text-align: center;
            cursor: pointer;
            border-radius: 40px;
            background: rgba(18, 12, 18, 0.75);
            border: 1px solid rgba(255, 100, 0, 0.3);
            backdrop-filter: blur(10px);
            transform: translateY(0);
        }
        .product-card:hover {
            transform: translateY(-12px) scale(1.02);
            border-color: #ff5e00;
            box-shadow: 0 30px 40px -10px #ff5e0033, 0 0 30px #ff5e0040;
        }
        .product-img {
            width: 100%;
            aspect-ratio: 1/1.1;
            object-fit: cover;
            border-radius: 28px;
            background: linear-gradient(145deg, #332211, #1f130a);
            margin-bottom: 1rem;
            border: 2px solid #ff5e0033;
            transition: transform 0.4s ease;
        }
        .product-card:hover .product-img {
            transform: scale(0.97) rotate(0.5deg);
            border-color: #ff983d;
        }
        .price-tag {
            font-size: 1.7rem;
            font-weight: 700;
            color: #ffaa33;
            text-shadow: 0 0 10px #ff5e00;
        }
        .stock-badge {
            background: rgba(255, 80, 0, 0.3);
            padding: 0.2rem 1rem;
            border-radius: 40px;
            font-size: 0.8rem;
            border: 1px solid #ff5e00;
            display: inline-block;
        }
        /* hero */
        .hero {
            padding: 3rem 2rem;
            border-radius: 60px;
            background: rgba(0,0,0,0.35);
            backdrop-filter: blur(8px);
            margin: 2rem 0 3rem;
            border: 1px solid #ff5e0040;
            box-shadow: 0 0 60px #ff2f0030;
            text-align: center;
        }
        .hero h1 {
            font-size: clamp(2.8rem, 8vw, 5.5rem);
            font-weight: 700;
            line-height: 1.1;
        }
        .urgent-banner {
            background: #ff3c00b3;
            padding: 0.7rem 1.8rem;
            border-radius: 60px;
            display: inline-block;
            font-weight: 600;
            backdrop-filter: blur(4px);
            box-shadow: 0 0 20px #ff5e00;
            border: 1px solid #ffb347;
            margin: 1rem 0;
            animation: pulseGlow 1.8s infinite;
        }
        @keyframes pulseGlow {
            0% { box-shadow: 0 0 10px #ff5e00; }
            50% { box-shadow: 0 0 30px #ff3c00; }
            100% { box-shadow: 0 0 10px #ff5e00; }
        }

        /* auth modal / glass card */
        .auth-card {
            max-width: 440px;
            margin: 2rem auto;
            padding: 2.2rem;
            border-radius: 48px;
        }
        .input-field {
            background: rgba(30, 20, 22, 0.8);
            border: 1px solid #ff5e0050;
            border-radius: 60px;
            padding: 1rem 1.5rem;
            width: 100%;
            color: #fff;
            font-size: 1rem;
            transition: 0.2s;
        }
        .input-field:focus {
            border-color: #ff983d;
            outline: none;
            box-shadow: 0 0 20px #ff5e00;
        }
        .floating-wa {
            position: fixed;
            bottom: 30px; right: 30px;
            background: #25D366;
            width: 70px; height: 70px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.5rem;
            color: white;
            box-shadow: 0 10px 25px #25D36680, 0 0 0 10px #25d36620;
            animation: pulseWa 2s infinite;
            z-index: 999;
            transition: 0.2s;
            border: 2px solid white;
        }
        .floating-wa:hover {
            transform: scale(1.1) rotate(5deg);
            background: #20b859;
        }
        @keyframes pulseWa {
            0% { box-shadow: 0 0 0 0 #25D366, 0 0 0 10px rgba(37, 211, 102,0.2); }
            70% { box-shadow: 0 0 0 15px #25D36630, 0 0 0 25px rgba(37,211,102,0); }
            100% { box-shadow: 0 0 0 0 #25D366, 0 0 0 10px rgba(37,211,102,0); }
        }
        /* admin panel */
        .admin-section {
            padding: 2rem;
            margin: 2rem 0;
            border-radius: 50px;
            background: rgba(10, 5, 10, 0.8);
        }
        .order-row {
            background: #2f1f1b60;
            padding: 1rem;
            border-radius: 30px;
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            align-items: center;
            border-left: 6px solid #ff5e00;
            margin: 0.5rem 0;
        }
        .chip {
            background: #3d2a24;
            padding: 0.4rem 1.2rem;
            border-radius: 60px;
            font-size: 0.8rem;
            font-weight: 600;
        }
        .expired { border-left-color: #5a5a5a; opacity: 0.8; background: #2a1e1e; }
        /* modal */
        .modal-overlay {
            position: fixed;
            top:0; left:0; width:100%; height:100%;
            background: rgba(0,0,0,0.7);
            backdrop-filter: blur(8px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 10000;
            opacity: 0;
            visibility: hidden;
            transition: 0.3s;
        }
        .modal-overlay.active {
            opacity: 1;
            visibility: visible;
        }
        .modal-content {
            max-width: 480px;
            width: 90%;
            padding: 2rem;
            border-radius: 60px;
            transform: scale(0.8);
            transition: 0.3s;
        }
        .modal-overlay.active .modal-content {
            transform: scale(1);
        }
        .quantity-selector {
            display: flex;
            gap: 1rem;
            align-items: center;
            justify-content: center;
            margin: 1.5rem 0;
        }
        .qty-btn {
            background: #2e1c16;
            border: none;
            color: #ffa55c;
            font-size: 2rem;
            width: 50px;
            height: 50px;
            border-radius: 30px;
            cursor: pointer;
            transition: 0.2s;
            border: 1px solid #ff5e00;
        }
        .qty-btn:hover {
            background: #ff5e00;
            color: black;
        }
        /* animations on page load */
        .fade-up { animation: fadeUp 0.6s both; }
        @keyframes fadeUp { from { opacity:0; transform: translateY(30px); } to { opacity:1; transform:translateY(0); } }
        
        /* legal footer */
        .legal-footer {
            background: #120d0e;
            border-radius: 60px;
            padding: 2rem;
            margin-top: 4rem;
            border: 1px solid #ff5e0040;
            font-size: 0.9rem;
        }
        hr { border-color: #ff5e0030; margin: 1.5rem 0; }
    </style>
</head>
<body>

<div class="container">

    <!-- HEADER with AUTH (simulated) -->
    <div class="flex-row" style="margin-bottom: 1rem;">
        <div class="logo" style="font-weight:700; font-size:1.9rem; letter-spacing:-0.5px;"><span style="color:#ff5e00;">✹</span> BLAST<span style="color:#ff983d;">PREMIUM</span></div>
        <div>
            <button class="btn-neon ripple-effect" id="showAuthBtn"><i class="fa-brands fa-google"></i> Google / Login</button>
        </div>
    </div>

    <!-- HERO -->
    <div class="hero fade-up">
        <div class="urgent-banner">🔥 LIMITED FESTIVAL STOCK – BOOK NOW 🔥</div>
        <h1 class="neon-glow">Premium Firecrackers<br>Pre‑Order Now</h1>
        <p style="font-size: 1.4rem; margin: 1rem 0; color: #ffcfaa;"><i class="fa-regular fa-clock"></i> Pickup valid only for 3 days after order.</p>
        <div id="countdown" style="font-size: 2rem; font-weight: 700; background: #00000040; display: inline-block; padding: 0.5rem 2.5rem; border-radius: 60px; border:1px solid #ff5e00;">🔥 DIWALI countdown 12d 04h</div>
    </div>

    <!-- PRODUCTS grid (glassmorphism) -->
    <h2 style="font-size: 2.4rem; margin: 2rem 0 1rem;">✨ Spark Collection</h2>
    <div class="grid-products" id="productGrid"></div>

    <!-- ADMIN PANEL (single dealer) visible by default for demo (toggle later) -->
    <div class="admin-section" id="adminPanel">
        <div style="display: flex; gap: 1rem; flex-wrap: wrap; align-items: center; justify-content: space-between;">
            <h2 style="color:#ffaa33;"><i class="fa-regular fa-pen-to-square"></i> Dealer dashboard</h2>
            <div>
                <button class="btn-neon" id="addProductBtn"><i class="fa-regular fa-plus"></i> Add product</button>
            </div>
        </div>
        <!-- product management forms (hidden by default) -->
        <div id="productFormContainer" style="display: none; margin: 2rem 0; background: #251a16; padding: 2rem; border-radius: 40px;">
            <h3 id="formTitle">Add product</h3>
            <input type="text" id="productName" placeholder="Name" class="input-field" value="Laser Crackers">
            <input type="number" id="productPrice" placeholder="Price (₹)" class="input-field" value="699">
            <input type="number" id="productStock" placeholder="Stock" class="input-field" value="50">
            <input type="text" id="productImg" placeholder="Image URL" class="input-field" value="https://images.pexels.com/photos/2573603/pexels-photo-2573603.jpeg?auto=compress&cs=tinysrgb&w=400">
            <button class="btn-neon" id="saveProductBtn">Save product</button>
            <button class="btn-neon" id="cancelProductBtn" style="background:transparent;">Cancel</button>
        </div>

        <h3 style="margin-top:2rem;">📋 All pre-orders</h3>
        <div id="ordersList"></div>
        <!-- small admin product list edit -->
        <h3 style="margin-top:2rem;">✎ Manage products (click to edit/delete)</h3>
        <div id="adminProductList"></div>
    </div>

    <!-- LEGAL & SAFETY -->
    <div class="legal-footer">
        <div style="display:flex; flex-wrap:wrap; gap:2rem; justify-content:center; text-align:center;">
            <span><i class="fa-regular fa-circle-check" style="color:#ff5e00;"></i> Age 18+ only</span>
            <span><i class="fa-regular fa-fire" style="color:#ff5e00;"></i> Use under adult supervision</span>
            <span><i class="fa-regular fa-shop"></i> Pickup from store only (3 days)</span>
            <span><i class="fa-regular fa-id-card"></i> License # FSTK/567/DEL</span>
        </div>
        <hr>
        <div style="font-size:0.8rem; color:#aaa;">⚠️ SAFETY: Keep water nearby, light one at a time, never relight duds. Store in cool dry place.</div>
    </div>
</div>

<!-- FLOATING WHATSAPP BUTTON -->
<a href="https://wa.me/9779806916002" target="_blank" class="floating-wa" id="waFloat"><i class="fa-brands fa-whatsapp"></i></a>

<!-- AUTH MODAL (glassmorphism) -->
<div class="modal-overlay" id="authModal">
    <div class="modal-content" style="text-align:center;">
        <h2 style="color:#ffaa33;">🔐 secure login</h2>
        <button class="btn-neon" style="width:100%; margin:1rem 0;"><i class="fa-brands fa-google"></i> Continue with Google</button>
        <div style="display:flex; gap:0.5rem;"><hr style="flex:1;">or<hr style="flex:1;"></div>
        <input type="email" placeholder="Email" class="input-field" value="demo@user.com">
        <input type="password" placeholder="Password" class="input-field" value="123456">
        <button class="btn-neon" style="width:100%;">Login / Sign up</button>
        <p style="margin-top:1rem;">smooth animated transitions ✦</p>
        <button class="btn-neon" id="closeAuthModal" style="background:none;">close</button>
    </div>
</div>

<!-- PRE-ORDER MODAL (product detail) -->
<div class="modal-overlay" id="preorderModal">
    <div class="modal-content" id="modalDynamic">
        <!-- filled by js -->
    </div>
</div>

<script>
    (function() {
        // ---------- STATE ----------
        let products = [
            { id: 'p1', name: '7-Shot Saturn', price: 1299, stock: 20, img: 'https://images.pexels.com/photos/1271592/pexels-photo-1271592.jpeg?auto=compress&cs=tinysrgb&w=400', festivalBanner: 'Diwali' },
            { id: 'p2', name: 'Phantom Rockets', price: 849, stock: 45, img: 'https://images.pexels.com/photos/2573609/pexels-photo-2573609.jpeg?auto=compress&cs=tinysrgb&w=400', festivalBanner: 'Diwali' },
            { id: 'p3', name: 'Neon Sparklers', price: 299, stock: 120, img: 'https://images.pexels.com/photos/2573637/pexels-photo-2573637.jpeg?auto=compress&cs=tinysrgb&w=400' },
            { id: 'p4', name: 'Ground Bloom', price: 590, stock: 15, img: 'https://images.pexels.com/photos/2573600/pexels-photo-2573600.jpeg?auto=compress&cs=tinysrgb&w=400' },
        ];
        let orders = [
            { id: 'o1', productId: 'p1', productName: '7-Shot Saturn', quantity: 2, customer: 'Aarav Khanna', orderDate: '2026-02-16', expiryDate: '2026-02-19', status: 'pending' },
            { id: 'o2', productId: 'p3', productName: 'Neon Sparklers', quantity: 5, customer: 'Priya Mehta', orderDate: '2026-02-10', expiryDate: '2026-02-13', status: 'expired' },
        ];

        // Helper: generate new IDs
        function newProductId() { return 'p'+Date.now()+Math.random().toString(36).substring(2,6); }
        function newOrderId() { return 'o'+Date.now()+Math.random().toString(36).substring(2,8); }

        // Render products (homepage)
        function renderProducts() {
            const grid = document.getElementById('productGrid');
            if (!grid) return;
            grid.innerHTML = products.map(p => {
                const banner = p.festivalBanner ? `<div class="chip" style="background:#ff5e00; color:#000;">🎆 ${p.festivalBanner}</div>` : '';
                return `<div class="product-card" data-id="${p.id}">
                    <img src="${p.img}" class="product-img" alt="${p.name}" loading="lazy">
                    <h3 style="font-size:1.8rem;">${p.name}</h3>
                    <div class="price-tag">₹${p.price}</div>
                    ${banner}
                    <div><span class="stock-badge"><i class="fa-regular fa-box"></i> stock ${p.stock}</span></div>
                </div>`;
            }).join('');
            // attach click listeners
            document.querySelectorAll('.product-card').forEach(card => {
                card.addEventListener('click', (e) => {
                    const pid = card.dataset.id;
                    const prod = products.find(p => p.id === pid);
                    if (prod) openPreorderModal(prod);
                });
            });
        }

        // Admin product list with edit/delete
        function renderAdminProducts() {
            const adminDiv = document.getElementById('adminProductList');
            if (!adminDiv) return;
            adminDiv.innerHTML = products.map(p => `
                <div style="display:flex; align-items:center; gap:1rem; background:#1f1412; margin:0.5rem 0; padding:0.8rem 1.5rem; border-radius:60px;">
                    <img src="${p.img}" style="width:45px; height:45px; border-radius:30px; object-fit:cover;">
                    <span style="flex:1;">${p.name} - ₹${p.price} (${p.stock})</span>
                    <button class="btn-neon edit-prod" data-id="${p.id}" style="padding:6px 18px;">edit</button>
                    <button class="btn-neon delete-prod" data-id="${p.id}" style="background:#b32f00;">del</button>
                </div>
            `).join('');
            // attach events
            document.querySelectorAll('.edit-prod').forEach(b => b.addEventListener('click', (e) => {
                e.stopPropagation();
                const id = b.dataset.id;
                const prod = products.find(p=>p.id===id);
                if(prod) {
                    document.getElementById('productName').value = prod.name;
                    document.getElementById('productPrice').value = prod.price;
                    document.getElementById('productStock').value = prod.stock;
                    document.getElementById('productImg').value = prod.img;
                    document.getElementById('formTitle').innerText = 'Edit product';
                    document.getElementById('saveProductBtn').dataset.editId = prod.id;
                    document.getElementById('productFormContainer').style.display = 'block';
                }
            }));
            document.querySelectorAll('.delete-prod').forEach(b => b.addEventListener('click', (e) => {
                e.stopPropagation();
                const id = b.dataset.id;
                products = products.filter(p => p.id !== id);
                renderProducts(); renderAdminProducts(); renderOrders();
            }));
        }

        // orders render + expiry check
        function renderOrders() {
            const list = document.getElementById('ordersList');
            if (!list) return;
            const today = new Date().toISOString().slice(0,10);
            // auto mark expired
            orders = orders.map(o => ({...o, status: o.expiryDate < today ? 'expired' : o.status }));
            list.innerHTML = orders.map(o => `
                <div class="order-row ${o.status === 'expired' ? 'expired' : ''}">
                    <span style="min-width:140px;">👤 ${o.customer}</span>
                    <span><b>${o.productName}</b> x${o.quantity}</span>
                    <span class="chip">order: ${o.orderDate}</span>
                    <span class="chip">exp: ${o.expiryDate} ${o.expiryDate < today ? '🔴' : '🟢'}</span>
                    <span>status: ${o.status}</span>
                    <button class="btn-neon mark-pickup" data-id="${o.id}" style="padding:6px 20px;">✓ Picked up</button>
                    <button class="btn-neon mark-expired" data-id="${o.id}" style="padding:6px 20px; background:#5a3c2e;">⏳ Expire</button>
                </div>
            `).join('');
            document.querySelectorAll('.mark-pickup').forEach(b => b.addEventListener('click', (e) => {
                const oid = b.dataset.id; orders = orders.map(o => o.id === oid ? {...o, status:'pickedup'} : o); renderOrders();
            }));
            document.querySelectorAll('.mark-expired').forEach(b => b.addEventListener('click', (e) => {
                const oid = b.dataset.id; orders = orders.map(o => o.id === oid ? {...o, status:'expired'} : o); renderOrders();
            }));
        }

        // open preorder modal
        function openPreorderModal(prod) {
            const modal = document.getElementById('preorderModal');
            const dyn = document.getElementById('modalDynamic');
            let qty = 1;
            dyn.innerHTML = `
                <h2 style="color:#ffaa33;">✨ ${prod.name}</h2>
                <img src="${prod.img}" style="width:100%; border-radius:40px; margin:1rem 0;">
                <p><span class="price-tag">₹${prod.price}</span>  | stock: ${prod.stock}</p>
                <div class="quantity-selector">
                    <button class="qty-btn" id="modalQtyMinus">−</button>
                    <span style="font-size:2rem; width:60px;" id="modalQty">1</span>
                    <button class="qty-btn" id="modalQtyPlus">+</button>
                </div>
                <input class="input-field" id="modalCustomer" placeholder="Your name" value="Demo User">
                <input class="input-field" type="date" id="modalPickupDate" value="${new Date().toISOString().slice(0,10)}">
                <p style="margin:10px 0;"><i class="fa-regular fa-hourglass-half"></i> Your order will expire after 3 days if not picked up.</p>
                <button class="btn-neon" id="confirmPreorderBtn" style="width:100%;">Pre-Order now</button>
                <button class="btn-neon" id="closeModalBtn" style="background:none; margin-top:10px;">close</button>
            `;
            modal.classList.add('active');
            document.getElementById('modalQtyPlus').addEventListener('click', ()=> { qty++; document.getElementById('modalQty').innerText = qty; });
            document.getElementById('modalQtyMinus').addEventListener('click', ()=> { if(qty>1) qty--; document.getElementById('modalQty').innerText = qty; });
            document.getElementById('closeModalBtn').addEventListener('click', ()=> modal.classList.remove('active'));
            document.getElementById('confirmPreorderBtn').addEventListener('click', ()=> {
                const cust = document.getElementById('modalCustomer').value;
                const pickupDate = document.getElementById('modalPickupDate').value; // order date = today
                const todayStr = new Date().toISOString().slice(0,10);
                const expiry = new Date(Date.now() + 3*24*60*60*1000).toISOString().slice(0,10);
                const newOrder = {
                    id: newOrderId(),
                    productId: prod.id,
                    productName: prod.name,
                    quantity: qty,
                    customer: cust,
                    orderDate: todayStr,
                    expiryDate: expiry,
                    status: 'pending'
                };
                orders.push(newOrder);
                // update stock (optional)
                prod.stock = Math.max(0, prod.stock - qty);
                renderProducts(); renderOrders(); renderAdminProducts();

                // WhatsApp dealer prefilled
                const msg = `Hello, I want to pre-order:%0AProduct: ${prod.name}%0AQuantity: ${qty}%0ACustomer Name: ${cust}%0AOrder Date: ${todayStr}%0APickup Expiry Date (3 days limit): ${expiry}`;
                window.open(`https://wa.me/9779806916002?text=${msg}`, '_blank');

                modal.classList.remove('active');
            });
        }

        // auth modal
        document.getElementById('showAuthBtn').addEventListener('click', ()=> document.getElementById('authModal').classList.add('active'));
        document.getElementById('closeAuthModal').addEventListener('click', ()=> document.getElementById('authModal').classList.remove('active'));

        // admin add product
        document.getElementById('addProductBtn').addEventListener('click', ()=>{
            document.getElementById('productFormContainer').style.display = 'block';
            document.getElementById('formTitle').innerText = 'Add product';
            document.getElementById('saveProductBtn').removeAttribute('data-edit-id');
            document.getElementById('productName').value = 'New Rocket';
            document.getElementById('productPrice').value = '999';
            document.getElementById('productStock').value = '10';
            document.getElementById('productImg').value = 'https://images.pexels.com/photos/2573637/pexels-photo-2573637.jpeg?auto=compress&cs=tinysrgb&w=400';
        });
        document.getElementById('cancelProductBtn').addEventListener('click', ()=> document.getElementById('productFormContainer').style.display = 'none');
        document.getElementById('saveProductBtn').addEventListener('click', (e)=>{
            const name = document.getElementById('productName').value;
            const price = parseInt(document.getElementById('productPrice').value);
            const stock = parseInt(document.getElementById('productStock').value);
            const img = document.getElementById('productImg').value;
            const editId = e.target.dataset.editId;
            if (editId) {
                const idx = products.findIndex(p=>p.id===editId);
                if(idx>=0) { products[idx] = {...products[idx], name, price, stock, img }; }
            } else {
                const newProd = { id: newProductId(), name, price, stock, img };
                products.push(newProd);
            }
            renderProducts(); renderAdminProducts(); renderOrders();
            document.getElementById('productFormContainer').style.display = 'none';
        });

        // init countdown mock
        setInterval(()=>{
            document.getElementById('countdown').innerHTML = '🔥 DIWALI countdown 11d 23h ' + Math.floor(Math.random()*59)+'m';
        }, 5000);

        // initial render
        renderProducts(); renderAdminProducts(); renderOrders();

        // ripple effect (simple)
        document.querySelectorAll('.ripple-effect').forEach(b => b.addEventListener('click', function(e){}));

        // animation on page load
        gsap.from('.hero', {duration:0.8, y:50, opacity:0, ease:'power2'});
        gsap.from('.product-card', {duration:0.6, scale:0.9, opacity:0, stagger:0.1, delay:0.2});
    })();
</script>
<!-- subtle spark canvas (optional) -->
<canvas id="sparkCanvas" style="position:fixed; top:0; left:0; width:100%; height:100%; pointer-events:none; z-index:2;"></canvas>
<script>
    (function sparkAnimation() {
        const canvas = document.getElementById('sparkCanvas');
        if (!canvas) return;
        const ctx = canvas.getContext('2d');
        let w = canvas.width = window.innerWidth;
        let h = canvas.height = window.innerHeight;
        let particles = [];
        for (let i=0; i<30; i++) particles.push({x:Math.random()*w, y:Math.random()*h, r:Math.random()*2+1, vx:(Math.random()-0.5)*0.3, vy:(Math.random()-0.5)*0.3, color: `rgba(255, ${Math.floor(70+Math.random()*100)}, 0, 0.5)` });
        function draw() {
            ctx.clearRect(0,0,w,h);
            particles.forEach(p => {
                ctx.beginPath();
                ctx.arc(p.x, p.y, p.r, 0, Math.PI*2);
                ctx.fillStyle = p.color;
                ctx.shadowColor = '#ff5e00';
                ctx.shadowBlur = 12;
                ctx.fill();
                p.x += p.vx; p.y += p.vy;
                if(p.x<0 || p.x>w) p.vx *= -1;
                if(p.y<0 || p.y>h) p.vy *= -1;
            });
            requestAnimationFrame(draw);
        }
        draw();
        window.addEventListener('resize', ()=>{ w=canvas.width=window.innerWidth; h=canvas.height=window.innerHeight; });
    })();
</script>
</body>
</html>