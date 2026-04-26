<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🏗️ Construction Cost Calculator - Bangladesh</title>
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
            max-width: 900px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #2c3e50, #3498db);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.2em;
            margin-bottom: 10px;
        }

        .input-section {
            padding: 40px;
            background: #f8f9fa;
            border-bottom: 1px solid #eee;
        }

        .input-group {
            display: flex;
            gap: 20px;
            align-items: center;
            justify-content: center;
            flex-wrap: wrap;
        }

        .input-field {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
        }

        input[type="number"] {
            width: 200px;
            padding: 15px 20px;
            font-size: 1.5em;
            border: 3px solid #ddd;
            border-radius: 12px;
            text-align: center;
            transition: all 0.3s;
        }

        input[type="number"]:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 20px rgba(52, 152, 219, 0.3);
        }

        .calculate-btn {
            background: linear-gradient(135deg, #27ae60, #2ecc71);
            color: white;
            border: none;
            padding: 18px 40px;
            font-size: 1.3em;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: bold;
        }

        .calculate-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(39, 174, 96, 0.4);
        }

        .results {
            padding: 40px;
            display: none;
        }

        .results.show {
            display: block;
            animation: slideIn 0.5s ease-out;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .summary-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            text-align: center;
        }

        .summary-card h2 {
            font-size: 1.8em;
            margin-bottom: 15px;
        }

        .total-cost {
            font-size: 3em;
            font-weight: bold;
            background: rgba(255,255,255,0.2);
            padding: 20px;
            border-radius: 12px;
            margin: 15px 0;
        }

        .cost-per-sqft {
            font-size: 1.5em;
            margin-top: 10px;
        }

        .breakdown {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .material-group, .labor-group {
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .group-title {
            font-size: 1.4em;
            font-weight: bold;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 3px solid #3498db;
            color: #2c3e50;
        }

        .item {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid #eee;
            font-size: 1.1em;
        }

        .item:last-child {
            border-bottom: none;
            font-weight: bold;
            background: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            color: #27ae60;
            font-size: 1.2em;
        }

        .timeline {
            background: linear-gradient(135deg, #f39c12, #e67e22);
            color: white;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            margin-top: 25px;
        }

        .quality-indicator {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin-top: 20px;
            flex-wrap: wrap;
        }

        .quality-badge {
            padding: 10px 20px;
            border-radius: 25px;
            font-weight: bold;
            font-size: 0.9em;
        }

        .normal { background: #f39c12; color: white; }
        .good { background: #27ae60; color: white; }
        .premium { background: #e74c3c; color: white; }

        @media (max-width: 768px) {
            .input-group {
                flex-direction: column;
            }
            
            input[type="number"] {
                width: 250px;
            }
            
            .total-cost {
                font-size: 2.2em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏗️ Construction Cost Calculator</h1>
            <p>বাংলাদেশের স্ট্যান্ডার্ড RCC বিল্ডিং - Complete Breakdown</p>
        </div>

        <div class="input-section">
            <div class="input-group">
                <div class="input-field">
                    <label for="area">📏 Building Area</label>
                    <input type="number" id="area" placeholder="1000" min="100" step="50">
                    <span>sq ft</span>
                </div>
                <button class="calculate-btn" onclick="calculateCost()">💰 Calculate Cost</button>
            </div>
        </div>

        <div class="results" id="results">
            <div class="summary-card">
                <h2 id="summaryTitle"></h2>
                <div class="total-cost" id="totalCost">0 BDT</div>
                <div class="cost-per-sqft" id="costPerSqft">0 BDT/sqft</div>
                <div class="quality-indicator" id="qualityIndicator"></div>
            </div>

            <div class="timeline">
                <h3 id="timeline">⏱️ Construction Time: 0 days</h3>
            </div>

            <div class="breakdown">
                <div class="material-group">
                    <div class="group-title">🔨 Material Breakdown</div>
                    <div id="materialsList"></div>
                    <div id="totalMaterials"></div>
                </div>

                <div class="labor-group">
                    <div class="group-title">👷 Labor Breakdown</div>
                    <div id="laborList"></div>
                    <div id="totalLabor"></div>
                </div>
            </div>

            <div class="summary-card">
                <h3>📈 Final Cost Breakdown</h3>
                <div id="finalBreakdown"></div>
            </div>
        </div>
    </div>

    <script>
        // Material Rates (BDT per unit)
        const materials = {
            bricks: { qty: 5, rate: 12, name: 'Bricks' },
            sand: { qty: 0.02, rate: 1500, name: 'Sand (cum)' },
            cement: { qty: 0.05, rate: 500, name: 'Cement (bag)' },
            iron: { qty: 2, rate: 90, name: 'Iron Rod (kg)' },
            stone: { qty: 0.015, rate: 2000, name: 'Stone Chips (cum)' },
            wood: { qty: 0.005, rate: 8000, name: 'Wood (cum)' },
            tiles: { qty: 0.8, rate: 60, name: 'Ceramic Tiles (sqft)' },
            paint: { qty: 0.02, rate: 200, name: 'Paint (L)' },
            electrical: { qty: 0.5, rate: 25, name: 'Electrical Wiring (m)' },
            plumbing: { qty: 0.1, rate: 50, name: 'Plumbing Pipe (m)' },
            glass: { qty: 0.1, rate: 250, name: 'Glass (sqft)' },
            sanitary: { qty: 0.02, rate: 5000, name: 'Sanitary Wares (set)' }
        };

        // Labor Rates (BDT per sqft)
        const labor = {
            mason: { rate: 400, name: 'Mason' },
            barbender: { rate: 210, name: 'Bar Bender' },
            carpenter: { rate: 150, name: 'Carpenter' },
            electrician: { rate: 105, name: 'Electrician' },
            plumber: { rate: 65, name: 'Plumber' },
            painter: { rate: 120, name: 'Painter' },
            helper: { rate: 150, name: 'Helper' }
        };

        function calculateCost() {
            const area = parseFloat(document.getElementById('area').value);
            if (!area || area < 100) {
                alert('Please enter valid area (minimum 100 sq ft)');
                return;
            }

            // Calculate Materials
            let totalMaterials = 0;
            let materialsHtml = '';
            for (let key in materials) {
                const item = materials[key];
                const qty = (item.qty * area).toFixed(1);
                const cost = item.qty * area * item.rate;
                totalMaterials += cost;
                materialsHtml += `
                    <div class="item">
                        <span>${item.name}: ${qty}</span>
                        <span>${formatNumber(cost)} BDT</span>
                    </div>
                `;
            }

            // Calculate Labor
            let totalLabor = 0;
            let laborHtml = '';
            for (let key in labor) {
                const item = labor[key];
                const cost = item.rate * area;
                totalLabor += cost;
                laborHtml += `
                    <div class="item">
                        <span>${item.name}</span>
                        <span>${formatNumber(cost)} BDT</span>
                    </div>
                `;
            }

            // Base Cost
            const baseCost = totalMaterials + totalLabor;

            // Additional Costs
            const architectFee = baseCost * 0.05;
            const govtFee = baseCost * 0.02;
            const contractorProfit = baseCost * 0.10;
            const contingency = baseCost * 0.08;

            // Grand Total
            const grandTotal = baseCost + architectFee + govtFee + contractorProfit + contingency;

            // Timeline
            const days = Math.ceil(area / 50);
            
            // Cost per sqft & Quality
            const costPerSqft = Math.round(grandTotal / area);
            let quality = 'Normal';
            let qualityClass = 'normal';
            if (costPerSqft > 2500) {
                quality = 'Premium';
                qualityClass = 'premium';
            } else if (costPerSqft > 1800) {
                quality = 'Good';
                qualityClass = 'good';
            }

            // Update DOM
            document.getElementById('materialsList').innerHTML = materialsHtml;
            document.getElementById('totalMaterials').innerHTML = `
                <div class="item">
                    <span>💰 Total Materials</span>
                    <span>${formatNumber(totalMaterials)} BDT</span>
                </div>
            `;

            document.getElementById('laborList').innerHTML = laborHtml;
            document.getElementById('totalLabor').innerHTML = `
                <div class="item">
                    <span>💰 Total Labor</span>
                    <span>${formatNumber(totalLabor)} BDT</span>
                </div>
            `;

            document.getElementById('totalCost').textContent = formatNumber(grandTotal) + ' BDT';
            document.getElementById('costPerSqft').textContent = costPerSqft + ' BDT/sqft';
            document.getElementById('summaryTitle').textContent = `🏠 ${area.toLocaleString()} sq ft Building`;
            document.getElementById('timeline').innerHTML = `⏱️ Construction Time: ${days} days (50sqft/day/team)`;
            
            document.getElementById('qualityIndicator').innerHTML = `
                <div class="quality-badge ${qualityClass}">${quality} Quality</div>
                <div class="quality-badge normal">Normal: <1500/sqft</div>
                <div class="quality-badge good">Good: 1500-2500/sqft</div>
                <div class="quality-badge premium">Premium: >2500/sqft</div>
            `;

            document.getElementById('finalBreakdown').innerHTML = `
                <div class="item"><span>🏗️ Base Cost (Materials + Labor)</span><span>${formatNumber(baseCost)} BDT</span></div>
                <div class="item"><span>📐 Architect/Engineer (5%)</span><span>${formatNumber(architectFee)} BDT</span></div>
                <div class="item"><span>🏛️ Govt Approval (2%)</span><span>${formatNumber(govtFee)} BDT</span></div>
                <div class="item"><span>💼 Contractor Profit (10%)</span><span>${formatNumber(contractorProfit)} BDT</span></div>
                <div class="item"><span>🛡️ Contingency (8%)</span><span>${formatNumber(contingency)} BDT</span></div>
                <div class="item" style="font-size:1.3em;color:#e74c3c;background:#ffeaa7;">
                    <span>🎯 GRAND TOTAL</span><span>${formatNumber(grandTotal)} BDT</span>
                </div>
            `;

            document.getElementById('results').classList.add('show');
            document.getElementById('results').scrollIntoView({ behavior: 'smooth' });
        }

        function formatNumber(num) {
            return num.toLocaleString('bn-BD', { maximumFractionDigits: 0 });
        }

        // Enter key support
        document.getElementById('area').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                calculateCost();
            }
        });
    </script>
</body>
</html>
