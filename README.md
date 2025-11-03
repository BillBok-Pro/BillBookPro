[Index.html](https://github.com/user-attachments/files/23305517/Index.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BillBok Pro v4 - Dashboard</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        /* Page Sections */
        .page {
            display: none;
        }

        .page.active {
            display: block;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Dashboard */
        .dashboard-header {
            background: white;
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 15px 50px rgba(0,0,0,0.2);
            margin-bottom: 30px;
            text-align: center;
        }

        .dashboard-header h1 {
            font-size: 36px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
        }

        .dashboard-header p {
            color: #666;
            font-size: 16px;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: white;
            padding: 35px;
            border-radius: 20px;
            box-shadow: 0 15px 40px rgba(0,0,0,0.15);
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }

        .stat-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 50px rgba(0,0,0,0.25);
        }

        .stat-card.clickable:hover {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .stat-card h3 {
            font-size: 48px;
            margin-bottom: 10px;
            font-weight: bold;
        }

        .stat-card p {
            font-size: 16px;
            opacity: 0.8;
        }

        .stat-card.clickable p::after {
            content: ' →';
            font-weight: bold;
        }

        /* Page Header */
        .page-header {
            background: white;
            padding: 25px 30px;
            border-radius: 15px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.15);
            margin-bottom: 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 15px;
        }

        .page-header h2 {
            font-size: 28px;
            color: #333;
        }

        .page-actions {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }

        /* Buttons */
        .btn {
            padding: 12px 28px;
            border: none;
            border-radius: 10px;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn-primary {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(102, 126, 234, 0.4);
        }

        .btn-secondary {
            background: #6c757d;
            color: white;
        }

        .btn-secondary:hover {
            background: #5a6268;
        }

        .btn-success {
            background: #28a745;
            color: white;
        }

        .btn-danger {
            background: #dc3545;
            color: white;
        }

        .btn-sm {
            padding: 8px 16px;
            font-size: 13px;
        }

        /* Products Page */
        .products-container {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.15);
        }

        .add-product-form {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 12px;
            margin-bottom: 25px;
            border: 2px solid #e9ecef;
        }

        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 15px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
        }

        .form-group label {
            font-weight: 600;
            margin-bottom: 6px;
            color: #333;
            font-size: 14px;
        }

        .form-group input {
            padding: 10px;
            border: 2px solid #dee2e6;
            border-radius: 8px;
            font-size: 14px;
            transition: all 0.3s;
        }

        .form-group input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        /* Table */
        .table-container {
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background: white;
        }

        table th {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 15px;
            text-align: left;
            font-size: 14px;
            font-weight: 600;
        }

        table td {
            padding: 15px;
            border-bottom: 1px solid #e9ecef;
            font-size: 14px;
        }

        table tr:hover {
            background: #f8f9fa;
        }

        /* Bills Page */
        .bills-container {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.15);
        }

        .bill-list {
            display: grid;
            gap: 15px;
            margin-top: 20px;
        }

        .bill-card {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 12px;
            border-left: 5px solid #667eea;
            cursor: pointer;
            transition: all 0.3s;
        }

        .bill-card:hover {
            background: #e9ecef;
            transform: translateX(5px);
        }

        .bill-card h4 {
            color: #333;
            margin-bottom: 8px;
        }

        .bill-card p {
            color: #666;
            font-size: 14px;
            margin: 4px 0;
        }

        /* Invoice */
        .invoice-box {
            background: #fffacd;
            border: 3px solid #000;
            padding: 0;
            margin-top: 25px;
        }

        .invoice-header {
            border-bottom: 3px solid #000;
            padding: 25px;
        }

        .shop-edit {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-bottom: 15px;
        }

        .shop-edit input,
        .shop-edit textarea {
            padding: 10px;
            border: 2px solid #000;
            background: white;
            font-size: 14px;
        }

        .shop-edit textarea {
            grid-column: 1/3;
            resize: vertical;
            min-height: 60px;
        }

        .shop-display {
            display: none;
            text-align: center;
        }

        .shop-display h2 {
            font-size: 28px;
            margin-bottom: 8px;
        }

        .shop-display p {
            margin: 4px 0;
            font-size: 14px;
        }

        .invoice-title {
            text-align: center;
            font-size: 32px;
            font-weight: bold;
            margin: 18px 0;
            text-decoration: underline;
        }

        .invoice-meta {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
        }

        .invoice-meta input {
            padding: 8px;
            border: 2px solid #000;
            background: white;
            font-size: 14px;
        }

        .customer-section {
            border-bottom: 3px solid #000;
            padding: 25px;
        }

        .customer-section h3 {
            font-size: 18px;
            margin-bottom: 15px;
            text-decoration: underline;
        }

        .customer-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
        }

        .invoice-field {
            margin-bottom: 10px;
        }

        .invoice-field label {
            display: block;
            font-weight: bold;
            margin-bottom: 4px;
            font-size: 13px;
        }

        .invoice-field input {
            width: 100%;
            padding: 8px;
            border: 2px solid #000;
            background: white;
            font-size: 14px;
        }

        .product-section {
            padding: 25px;
        }

        .product-section table th {
            background: #000;
            color: white;
            border: 2px solid #000;
        }

        .product-section table td {
            border: 2px solid #000;
            text-align: center;
        }

        .product-section table td input,
        .product-section table td select {
            width: 100%;
            padding: 6px;
            border: 1px solid #666;
            text-align: center;
            font-size: 13px;
        }

        .autocomplete-box {
            position: relative;
        }

        .autocomplete-list {
            position: absolute;
            top: 100%;
            left: 0;
            right: 0;
            background: white;
            border: 2px solid #000;
            max-height: 150px;
            overflow-y: auto;
            z-index: 1000;
            display: none;
        }

        .autocomplete-list div {
            padding: 8px;
            cursor: pointer;
            border-bottom: 1px solid #ddd;
        }

        .autocomplete-list div:hover {
            background: #f0f0f0;
        }

        .calc-section {
            border-top: 3px solid #000;
            padding: 25px;
        }

        .calc-layout {
            display: grid;
            grid-template-columns: 1fr 280px;
            gap: 20px;
        }

        .amount-words {
            border: 2px solid #000;
            padding: 20px;
            background: white;
            min-height: 100px;
            font-weight: bold;
        }

        .totals-table {
            border: 2px solid #000;
            background: white;
        }

        .totals-table table {
            margin: 0;
        }

        .totals-table td {
            padding: 12px 15px;
            font-size: 15px;
        }

        .total-row {
            background: #f0f0f0;
            font-weight: bold;
            font-size: 18px;
        }

        .footer-section {
            border-top: 3px solid #000;
            padding: 25px;
        }

        .thank-you {
            text-align: center;
            font-size: 20px;
            font-weight: bold;
            margin: 20px 0;
        }

        .signature-line {
            text-align: right;
            margin-top: 60px;
        }

        .signature-line p {
            border-top: 2px solid #000;
            display: inline-block;
            padding-top: 8px;
            min-width: 200px;
        }

        /* History Page */
        .history-container {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.15);
        }

        .search-box {
            margin-bottom: 20px;
        }

        .search-box input {
            width: 100%;
            padding: 12px 20px;
            border: 2px solid #dee2e6;
            border-radius: 10px;
            font-size: 15px;
        }

        .search-box input:focus {
            outline: none;
            border-color: #667eea;
        }

        /* Ad Section */
        .ad-section {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.15);
            margin-top: 30px;
            text-align: center;
            border: 3px dashed #dee2e6;
        }

        .ad-section p {
            color: #999;
            font-size: 16px;
        }

        /* Toast */
        .toast {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #28a745;
            color: white;
            padding: 18px 28px;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            z-index: 99999;
            display: none;
            animation: slideIn 0.3s;
        }

        .toast.show {
            display: block;
        }

        @keyframes slideIn {
            from { transform: translateX(400px); }
            to { transform: translateX(0); }
        }

        /* Print */
        @media print {
            body {
                background: white;
                padding: 0;
            }

            .page-header,
            .btn,
            .ad-section,
            .no-print {
                display: none !important;
            }

            .invoice-box {
                box-shadow: none;
            }

            .shop-edit {
                display: none !important;
            }

            .shop-display {
                display: block !important;
            }

            .invoice-meta input,
            .invoice-field input,
            table td input,
            table td select {
                border: none;
                background: transparent;
            }
        }

        /* Responsive */
        @media (max-width: 768px) {
            .stats-grid {
                grid-template-columns: 1fr;
            }

            .shop-edit,
            .customer-grid,
            .calc-layout,
            .invoice-meta {
                grid-template-columns: 1fr;
            }

            .page-header {
                flex-direction: column;
                align-items: stretch;
            }

            .page-actions {
                flex-direction: column;
            }

            .btn {
                width: 100%;
                justify-content: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- DASHBOARD PAGE -->
        <div id="dashboardPage" class="page active">
            <div class="dashboard-header">
                <h1>📊 BillBok Pro v4</h1>
                <p>Complete Billing & Inventory Management System</p>
            </div>

            <div class="stats-grid">
                <div class="stat-card clickable" onclick="showPage('productsPage')">
                    <h3 id="totalProducts">0</h3>
                    <p>Total Products</p>
                </div>
                <div class="stat-card clickable" onclick="showPage('billsPage')">
                    <h3 id="totalBills">0</h3>
                    <p>Total Bills Created</p>
                </div>
                <div class="stat-card">
                    <h3 id="todayRevenue">₹0</h3>
                    <p>Today's Revenue</p>
                </div>
                <div class="stat-card">
                    <h3 id="totalRevenue">₹0</h3>
                    <p>Total Revenue (All Time)</p>
                </div>
            </div>

            <div class="ad-section no-print">
                <p>📢 Advertisement Space - Place your AdsTerra code here</p>
            </div>
        </div>

        <!-- PRODUCTS PAGE -->
        <div id="productsPage" class="page">
            <div class="page-header">
                <h2>📦 Manage Products</h2>
                <div class="page-actions">
                    <button class="btn btn-secondary" onclick="showPage('dashboardPage')">← Back to Dashboard</button>
                </div>
            </div>

            <div class="products-container">
                <div class="add-product-form">
                    <h3 style="margin-bottom: 15px; color: #333;">Add New Product</h3>
                    <div class="form-grid">
                        <div class="form-group">
                            <label>Product Name</label>
                            <input type="text" id="productName" placeholder="Enter product name">
                        </div>
                        <div class="form-group">
                            <label>Rate (₹)</label>
                            <input type="number" id="productRate" placeholder="0.00" min="0" step="0.01">
                        </div>
                        <div class="form-group">
                            <label>Stock Quantity</label>
                            <input type="number" id="productStock" placeholder="0" min="0">
                        </div>
                    </div>
                    <button class="btn btn-success" onclick="addProduct()">➕ Add Product</button>
                </div>

                <div class="table-container">
                    <table>
                        <thead>
                            <tr>
                                <th>Product Name</th>
                                <th>Rate (₹)</th>
                                <th>Stock</th>
                                <th>Actions</th>
                            </tr>
                        </thead>
                        <tbody id="productsTableBody">
                            <tr><td colspan="4" style="text-align:center; padding: 30px;">No products added yet</td></tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- BILLS PAGE -->
        <div id="billsPage" class="page">
            <div class="page-header">
                <h2>🧾 Billing</h2>
                <div class="page-actions">
                    <button class="btn btn-primary" onclick="createNewBill()">+ New Bill</button>
                    <button class="btn btn-primary" onclick="showPage('historyPage')">📜 View History</button>
                    <button class="btn btn-secondary" onclick="showPage('dashboardPage')">← Back to Dashboard</button>
                </div>
            </div>

            <div id="billListSection" class="bills-container">
                <h3 style="margin-bottom: 15px; color: #333;">Recent Bills</h3>
                <div class="bill-list" id="billsList"></div>
            </div>

            <div id="invoiceSection" class="bills-container" style="display: none;">
                <div class="invoice-box">
                    <!-- HEADER -->
                    <div class="invoice-header">
                        <div class="shop-edit no-print">
                            <input type="text" id="shopName" placeholder="Shop Name" style="grid-column: 1/3; font-size: 18px; font-weight: bold; text-align: center;">
                            <input type="text" id="shopMobile" placeholder="Mobile Number">
                            <input type="text" id="shopGST" placeholder="GST Number">
                            <textarea id="shopAddress" placeholder="Shop Address"></textarea>
                        </div>

                        <div class="shop-display">
                            <h2 id="displayShopName">SHOP NAME</h2>
                            <p id="displayShopMobile"></p>
                            <p id="displayShopGST"></p>
                            <p id="displayShopAddress"></p>
                        </div>

                        <div class="invoice-title">TAX INVOICE BILL</div>

                        <div class="invoice-meta">
                            <input type="text" id="billNumber" placeholder="Bill No." readonly>
                            <input type="date" id="billDate">
                        </div>
                    </div>

                    <!-- CUSTOMER -->
                    <div class="customer-section">
                        <h3>Customer Details</h3>
                        <div class="customer-grid">
                            <div class="invoice-field">
                                <label>Customer Name:</label>
                                <input type="text" id="customerName" placeholder="Customer Name">
                            </div>
                            <div class="invoice-field">
                                <label>Mobile:</label>
                                <input type="text" id="customerMobile" placeholder="Mobile Number">
                            </div>
                            <div class="invoice-field" style="grid-column: 1/3;">
                                <label>Warranty / Guarantee:</label>
                                <input type="text" id="warrantyDetails" placeholder="Warranty details">
                            </div>
                        </div>
                    </div>

                    <!-- PRODUCTS -->
                    <div class="product-section">
                        <table>
                            <thead>
                                <tr>
                                    <th style="width: 50px;">Sl</th>
                                    <th style="width: 40%;">Particulars</th>
                                    <th style="width: 80px;">Qty</th>
                                    <th style="width: 100px;">Rate</th>
                                    <th style="width: 120px;">Amount</th>
                                    <th style="width: 60px;" class="no-print">×</th>
                                </tr>
                            </thead>
                            <tbody id="billTableBody"></tbody>
                        </table>
                        <button class="btn btn-primary btn-sm no-print" onclick="addBillRow()">➕ Add Item</button>
                    </div>

                    <!-- CALCULATIONS -->
                    <div class="calc-section">
                        <div class="calc-layout">
                            <div>
                                <label style="font-weight: bold; margin-bottom: 8px; display: block;">Amount in Words:</label>
                                <div class="amount-words" id="amountWords">Zero Rupees Only</div>
                            </div>
                            <div class="totals-table">
                                <table>
                                    <tr>
                                        <td style="text-align: right;">Subtotal:</td>
                                        <td style="text-align: right;">₹<span id="subtotal">0.00</span></td>
                                    </tr>
                                    <tr class="no-print">
                                        <td style="text-align: right;">Discount (%):</td>
                                        <td><input type="number" id="discountPercent" value="0" min="0" max="100" style="width: 100%; padding: 4px;" onchange="calculateTotal()"></td>
                                    </tr>
                                    <tr>
                                        <td style="text-align: right;">Discount:</td>
                                        <td style="text-align: right;">-₹<span id="discountAmount">0.00</span></td>
                                    </tr>
                                    <tr class="total-row">
                                        <td style="text-align: right;">Total:</td>
                                        <td style="text-align: right;">₹<span id="grandTotal">0.00</span></td>
                                    </tr>
                                </table>
                            </div>
                        </div>
                    </div>

                    <!-- FOOTER -->
                    <div class="footer-section">
                        <div class="thank-you">Thank You and Visit Again.</div>
                        <div class="signature-line">
                            <p>Signature:</p>
                        </div>
                    </div>
                </div>

                <div style="margin-top: 20px; text-align: center;" class="no-print">
                    <button class="btn btn-success" onclick="saveBill()">💾 Save Bill</button>
                    <button class="btn btn-primary" onclick="printBill()">🖨️ Print Bill</button>
                    <button class="btn btn-secondary" onclick="cancelBill()">✖ Cancel</button>
                </div>
            </div>
        </div>

        <!-- HISTORY PAGE -->
        <div id="historyPage" class="page">
            <div class="page-header">
                <h2>📜 Bill History</h2>
                <div class="page-actions">
                    <button class="btn btn-secondary" onclick="showPage('billsPage')">← Back to Bills</button>
                </div>
            </div>

            <div class="history-container">
                <div class="search-box">
                    <input type="text" id="searchHistory" placeholder="🔍 Search by Customer Name, Bill Number or Date" onkeyup="searchHistory()">
                </div>

                <div class="table-container">
                    <table>
                        <thead>
                            <tr>
                                <th>Bill No</th>
                                <th>Date</th>
                                <th>Customer</th>
                                <th>Total</th>
                                <th>Actions</th>
                            </tr>
                        </thead>
                        <tbody id="historyTableBody">
                            <tr><td colspan="5" style="text-align:center; padding: 30px;">No bills found</td></tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <!-- TOAST -->
    <div id="toast" class="toast"></div>

    <script>
        // Data
        let products = JSON.parse(localStorage.getItem('billbok_products')) || [];
        let bills = JSON.parse(localStorage.getItem('billbok_bills')) || [];
        let billCounter = parseInt(localStorage.getItem('billbok_counter')) || 1;
        let shopInfo = JSON.parse(localStorage.getItem('billbok_shop')) || {};

        // Initialize
        window.onload = function() {
            updateDashboard();
            loadShopInfo();
        };

        // Navigation
        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');

            if (pageId === 'productsPage') renderProducts();
            if (pageId === 'billsPage') {
                document.getElementById('billListSection').style.display = 'block';
                document.getElementById('invoiceSection').style.display = 'none';
                renderBillsList();
            }
            if (pageId === 'historyPage') renderHistory();
        }

        // Dashboard
        function updateDashboard() {
            document.getElementById('totalProducts').textContent = products.length;
            document.getElementById('totalBills').textContent = bills.length;

            const today = new Date().toDateString();
            const todayBills = bills.filter(b => new Date(b.date).toDateString() === today);
            const todayRev = todayBills.reduce((sum, b) => sum + b.total, 0);
            document.getElementById('todayRevenue').textContent = '₹' + todayRev.toFixed(2);

            const totalRev = bills.reduce((sum, b) => sum + b.total, 0);
            document.getElementById('totalRevenue').textContent = '₹' + totalRev.toFixed(2);
        }

        // Products
        function addProduct() {
            const name = document.getElementById('productName').value.trim();
            const rate = parseFloat(document.getElementById('productRate').value);
            const stock = parseInt(document.getElementById('productStock').value);

            if (!name || isNaN(rate) || isNaN(stock)) {
                showToast('⚠️ Fill all fields', 'warning');
                return;
            }

            products.push({ id: Date.now(), name, rate, stock });
            localStorage.setItem('billbok_products', JSON.stringify(products));

            document.getElementById('productName').value = '';
            document.getElementById('productRate').value = '';
            document.getElementById('productStock').value = '';

            renderProducts();
            updateDashboard();
            showToast('✅ Product Added!', 'success');
        }

        function renderProducts() {
            const tbody = document.getElementById('productsTableBody');
            if (products.length === 0) {
                tbody.innerHTML = '<tr><td colspan="4" style="text-align:center; padding: 30px;">No products added yet</td></tr>';
                return;
            }
            tbody.innerHTML = products.map(p => `
                <tr>
                    <td>${p.name || ''}</td>
                    <td>₹${(p.rate || 0).toFixed(2)}</td>
                    <td>${p.stock || 0}</td>
                    <td><button class="btn btn-danger btn-sm" onclick="deleteProduct(${p.id})">Delete</button></td>
                </tr>
            `).join('');
        }

        function deleteProduct(id) {
            if (!confirm('Delete this product?')) return;
            products = products.filter(p => p.id !== id);
            localStorage.setItem('billbok_products', JSON.stringify(products));
            renderProducts();
            updateDashboard();
            showToast('✅ Product Deleted', 'success');
        }

        // Shop Info
        function loadShopInfo() {
            if (shopInfo.name) {
                document.getElementById('shopName').value = shopInfo.name;
                document.getElementById('shopMobile').value = shopInfo.mobile || '';
                document.getElementById('shopGST').value = shopInfo.gst || '';
                document.getElementById('shopAddress').value = shopInfo.address || '';
            }
        }

        function saveShopInfo() {
            shopInfo = {
                name: document.getElementById('shopName').value.trim(),
                mobile: document.getElementById('shopMobile').value.trim(),
                gst: document.getElementById('shopGST').value.trim(),
                address: document.getElementById('shopAddress').value.trim()
            };
            localStorage.setItem('billbok_shop', JSON.stringify(shopInfo));
        }

        // Bills
        function renderBillsList() {
            const container = document.getElementById('billsList');
            if (bills.length === 0) {
                container.innerHTML = '<p style="text-align:center; padding: 30px; color: #999;">No bills created yet. Click "+ New Bill" to create one.</p>';
                return;
            }
            const recent = bills.slice(-10).reverse();
            
            container.innerHTML = recent.map(bill => `
                <div class="bill-card" onclick="viewBill('${bill.billNo}')">
                    <h4>📄 ${bill.billNo || ''}</h4>
                    <p>📅 Date: ${new Date(bill.date).toLocaleDateString()}</p>
                    <p>👤 Customer: ${bill.customer?.name || 'N/A'}</p>
                    <p>💰 Total: ₹${(bill.total || 0).toFixed(2)}</p>
                </div>
            `).join('');
        }

        function createNewBill() {
            document.getElementById('billListSection').style.display = 'none';
            document.getElementById('invoiceSection').style.display = 'block';
            
            // Reset form
            document.getElementById('billNumber').value = 'BILL-' + String(billCounter).padStart(4, '0');
            document.getElementById('billDate').valueAsDate = new Date();
            document.getElementById('customerName').value = '';
            document.getElementById('customerMobile').value = '';
            document.getElementById('warrantyDetails').value = '';
            document.getElementById('discountPercent').value = '0';
            document.getElementById('billTableBody').innerHTML = '';
            
            calculateTotal();
            addBillRow();
            loadShopInfo();
        }

        function cancelBill() {
            if (confirm('Cancel this bill?')) {
                document.getElementById('billListSection').style.display = 'block';
                document.getElementById('invoiceSection').style.display = 'none';
            }
        }

        // Bill Items
        function addBillRow() {
            const tbody = document.getElementById('billTableBody');
            const rowNum = tbody.rows.length + 1;
            const rowId = Date.now();

            const row = tbody.insertRow();
            row.innerHTML = `
                <td>${rowNum}</td>
                <td class="autocomplete-box">
                    <input type="text" id="search_${rowId}" placeholder="Search product..." onkeyup="searchProduct(${rowId})" onfocus="searchProduct(${rowId})" style="text-align: left;">
                    <div id="autocomplete_${rowId}" class="autocomplete-list"></div>
                    <input type="hidden" id="productId_${rowId}">
                </td>
                <td><input type="number" id="qty_${rowId}" value="1" min="1" onchange="calculateRow(${rowId})"></td>
                <td><input type="number" id="rate_${rowId}" value="0" readonly></td>
                <td><input type="number" id="amount_${rowId}" value="0" readonly></td>
                <td class="no-print"><button class="btn btn-danger btn-sm" onclick="removeRow(this)">×</button></td>
            `;
        }

        function searchProduct(rowId) {
            const query = document.getElementById('search_' + rowId).value.toLowerCase();
            const list = document.getElementById('autocomplete_' + rowId);

            if (query.length < 1) {
                list.style.display = 'none';
                return;
            }

            const filtered = products.filter(p => p.name.toLowerCase().includes(query));

            if (filtered.length === 0) {
                list.innerHTML = '<div>No products found</div>';
                list.style.display = 'block';
                return;
            }

            list.innerHTML = filtered.map(p => `
                <div onclick="selectProduct(${rowId}, ${p.id})">
                    ${p.name} - ₹${p.rate} (Stock: ${p.stock})
                </div>
            `).join('');
            list.style.display = 'block';
        }

        function selectProduct(rowId, productId) {
            const product = products.find(p => p.id === productId);
            if (!product) return;

            document.getElementById('search_' + rowId).value = product.name || '';
            document.getElementById('productId_' + rowId).value = productId;
            document.getElementById('rate_' + rowId).value = (product.rate || 0).toFixed(2);
            document.getElementById('autocomplete_' + rowId).style.display = 'none';

            calculateRow(rowId);
        }

        function calculateRow(rowId) {
            const productId = document.getElementById('productId_' + rowId).value;
            const qty = parseInt(document.getElementById('qty_' + rowId).value) || 0;
            const rate = parseFloat(document.getElementById('rate_' + rowId).value) || 0;

            if (productId) {
                const product = products.find(p => p.id == productId);
                if (product && qty > product.stock) {
                    showToast('⚠️ Insufficient stock! Available: ' + product.stock, 'warning');
                    document.getElementById('qty_' + rowId).value = product.stock;
                    return;
                }
            }

            const amount = qty * rate;
            document.getElementById('amount_' + rowId).value = amount.toFixed(2);
            calculateTotal();
        }

        function removeRow(btn) {
            const tbody = document.getElementById('billTableBody');
            if (tbody.rows.length === 1) {
                showToast('⚠️ At least one row required', 'warning');
                return;
            }
            btn.closest('tr').remove();
            updateRowNumbers();
            calculateTotal();
        }

        function updateRowNumbers() {
            const tbody = document.getElementById('billTableBody');
            Array.from(tbody.rows).forEach((row, i) => {
                row.cells[0].textContent = i + 1;
            });
        }

        // Calculations
        function calculateTotal() {
            const tbody = document.getElementById('billTableBody');
            let subtotal = 0;

            Array.from(tbody.rows).forEach(row => {
                const amount = parseFloat(row.cells[4].querySelector('input').value) || 0;
                subtotal += amount;
            });

            const discountPercent = parseFloat(document.getElementById('discountPercent').value) || 0;
            const discountAmount = subtotal * discountPercent / 100;
            const grandTotal = subtotal - discountAmount;

            document.getElementById('subtotal').textContent = subtotal.toFixed(2);
            document.getElementById('discountAmount').textContent = discountAmount.toFixed(2);
            document.getElementById('grandTotal').textContent = grandTotal.toFixed(2);
            document.getElementById('amountWords').textContent = numberToWords(grandTotal) + ' Only';
        }

        function numberToWords(num) {
            if (num === 0) return 'Zero Rupees';

            const ones = ['', 'One', 'Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine'];
            const tens = ['', '', 'Twenty', 'Thirty', 'Forty', 'Fifty', 'Sixty', 'Seventy', 'Eighty', 'Ninety'];
            const teens = ['Ten', 'Eleven', 'Twelve', 'Thirteen', 'Fourteen', 'Fifteen', 'Sixteen', 'Seventeen', 'Eighteen', 'Nineteen'];

            function convert(n) {
                if (n === 0) return '';
                if (n < 10) return ones[n];
                if (n >= 10 && n < 20) return teens[n - 10];
                if (n < 100) return tens[Math.floor(n / 10)] + (n % 10 ? ' ' + ones[n % 10] : '');
                return ones[Math.floor(n / 100)] + ' Hundred' + (n % 100 ? ' ' + convert(n % 100) : '');
            }

            const crore = Math.floor(num / 10000000);
            const lakh = Math.floor((num % 10000000) / 100000);
            const thousand = Math.floor((num % 100000) / 1000);
            const remainder = Math.floor(num % 1000);

            let words = '';
            if (crore > 0) words += convert(crore) + ' Crore ';
            if (lakh > 0) words += convert(lakh) + ' Lakh ';
            if (thousand > 0) words += convert(thousand) + ' Thousand ';
            if (remainder > 0) words += convert(remainder);

            return words.trim() + ' Rupees';
        }

        // Save Bill
        function saveBill() {
            saveShopInfo();

            if (!shopInfo.name) {
                showToast('⚠️ Enter Shop Name first', 'warning');
                return;
            }

            const tbody = document.getElementById('billTableBody');
            const items = [];
            let canSave = true;

            Array.from(tbody.rows).forEach(row => {
                const productId = row.cells[1].querySelector('input[type="hidden"]').value;
                const qty = parseInt(row.cells[2].querySelector('input').value) || 0;
                const rate = parseFloat(row.cells[3].querySelector('input').value) || 0;
                const amount = parseFloat(row.cells[4].querySelector('input').value) || 0;

                if (productId && qty > 0) {
                    const product = products.find(p => p.id == productId);
                    if (product) {
                        if (product.stock < qty) {
                            showToast('⚠️ Insufficient stock for ' + product.name, 'warning');
                            canSave = false;
                            return;
                        }
                        items.push({ productId, name: product.name, qty, rate, amount });
                    }
                }
            });

            if (!canSave || items.length === 0) {
                showToast('⚠️ Add valid items', 'warning');
                return;
            }

            const grandTotal = parseFloat(document.getElementById('grandTotal').textContent);

            const bill = {
                billNo: document.getElementById('billNumber').value,
                date: document.getElementById('billDate').value,
                customer: {
                    name: document.getElementById('customerName').value.trim() || 'Walk-in',
                    mobile: document.getElementById('customerMobile').value.trim()
                },
                warranty: document.getElementById('warrantyDetails').value.trim(),
                items: items,
                subtotal: parseFloat(document.getElementById('subtotal').textContent),
                discount: parseFloat(document.getElementById('discountAmount').textContent),
                total: grandTotal
            };

            // Reduce stock
            items.forEach(item => {
                const product = products.find(p => p.id == item.productId);
                if (product) product.stock -= item.qty;
            });

            bills.push(bill);
            billCounter++;

            localStorage.setItem('billbok_products', JSON.stringify(products));
            localStorage.setItem('billbok_bills', JSON.stringify(bills));
            localStorage.setItem('billbok_counter', billCounter);

            updateDashboard();
            showToast('✅ Bill Saved Successfully!', 'success');

            setTimeout(() => {
                document.getElementById('billListSection').style.display = 'block';
                document.getElementById('invoiceSection').style.display = 'none';
                renderBillsList();
            }, 1500);
        }

        // Print
        function printBill() {
            saveShopInfo();
            
            document.getElementById('displayShopName').textContent = shopInfo.name || 'SHOP NAME';
            document.getElementById('displayShopMobile').textContent = shopInfo.mobile ? 'Mobile: ' + shopInfo.mobile : '';
            document.getElementById('displayShopGST').textContent = shopInfo.gst ? 'GST: ' + shopInfo.gst : '';
            document.getElementById('displayShopAddress').textContent = shopInfo.address || '';

            window.print();
        }

        // History
        function renderHistory() {
            const tbody = document.getElementById('historyTableBody');
            if (bills.length === 0) {
                tbody.innerHTML = '<tr><td colspan="5" style="text-align:center; padding: 30px;">No bills found</td></tr>';
                return;
            }
            const sorted = [...bills].reverse();

            tbody.innerHTML = sorted.map(bill => `
                <tr>
                    <td>${bill.billNo || ''}</td>
                    <td>${new Date(bill.date).toLocaleDateString()}</td>
                    <td>${bill.customer?.name || 'N/A'}${bill.customer?.mobile ? '<br><small>' + bill.customer.mobile + '</small>' : ''}</td>
                    <td>₹${(bill.total || 0).toFixed(2)}</td>
                    <td><button class="btn btn-danger btn-sm" onclick="deleteBill('${bill.billNo}')">Delete</button></td>
                </tr>
            `).join('');
        }

        function searchHistory() {
            const query = document.getElementById('searchHistory').value.toLowerCase();
            const tbody = document.getElementById('historyTableBody');

            const filtered = bills.filter(b =>
                (b.customer?.name || '').toLowerCase().includes(query) ||
                (b.billNo || '').toLowerCase().includes(query) ||
                (b.date || '').includes(query)
            );

            if (filtered.length === 0) {
                tbody.innerHTML = '<tr><td colspan="5" style="text-align:center; padding: 30px;">No bills found</td></tr>';
                return;
            }

            tbody.innerHTML = filtered.reverse().map(bill => `
                <tr>
                    <td>${bill.billNo || ''}</td>
                    <td>${new Date(bill.date).toLocaleDateString()}</td>
                    <td>${bill.customer?.name || 'N/A'}${bill.customer?.mobile ? '<br><small>' + bill.customer.mobile + '</small>' : ''}</td>
                    <td>₹${(bill.total || 0).toFixed(2)}</td>
                    <td><button class="btn btn-danger btn-sm" onclick="deleteBill('${bill.billNo}')">Delete</button></td>
                </tr>
            `).join('');
        }

        function deleteBill(billNo) {
            if (!confirm('Delete this bill?')) return;
            bills = bills.filter(b => b.billNo !== billNo);
            localStorage.setItem('billbok_bills', JSON.stringify(bills));
            renderHistory();
            updateDashboard();
            showToast('✅ Bill Deleted', 'success');
        }

        function viewBill(billNo) {
            showToast('ℹ️ Bill view feature - Coming soon!', 'info');
        }

        // Toast
        function showToast(message, type = 'success') {
            const toast = document.getElementById('toast');
            toast.textContent = message;
            toast.style.background = type === 'success' ? '#28a745' : type === 'warning' ? '#ffc107' : type === 'info' ? '#17a2b8' : '#dc3545';
            toast.style.color = type === 'warning' ? '#000' : 'white';
            toast.classList.add('show');

            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }

        // Close autocomplete on outside click
        document.addEventListener('click', function(e) {
            if (!e.target.closest('.autocomplete-box')) {
                document.querySelectorAll('.autocomplete-list').forEach(list => {
                    list.style.display = 'none';
                });
            }
        });
    </script>
</body>
</html>
