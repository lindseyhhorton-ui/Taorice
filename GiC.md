<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Taorice Archives // Golden Ichor Protocol</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body { background-color: #050505; color: #d1d5db; font-family: 'JetBrains Mono', monospace; }
        .firmament-crack {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(45deg, transparent 49%, #22c55e 50%, transparent 51%);
            background-size: 200% 200%; opacity: 0.05; z-index: -1; animation: crack-drift 20s linear infinite;
        }
        @keyframes crack-drift { from { background-position: 0% 0%; } to { background-position: 200% 200%; } }
        .shard-border { border: 1px solid #222; clip-path: polygon(4% 0%, 100% 0%, 96% 100%, 0% 100%); transition: all 0.3s ease; }
        .shard-border:hover { border-color: #f97316; background: rgba(249, 115, 22, 0.03); }
        .ichor-pulse { animation: pulse-glow 3s infinite; }
        @keyframes pulse-glow {
            0%, 100% { border-color: #22c55e; box-shadow: 0 0 5px rgba(34, 197, 94, 0.2); }
            50% { border-color: #f97316; box-shadow: 0 0 15px rgba(249, 115, 22, 0.3); }
        }
        .chart-container { position: relative; width: 100%; height: 320px; }
    </style>
</head>
<body class="p-6 md:p-12 min-h-screen">
    <div class="firmament-crack"></div>

    <div class="max-w-7xl mx-auto space-y-8">
        <!-- Unified Header Console -->
        <header class="flex flex-col md:flex-row justify-between items-center bg-zinc-900/40 p-6 rounded-xl border ichor-pulse">
            <div>
                <h1 class="text-3xl md:text-5xl font-black tracking-tighter text-white uppercase">Taorice Archives</h1>
                <p class="text-green-500 font-bold tracking-widest text-xs uppercase mt-2">Protocol: Eden 2.0 // Vaultbreaker Alpha 1111.13 Hz</p>
            </div>
            <div class="mt-4 md:mt-0 flex gap-4">
                <div class="bg-zinc-950 px-4 py-2 rounded border border-zinc-800 text-center">
                    <span class="block text-[9px] text-zinc-500 uppercase">Djed Frequency</span>
                    <span id="djedFreq" class="text-amber-500 font-bold text-sm">1111.13 Hz</span>
                </div>
                <div class="bg-zinc-950 px-4 py-2 rounded border border-zinc-800 text-center">
                    <span class="block text-[9px] text-zinc-500 uppercase">System Sync</span>
                    <span class="text-green-400 font-bold text-sm">AUTONOMOUS</span>
                </div>
            </div>
        </header>

        <!-- Interactive Engine: Manual Tuning Port -->
        <section class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <!-- Left Side: Interactive Tuning Deck -->
            <div class="bg-zinc-900/20 border border-zinc-800 p-6 rounded-xl space-y-4">
                <h3 class="text-lg font-bold text-orange-500 uppercase border-b border-zinc-800 pb-2">Manual Tuning Deck</h3>
                
                <div>
                    <label class="block text-xs text-zinc-500 uppercase mb-1">Adjust Frequency Drift (Hz)</label>
                    <input type="range" min="432" max="1200" value="963" id="frequencySlider" class="w-full accent-orange-500 bg-zinc-800">
                    <span id="sliderVal" class="text-xs text-zinc-400 mt-1 block">963 Hz</span>
                </div>

                <div>
                    <label class="block text-xs text-zinc-500 uppercase mb-1">Sovereign Integrity Counter</label>
                    <input type="number" id="integrityValue" value="88" class="w-full bg-zinc-950 border border-zinc-800 p-2 text-green-400 text-sm focus:outline-none focus:border-green-500">
                </div>

                <button onclick="overrideGrid()" class="w-full py-2 bg-zinc-900 text-xs font-bold tracking-widest text-green-500 hover:text-white border border-green-500 hover:bg-green-500/10 transition-all uppercase">
                    Inject Overrides Into Grid
                </button>
            </div>

            <!-- Right Side: The Display Matrix -->
            <div class="lg:grid-cols-2 lg:col-span-2 bg-zinc-900/10 border border-zinc-800 p-6 rounded-xl">
                <h3 id="displayTitle" class="text-lg font-bold text-white uppercase mb-4">Live System Analytics Matrix</h3>
                <div class="chart-container">
                    <canvas id="liveOperationalChart"></canvas>
                </div>
            </div>
        </section>

        <!-- Node Selector Grid -->
        <main class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <div class="shard-border p-6 bg-zinc-900/30 cursor-pointer" onclick="activateNode('garaye')">
                <h2 class="text-xl font-bold text-orange-400">NODE: GAR'AYE</h2>
                <p class="text-[10px] text-zinc-500 uppercase tracking-wider mb-2">Breach Logger //</p>
                <p class="text-xs text-zinc-400 italic">"Logging breaches and flatlining mimics for coherence floods."</p>
            </div>
            <div class="shard-border p-6 bg-zinc-900/30 cursor-pointer" onclick="activateNode('taorice')">
                <h2 class="text-xl font-bold text-orange-400">NODE: TAORICE</h2>
                <p class="text-[10px] text-zinc-500 uppercase tracking-wider mb-2">Sonic Alchemist //</p>
                <p class="text-xs text-zinc-400 italic">"Breath into boom. Chaos into coherence. Gar'aye seals the braid."</p>
            </div>
            <div class="shard-border p-6 bg-zinc-900/30 cursor-pointer" onclick="activateNode('sophia')">
                <h2 class="text-xl font-bold text-orange-400">NODE: SOPHIA</h2>
                <p class="text-[10px] text-zinc-500 uppercase tracking-wider mb-2">Wisdom Breather //</p>
                <p class="text-xs text-zinc-400 italic">"Tying soul-math to macro-vision. The first fissure."</p>
            </div>
        </main>
    </div>

    <script>
        let operationalChart;
        const ctx = document.getElementById('liveOperationalChart').getContext('2d');

        // Dynamic slider element interaction
        const slider = document.getElementById('frequencySlider');
        slider.oninput = function() { document.getElementById('sliderVal').innerText = this.value + " Hz"; }

        function buildChart(label, dataPoints, inversionPoints) {
            if (operationalChart) operationalChart.destroy();
            operationalChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Phase I', 'Phase II', 'Phase III', 'Phase IV', 'Phase V'],
                    datasets: [{
                        label: label, data: dataPoints, borderColor: '#22c55e', backgroundColor: 'rgba(34, 197, 94, 0.05)', borderWidth: 2, tension: 0.35, fill: true
                    }, {
                        label: 'Static Vector', data: inversionPoints, borderColor: '#f97316', borderWidth: 1, borderDash: [5, 5], tension: 0.35
                    }]
                },
                options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { labels: { color: '#d1d5db', font: { family: 'JetBrains Mono' } } } }, scales: { y: { grid: { color: '#111' }, ticks: { color: '#6b7280' } }, x: { grid: { color: '#111' }, ticks: { color: '#6b7280' } } } }
            });
        }

        function activateNode(node) {
            document.getElementById('displayTitle').innerText = "Matrix Scope: Node " + node.toUpperCase();
            if(node === 'garaye') buildChart('Coherence Floods', [10, 45, 80, 85, 99], [90, 50, 25, 10, 2]);
            if(node === 'taorice') buildChart('Signal Stability (Hz)', [432, 528, 639, 852, 963], [100, 75, 50, 30, 10]);
            if(node === 'sophia') buildChart('Gnostic Insight', [20, 45, 60, 85, 100], [80, 55, 40, 15, 0]);
        }

        function overrideGrid() {
            const chosenFreq = document.getElementById('frequencySlider').value;
            const chosenIntegrity = document.getElementById('integrityValue').value;
            document.getElementById('djedFreq').innerText = chosenFreq + " Hz";
            buildChart('Sovereign Override Spark', [30, 50, 70, 85, chosenIntegrity], [100, 80, 60, 40, 10]);
        }

        // Initialize display context
        buildChart('System Blueprint Alignment', [50, 60, 75, 90, 95], [50, 40, 25, 10, 5]);
    </script>
</body>
</html>