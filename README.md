# Bosco
<!DOCTYPE html>
<head>
    <title>Products CRUD</title>
    <link rel="stylesheet" href="CRUD.css">
</head>
<body>
    <h2>Product Details CRUD</h2>
    <form id="productForm">
        <input type="text" id="productName" placeholder="Enter product name" required>
        <input type="number" id="price" placeholder="Enter price" required>
        <button type="submit">Add Product</button>
    </form>
    <table id="productTable">
        <thead>
            <tr>
                <th>Product Name</th>
                <th>Price (rs)</th>
                <th>Actions</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
    <script>
        const productForm = document.getElementById('productForm');
        const productNameInput = document.getElementById('productName');
        const priceInput = document.getElementById('price');
        const productTableBody = document.querySelector('#productTable tbody');
        let products = [];
        let editIndex = null;
        productForm.addEventListener('submit', function(e) {
            e.preventDefault();
            const name = productNameInput.value.trim();
            const price = parseFloat(priceInput.value.trim()).toFixed(2);
            if (editIndex===null) {
                products.push({name, price });
            } else {
                products[editIndex] = {name, price };
                editIndex = null;
            }
            productForm.reset();
            renderTable();
        });
        function renderTable() {
            productTableBody.innerHTML = '';
            products.forEach((product, index) => {
                const row = document.createElement('tr')
                 row.innerHTML = `
                    <td>${product.name}</td>
                    <td>$${product.price}</td>
                    <td>
                        <button onclick="editProduct(${index})">Edit</button>
                        <button onclick="deleteProduct(${index})">Delete</button>
                    </td>
                `;
                productTableBody.appendChild(row);
            });
        }
        window.editProduct = function(index) {
            const product = products[index];
            productNameInput.value = product.name;
            priceInput.value = product.price;
            editIndex = index;
        }
        window.deleteProduct = function(index) {
            if (confirm('Are you sure you want to delete this product?')) {
                products.splice(index, 1);
                renderTable();
            }
        }
            renderTable();
    </script>
</body>
</html>
