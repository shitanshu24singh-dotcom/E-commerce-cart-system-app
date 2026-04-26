<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>E-commerce Cart System</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f9;
      margin: 0;
      padding: 20px;
    }
    h2 {
      text-align: center;
    }
    .products, .cart {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      justify-content: center;
      margin-top: 20px;
    }
    .card {
      background: #fff;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      padding: 15px;
      width: 200px;
      text-align: center;
    }
    .card img {
      max-width: 100%;
      border-radius: 5px;
    }
    button {
      margin-top: 10px;
      padding: 8px 12px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      background: #2196F3;
      color: white;
    }
    button:hover {
      background: #1976D2;
    }
    .cart-item {
      background: #fff;
      padding: 10px;
      border-radius: 5px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      display: flex;
      justify-content: space-between;
      align-items: center;
      width: 300px;
    }
    .total {
      text-align: center;
      margin-top: 20px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <h2>Products</h2>
  <div class="products" id="products"></div>

  <h2>Shopping Cart</h2>
  <div class="cart" id="cart"></div>
  <p class="total">Total: $<span id="total">0</span></p>

  <script>
    const products = [
      { id: 1, name: "Laptop", price: 800, img: "https://via.placeholder.com/150" },
      { id: 2, name: "Phone", price: 500, img: "https://via.placeholder.com/150" },
      { id: 3, name: "Headphones", price: 100, img: "https://via.placeholder.com/150" },
      { id: 4, name: "Watch", price: 200, img: "https://via.placeholder.com/150" }
    ];

    const cart = [];
    const productsEl = document.getElementById("products");
    const cartEl = document.getElementById("cart");
    const totalEl = document.getElementById("total");

    function renderProducts() {
      products.forEach(p => {
        const card = document.createElement("div");
        card.className = "card";
        card.innerHTML = `
          <img src="${p.img}" alt="${p.name}">
          <h3>${p.name}</h3>
          <p>$${p.price}</p>
          <button onclick="addToCart(${p.id})">Add to Cart</button>
        `;
        productsEl.appendChild(card);
      });
    }

    function addToCart(id) {
      const product = products.find(p => p.id === id);
      cart.push(product);
      renderCart();
    }

    function removeFromCart(index) {
      cart.splice(index, 1);
      renderCart();
    }

    function renderCart() {
      cartEl.innerHTML = "";
      let total = 0;
      cart.forEach((item, index) => {
        total += item.price;
        const cartItem = document.createElement("div");
        cartItem.className = "cart-item";
        cartItem.innerHTML = `
          ${item.name} - $${item.price}
          <button onclick="removeFromCart(${index})">Remove</button>
        `;
        cartEl.appendChild(cartItem);
      });
      totalEl.textContent = total;
    }

    renderProducts();
  </script>
</body>
</html>
