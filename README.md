<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🏗️ Advanced Construction Cost Calculator - Bangladesh</title>
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
            position: relative;
            overflow: hidden;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        .input-section {
            padding: 40px;
            background: #f8f9fa;
            border-bottom: 1px solid #eee;
        }

        .input-tabs {
            display: flex;
            justify-content: center;
            margin-bottom: 30px;
            background: white;
            border-radius: 50px;
            padding: 5px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .tab-btn {
            padding: 12px 30px;
            border: none;
            background: transparent;
            border-radius: 40px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
            font-size: 1em;
        }

        .tab-btn.active {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.4);
        }

        .input-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            align-items: end;
        }

        .input-field {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
        }

        .input-field.full-width {
            grid-column: 1 / -1;
        }

        select, input[type="number"], input[type="range"] {
            width: 100%;
            padding: 15px;
            font-size: 1.2em;
            border: 3px solid #ddd;
            border-radius: 12px;
            text-align: center;
            transition: all 0.3s;
            background: white;
        }

        input[type="range"] {
            padding: 10px 0;
        }

        select:focus, input[type="number"]:focus, input[type="range"]:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 20px rgba(52, 152, 219, 0.3);
        }

        .range-label {
            display: flex;
            justify-content: space-between;
            font-size: 0.9em;
            color: #666;
            margin-top: -10px;
        }

        .calculate-btn {
            background: linear-gradient(135deg, #27ae60, #2ecc71);
            color: white;
            border: none;
            padding: 20px 50px;
            font-size: 1.4em;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: bold;
            grid-column: 1 / -1;
        }

        .calculate-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 30px rgba(39, 174, 96, 0.4);
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
            padding: 30px;
            border-radius: 20px;
            margin-bottom: 30px;
            text-align: center;
        }

        .total-cost {
            font-size: 3.5em;
            font-weight: bold;
            background: rgba(255,255,255,0.2);
            padding: 25px;
            border-radius: 15px;
            margin: 20px 0;
        }

        .cost-comparison {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .comparison-item {
            background: rgba(255,255,255,0.2);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
        }

        .breakdown {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 25px;
            margin-top: 30px;
        }

        .card {
            background: white;
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            border-top: 5px solid #3498db;
        }

        .group-title {
            font-size: 1.5em;
            font-weight: bold;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 4px solid #3498db;
            color: #2c3e50;
        }

        .item {
            display: flex;
            justify-content: space-between;
            padding: 15px 0;
            border-bottom: 1px solid #eee;
            font-size: 1.1em;
        }

        .item:last-child {
            border-bottom: none;
            font-weight: bold;
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            padding: 20px;
            border-radius: 12px;
            color: #27ae60;
            font-size: 1.3em;
            margin-top: 10px;
        }

        .timeline-section {
            background: linear-gradient(135deg, #f39c12, #e67e22);
            color: white;
            padding: 30px;
            border-radius: 20px;
            text-align: center;
            margin: 30px 0;
        }

        .gantt-chart {
            display: flex;
            gap: 10px;
            justify-content: center;
            flex-wrap: wrap;
            margin-top: 20px;
        }

        .gantt-item {
            background: rgba(255,255,255,0.3);
            padding: 12px 20px;
            border-radius: 25px;
            font-size: 0.9em;
            font-weight: bold;
        }

        .savings-section {
            background: linear-gradient(135deg, #27ae60, #2ecc71);
            color: white;
            padding: 25px;
            border-radius: 20px;
            text-align: center;
            margin: 30px 0;
        }

        .print-btn {
            background: #e74c3c;
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-weight: bold;
            margin-top: 15px;
            transition: all 0.3s;
            font-size: 1.1em;
        }

        .print-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(231, 76, 60, 0.4);
        }

        .quality-badge {
            padding: 12px 25px;
            border-radius: 25px;
            font-weight: bold;
            font-size: 1em;
            margin: 5px;
        }

        .normal { background: #f39c12; color: white; }
        .good { background: #27ae60; color: white; }
        .premium { background: #e74c3c; color: white; }

        @media (max-width: 768px) {
            .input-grid {
                grid-template-columns: 1fr;
            }
            .total-cost {
                font-size: 2.5em;
            }
            .breakdown {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏗️ Advanced Construction Cost Calculator</h1>
            <p>বাংলাদেশের সবচেয়ে নির্ভুল RCC বিল্ডিং কস্ট ক্যালকুলেটর - ২০২৪ Rates</p>
        </div>

        <div class="input-section">
            <div class="input-tabs">
                <button class="tab-btn active" onclick="switchTab('basic')">Basic</button>
                <button class="tab-btn" onclick="switchTab('advanced')">Advanced</button>
                <button class="tab-btn" onclick="switchTab('custom')">Custom</button>
            </div>

            <div id="basic-tab" class="input-grid">
                <div class="input-field">
                    <label for="area">📏 Building Area</label>
                    <input type="number" id="area" placeholder="1000" min="100" step="50" value="1000">
                    <span>sq ft</span>
                </div>
                <div class="input-field">
                    <label for="floors">🏢 Floors</label>
                    <input type="number" id="floors" min="1" max="10" value="3">
                </div>
                <div class="input-field">
                    <label for="quality">⭐ Quality</label>
                    <select id="quality">
                        <option value="normal">Normal</option>
                        <option value="good" selected>Good</option>
                        <option value="premium">Premium</option>
                    </select>
                </div>
                <button class="calculate-btn" onclick="calculateCost()">🚀 Calculate Complete Cost</button>
            </div>

            <div id="advanced-tab" class="input-grid" style="display: none;">
                <div class="input-field">
                    <label for="areaAdv">📏 Total Area</label>
                    <input type="number" id="areaAdv" placeholder="1000" min="100" step="50" value="1000">
                    <span>sq ft</span>
                </div>
                <div class="input-field">
                    <label for="locationMultiplier">📍 Location</label>
                    <select id="locationMultiplier">
                        <option value="1.0">Dhaka City (100%)</option>
                        <option value="0.85">Dhaka Suburb (85%)</option>
                        <option value="0.75">Divisional City (75%)</option>
                        <option value="0.65">Rural Area (65%)</option>
                    </select>
                </div>
                <div class="input-field">
                    <label for="foundationType">🏗️ Foundation</label>
                    <select id="foundationType">
                        <option value="1.0">Pile Foundation</option>
                        <option value="0.9">Raft Foundation</option>
                        <option value="0.8" selected>Pad Foundation</option>
                    </select>
                </div>
                <div class="input-field">
                    <label for="roofType">🏠 Roof Type</label>
                    <select id="roofType">
                        <option value="1.0">RCC Slab</option>
                        <option value="1.2">Premium RCC</option>
                        <option value="0.9">Tin Shed</option>
                    </select>
                </div>
                <div class="input-field">
                    <label for="inflationRate">📈 Inflation (2024)</label>
                    <input type="range" id="inflationRate" min="0" max="30" value="10">
                    <div class="range-label">
                        <span>0%</span>
                        <span id="inflationValue">10%</span>
                        <span>30%</span>
                    </div>
                </div>
                <button class="calculate-btn" onclick="calculateCost()">💎 Advanced Calculation</button>
            </div>

            <div id="custom-tab" class="input-grid" style="display: none;">
                <div class="input-field">
                    <label for="customArea">📏 Custom Area</label>
                    <input type="number" id="customArea" placeholder="1000" min="100" step="50" value="1000">
                    <span>sq ft</span>
                </div>
                <div class="input-field full-width">
                    <label>💰 Material Multiplier</label>
                    <input type="range" id="materialMultiplier" min="0.5" max="2.0" value="1.0" step="0.1">
                    <div class="range-label">
                        <span>50%</span>
                        <span id="materialValue">100%</span>
                        <span>200%</span>
                    </div>
                </div>
                <div class="input-field full-width">
                    <label>👷 Labor Multiplier</label>
                    <input type="range" id="laborMultiplier" min="0.5" max="2.0" value="1.0" step="0.1">
                    <div class="range-label">
                        <span>50%</span>
                        <span id="laborValue">100%</span>
                        <span>200%</span>
                    </div>
                </div>
                <button class="calculate-btn" onclick="calculateCost()">✨ Custom Calculate</button>
            </div>
        </div>

        <div class="results" id="results">
            <div class="summary-card">
                <h2 id="summaryTitle">Building Cost Summary</h2>
                <div class="total-cost" id="totalCost">0 BDT</div>
                <div id="costPerSqft"></div>
                
                <div class="cost-comparison">
                    <div class="comparison-item">
                        <div style="font-size: 1.5em;">🏆 Market Avg</div>
                        <div id="marketAvg" style="font-size: 1.8em; font-weight: bold;">1800</div>
                        <span>BDT/sqft</span>
                    </div>
                    <div class="comparison-item">
                        <div>💰 Your Cost</div>
                        <div id="yourCost" style="font-size: 1.8em; font-weight: bold; color: #27ae60;">1800</div>
                        <span>BDT/sqft</span>
                    </div>
                    <div class="comparison-item">
                        <div>⭐ Savings</div>
                        <div id="savings" style="font-size: 1.8em; font-weight: bold;">0%</div>
                        <span>vs Market</span>
                    </div>
                </div>

                <div id="qualityIndicator"></div>
                <button class="print-btn" onclick="printReport()">🖨️ Print Report</button>
            </div>

            <div class="timeline-section">
                <h3 id="timelineTitle">⏱️ Construction Timeline</h3>
                <div id="timeline"></div>
                <div class="gantt-chart" id="ganttChart"></div>
            </div>

            <div class="savings-section">
                <h3>💡 Pro Tips to Save Money</h3>
                <ul style="text-align: left; max-width: 600px; margin: 0 auto; font-size: 1.1em;">
                    <li>✅ Buy materials in bulk (5-10% discount)</li>
                    <li>✅ Local labor (15-20% cheaper)</li>
                    <li>✅ Standard sizes (avoid cutting waste)</li>
                    <li>✅ Rainy season construction (labor 20% cheaper)</li>
                </ul>
            </div>

            <div class="breakdown">
                <div class="card">
                    <div class="group-title">🔨 Material Breakdown</div>
                    <div id="materialsList"></div>
                    <div id="totalMaterials"></div>
                </div>

                <div class="card">
                    <div class="group-title">👷 Labor Breakdown</div>
                    <div id="laborList"></div>
                    <div id="totalLabor"></div>
                </div>

                <div class="card">
                    <div class="group-title">📊 Additional Costs</div>
                    <div id="finalBreakdown"></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Material Rates (BDT per unit) - Updated 2024 rates
        const materials = {
            bricks: { qty: 5, rate: 14, name: 'ব্রিক (পিস)' },
            sand: { qty: 0.02, rate: 1800, name: 'বালি (কিউবিক)' },
            cement: { qty: 0.055, rate: 580, name: 'সিমেন্ট (ব্যাগ)' },
            iron: { qty: 2.2, rate: 105, name: 'ইস্পাত (কেজি)' },
            stone: { qty: 0.018, rate: 2400, name: 'পাথরের চিপস (কিউবিক)' },            wood: { qty: 0.006, rate: 9500, name: 'কাঠ (কিউবিক)' },
            tiles: { qty: 0.85, rate: 75, name: 'টাইলস (স্কয়ার ফুট)' },
            paint: { qty: 0.025, rate: 250, name: 'পেইন্ট (লিটার)' },
            electrical: { qty: 0.6, rate: 32, name: 'ইলেকট্রিক্যাল (মিটার)' },
            plumbing: { qty: 0.12, rate: 65, name: 'প্লাম্বিং (মিটার)' },
            glass: { qty: 0.12, rate: 320, name: 'গ্লাস (স্কয়ার ফুট)' },
            sanitary: { qty: 0.025, rate: 6500, name: 'স্যানিটারি (সেট)' }
        };

        // Labor Rates (BDT per sqft)
        const labor = {
            mason: { rate: 450, name: 'মিস্ত্রি' },
            barbender: { rate: 250, name: 'বারবেন্ডার' },
            carpenter: { rate: 180, name: 'কার্পেন্টার' },
            electrician: { rate: 130, name: 'ইলেকট্রিশিয়ান' },
            plumber: { rate: 80, name: 'প্লাম্বার' },
            painter: { rate: 150, name: 'পেইন্টার' },
            helper: { rate: 170, name: 'হেল্পার' }
        };

        // Quality multipliers
        const qualityMultipliers = {
            normal: { material: 0.85, labor: 0.9 },
            good: { material: 1.0, labor: 1.0 },
            premium: { material: 1.25, labor: 1.15 }
        };

        let currentTab = 'basic';

        // Tab switching
        function switchTab(tab) {
            currentTab = tab;
            
            // Hide all tabs
            document.getElementById('basic-tab').style.display = 'none';
            document.getElementById('advanced-tab').style.display = 'none';
            document.getElementById('custom-tab').style.display = 'none';
            
            // Show selected tab
            document.getElementById(tab + '-tab').style.display = 'grid';
            
            // Update active tab button
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
        }

        // Update range values
        document.getElementById('inflationRate').addEventListener('input', function() {
            document.getElementById('inflationValue').textContent = this.value + '%';
        });

        document.getElementById('materialMultiplier').addEventListener('input', function() {
            document.getElementById('materialValue').textContent = (this.value * 100) + '%';
        });

        document.getElementById('laborMultiplier').addEventListener('input', function() {
            document.getElementById('laborValue').textContent = (this.value * 100) + '%';
        });

        function calculateCost() {
            let area;
            if (currentTab === 'basic') {
                area = parseFloat(document.getElementById('area').value);
            } else if (currentTab === 'advanced') {
                area = parseFloat(document.getElementById('areaAdv').value);
            } else {
                area = parseFloat(document.getElementById('customArea').value);
            }

            if (!area || area < 100) {
                alert('দয়া করে সঠিক এরিয়া দিন (ন্যূনতম ১০০ স্কয়ার ফুট)');
                return;
            }

            // Get multipliers
            let materialMultiplier = 1.0;
            let laborMultiplier = 1.0;
            let locationMultiplier = 1.0;
            let foundationMultiplier = 1.0;
            let roofMultiplier = 1.0;
            let inflationMultiplier = 1.0;
            let floors = 3;

            if (currentTab === 'basic') {
                const quality = document.getElementById('quality').value;
                materialMultiplier = qualityMultipliers[quality].material;
                laborMultiplier = qualityMultipliers[quality].labor;
                floors = parseInt(document.getElementById('floors').value);
            } else if (currentTab === 'advanced') {
                locationMultiplier = parseFloat(document.getElementById('locationMultiplier').value);
                foundationMultiplier = parseFloat(document.getElementById('foundationType').value);
                roofMultiplier = parseFloat(document.getElementById('roofType').value);
                inflationMultiplier = 1 + (parseInt(document.getElementById('inflationRate').value) / 100);
            } else {
                materialMultiplier = parseFloat(document.getElementById('materialMultiplier').value);
                laborMultiplier = parseFloat(document.getElementById('laborMultiplier').value);
            }

            // Calculate Materials
            let totalMaterials = 0;
            let materialsHtml = '';
            for (let key in materials) {
                const item = materials[key];
                const qty = (item.qty * area * materialMultiplier * locationMultiplier).toFixed(1);
                const cost = item.qty * area * item.rate * materialMultiplier * locationMultiplier * foundationMultiplier * roofMultiplier * inflationMultiplier;
                totalMaterials += cost;
                materialsHtml += `
                    <div class="item">
                        <span>${item.name}: ${qty}</span>
                        <span>${formatNumber(cost)} ৳</span>
                    </div>
                `;
            }

            // Calculate Labor
            let totalLabor = 0;
            let laborHtml = '';
            for (let key in labor) {
                const item = labor[key];
                const cost = item.rate * area * laborMultiplier * locationMultiplier * inflationMultiplier * floors * 0.3;
                totalLabor += cost;
                laborHtml += `
                    <div class="item">
                        <span>${item.name}</span>
                        <span>${formatNumber(cost)} ৳</span>
                    </div>
                `;
            }

            // Base Cost
            const baseCost = totalMaterials + totalLabor;

            // Additional Costs
            const architectFee = baseCost * 0.05;
            const govtFee = baseCost * 0.025;
            const contractorProfit = baseCost * 0.12;
            const contingency = baseCost * 0.10;
            const utilities = baseCost * 0.03;

            // Grand Total
            const grandTotal = baseCost + architectFee + govtFee + contractorProfit + contingency + utilities;

            // Timeline
            const days = Math.ceil((area * floors * 0.8) / 40);
            const months = Math.ceil(days / 30);
            
            // Cost per sqft & Market comparison
            const costPerSqft = Math.round(grandTotal / area);
            const marketAvg = 2200;
            const savings = Math.max(0, ((marketAvg - costPerSqft) / marketAvg * 100)).toFixed(1);

            let quality = 'Normal';
            if (costPerSqft > 2800) quality = 'Premium';
            else if (costPerSqft > 2000) quality = 'Good';

            // Update DOM
            document.getElementById('materialsList').innerHTML = materialsHtml;
            document.getElementById('totalMaterials').innerHTML = `
                <div class="item">
                    <span>💰 মোট ম্যাটেরিয়াল</span>
                    <span>${formatNumber(totalMaterials)} ৳</span>
                </div>
            `;

            document.getElementById('laborList').innerHTML = laborHtml;
            document.getElementById('totalLabor').innerHTML = `
                <div class="item">
                    <span>💰 মোট লেবার</span>
                    <span>${formatNumber(totalLabor)} ৳</span>
                </div>
            `;

            document.getElementById('totalCost').textContent = formatNumber(grandTotal) + ' ৳';
            document.getElementById('costPerSqft').innerHTML = `<strong>${costPerSqft} ৳/স্কয়ার ফুট</strong>`;
            document.getElementById('summaryTitle').textContent = `🏠 ${area.toLocaleString()} স্কয়ার ফুট বিল্ডিং`;
            
            document.getElementById('marketAvg').textContent = marketAvg;
            document.getElementById('yourCost').textContent = costPerSqft;
            document.getElementById('savings').textContent = savings + '%';
            
            document.getElementById('qualityIndicator').innerHTML = `
                <div class="quality-badge ${quality.toLowerCase()}">${quality} কোয়ালিটি</div>
                <div class="quality-badge normal">Normal: <2000 ৳/স্কয়ার ফুট</div>
                <div class="quality-badge good">Good: 2000-2800 ৳/স্কয়ার ফুট</div>
                <div class="quality-badge premium">Premium: >2800 ৳/স্কয়ার ফুট</div>
            `;

            document.getElementById('timelineTitle').innerHTML = `⏱️ নির্মাণ সময়: ${days} দিন (${months} মাস)`;
            document.getElementById('ganttChart').innerHTML = `
                <div class="gantt-item">🏗️ Foundation: ${Math.ceil(days*0.2)} দিন</div>
                <div class="gantt-item">🔨 Structure: ${Math.ceil(days*0.4)} দিন</div>
                <div class="gantt-item">⚡ Wiring: ${Math.ceil(days*0.15)} দিন</div>
                <div class="gantt-item">🪚 Finishing: ${Math.ceil(days*0.25)} দিন</div>
            `;

            document.getElementById('finalBreakdown').innerHTML = `
                <div class="item"><span>🏗️ মৌলিক খরচ</span><span>${formatNumber(baseCost)} ৳</span></div>
                <div class="item"><span>📐 আর্কিটেক্ট (৫%)</span><span>${formatNumber(architectFee)} ৳</span></div>
                <div class="item"><span>🏛️ সরকারি ফি (২.৫%)</span><span>${formatNumber(govtFee)} ৳</span></div>
                <div class="item"><span>💼 কন্ট্রাক্টর লাভ (১২%)</span><span>${formatNumber(contractorProfit)} ৳</span></div>
                <div class="item"><span>🛡️ জরুরি তহবিল (১০%)</span><span>${formatNumber(contingency)} ৳</span></div>
                <div class="item"><span>🔌 ইউটিলিটিস (৩%)</span><span>${formatNumber(utilities)} ৳</span></div>
                <div class="item" style="font-size:1.4em;color:#e74c3c;background:linear-gradient(135deg,#ffeaa7,#ffd93d);border-radius:12px;padding:20px;">
                    <span>🎯 মোট খরচ</span><span>${formatNumber(grandTotal)} ৳</span>
                </div>
            `;

            document.getElementById('results').classList.add('show');
            document.getElementById('results').scrollIntoView({ behavior: 'smooth' });
        }

        function formatNumber(num) {
            return num.toLocaleString('bn-BD', { maximumFractionDigits: 0 });
        }

        function printReport() {
            window.print();
        }

        // Enter key support
        document.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                const activeInput = document.activeElement;
                if (activeInput.type === 'number') {
                    calculateCost();
                }
            }
        });

        // Auto-save to localStorage
        document.querySelectorAll('input, select').forEach(input => {
            input.addEventListener('change', function() {
                localStorage.setItem(this.id, this.value);
            });
        });

        // Load saved values
        window.addEventListener('load', function() {
            document.querySelectorAll('input, select').forEach(input => {
                const saved = localStorage.getItem(input.id);
                if (saved) {
                    input.value = saved;
                }
            });
            // Trigger range updates
            document.getElementById('inflationRate').dispatchEvent(new Event('input'));
            document.getElementById('materialMultiplier').dispatchEvent(new Event('input'));
            document.getElementById('laborMultiplier').dispatchEvent(new Event('input'));
        });

        // Initial calculation
        window.addEventListener('load', function() {
            setTimeout(calculateCost, 500);
        });
    </script>
</body>
</html>
