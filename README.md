<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Electronics Store</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 0; padding: 0; }
        header, footer { background-color: #333; color: white; padding: 10px 20px; text-align: center; }
        nav a { color: white; margin: 0 10px; text-decoration: none; }
        .container { padding: 20px; }
        .page-content { display: none; }
        .page-content.active { display: block; }
        .product { border: 1px solid #ddd; padding: 10px; margin: 10px; }
        .product img { width: 100px; }
        .product-list { display: flex; flex-wrap: wrap; }
        .product-list .product { width: 30%; box-sizing: border-box; }
        .sorting { margin-bottom: 20px; }
        #cart-items { list-style-type: none; padding: 0; }
        #cart-items li { margin: 10px 0; }
    </style>
</head>
<body>
    <header>
        <nav>
            <a href="#" onclick="showPage('home')">Home</a>
            <a href="#" onclick="showPage('about')">About</a>
            <a href="#" onclick="showPage('contact')">Contact</a>
            <a href="#" onclick="showPage('cart')">Cart</a>
            <a href="#" onclick="showPage('products')">Products</a>
            <a href="#" onclick="showPage('login')">Login</a>
        </nav>
    </header>

    <div class="container">
        <div id="home" class="page-content active">
            <h1>Welcome to the Electronics Store</h1>
            <p>Find the latest gadgets and electronics here!</p>
        </div>

        <div id="about" class="page-content">
            <h1>About Us</h1>
            <p>We offer a wide range of electronics including laptops, smartphones, and more. Our goal is to provide the best products at competitive prices.</p>
        </div>

        <div id="contact" class="page-content">
            <h1>Contact Us</h1>
            <p>Email: tannu@electronicsstore.com</p>
            <p>Phone: 9392518051</p>
            <p>Address: 7-1-282/C/2A Balkampet</p>
        </div>

        <div id="cart" class="page-content">
            <h1>Shopping Cart</h1>
            <ul id="cart-items">
                <!-- Cart items will be dynamically inserted here -->
            </ul>
            <p id="cart-total">Total: $0.00</p>
        </div>

        <div id="products" class="page-content">
            <h1>Products</h1>
            <div class="sorting">
                <label for="sort">Sort by:</label>
                <select id="sort" onchange="sortProducts()">
                    <option value="name">Name</option>
                    <option value="price">Price</option>
                </select>
            </div>
            <div class="product-list" id="product-list">
                <!-- Products will be dynamically inserted here -->
            </div>
        </div>

        <div id="login" class="page-content">
            <h1>Login</h1>
            <form onsubmit="handleLogin(event)">
                <label for="username">Username:</label>
                <input type="text" id="username" name="username" required><br><br>
                <label for="password">Password:</label>
                <input type="password" id="password" name="password" required><br><br>
                <button type="submit">Login</button>
            </form>
        </div>
    </div>

    <footer>
        <p>&copy; 2024 Electronics Store. All rights reserved.</p>
    </footer>

    <script>
        const products = [
            { id: 1, name: 'Smartphone', price: 299, image: 'https://via.placeholder.com/100' },
            { id: 2, name: 'Laptop', price: 899, image: 'https://via.placeholder.com/100' },
            { id: 3, name: 'Headphones', price: 89, image: 'https://via.placeholder.com/100' },
            { id: 4, name: 'Smartwatch', price: 199, image: 'https://via.placeholder.com/100' }
        ];

        let cart = [];

        function showPage(pageId) {
            const pages = document.querySelectorAll('.page-content');
            pages.forEach(page => page.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
            if (pageId === 'products') {
                renderProducts();
            } else if (pageId === 'cart') {
                renderCart();
            }
        }

        function renderProducts() {
            const productList = document.getElementById('product-list');
            productList.innerHTML = '';
            products.forEach(product => {
                const productDiv = document.createElement('div');
                productDiv.className = 'product';
                productDiv.innerHTML = `
                    <img src="${product.image}" alt="${product.name}">
                    <h2>${product.name}</h2>
                    <p>Price: $${product.price}</p>
                    <button onclick="addToCart(${product.id})">Add to Cart</button>
                `;
                productList.appendChild(productDiv);
            });
        }

        function sortProducts() {
            const sortOption = document.getElementById('sort').value;
            if (sortOption === 'name') {
                products.sort((a, b) => a.name.localeCompare(b.name));
            } else if (sortOption === 'price') {
                products.sort((a, b) => a.price - b.price);
            }
            renderProducts();
        }

        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const cartItem = cart.find(item => item.product.id === productId);
            if (cartItem) {
                cartItem.quantity++;
            } else {
                cart.push({ product, quantity: 1 });
            }
            renderCart();
        }

        function renderCart() {
            const cartItems = document.getElementById('cart-items');
            const cartTotal = document.getElementById('cart-total');
            cartItems.innerHTML = '';
            let total = 0;
            cart.forEach(item => {
                total += item.product.price * item.quantity;
                const itemLi = document.createElement('li');
                itemLi.textContent = `${item.product.name} x${item.quantity} - $${item.product.price * item.quantity}`;
                cartItems.appendChild(itemLi);
            });
            cartTotal.textContent = `Total: $${total.toFixed(2)}`;
        }

        function handleLogin(event) {
            event.preventDefault();
            alert('Login functionality is not implemented in this demo.');
        }
    </script>
</body>
</html>

