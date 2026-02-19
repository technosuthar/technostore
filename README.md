# technostore
<!DOCTYPE html>
<html>
<head>
    <title>techno Store</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            background: #f4f6f9;
        }

        header {
            background: #2c3e50;
            color: white;
            padding: 15px;
            text-align: center;
            font-size: 24px;
        }

        .container {
            display: flex;
            padding: 20px;
        }

        .products {
            width: 65%;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
        }

        .card {
            background: white;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            text-align: center;
        }

        .card h3 {
            margin: 10px 0;
        }

        .card button {
            background: #27ae60;
            color: white;
            border: none;
            padding: 8px 12px;
            border-radius: 5px;
            cursor: pointer;
        }

        .card button:hover {
            background: #219150;
        }

        .cart {
            width: 35%;
            background: white;
            margin-left: 20px;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .cart h2 {
            margin-top: 0;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
        }

        .remove-btn {
            background: red;
            color: white;
            border: none;
            padding: 4px 8px;
            border-radius: 4px;
            cursor: pointer;
        }

        .total {
            font-weight: bold;
            margin-top: 15px;
        }
    </style>
</head>
<body>

<header> techno Store</header>

<div class="container">
    <div class="products">
        <div class="card">
            <img src="24.png"  width="100" height="100">
            <h3>Laptop</h3>
            <p>50000</p>
            <button onclick="addToCart('Laptop', 50000)">Add to Cart</button>
        </div>

        <div class="card">
             <img src="iphone.jpeg"  width="100" height="100">
            <h3>Mobile</h3>
            <p>20000</p>
            <button onclick="addToCart('Mobile', 20000)">Add to Cart</button>
        </div>

        <div class="card">
            <img src="images.jpeg"  width="100" height="100">
            <h3>Headphones</h3>
            <p>2000</p>
            <button onclick="addToCart('Headphones', 2000)">Add to Cart</button>
        </div>

        <div class="card">
            <img src="pngtree-the-smartwatch-banner-png-image_11919210.png"  width="100" height="100">
            <h3>Smart Watch</h3>
            <p>5000</p>
            <button onclick="addToCart('Smart Watch', 5000)">Add to Cart</button>
        </div>

        <div class="card">
            <img src="123432.jpeg"  width="100" height="100">
            <h3>Keyboard</h3>
            <p>1500</p>
            <button onclick="addToCart('Keyboard', 1500)">Add to Cart</button>
        </div>

        
    </div>

    <div class="cart">
        <h2> techno Cart</h2>
        <div id="cartItems"></div>
        <div class="total">Total: <span id="total">0</span></div>
        <input type="text" id="customerName" placeholder="Enter Your Name" style="width:100%; padding:8px; margin-top:10px;">
<button onclick="buyNow()" style="margin-top:10px; width:100%; background:#2980b9; color:white; border:none; padding:10px; border-radius:5px; cursor:pointer;">
    Buy Now
</button>

<div id="message" style="margin-top:10px; color:green; font-weight:bold;"></div>

    </div>
</div>

<script>
    let cart = [];
    let total = 0;

    function addToCart(product, price) {
        cart.push({product, price});
        total += price;
        updateCart();
    }

    function removeFromCart(index) {
        total -= cart[index].price;
        cart.splice(index, 1);
        updateCart();
    }

    function updateCart() {
        let cartItems = document.getElementById("cartItems");
        cartItems.innerHTML = "";

        cart.forEach((item, index) => {
            cartItems.innerHTML += `
                <div class="cart-item">
                    ${item.product} - ₹${item.price}
                    <button class="remove-btn" onclick="removeFromCart(${index})">X</button>
                </div>
            `;
        });

        document.getElementById("total").innerText = total;
    }
</script>
<script>
function buyNow() {
    let name = document.getElementById("customerName").value;

    if (cart.length === 0) {
        alert("Your cart is empty!");
        return;
    }

    if (name === "") {
        alert("Please enter your name!");
        return;
    }

    let upiID = "yourname@upi";  // 🔴 Replace with your UPI ID
    let amount = total;
    let note = "Shopping Payment";

    let upiLink = `upi://pay?pa=${upiID}&pn=${name}&am=${amount}&cu=INR&tn=${note}`;

    window.location.href = upiLink;
    
}
</script>



</body>
</html>
