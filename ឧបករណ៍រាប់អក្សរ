```html
<!DOCTYPE html>
<html lang="km">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ឧបករណ៍រាប់ចំនួនអក្សរ | Rithy × Gemini</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Kanten:wght@400;700&family=Hanuman:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Hanuman', serif;
            background-color: #f8fafc;
        }
        .khmer-title {
            font-family: 'Kanten', sans-serif;
        }
        .glass-morphism {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 10px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
    </style>
</head>
<body class="min-h-screen py-8 px-4 sm:px-6 lg:px-8">
    <div class="max-w-3xl mx-auto">
        <!-- Header Section -->
        <div class="text-center mb-8">
            <h1 class="khmer-title text-3xl sm:text-4xl font-bold text-blue-800 mb-2">ឧបករណ៍រាប់ចំនួនអក្សរ</h1>
            <p class="text-gray-600">វិភាគ និងរាប់ចំនួនដងនៃអក្សរនីមួយៗដែលមាននៅក្នុងអត្ថបទរបស់អ្នក</p>
            <div class="mt-4 inline-block px-4 py-1 bg-blue-100 text-blue-700 rounded-full text-sm font-semibold">
                បង្កើតឡើងដោយ៖ Rithy × Gemini
            </div>
        </div>

        <!-- Main Card -->
        <div class="glass-morphism rounded-2xl shadow-xl p-6 mb-8 border border-gray-200">
            <label for="inputText" class="block text-lg font-bold text-gray-700 mb-2">សូមបញ្ចូលអត្ថបទនៅទីនេះ៖</label>
            <textarea 
                id="inputText" 
                rows="8" 
                class="w-full p-4 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none transition-all text-gray-800 bg-white shadow-sm mb-4"
                placeholder="វាយ ឬចម្លងអត្ថបទរបស់អ្នកដាក់នៅទីនេះ..."></textarea>
            
            <div class="flex flex-wrap gap-3">
                <button 
                    onclick="analyzeText()" 
                    class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-8 rounded-xl transition-all shadow-lg active:scale-95 flex-grow sm:flex-grow-0">
                    វិភាគអត្ថបទ
                </button>
                <button 
                    onclick="clearAll()" 
                    class="bg-gray-200 hover:bg-gray-300 text-gray-700 font-bold py-3 px-8 rounded-xl transition-all flex-grow sm:flex-grow-0">
                    សម្អាត
                </button>
            </div>
        </div>

        <!-- Stats Grid -->
        <div id="statsSection" class="hidden grid grid-cols-2 sm:grid-cols-3 gap-4 mb-8">
            <div class="bg-white p-4 rounded-xl shadow-sm border border-gray-100 text-center">
                <div class="text-sm text-gray-500">អក្សរសរុប</div>
                <div id="totalChars" class="text-2xl font-bold text-blue-600">0</div>
            </div>
            <div class="bg-white p-4 rounded-xl shadow-sm border border-gray-100 text-center">
                <div class="text-sm text-gray-500">អក្សរមិនស្ទួន</div>
                <div id="uniqueChars" class="text-2xl font-bold text-green-600">0</div>
            </div>
            <div class="bg-white p-4 rounded-xl shadow-sm border border-gray-100 text-center col-span-2 sm:col-span-1">
                <div class="text-sm text-gray-500">ពាក្យសរុប</div>
                <div id="wordCount" class="text-2xl font-bold text-purple-600">0</div>
            </div>
        </div>

        <!-- Results Table -->
        <div id="resultCard" class="hidden glass-morphism rounded-2xl shadow-lg border border-gray-200 overflow-hidden">
            <div class="bg-blue-50 px-6 py-4 border-b border-gray-200">
                <h2 class="text-lg font-bold text-blue-800">លទ្ធផលនៃការវិភាគ</h2>
            </div>
            <div class="max-h-[500px] overflow-y-auto custom-scrollbar">
                <table class="w-full text-left">
                    <thead class="bg-gray-50 sticky top-0">
                        <tr>
                            <th class="px-6 py-3 text-sm font-bold text-gray-600 border-b">អក្សរ/សញ្ញា</th>
                            <th class="px-6 py-3 text-sm font-bold text-gray-600 border-b">ចំនួនដង</th>
                            <th class="px-6 py-3 text-sm font-bold text-gray-600 border-b">ភាគរយ (%)</th>
                        </tr>
                    </thead>
                    <tbody id="resultBody" class="divide-y divide-gray-100">
                        <!-- Content will be injected here -->
                    </tbody>
                </table>
            </div>
            <div class="bg-gray-50 px-6 py-3 text-xs text-center text-gray-400">
                &copy; 2024 រចនាដោយ Rithy × Gemini
            </div>
        </div>
    </div>

    <script>
        function analyzeText() {
            const text = document.getElementById('inputText').value;
            if (!text.trim()) {
                alert("សូមបញ្ចូលអត្ថបទជាមុនសិន!");
                return;
            }

            const charMap = {};
            // Filter out newlines and handle each character including Khmer clusters correctly
            // Note: In JS, spread operator [...text] is better for Unicode/Emoji handling
            const chars = [...text].filter(char => char !== '\n' && char !== '\r');
            
            chars.forEach(char => {
                const displayChar = char === ' ' ? '[ចន្លោះ]' : char;
                charMap[displayChar] = (charMap[displayChar] || 0) + 1;
            });

            // Sorting results from highest frequency
            const sortedChars = Object.entries(charMap).sort((a, b) => b[1] - a[1]);
            
            const total = chars.length;
            const unique = sortedChars.length;
            const words = text.trim() === "" ? 0 : text.trim().split(/\s+/).length;

            // Update Stats
            document.getElementById('totalChars').innerText = total.toLocaleString('km-KH');
            document.getElementById('uniqueChars').innerText = unique.toLocaleString('km-KH');
            document.getElementById('wordCount').innerText = words.toLocaleString('km-KH');

            // Render Table
            const tbody = document.getElementById('resultBody');
            tbody.innerHTML = '';

            sortedChars.forEach(([char, count]) => {
                const percentage = ((count / total) * 100).toFixed(2);
                const row = `
                    <tr class="hover:bg-blue-50 transition-colors">
                        <td class="px-6 py-4 font-medium text-gray-900 text-lg">${char}</td>
                        <td class="px-6 py-4 text-gray-700 font-bold">${count.toLocaleString('km-KH')}</td>
                        <td class="px-6 py-4">
                            <div class="flex items-center gap-3">
                                <div class="w-24 bg-gray-200 rounded-full h-2">
                                    <div class="bg-blue-500 h-2 rounded-full" style="width: ${percentage}%"></div>
                                </div>
                                <span class="text-sm font-semibold text-gray-600">${percentage}%</span>
                            </div>
                        </td>
                    </tr>
                `;
                tbody.innerHTML += row;
            });

            // Show UI elements
            document.getElementById('statsSection').classList.remove('hidden');
            document.getElementById('resultCard').classList.remove('hidden');
            
            // Scroll to results on mobile
            document.getElementById('resultCard').scrollIntoView({ behavior: 'smooth', block: 'start' });
        }

        function clearAll() {
            document.getElementById('inputText').value = '';
            document.getElementById('statsSection').classList.add('hidden');
            document.getElementById('resultCard').classList.add('hidden');
            document.getElementById('inputText').focus();
        }
    </script>
</body>
</html>

```
