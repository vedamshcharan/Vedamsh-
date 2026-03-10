<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Loyalty Card SaaS</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .stamp-slot {
            transition: all 0.3s ease;
        }
        .active-stamp {
            background-color: #fbbf24; /* Gold color */
            transform: scale(1.1);
            border-color: #d97706;
        }
        @keyframes pop {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); }
            100% { transform: scale(1.1); }
        }
        .animate-pop { animation: pop 0.4s ease forwards; }
    </style>
</head>
<body class="bg-slate-900 flex items-center justify-center min-h-screen p-4 font-sans">

    <!-- Loyalty Card Container -->
    <div class="bg-white rounded-3xl shadow-2xl overflow-hidden max-w-sm w-full border-4 border-slate-800">
        
        <!-- Header -->
        <div class="bg-slate-800 p-6 text-center">
            <h1 class="text-white font-bold text-2xl tracking-tight">COFFEE CLUB</h1>
            <p class="text-slate-400 text-sm">Collect 7 stamps for a free drink!</p>
        </div>

        <!-- Grid of Stamps -->
        <div class="p-8 grid grid-cols-4 gap-4 justify-items-center" id="stamp-grid">
            <!-- Slots 1-7 -->
            <div class="stamp-slot w-14 h-14 rounded-full border-2 border-dashed border-slate-300 flex items-center justify-center text-slate-300 font-bold text-xl">1</div>
            <div class="stamp-slot w-14 h-14 rounded-full border-2 border-dashed border-slate-300 flex items-center justify-center text-slate-300 font-bold text-xl">2</div>
            <div class="stamp-slot w-14 h-14 rounded-full border-2 border-dashed border-slate-300 flex items-center justify-center text-slate-300 font-bold text-xl">3</div>
            <div class="stamp-slot w-14 h-14 rounded-full border-2 border-dashed border-slate-300 flex items-center justify-center text-slate-300 font-bold text-xl">4</div>
            <div class="stamp-slot w-14 h-14 rounded-full border-2 border-dashed border-slate-300 flex items-center justify-center text-slate-300 font-bold text-xl">5</div>
            <div class="stamp-slot w-14 h-14 rounded-full border-2 border-dashed border-slate-300 flex items-center justify-center text-slate-300 font-bold text-xl">6</div>
            <div class="stamp-slot w-14 h-14 rounded-full border-2 border-dashed border-slate-300 flex items-center justify-center text-slate-300 font-bold text-xl">7</div>
            
            <!-- Reward Slot -->
            <div class="w-14 h-14 rounded-full border-2 border-slate-800 flex items-center justify-center bg-slate-100">
                <span class="text-2xl">🎁</span>
            </div>
        </div>

        <!-- Progress Text -->
        <div class="px-8 pb-4 text-center">
            <p id="status-text" class="text-slate-600 font-medium text-sm">You have <span id="count" class="font-bold text-slate-900">0</span>/7 stamps</p>
        </div>

        <!-- Action Area (Merchant Only in real app) -->
        <div class="p-6 bg-slate-50 border-t border-slate-100 flex flex-col gap-3">
            <button onclick="addStamp()" id="stamp-btn" class="bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 rounded-xl shadow-lg transition active:scale-95">
                Add Stamp (Merchant)
            </button>
            <button onclick="resetCard()" class="text-slate-400 text-xs hover:underline">Reset Card</button>
        </div>
    </div>

    <!-- Script for Logic -->
    <script>
        let currentStamps = 0;
        const slots = document.querySelectorAll('.stamp-slot');
        const countDisplay = document.getElementById('count');
        const statusText = document.getElementById('status-text');
        const stampBtn = document.getElementById('stamp-btn');

        function addStamp() {
            if (currentStamps < 7) {
                const slot = slots[currentStamps];
                slot.innerHTML = "⭐"; // Stamp icon
                slot.classList.add('active-stamp', 'animate-pop', 'text-white', 'border-none');
                currentStamps++;
                countDisplay.innerText = currentStamps;

                if (currentStamps === 7) {
                    statusText.innerHTML = "<span class='text-green-600 font-bold'>🎉 REWARD READY! Show this to the cashier.</span>";
                    stampBtn.innerText = "Redeem Reward";
                    stampBtn.classList.replace('bg-indigo-600', 'bg-green-600');
                }
            } else {
                alert("Reward Redeemed! Starting new card.");
                resetCard();
            }
        }

        function resetCard() {
            currentStamps = 0;
            countDisplay.innerText = 0;
            statusText.innerHTML = 'You have <span id="count" class="font-bold text-slate-900">0</span>/7 stamps';
            stampBtn.innerText = "Add Stamp (Merchant)";
            stampBtn.classList.replace('bg-green-600', 'bg-indigo-600');
            slots.forEach((slot, index) => {
                slot.innerHTML = index + 1;
                slot.className = "stamp-slot w-14 h-14 rounded-full border-2 border-dashed border-slate-300 flex items-center justify-center text-slate-300 font-bold text-xl";
            });
        }
    </script>
</body>
</html>
# Vedamsh-
