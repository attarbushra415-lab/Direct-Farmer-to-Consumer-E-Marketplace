<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Farmer Marketplace</title>
  <style>
    :root {
      --primary: #2e7d32;
      --secondary: #388e3c;
      --accent: #fbc02d;
      --bg: #f9fbf9;
    }

    body {
      margin: 0;
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
      background: var(--bg);
      color: #333;
    }

    /* Navbar */
    header {
      background: var(--primary);
      color: white;
      padding: 1rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      position: sticky;
      top: 0;
      z-index: 100;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    .logo { font-size: 1.5rem; font-weight: bold; display: flex; align-items: center; gap: 10px; }
    
    .cart-btn {
      background: white;
      color: var(--primary);
      padding: 8px 15px;
      border-radius: 20px;
      font-weight: bold;
      cursor: pointer;
    }

    /* Hero Section */
    .hero {
      height: 300px;
      background: linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.4)), 
                  url('https://images.unsplash.com/photo-1464226184884-fa280b87c399?q=80&w=1000&auto=format&fit=crop') center/cover;
      color: white;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
    }

    /* Product Grid */
    .container { max-width: 1200px; margin: 2rem auto; padding: 0 20px; }
    
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
      gap: 25px;
    }

    .card {
      background: white;
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 4px 6px rgba(0,0,0,0.05);
      transition: 0.3s;
      border: 1px solid #eee;
    }

    .card:hover { transform: translateY(-5px); box-shadow: 0 8px 15px rgba(0,0,0,0.1); }

    .img-container {
      width: 100%;
      height: 180px;
      background: #e0e0e0; /* Fallback color */
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .card img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .card-info { padding: 15px; text-align: center; }
    
    .price {
      color: var(--primary);
      font-size: 1.2rem;
      font-weight: bold;
      margin: 10px 0;
    }

    .btn {
      background: var(--primary);
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 5px;
      cursor: pointer;
      width: 100%;
      font-weight: bold;
    }

    .btn:hover { background: var(--secondary); }

    footer {
      background: #222;
      color: #999;
      text-align: center;
      padding: 2rem;
      margin-top: 4rem;
    }
  </style>
</head>
<body>

<header>
  <div class="logo"><span>🌾</span> Farm2Fork</div>
  <div class="cart-btn">🛒 Cart (<span id="count">0</span>)</div>
</header>

<section class="hero">
  <h1>Directly From the Roots</h1>
  <p>Freshly picked this morning, delivered to you tonight.</p>
</section>

<div class="container">
  <h2 style="text-align:center; margin-bottom: 30px;">Seasonal Fresh Produce</h2>
  
  <div class="grid">
    <div class="card">
      <div class="img-container">
        <img src="https://images.unsplash.com/photo-1518977676601-b53f02ac6d31?q=80&w=500&auto=format&fit=crop" alt="Organic Potato">
      </div>
      <div class="card-info">
        <h3>Russet Potatoes</h3>
        <p class="price">₹40/kg</p>
        <button class="btn" onclick="add()">Add to Cart</button>
      </div>
    </div>

    <div class="card">
      <div class="img-container">
        <img src="https://images.unsplash.com/photo-1582284738083-0c444b05908c?q=80&w=500&auto=format&fit=crop" alt="Tomatoes">
      </div>
      <div class="card-info">
        <h3>Cherry Tomatoes</h3>
        <p class="price">₹60/kg</p>
        <button class="btn" onclick="add()">Add to Cart</button>
      </div>
    </div>

    <div class="card">
      <div class="img-container">
        <img src="https://images.unsplash.com/photo-1598170845058-32b9d6a5da37?q=80&w=500&auto=format&fit=crop" alt="Carrots">
      </div>
      <div class="card-info">
        <h3>Organic Carrots</h3>
        <p class="price">₹50/kg</p>
        <button class="btn" onclick="add()">Add to Cart</button>
      </div>
    </div>

    <div class="card">
      <div class="img-container">
        <img src="https://images.unsplash.com/photo-1550583724-1255818c053b?q=80&w=500&auto=format&fit=crop" alt="Fresh Milk">
      </div>
      <div class="card-info">
        <h3>Farm Fresh Milk</h3>
        <p class="price">₹65/L</p>
        <button class="btn" onclick="add()">Add to Cart</button>
      </div>
    </div>

    <div class="card">
      <div class="img-container">
        <img src="https://images.unsplash.com/photo-1587049352846-4a222e784d38?q=80&w=500&auto=format&fit=crop" alt="Honey">
      </div>
      <div class="card-info">
        <h3>Wild Forest Honey</h3>
        <p class="price">₹280/500g</p>
        <button class="btn" onclick="add()">Add to Cart</button>
      </div>
    </div>

    <div class="card">
      <div class="img-container">
        <img src="https://images.unsplash.com/photo-1582722872445-44c5b7c3c8f7?q=80&w=500&auto=format&fit=crop" alt="Eggs">
      </div>
      <div class="card-info">
        <h3>Free Range Eggs</h3>
        <p class="price">₹90/Dozen</p>
        <button class="btn" onclick="add()">Add to Cart</button>
      </div>
    </div>
  </div>
</div>

<footer>
  <p>© 2026 Farmer Marketplace | Supporting Local Agriculture</p>
</footer>

<script>
  let cartCount = 0;
  function add() {
    cartCount++;
    document.getElementById('count').innerText = cartCount;
    // Simple UI feedback
    const btn = event.target;
    const originalText = btn.innerText;
    btn.innerText = "✓ Added";
    btn.style.background = "#388e3c";
    setTimeout(() => {
      btn.innerText = originalText;
      btn.style.background = "#2e7d32";
    }, 1000);
  }
</script>

</body>
</html>

