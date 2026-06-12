<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Leather Craft Store</title>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #111;
    color: #fff;
}

header {
    background: #1c1c1c;
    padding: 20px;
    font-size: 24px;
    font-weight: bold;
}

/* TOP BAR FLEX (UPDATED) */
.header-container{
    display:flex;
    justify-content:space-between;
    align-items:center;
}

/* CART BUTTON */
.cart-btn {
    cursor: pointer;
    font-size: 18px;
    background: #333;
    padding: 8px 12px;
    border-radius: 6px;
}

.cart-btn:hover {
    background:#555;
}

nav {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    background: #222;
    padding: 10px;
}

nav button {
    margin: 5px;
    padding: 10px 15px;
    border: none;
    cursor: pointer;
    background: #444;
    color: white;
    border-radius: 5px;
}

nav button:hover {
    background: #666;
}

.products {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 15px;
    padding: 20px;
}

.product {
    background: #1b1b1b;
    padding: 10px;
    border-radius: 10px;
    text-align: center;
}

.product img {
    width: 100%;
    height: 160px;
    object-fit: cover;
    border-radius: 10px;
}

button.add {
    margin-top: 10px;
    padding: 8px;
    background: green;
    border: none;
    color: white;
    width: 100%;
    cursor: pointer;
}

/* CART PANEL (UPDATED - hidden by default) */
.cart {
    position: fixed;
    right: 0;
    top: 0;
    width: 300px;
    height: 100%;
    background: #000;
    padding: 15px;
    overflow-y: auto;
    border-left: 2px solid #333;
    display: none;
    z-index: 999;
}

.cart h2 {
    text-align: center;
}

.cart-item {
    border-bottom: 1px solid #333;
    padding: 10px 0;
}

.checkout {
    margin-top: 15px;
    padding: 10px;
    background: gold;
    color: black;
    text-align: center;
    cursor: pointer;
    font-weight: bold;
}
</style>
</head>

<body>

<header>
<div class="header-container">
    <div>Moody Leather Craft Store</div>

    <div class="cart-btn" onclick="toggleCart()">
        🛒 Cart (<span id="cartCount">0</span>)
    </div>
</div>
</header>

<nav>
<button onclick="filter('all')">All</button>
<button onclick="filter('Wallets')">Wallets</button>
<button onclick="filter('Belts')">Belts</button>
<button onclick="filter('Collars')">Collars</button>
<button onclick="filter('Bracelets')">Bracelets</button>
<button onclick="filter('Keychains')">Keychains</button>
<button onclick="filter('Notebook Covers')">Notebook Covers</button>
<button onclick="filter('Bible Covers')">Bible Covers</button>
<button onclick="filter('Laptop Covers')">Laptop Covers</button>
<button onclick="filter('Glasses Cases')">Glasses Cases</button>
<button onclick="filter('Custom Orders')">Custom Orders</button>
</nav>

<div class="products" id="productList"></div>

<!-- CART (NOW HIDDEN UNTIL CLICKED) -->
<div class="cart" id="cartPanel">
<h2>Cart</h2>
<div id="cartItems"></div>
<div class="checkout" onclick="checkout()">Checkout (PayPal)</div>
</div>

<script>
const PAYPAL_EMAIL = "your-paypal-email@example.com";

const products = [
    {id:1, name:"Classic Wallet", category:"Wallets"},
    {id:2, name:"Rugged Belt", category:"Belts"},
    {id:3, name:"Dog Collar", category:"Collars"},
    {id:4, name:"Leather Bracelet", category:"Bracelets"},
    {id:5, name:"Keychain Tag", category:"Keychains"},
    {id:6, name:"Notebook Cover A5", category:"Notebook Covers"},
    {id:7, name:"Bible Cover Premium", category:"Bible Covers"},
    {id:8, name:"Laptop Sleeve 13”", category:"Laptop Covers"},
    {id:9, name:"Glasses Case Soft", category:"Glasses Cases"},
    {id:10, name:"Custom Order Request", category:"Custom Orders"},
    {id:11, name:"Vintage Wallet", category:"Wallets"},
    {id:12, name:"Double Stitch Belt", category:"Belts"},
    {id:13, name:"Studded Collar", category:"Collars"},
    {id:14, name:"Braided Bracelet", category:"Bracelets"},
    {id:15, name:"Metal Key Clip", category:"Keychains"},
    {id:16, name:"Journal Cover Rustic", category:"Notebook Covers"},
    {id:17, name:"Bible Cover Deluxe", category:"Bible Covers"},
    {id:18, name:"Laptop Case Pro", category:"Laptop Covers"},
    {id:19, name:"Hard Glasses Case", category:"Glasses Cases"},
    {id:20, name:"Personal Custom Design", category:"Custom Orders"},
];

let cart = JSON.parse(localStorage.getItem("cart")) || [];
let currentFilter = "all";

function img(id){
    return `https://via.placeholder.com/300x200.png?text=Product+${id}`;
}

function displayProducts(){
    const list = document.getElementById("productList");
    list.innerHTML = "";

    products
    .filter(p => currentFilter === "all" || p.category === currentFilter)
    .forEach(p => {
        list.innerHTML += `
        <div class="product">
            <img src="${img(p.id)}"/>
            <h3>${p.name}</h3>
            <p>${p.category}</p>
            <button class="add" onclick="addToCart(${p.id})">Add to Cart</button>
        </div>`;
    });
}

function filter(cat){
    currentFilter = cat;
    displayProducts();
}

/* TOGGLE CART (NEW) */
function toggleCart(){
    const panel = document.getElementById("cartPanel");
    panel.style.display = panel.style.display === "block" ? "none" : "block";
}

function addToCart(id){
    const item = products.find(p => p.id === id);
    cart.push(item);
    updateCart();
}

function removeItem(index){
    cart.splice(index,1);
    updateCart();
}

function updateCart(){
    localStorage.setItem("cart", JSON.stringify(cart));

    const cartDiv = document.getElementById("cartItems");
    const count = document.getElementById("cartCount");

    cartDiv.innerHTML = "";

    cart.forEach((item,i)=>{
        cartDiv.innerHTML += `
        <div class="cart-item">
            ${item.name}
            <button onclick="removeItem(${i})">X</button>
        </div>`;
    });

    count.innerText = cart.length;
}

function checkout(){
    if(cart.length === 0){
        alert("Cart is empty");
        return;
    }

    alert("Redirecting to PayPal checkout...\nEmail: " + PAYPAL_EMAIL);
    window.open("https://www.paypal.com/cgi-bin/webscr", "_blank");
}

displayProducts();
updateCart();
</script>

</body>
</html>
