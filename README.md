<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GreenRoot Marketplace</title>
  <style>
    :root {
      --primary-green: #1b5e20;
      --soft-green: #e8f5e9;
      --accent-orange: #ff9800;
      --text-main: #333;
    }

    body {
      margin: 0;
      font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
      background-color: #fcfcfc;
      color: var(--text-main);
    }

    /* Navigation */
    nav {
      background: white;
      padding: 1rem 5%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 2px 10px rgba(0,0,0,0.05);
      position: sticky;
      top: 0;
      z-index: 1000;
    }

    .logo {
      font-size: 1.5rem;
      font-weight: bold;
      color: var(--primary-green);
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .cart-box {
      background: var(--primary-green);
      color: white;
      padding: 8px 16px;
      border-radius: 50px;
      font-weight: 600;
    }

    /* Hero Section */
    .hero {
      background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), 
                  url('https://images.unsplash.com/photo-1500382017468-9049fed747ef?auto=format&fit=crop&w=1200&q=80');
      background-size: cover;
      background-position: center;
      height: 350px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      color: white;
      text-align: center;
    }

    /* Filter Buttons */
    .filters {
      display: flex;
      justify-content: center;
      gap: 15px;
      padding: 2rem;
    }

    .filter-btn {
      border: 1px solid var(--primary-green);
      background: transparent;
      padding: 8px 20px;
      border-radius: 20px;
      cursor: pointer;
      transition: 0.3s;
    }

    .filter-btn.active, .filter-btn:hover {
      background: var(--primary-green);
      color: white;
    }

    /* Product Grid */
    .market-container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 20px 50px 20px;
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
      gap: 30px;
    }

    .product-card {
      background: white;
      border-radius: 15px;
      overflow: hidden;
      box-shadow: 0 5px 15px rgba(0,0,0,0.08);
      transition: transform 0.3s ease;
      display: flex;
      flex-direction: column;
    }

    .product-card:hover {
      transform: translateY(-8px);
    }

    .product-card img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      background-color: #eee;
    }

    .info {
      padding: 20px;
      text-align: center;
    }

    .info h3 { margin: 0 0 10px 0; font-size: 1.2rem; }
    
    .price-tag {
      font-size: 1.3rem;
      font-weight: bold;
      color: var(--primary-green);
      margin-bottom: 15px;
    }

    .add-btn {
      background: var(--primary-green);
      color: white;
      border: none;
      width: 100%;
      padding: 12px;
      border-radius: 8px;
      font-weight: 600;
      cursor: pointer;
      transition: 0.2s;
    }

    .add-btn:active { transform: scale(0.95); }

    footer {
      background: #111;
      color: #777;
      text-align: center;
      padding: 40px;
    }
  </style>
</head>
<body>

<nav>
  <div class="logo">🌿 GreenRoot</div>
  <div class="cart-box">🛒 Cart: <span id="cart-qty">0</span></div>
</nav>

<section class="hero">
  <h1>Fresh From The Soil</h1>
  <p>Support your local farmers, eat healthy, live better.</p>
</section>

<div class="filters">
  <button class="filter-btn active">All</button>
  <button class="filter-btn">Vegetables</button>
  <button class="filter-btn">Fruits</button>
  <button class="filter-btn">Organic Dairy</button>
</div>

<main class="market-container">
  <div class="product-card">
    <img src="https://images.unsplash.com/photo-1592924357228-91a4daadcfea?auto=format&fit=crop&w=500&q=80" alt="Fresh Tomatoes">
    <div class="info">
      <h3>Vine-Ripened Tomatoes</h3>
      <div class="price-tag">₹45/kg</div>
      <button class="add-btn" onclick="updateCart()">Add to Cart</button>
    </div>
  </div>

  <div class="product-card">
    <img src="https://images.unsplash.com/photo-1568584711075-3d021a7c3ec3?auto=format&fit=crop&w=500&q=80" alt="Cauliflower">
    <div class="info">
      <h3>Organic Cauliflower</h3>
      <div class="price-tag">₹35/unit</div>
      <button class="add-btn" onclick="updateCart()">Add to Cart</button>
    </div>
  </div>

  <div class="product-card">
    <img src="https://images.unsplash.com/photo-1553279768-865429fa0078?auto=format&fit=crop&w=500&q=80" alt="Mangoes">
    <div class="info">
      <h3>Alphonso Mangoes</h3>
      <div class="price-tag">₹600/box</div>
      <button class="add-btn" onclick="updateCart()">Add to Cart</button>
    </div>
  </div>

  <div class="product-card">
    <img src="https://images.unsplash.com/photo-1537640538966-79f369b41f8f?auto=format&fit=crop&w=500&q=80" alt="Grapes">
    <div class="info">
      <h3>Seedless Grapes</h3>
      <div class="price-tag">₹120/kg</div>
      <button class="add-btn" onclick="updateCart()">Add to Cart</button>
    </div>
  </div>

  <div class="product-card">
    <img src="https://images.unsplash.com/photo-1516448424440-272e293a38f7?auto=format&fit=crop&w=500&q=80" alt="Farm Eggs">
    <div class="info">
      <h3>Farm-Fresh Eggs</h3>
      <div class="price-tag">₹80/dozen</div>
      <button class="add-btn" onclick="updateCart()">Add to Cart</button>
    </div>
  </div>

  <div class="product-card">
    <img src="https://images.unsplash.com/photo-1528750955925-53f5a173752c?auto=format&fit=crop&w=500&q=80" alt="Milk">
    <div class="info">
      <h3>Pure Buffalo Milk</h3>
      <div class="price-tag">₹70/L</div>
      <button class="add-btn" onclick="updateCart()">Add to Cart</button>
    </div>
  </div>
</main>

<footer>
  <p>© 2026 GreenRoot Farmer Marketplace</p>
  <p>Hand-picked quality guaranteed.</p>
</footer>

<script>
  let count = 0;
  function updateCart() {
    count++;
    document.getElementById('cart-qty').innerText = count;
    
    // Visual confirmation
    const btn = event.target;
    btn.innerText = "Added!";
    btn.style.backgroundColor = "#ff9800";
    
    setTimeout(() => {
      btn.innerText = "Add to Cart";
      btn.style.backgroundColor = "#1b5e20";
    }, 800);
  }
</script>

</body>
</html>


