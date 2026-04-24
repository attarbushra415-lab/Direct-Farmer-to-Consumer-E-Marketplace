<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FarmDirect Premium UI</title>

<style>
body {
    margin: 0;
    font-family: 'Segoe UI', sans-serif;
    background: #eaeaea;
    display: flex;
    gap: 20px;
    padding: 20px;
}

/* PHONE FRAME */
.phone {
    width: 260px;
    height: 540px;
    background: #fff;
    border-radius: 30px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.2);
    overflow: hidden;
    position: relative;
}

/* HEADER */
.header {
    background: #0c831f;
    color: white;
    padding: 12px;
    text-align: center;
    font-weight: bold;
}

/* SPLASH */
.splash {
    background: url('https://images.unsplash.com/photo-1542838132-92c53300491e');
    background-size: cover;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-size: 24px;
    font-weight: bold;
    text-shadow: 0 2px 5px black;
}

/* HOME */
.content {
    padding: 10px;
    overflow-y: auto;
    height: 100%;
}

.banner {
    background: #f7d54d;
    padding: 10px;
    border-radius: 10px;
    margin-bottom: 10px;
    font-weight: bold;
}

/* PRODUCTS */
.product {
    display: flex;
    gap: 10px;
    background: #fafafa;
    margin-bottom: 10px;
    padding: 8px;
    border-radius: 10px;
}

.product img {
    width: 60px;
    height: 60px;
    border-radius: 10px;
}

.price {
    color: green;
    font-weight: bold;
}

.stock {
    font-size: 11px;
    color: gray;
}

button {
    padding: 5px 8px;
    border: none;
    background: #0c831f;
    color: white;
    border-radius: 6px;
    cursor: pointer;
    margin-top: 5px;
}

/* CART */
.cart-item {
    border-bottom: 1px solid #ddd;
    padding: 5px 0;
}

.total {
    font-weight: bold;
    margin-top: 10px;
}

/* FOOTER */
.footer {
    position: absolute;
    bottom: 0;
    width: 100%;
    background: #fff;
    border-top: 1px solid #ddd;
    display: flex;
    justify-content: space-around;
    padding: 8px 0;
    font-size: 12px;
}
</style>
</head>

<body>

<!-- SPLASH SCREEN -->
<div class="phone">
    <div class="splash">
        🌾 FarmDirect
    </div>
</div>

<!-- HOME SCREEN -->
<div class="phone">
    <div class="header">FarmDirect</div>
    <div class="content" id="homeProducts">
        <div class="banner">⚡ Fresh from Nearby Farms (6–24 hrs)</div>
    </div>
    <div class="footer">
        <div>🏠 Home</div>
        <div>🛒 Cart</div>
        <div>👤 Profile</div>
    </div>
</div>

<!-- PRODUCT SCREEN -->
<div class="phone">
    <div class="header">Product Details</div>
    <div class="content">
        <img src="https://images.unsplash.com/photo-1582281298055-e25b84a30b0b" style="width:100%; border-radius:10px;">
        <h3>Tomatoes</h3>
        <p class="price">₹32/kg</p>
        <p>Farmer: Ramesh (Nashik)</p>
        <p class="stock">Stock: 10kg nearby</p>
        <button>Add to Cart</button>
    </div>
</div>

<!-- CART SCREEN -->
<div class="phone">
    <div class="header">Cart</div>
    <div class="content" id="cartItems"></div>
    <div class="content total">Total: ₹<span id="total">0</span></div>
</div>

<script>
const products = [
{
name:"Tomatoes",
price:30,
farmer:"Ramesh (Nashik)",
stock:10,
img:"https://images.unsplash.com/photo-1582281298055-e25b84a30b0b"
},
{
name:"Potatoes",
price:20,
farmer:"Suresh (Pune)",
stock:8,
img:"https://images.unsplash.com/photo-1582515073490-dc43e1c7d1b7"
},
{
name:"Carrots",
price:25,
farmer:"Anita (Satara)",
stock:5,
img:"https://images.unsplash.com/photo-1447175008436-170170d0d3e0"
},
{
name:"Onions",
price:22,
farmer:"Mahesh (Ahmednagar)",
stock:12,
img:"https://images.unsplash.com/photo-1587049352846-4a222e784d38"
}
];

let cart = [];

function loadProducts(){
    let html = "";
    products.forEach((p,i)=>{
        let dynamicPrice = p.price + Math.floor(Math.random()*5);

        html += `
        <div class="product">
            <img src="${p.img}">
            <div>
                <b>${p.name}</b><br>
                <span class="price">₹${dynamicPrice}</span><br>
                <small>${p.farmer}</small><br>
                <span class="stock">${p.stock}kg nearby</span><br>
                <button onclick="addToCart('${p.name}',${dynamicPrice})">Add</button>
            </div>
        </div>`;
    });

    document.getElementById("homeProducts").innerHTML += html;
}

function addToCart(name,price){
    cart.push({name,price});
    updateCart();
}

function updateCart(){
    let html = "";
    let total = 0;

    cart.forEach(item=>{
        total += item.price;
        html += `<div class="cart-item">${item.name} - ₹${item.price}</div>`;
    });

    document.getElementById("cartItems").innerHTML = html;
    document.getElementById("total").innerText = total;
}

loadProducts();
</script>

</body>
</html>

