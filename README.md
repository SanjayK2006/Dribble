# Project Responsive Web Design using Bootstrap
## Date:19-11-24

## AIM:
To create a simplified clone of Dribbble (https://dribbble.com/) landing page.


## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Insert the necessary CSS and JavaScript files as external in order to use Bootstrap.

### Step 5:
Create a HTML file and include the needed Bootstrap components.

### Step 6:
Publish the website in the LocalHost.

## PROGRAM :
### index.html:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grocery Store</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- Custom CSS -->
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-success">
        <div class="container">
            <a class="navbar-brand" href="#">GroceryMart</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <!-- Centered Search Bar -->
                <form class="d-flex mx-auto" role="search">
                    <input class="form-control me-2" type="search" placeholder="Search groceries..." aria-label="Search">
                    <button class="btn btn-outline-light" type="submit">Search</button>
                </form>
                <!-- Right-aligned Buttons -->
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item">
                        <button class="btn btn-outline-light me-2" onclick="alert('Signup page coming soon!')">Signup</button>
                    </li>
                    <li class="nav-item">
                        <button class="btn btn-outline-light" onclick="alert('Login page coming soon!')">Login</button>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <header class="bg-light text-center py-5">
        <div class="container">
            <h1>Welcome to GroceryMart</h1>
            <p class="lead">Your one-stop shop for fresh groceries and daily essentials!</p>
        </div>
    </header>

    <!-- Featured Products Section -->
    <section id="products" class="py-5">
        <div class="container">
            <h2 class="text-center mb-4">Featured Products</h2>
            <div class="row">
                <div class="col-md-4">
                    <div class="card">
                        <img src="4.png" class="card-img-top" alt="Apples">
                        <div class="card-body text-center">
                            <h5 class="card-title">Fresh Apples</h5>
                            <p class="card-text">$3.50 per kg</p>
                            <button class="btn btn-success add-to-cart" data-name="Fresh Apples" data-price="3.5">Add to Cart</button>
                        </div>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="card">
                        <img src="3.png" class="card-img-top" alt="Tomatoes">
                        <div class="card-body text-center">
                            <h5 class="card-title">Tomatoes</h5>
                            <p class="card-text">$2.00 per kg</p>
                            <button class="btn btn-success add-to-cart" data-name="Tomatoes" data-price="2">Add to Cart</button>
                        </div>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="card">
                        <img src="1.jpg" class="card-img-top" alt="Milk">
                        <div class="card-body text-center">
                            <h5 class="card-title">Magiee</h5>
                            <p class="card-text">$5 each packet</p>
                            <button class="btn btn-success add-to-cart" data-name="Magiee" data-price="1.2">Add to Cart</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Cart Section -->
    <section id="cart" class="py-5 bg-light">
        <div class="container">
            <h2 class="text-center mb-4">Shopping Cart</h2>
            <table class="table table-bordered">
                <thead>
                    <tr>
                        <th>Product</th>
                        <th>Price</th>
                        <th>Quantity</th>
                        <th>Total</th>
                        <th>Action</th>
                    </tr>
                </thead>
                <tbody id="cartItems">
                    <tr>
                        <td colspan="5" class="text-center">Your cart is empty</td>
                    </tr>
                </tbody>
            </table>
            <h3 class="text-end">Total: $<span id="cartTotal">0.00</span></h3>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-success text-center text-white py-3">
        <p>&copy; 2024 GroceryMart. All Rights Reserved.</p>
    </footer>

    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
    <!-- Custom JS -->
    <script src="script.js"></script>
</body>
</html>
```

## styles.css:
```
/* Center hero text */
header {
    background: url('image.png') center/cover no-repeat;
    color: #fff;
    text-shadow: 1px 1px 5px rgba(0, 0, 0, 0.5);
}

/* Adjust product card hover */
.card:hover {
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
    transform: scale(1.05);
    transition: transform 0.2s, box-shadow 0.2s;
}

/* Footer styling */
footer {
    font-size: 0.9rem;
    letter-spacing: 0.5px;
}
```
## script.js:
```
let cart = [];
const cartItems = document.getElementById('cartItems');
const cartTotal = document.getElementById('cartTotal');

// Add to cart functionality
document.querySelectorAll('.add-to-cart').forEach((button) => {
    button.addEventListener('click', function () {
        const productName = this.dataset.name;
        const productPrice = parseFloat(this.dataset.price);

        const existingProduct = cart.find((item) => item.name === productName);

        if (existingProduct) {
            existingProduct.quantity += 1;
        } else {
            cart.push({ name: productName, price: productPrice, quantity: 1 });
        }

        updateCart();
    });
});

// Update cart display
function updateCart() {
    cartItems.innerHTML = '';
    let total = 0;

    if (cart.length === 0) {
        cartItems.innerHTML = <tr><td colspan="5" class="text-center">Your cart is empty</td></tr>;
    } else {
        cart.forEach((item) => {
            const itemTotal = item.price * item.quantity;
            total += itemTotal;

            cartItems.innerHTML += `
                <tr>
                    <td>${item.name}</td>
                    <td>$${item.price.toFixed(2)}</td>
                    <td>${item.quantity}</td>
                    <td>$${itemTotal.toFixed(2)}</td>
                    <td><button class="btn btn-danger btn-sm" onclick="removeItem('${item.name}')">Remove</button></td>
                </tr>
            `;
        });
    }

    cartTotal.textContent = total.toFixed(2);
}

// Remove item from cart
function removeItem(name) {
    cart = cart.filter((item) => item.name !== name);
    updateCart();
}
```


## OUTPUT:
![project](https://github.com/user-attachments/assets/918f8ff8-1470-4c59-acac-3799ce6fd491)



## RESULT:
The Project for responsive web design using Bootstrap is completed successfully.
