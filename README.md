<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Farmer Cart | Blinkit Style Grocery</title>
    <style>
        :root {
            --blinkit-green: #0c831f;
            --blinkit-yellow: #f7d54d;
            --light-gray: #f5f7f9;
            --text-main: #1f1f1f;
            --text-muted: #666;
            --border: #e8e8e8;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', system-ui, -apple-system, sans-serif;
        }

        body {
            background-color: var(--light-gray);
            color: var(--text-main);
            line-height: 1.5;
        }

        /* Container to keep mobile feel on Desktop */
        .app-container {
            max-width: 500px;
            margin: 0 auto;
            background: white;
            min-height: 100vh;
            position: relative;
            box-shadow: 0 0 20px rgba(0,0,0,0.05);
        }

        /* Screen Sections */
        section {
            padding: 20px;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            border-bottom: 8px solid var(--light-gray);
        }

        h2 { font-weight: 800; margin-bottom: 15px; font-size: 24px; }

        /* 1. Splash Screen */
        .splash {
            background: linear-gradient(135deg, var(--blinkit-yellow) 0%, #ffeb3b 100%);
            justify-content: center;
            align-items: center;
            text-align: center;
        }
        .logo-box {
            background: white;
            padding: 20px;
            border-radius: 30px;
            font-size: 50px;
            margin-bottom: 20px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }

        /* 2. Language Screen */
        .lang-option {
            border: 2px solid var(--border);
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 12px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            font-weight: 600;
        }
        .lang-option.selected {
            border-color: var(--blinkit-green);
            background-color: #f0fff0;
        }

        /* 3. Signup Form (User Interactive) */
        .form-group { margin-bottom: 20px; }
        label { display: block; font-size: 13px; font-weight: 600; color: var(--text-muted); margin-bottom: 6px; }
        input {
            width: 100%;
            padding: 14px;
            border: 1px solid var(--border);
            border-radius: 12px;
            font-size: 16px;
            outline: none;
            transition: 0.2s;
        }
        input:focus { border-color: var(--blinkit-green); box-shadow: 0 0 0 3px rgba(12,131,31,0.1); }

        /* 4. Product Listing (The Blinkit UI) */
        .header-sticky {
            position: sticky;
            top: 0;
            background: white;
            z-index: 100;
            padding: 15px;
            border-bottom: 1px solid var(--border);
        }
        .search-box {
            background: var(--light-gray);
            border-radius: 10px;
            display: flex;
            align-items: center;
            padding: 0 12px;
            margin-top: 10px;
        }
        .search-box input { background: transparent; border: none; padding: 10px; font-size: 14px; }

        .product-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            padding-top: 20px;
        }
        .product-card {
            border: 1px solid var(--border);
            border-radius: 15px;
            padding: 10px;
            background: white;
            display: flex;
            flex-direction: column;
        }
        .product-card img {
            width: 100%;
            height: 120px;
            object-fit: contain;
            margin-bottom: 10px;
        }
        .p-title { font-size: 14px; font-weight: 600; height: 40px; overflow: hidden; }
        .p-qty { font-size: 12px; color: var(--text-muted); margin-bottom: 10px; }
        .p-footer { display: flex; justify-content: space-between; align-items: center; }
        .p-price { font-weight: 700; font-size: 15px; }
        
        .add-btn {
            background: white;
            color: var(--blinkit-green);
            border: 1px solid var(--blinkit-green);
            padding: 5px 15px;
            border-radius: 8px;
            font-weight: 700;
            cursor: pointer;
            transition: 0.2s;
        }
        .add-btn:active { transform: scale(0.9); background: var(--blinkit-green); color: white; }

        /* Buttons */
        .btn-large {
            background: var(--blinkit-green);
            color: white;
            border: none;
            width: 100%;
            padding: 16px;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 700;
            cursor: pointer;
            margin-top: auto;
        }

        /* 5. Floating Cart Area */
        .cart-float {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            width: 90%;
            max-width: 450px;
            background: var(--blinkit-green);
            color: white;
            padding: 15px 20px;
            border-radius: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 10px 30px rgba(12,131,31,0.3);
            display: none; /* Hidden by default */
            z-index: 1000;
        }
    </style>
</head>
<body>

<div class="app-container">

    <section class="splash">
        <div class="logo-box">👨‍🌾</div>
        <h1 style="font-size: 32px; font-weight: 900;">Farmer Cart</h1>
        <p style="color: #444;">Freshness delivered in 10 minutes</p>
        <p style="margin-top: 40px; font-size: 12px; color: #666;">Scroll down to start ↓</p>
    </section>

    <section id="language">
        <h2>Choose Language</h2>
        <div class="lang-option selected" onclick="selectLang(this)">
            English <span>✓</span>
        </div>
        <div class="lang-option" onclick="selectLang(this)">Hindi (हिंदी)</div>
        <div class="lang-option" onclick="selectLang(this)">Marathi (मराठी)</div>
        <div class="lang-option" onclick="selectLang(this)">Telugu (తెలుగు)</div>
        <button class="btn-large" onclick="scrollToId('signup')">Continue</button>
    </section>

    <section id="signup">
        <h2>Create Account</h2>
        <p style="color: var(--text-muted); margin-bottom: 20px;">Please enter your details to browse vegetables.</p>
        
        <div class="form-group">
            <label>FULL NAME</label>
            <input type="text" id="userName" placeholder="Enter your name">
        </div>
        <div class="form-group">
            <label>MOBILE NUMBER</label>
            <input type="tel" id="userPhone" placeholder="+91 00000 00000">
        </div>
        <div class="form-group">
            <label>EMAIL ADDRESS</label>
            <input type="email" id="userEmail" placeholder="name@example.com">
        </div>
        
        <button class="btn-large" onclick="saveUser()">Browse Products</button>
    </section>

    <section id="products" style="padding: 0;">
        <div class="header-sticky">
            <div style="font-size: 12px; font-weight: 700; color: var(--blinkit-green);">DELIVERING TO</div>
            <div style="font-size: 14px; font-weight: 600;">Home - Current Location ▾</div>
            <div class="search-box">
                <span>🔍</span>
                <input type="text" id="searchInput" onkeyup="filterProducts()" placeholder="Search 'potato' or 'onion'">
            </div>
        </div>

        <div style="padding: 15px;">
            <h3 style="margin-bottom: 10px;">Fresh Vegetables</h3>
            <div class="product-grid" id="productGrid">
                </div>
        </div>
        <div style="height: 100px;"></div> </section>

</div>

<div class="cart-float" id="cartFloat" onclick="checkout()">
    <div>
        <span id="cartQty">1 Item</span>
        <div id="cartPrice" style="font-weight: 800; font-size: 18px;">₹0</div>
    </div>
    <div style="font-weight: 700;">View Cart 🛒</div>
</div>

<script>
    // 1. Data Store
    const products = [
        { id: 1, name: "Hybrid Tomato", qty: "500 g", price: 32, img: "https://cdn-icons-png.flaticon.com/512/1202/1202125.png" },
        { id: 2, name: "Red Onion", qty: "1 kg", price: 45, img: "https://cdn-icons-png.flaticon.com/512/7230/7230868.png" },
        { id: 3, name: "Fresh Potato", qty: "1 kg", price: 38, img: "https://cdn-icons-png.flaticon.com/512/1135/1135544.png" },
        { id: 4, name: "Green Chili", qty: "100 g", price: 12, img: "https://cdn-icons-png.flaticon.com/512/2324/2324631.png" },
        { id: 5, name: "Carrot (Gajar)", qty: "500 g", price: 40, img: "https://cdn-icons-png.flaticon.com/512/2224/2224115.png" },
        { id: 6, name: "Coriander (Dhaniya)", qty: "1 unit", price: 10, img: "https://cdn-icons-png.flaticon.com/512/1514/1514931.png" },
        { id: 7, name: "Garlic (Lehsun)", qty: "100 g", price: 50, img: "https://cdn-icons-png.flaticon.com/512/1041/1041344.png" },
        { id: 8, name: "Ginger (Adrak)", qty: "250 g", price: 60, img: "https://cdn-icons-png.flaticon.com/512/2909/2909772.png" }
    ];

    let cart = [];

    // 2. Navigation
    function scrollToId(id) {
        document.getElementById(id).scrollIntoView({ behavior: 'smooth' });
    }

    function selectLang(el) {
        document.querySelectorAll('.lang-option').forEach(opt => opt.classList.remove('selected'));
        el.classList.add('selected');
    }

    // 3. Form Handling
    function saveUser() {
        const name = document.getElementById('userName').value;
        if(!name) {
            alert("Please enter your name to continue!");
            return;
        }
        alert(`Welcome ${name}! Start shopping.`);
        scrollToId('products');
    }

    // 4. Product Logic
    function renderProducts(items) {
        const grid = document.getElementById('productGrid');
        grid.innerHTML = items.map(p => `
            <div class="product-card">
                <img src="${p.img}" alt="${p.name}">
                <div class="p-title">${p.name}</div>
                <div class="p-qty">${p.qty}</div>
                <div class="p-footer">
                    <span class="p-price">₹${p.price}</span>
                    <button class="add-btn" onclick="addToCart(${p.id})">ADD</button>
                </div>
            </div>
        `).join('');
    }

    function filterProducts() {
        const query = document.getElementById('searchInput').value.toLowerCase();
        const filtered = products.filter(p => p.name.toLowerCase().includes(query));
        renderProducts(filtered);
    }

    // 5. Cart Logic
    function addToCart(id) {
        const item = products.find(p => p.id === id);
        cart.push(item);
        
        const cartFloat = document.getElementById('cartFloat');
        const cartQty = document.getElementById('cartQty');
        const cartPrice = document.getElementById('cartPrice');

        cartFloat.style.display = 'flex';
        cartQty.innerText = `${cart.length} Item${cart.length > 1 ? 's' : ''}`;
        
        const total = cart.reduce((sum, current) => sum + current.price, 0);
        cartPrice.innerText = `₹${total}`;
    }

    function checkout() {
        const total = cart.reduce((sum, i) => sum + i.price, 0);
        alert(`Order Summary:\nTotal Items: ${cart.length}\nFinal Bill: ₹${total}\n\nYour fresh veggies are on the way!`);
        cart = [];
        document.getElementById('cartFloat').style.display = 'none';
    }

    // Initial Load
    renderProducts(products);
</script>

</body>
</html>

