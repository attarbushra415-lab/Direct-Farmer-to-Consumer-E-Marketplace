<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Farmer Cart - Modern Grocery UI</title>
    <style>
        :root {
            --blinkit-green: #0c831f;
            --blinkit-yellow: #f7d54d;
            --bg-light: #f5f7f9;
            --text-dark: #1f1f1f;
            --text-muted: #666;
            --shadow: 0 4px 12px rgba(0,0,0,0.08);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }

        body {
            background-color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            padding: 40px;
            gap: 30px;
            overflow-x: auto;
        }

        /* Smartphone Frame */
        .phone-frame {
            min-width: 360px;
            width: 360px;
            height: 740px;
            background: white;
            border-radius: 40px;
            border: 8px solid #1a1a1a;
            position: relative;
            overflow: hidden;
            box-shadow: 0 20px 40px rgba(0,0,0,0.4);
            display: flex;
            flex-direction: column;
        }

        /* Utility Classes */
        .screen { height: 100%; width: 100%; display: flex; flex-direction: column; position: relative; }
        .hidden { display: none; }
        .btn-primary {
            background: var(--blinkit-green);
            color: white;
            border: none;
            padding: 14px;
            border-radius: 12px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
        }

        /* 1. Splash Screen */
        #splash-screen {
            background: linear-gradient(rgba(0,0,0,0.3), rgba(0,0,0,0.3)), 
                        url('https://images.unsplash.com/photo-1542838132-92c53300491e?auto=format&fit=crop&q=80&w=600');
            background-size: cover;
            justify-content: center;
            align-items: center;
            color: white;
            text-align: center;
        }
        .logo-circle {
            width: 100px; height: 100px;
            background: var(--blinkit-yellow);
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 40px;
            margin-bottom: 15px;
            box-shadow: 0 0 20px rgba(0,0,0,0.2);
        }

        /* 2. Language Screen */
        #lang-screen {
            background: url('https://images.unsplash.com/photo-1610348725531-843dff563e2c?auto=format&fit=crop&q=80&w=600') center;
            background-size: cover;
            padding: 20px;
            justify-content: flex-end;
        }
        .lang-card {
            background: white;
            padding: 25px;
            border-radius: 24px;
            box-shadow: var(--shadow);
        }
        .lang-option {
            padding: 12px;
            border: 1px solid #eee;
            margin-bottom: 10px;
            border-radius: 10px;
            display: flex;
            justify-content: space-between;
        }
        .lang-option.active { border-color: var(--blinkit-green); background: #f0fff0; }

        /* 3. Signup Screen */
        #signup-screen { padding: 30px 20px; }
        .input-group { margin-bottom: 15px; }
        .input-group label { display: block; font-size: 12px; color: var(--text-muted); margin-bottom: 5px; }
        .input-group input {
            width: 100%; padding: 12px;
            border: 1px solid #ddd;
            border-radius: 10px;
            outline-color: var(--blinkit-green);
        }

        /* 4. Product Listing (Blinkit Style) */
        .app-header {
            padding: 15px;
            background: white;
            border-bottom: 1px solid #f0f0f0;
            position: sticky;
            top: 0;
            z-index: 10;
        }
        .search-bar {
            background: #f1f2f4;
            padding: 10px;
            border-radius: 10px;
            font-size: 14px;
            color: #888;
            margin-top: 10px;
        }
        .product-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            padding: 12px;
            overflow-y: auto;
            background: #fff;
        }
        .product-card {
            border: 1px solid #e8e8e8;
            border-radius: 12px;
            padding: 8px;
            display: flex;
            flex-direction: column;
            position: relative;
        }
        .product-img {
            width: 100%;
            height: 100px;
            object-fit: contain;
            margin-bottom: 8px;
        }
        .product-name { font-size: 13px; font-weight: 500; height: 36px; overflow: hidden; }
        .product-weight { font-size: 11px; color: var(--text-muted); margin: 4px 0; }
        .card-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 8px;
        }
        .price { font-weight: 700; font-size: 14px; }
        .add-btn {
            background: white;
            color: var(--blinkit-green);
            border: 1px solid var(--blinkit-green);
            padding: 4px 16px;
            border-radius: 6px;
            font-weight: bold;
            font-size: 12px;
            cursor: pointer;
        }
        .add-btn:hover { background: #f0fff0; }

        /* Cart Drawer */
        .cart-bar {
            background: var(--blinkit-green);
            color: white;
            padding: 12px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            margin: 10px;
            border-radius: 12px;
        }
    </style>
</head>
<body>

    <div class="phone-frame">
        <div id="splash-screen" class="screen">
            <div class="logo-circle">🛒</div>
            <h1 style="font-weight: 800; letter-spacing: -1px;">Farmer Cart</h1>
            <p style="font-size: 14px; opacity: 0.9;">Everything in minutes</p>
        </div>
    </div>

    <div class="phone-frame">
        <div id="lang-screen" class="screen">
            <div class="lang-card">
                <h3 style="margin-bottom: 15px;">Choose Language</h3>
                <div class="lang-option active"><span>English</span> <span>✓</span></div>
                <div class="lang-option"><span>Hindi (हिंदी)</span></div>
                <div class="lang-option"><span>Marathi (मराठी)</span></div>
                <div class="lang-option"><span>Tamil (தமிழ்)</span></div>
                <button class="btn-primary" style="margin-top: 10px;">Continue</button>
            </div>
        </div>
    </div>

    <div class="phone-frame">
        <div id="signup-screen" class="screen">
            <h2 style="margin-bottom: 8px;">Welcome!</h2>
            <p style="color: #666; font-size: 14px; margin-bottom: 30px;">Sign up to get started</p>
            
            <div class="input-group">
                <label>Mobile Number / Email</label>
                <input type="text" placeholder="e.g. 9876543210">
            </div>
            <div class="input-group">
                <label>Username</label>
                <input type="text" placeholder="John Doe">
            </div>
            <div class="input-group">
                <label>Password</label>
                <input type="password" placeholder="••••••••">
            </div>
            <button class="btn-primary" style="margin-top: 20px;">Create Account</button>
        </div>
    </div>

    <div class="phone-frame">
        <div id="main-app" class="screen">
            <div class="app-header">
                <div style="display: flex; justify-content: space-between; align-items: center;">
                    <div>
                        <p style="font-weight: 800; font-size: 14px;">Delivery in 9 mins</p>
                        <p style="font-size: 12px; color: var(--text-muted);">Home - H-12, Green Park...</p>
                    </div>
                    <div style="font-size: 20px;">👤</div>
                </div>
                <div class="search-bar">Search "milk"</div>
            </div>

            <div class="product-grid" id="product-list">
                </div>

            <div id="cart-container" class="hidden">
                <div class="cart-bar" onclick="checkout()">
                    <div>
                        <span id="cart-count">0 ITEMS</span>
                        <div id="cart-total" style="font-weight: bold; font-size: 16px;">₹0</div>
                    </div>
                    <div style="font-weight: bold;">View Cart ➜</div>
                </div>
            </div>
        </div>
    </div>

    <script>
        const products = [
            { id: 1, name: "Fresh Tomato (Hybrid)", weight: "500 g", price: 34, img: "https://cdn.pixabay.com/photo/2011/03/16/16/01/tomatoes-5356_1280.jpg" },
            { id: 2, name: "Onion (Pyaz)", weight: "1 kg", price: 48, img: "https://images.unsplash.com/photo-1508747703725-719777637510?auto=format&fit=crop&q=80&w=200" },
            { id: 3, name: "Fresh Broccoli", weight: "250 g", price: 85, img: "https://images.unsplash.com/photo-1459411552884-841db9b3cc2a?auto=format&fit=crop&q=80&w=200" },
            { id: 4, name: "Organic Banana", weight: "6 pcs", price: 45, img: "https://images.unsplash.com/photo-1571771894821-ad9958a3f747?auto=format&fit=crop&q=80&w=200" },
            { id: 5, name: "Alphonso Mango", weight: "1 kg", price: 450, img: "https://images.unsplash.com/photo-1553279768-865429fa0078?auto=format&fit=crop&q=80&w=200" },
            { id: 6, name: "Green Capsicum", weight: "250 g", price: 28, img: "https://images.unsplash.com/photo-1563513307167-6d9ddcd3bb7a?auto=format&fit=crop&q=80&w=200" }
        ];

        let cart = [];

        function renderProducts() {
            const grid = document.getElementById('product-list');
            grid.innerHTML = products.map(p => `
                <div class="product-card">
                    <img src="${p.img}" class="product-img" alt="${p.name}">
                    <div class="product-name">${p.name}</div>
                    <div class="product-weight">${p.weight}</div>
                    <div class="card-footer">
                        <span class="price">₹${p.price}</span>
                        <button class="add-btn" onclick="addToCart(${p.id})">ADD</button>
                    </div>
                </div>
            `).join('');
        }

        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            cart.push(product);
            updateCartUI();
        }

        function updateCartUI() {
            const cartContainer = document.getElementById('cart-container');
            const cartCount = document.getElementById('cart-count');
            const cartTotal = document.getElementById('cart-total');

            if (cart.length > 0) {
                cartContainer.classList.remove('hidden');
                cartCount.innerText = `${cart.length} ITEM${cart.length > 1 ? 'S' : ''}`;
                const total = cart.reduce((sum, item) => sum + item.price, 0);
                cartTotal.innerText = `₹${total}`;
            }
        }

        function checkout() {
            const total = cart.reduce((sum, item) => sum + item.price, 0);
            alert(`Order Placed Successfully!\nTotal Amount: ₹${total}\nItems: ${cart.length}\n\nThank you for shopping with Farmer Cart!`);
            cart = [];
            document.getElementById('cart-container').classList.add('hidden');
        }

        // Initialize
        renderProducts();
    </script>
</body>
</html>
