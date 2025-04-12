<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Percent Off Calculator</title>
    <style>
        /* Modern CSS Reset with Custom Variables */
        :root {
            --primary-teal: #26a69a;
            --secondary-orange: #ff7043;
            --accent-blue: #42a5f5;
            --light-bg: #f5f5f5;
            --dark-text: #263238;
            --light-text: #eceff1;
            --shadow-sm: 0 2px 8px rgba(0,0,0,0.1);
            --shadow-md: 0 4px 12px rgba(0,0,0,0.15);
            --transition-fast: all 0.2s ease;
            --border-radius: 8px;
            --success-green: #66bb6a;
            --warning-amber: #ffa726;
            --error-red: #ef5350;
        }
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', sans-serif;
        }
        body {
            background-color: var(--light-bg);
            color: var(--dark-text);
            line-height: 1.6;
        }
        .poc-container-main {
            max-width: 800px;
            margin: 0 auto;
            padding: 0.8rem;
            background: white;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow-sm);
        }
        .poc-header-section {
            text-align: center;
            margin-bottom: 1.5rem;
            padding: 0.8rem;
            background: linear-gradient(135deg, var(--primary-teal), var(--accent-blue));
            color: white;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow-md);
        }
        .poc-title-heading {
            font-size: 2rem;
            margin-bottom: 0.5rem;
            text-shadow: 1px 1px 3px rgba(0,0,0,0.2);
        }
        .poc-subtitle-text {
            font-size: 1rem;
            opacity: 0.9;
        }
        .poc-input-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1rem;
            margin-bottom: 1.5rem;
        }
        .poc-input-group {
            position: relative;
        }
        .poc-input-label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
            color: var(--primary-teal);
        }
        .poc-input-field {
            width: 100%;
            padding: 0.8rem;
            border: 2px solid #e0e0e0;
            border-radius: var(--border-radius);
            font-size: 1rem;
            transition: var(--transition-fast);
            background-color: #f8f9fa;
        }
        .poc-input-field:focus {
            outline: none;
            border-color: var(--primary-teal);
            background-color: white;
            box-shadow: 0 0 0 3px rgba(38, 166, 154, 0.2);
        }
        .poc-unit-indicator {
            position: absolute;
            right: 10px;
            top: 38px;
            color: #7f8c8d;
            font-size: 0.9rem;
        }
        .poc-result-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
            margin-bottom: 2rem;
        }
        .poc-result-card {
            padding: 1.2rem;
            border-radius: var(--border-radius);
            text-align: center;
            background: white;
            box-shadow: var(--shadow-sm);
            border-top: 4px solid var(--primary-teal);
        }
        .poc-result-value {
            font-size: 2rem;
            font-weight: 700;
            margin: 0.5rem 0;
            color: var(--secondary-orange);
        }
        .poc-result-label {
            font-size: 1rem;
            color: var(--dark-text);
            opacity: 0.8;
        }
        .poc-savings-container {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            margin-bottom: 2rem;
        }
        .poc-savings-card {
            flex: 1 1 200px;
            padding: 1rem;
            border-radius: var(--border-radius);
            background: white;
            box-shadow: var(--shadow-sm);
            border-left: 4px solid var(--secondary-orange);
        }
        .poc-savings-title {
            font-weight: 600;
            color: var(--accent-blue);
            margin-bottom: 0.5rem;
        }
        .poc-visual-container {
            height: 120px;
            margin-bottom: 2rem;
            position: relative;
            display: flex;
            align-items: flex-end;
            justify-content: space-between;
        }
        .poc-visual-bar {
            flex: 1;
            max-width: 45%;
            background: linear-gradient(to top, var(--primary-teal), var(--accent-blue));
            border-radius: var(--border-radius) var(--border-radius) 0 0;
            transition: height 0.5s ease;
            position: relative;
            box-shadow: var(--shadow-sm);
        }
        .poc-visual-label {
            position: absolute;
            bottom: -30px;
            width: 100%;
            text-align: center;
            font-size: 0.9rem;
        }
        .poc-visual-percent {
            position: absolute;
            top: -25px;
            width: 100%;
            text-align: center;
            font-weight: 600;
            color: var(--primary-teal);
        }
        .poc-table-responsive {
            width: 100%;
            overflow-x: auto;
            margin-bottom: 2rem;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow-sm);
        }
        .poc-data-table {
            width: 100%;
            border-collapse: collapse;
            min-width: 500px;
        }
        .poc-data-table th, .poc-data-table td {
            padding: 0.8rem;
            text-align: left;
            border-bottom: 1px solid #e0e0e0;
        }
        .poc-data-table th {
            background-color: var(--primary-teal);
            color: white;
            font-weight: 600;
        }
        .poc-data-table tr:nth-child(even) {
            background-color: #f8f9fa;
        }
        .poc-data-table tr:hover {
            background-color: #e0f2f1;
        }
        .poc-info-section {
            background: #f0f4f8;
            padding: 1.2rem;
            border-radius: var(--border-radius);
            margin-top: 1.5rem;
        }
        .poc-info-heading {
            color: var(--primary-teal);
            margin-bottom: 0.8rem;
        }
        @media (max-width: 768px) {
            .poc-result-container, .poc-savings-container {
                grid-template-columns: 1fr;
            }
            .poc-input-grid {
                grid-template-columns: 1fr;
            }
            .poc-title-heading {
                font-size: 1.5rem;
            }
            .poc-visual-container {
                height: 150px;
            }
        }
    </style>
</head>
<body>
    <div class="poc-container-main">
        <div class="poc-header-section">
            <h1 class="poc-title-heading">Percent Off Calculator</h1>
            <p class="poc-subtitle-text">Calculate discounts and savings instantly</p>
        </div>
        <div class="poc-input-grid">
            <div class="poc-input-group">
                <label for="originalPrice" class="poc-input-label">Original Price</label>
                <input type="number" id="originalPrice" class="poc-input-field" placeholder="Enter original price">
                <span class="poc-unit-indicator">$</span>
            </div>
            <div class="poc-input-group">
                <label for="discountPercent" class="poc-input-label">Discount Percent</label>
                <input type="number" id="discountPercent" class="poc-input-field" placeholder="Enter discount percent">
                <span class="poc-unit-indicator">%</span>
            </div>
            <div class="poc-input-group">
                <label for="finalPrice" class="poc-input-label">Final Price (optional)</label>
                <input type="number" id="finalPrice" class="poc-input-field" placeholder="Enter final price">
                <span class="poc-unit-indicator">$</span>
            </div>
        </div>
        <div class="poc-result-container">
            <div class="poc-result-card">
                <div class="poc-result-label">Discounted Price</div>
                <div id="discountedPrice" class="poc-result-value">--</div>
                <div class="poc-result-label">Price after discount</div>
            </div>
            <div class="poc-result-card">
                <div class="poc-result-label">You Save</div>
                <div id="savingsAmount" class="poc-result-value">--</div>
                <div class="poc-result-label">Total savings</div>
            </div>
            <div class="poc-result-card">
                <div class="poc-result-label">Effective Discount</div>
                <div id="effectiveDiscount" class="poc-result-value">--</div>
                <div class="poc-result-label">Calculated from prices</div>
            </div>
        </div>
        <div class="poc-visual-container">
            <div class="poc-visual-bar" id="originalBar" style="height: 100%;">
                <div class="poc-visual-percent">100%</div>
                <div class="poc-visual-label">Original Price</div>
            </div>
            <div class="poc-visual-bar" id="discountedBar" style="height: 100%;">
                <div class="poc-visual-percent">0%</div>
                <div class="poc-visual-label">Discounted Price</div>
            </div>
        </div>
        <div class="poc-savings-container">
            <div class="poc-savings-card">
                <div class="poc-savings-title">Monthly Savings</div>
                <div id="monthlySavings">--</div>
                <div class="poc-result-label">If purchased every month</div>
            </div>
            <div class="poc-savings-card">
                <div class="poc-savings-title">Yearly Savings</div>
                <div id="yearlySavings">--</div>
                <div class="poc-result-label">If purchased every year</div>
            </div>
            <div class="poc-savings-card">
                <div class="poc-savings-title">Price per Unit</div>
                <div id="pricePerUnit">--</div>
                <div class="poc-result-label">If buying multiple items</div>
            </div>
        </div>
        <div class="poc-table-responsive">
            <table class="poc-data-table">
                <thead>
                    <tr>
                        <th>Discount %</th>
                        <th>You Save</th>
                        <th>Final Price</th>
                        <th>Equivalent To</th>
                    </tr>
                </thead>
                <tbody id="discountTableBody">
                    <!-- Discount table rows will be added here dynamically -->
                </tbody>
            </table>
        </div>
        <div class="poc-info-section">
            <h3 class="poc-info-heading">About Discount Calculations</h3>
            <p>This calculator helps you determine the final price after discount, the amount you'll save, and the effective discount percentage. To calculate the discounted price, multiply the original price by (100% - discount percentage).</p>
            <p>If you enter the final price instead of the discount percentage, we'll calculate the effective discount for you. The visual comparison shows the relative difference between the original and discounted prices.</p>
        </div>
    </div>
    <script>
        // DOM Elements
        const originalPriceInput = document.getElementById('originalPrice');
        const discountPercentInput = document.getElementById('discountPercent');
        const finalPriceInput = document.getElementById('finalPrice');
        // Result elements
        const discountedPriceElement = document.getElementById('discountedPrice');
        const savingsAmountElement = document.getElementById('savingsAmount');
        const effectiveDiscountElement = document.getElementById('effectiveDiscount');
        // Visual elements
        const originalBar = document.getElementById('originalBar');
        const discountedBar = document.getElementById('discountedBar');
        // Savings elements
        const monthlySavingsElement = document.getElementById('monthlySavings');
        const yearlySavingsElement = document.getElementById('yearlySavings');
        const pricePerUnitElement = document.getElementById('pricePerUnit');
        // Table element
        const discountTableBody = document.getElementById('discountTableBody');
        // Event listeners for auto-calculation
        [originalPriceInput, discountPercentInput, finalPriceInput].forEach(input => {
            input.addEventListener('input', calculateDiscount);
        });
        // Initial calculation
        calculateDiscount();
        // Main calculation function
        function calculateDiscount() {
            const originalPrice = parseFloat(originalPriceInput.value);
            const discountPercent = parseFloat(discountPercentInput.value);
            const finalPrice = parseFloat(finalPriceInput.value);
            if (originalPrice) {
                // Calculate based on what inputs are provided
                if (!isNaN(discountPercent) {
                    // Calculate from original price and discount percent
                    const discountDecimal = discountPercent / 100;
                    const savings = originalPrice * discountDecimal;
                    const discountedPrice = originalPrice - savings;
                    // Display results
                    discountedPriceElement.textContent = formatCurrency(discountedPrice);
                    savingsAmountElement.textContent = formatCurrency(savings);
                    effectiveDiscountElement.textContent = `${discountPercent}%`;
                    // Update visual comparison
                    updateVisualComparison(originalPrice, discountedPrice);
                    // Calculate additional savings
                    calculateAdditionalSavings(savings);
                    // Generate discount table
                    generateDiscountTable(originalPrice);
                } else if (!isNaN(finalPrice) {
                    // Calculate discount percent from final price
                    const savings = originalPrice - finalPrice;
                    const discountPercentCalculated = (savings / originalPrice) * 100;
                    // Display results
                    discountedPriceElement.textContent = formatCurrency(finalPrice);
                    savingsAmountElement.textContent = formatCurrency(savings);
                    effectiveDiscountElement.textContent = `${discountPercentCalculated.toFixed(2)}%`;
                    // Update visual comparison
                    updateVisualComparison(originalPrice, finalPrice);
                    // Calculate additional savings
                    calculateAdditionalSavings(savings);
                    // Generate discount table
                    generateDiscountTable(originalPrice);
                } else {
                    // Only original price entered
                    discountedPriceElement.textContent = '--';
                    savingsAmountElement.textContent = '--';
                    effectiveDiscountElement.textContent = '--';
                    // Reset visual comparison
                    originalBar.style.height = '100%';
                    discountedBar.style.height = '100%';
                    originalBar.querySelector('.poc-visual-percent').textContent = '100%';
                    discountedBar.querySelector('.poc-visual-percent').textContent = '0%';
                    // Generate discount table
                    generateDiscountTable(originalPrice);
                }
            } else {
                // No original price entered
                discountedPriceElement.textContent = '--';
                savingsAmountElement.textContent = '--';
                effectiveDiscountElement.textContent = '--';
                // Reset visual comparison
                originalBar.style.height = '100%';
                discountedBar.style.height = '100%';
                originalBar.querySelector('.poc-visual-percent').textContent = '100%';
                discountedBar.querySelector('.poc-visual-percent').textContent = '0%';
                // Clear additional savings
                monthlySavingsElement.textContent = '--';
                yearlySavingsElement.textContent = '--';
                pricePerUnitElement.textContent = '--';
                // Clear discount table
                discountTableBody.innerHTML = '';
            }
        }
        // Update the visual comparison bars
        function updateVisualComparison(originalPrice, discountedPrice) {
            const discountPercent = ((originalPrice - discountedPrice) / originalPrice) * 100;
            const discountedPercent = 100 - discountPercent;
            originalBar.style.height = '100%';
            discountedBar.style.height = `${discountedPercent}%`;
            originalBar.querySelector('.poc-visual-percent').textContent = '100%';
            discountedBar.querySelector('.poc-visual-percent').textContent = `${discountedPercent.toFixed(1)}%`;
        }
        // Calculate additional savings scenarios
        function calculateAdditionalSavings(savings) {
            if (isNaN(savings)) {
                monthlySavingsElement.textContent = '--';
                yearlySavingsElement.textContent = '--';
                pricePerUnitElement.textContent = '--';
                return;
            }
            // Monthly and yearly savings
            monthlySavingsElement.textContent = formatCurrency(savings * 1);
            yearlySavingsElement.textContent = formatCurrency(savings * 12);
            // Price per unit (assuming 10 units)
            const originalPrice = parseFloat(originalPriceInput.value);
            if (!isNaN(originalPrice)) {
                const discountedPrice = originalPrice - savings;
                pricePerUnitElement.textContent = `10 for ${formatCurrency(discountedPrice * 10)} (${formatCurrency(discountedPrice)} each)`;
            } else {
                pricePerUnitElement.textContent = '--';
            }
        }
        // Generate the discount table
        function generateDiscountTable(originalPrice) {
            discountTableBody.innerHTML = '';
            if (isNaN(originalPrice) || originalPrice <= 0) return;
            const discountPercentages = [5, 10, 15, 20, 25, 30, 40, 50, 60, 75];
            discountPercentages.forEach(percent => {
                const savings = originalPrice * (percent / 100);
                const finalPrice = originalPrice - savings;
                const row = document.createElement('tr');
                const percentCell = document.createElement('td');
                percentCell.textContent = `${percent}%`;
                row.appendChild(percentCell);
                const savingsCell = document.createElement('td');
                savingsCell.textContent = formatCurrency(savings);
                row.appendChild(savingsCell);
                const priceCell = document.createElement('td');
                priceCell.textContent = formatCurrency(finalPrice);
                row.appendChild(priceCell);
                const equivalentCell = document.createElement('td');
                equivalentCell.textContent = getEquivalentDescription(percent);
                row.appendChild(equivalentCell);
                discountTableBody.appendChild(row);
            });
        }
        // Helper function to format currency
        function formatCurrency(amount) {
            if (isNaN(amount)) return '--';
            return new Intl.NumberFormat('en-US', {
                style: 'currency',
                currency: 'USD',
                minimumFractionDigits: 2,
                maximumFractionDigits: 2
            }).format(amount);
        }
        // Helper function to get equivalent description
        function getEquivalentDescription(percent) {
            if (percent === 5) return "Typical sale";
            if (percent === 10) return "Common discount";
            if (percent === 15) return "Student discount";
            if (percent === 20) return "Seasonal sale";
            if (percent === 25) return "Quarter off";
            if (percent === 30) return "Clearance price";
            if (percent === 40) return "Big discount";
            if (percent === 50) return "Half price";
            if (percent === 60) return "Major sale";
            if (percent === 75) return "Huge discount";
            return "";
        }
    </script>
</body>
</html>
