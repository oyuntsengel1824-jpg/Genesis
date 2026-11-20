# Genesis
A real-time, crowdsourced bus status and delay-tracking web app designed for students commuting from ger districts in Orkhon Province.
<!DOCTYPE html>
<html lang="mn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Эрдэнэт Сурагч Транзит - Ухаалаг Цаг Тооцоолуур</title>
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
</head>
<body class="bg-slate-50 text-slate-800 font-sans min-h-screen flex flex-col justify-between">

    <!-- Header -->
    <header class="bg-indigo-600 text-white shadow-md py-4 px-6">
        <div class="max-w-2xl mx-auto flex justify-between items-center">
            <h1 class="text-xl font-bold">🚍 Erdenet Student Commute</h1>
            <span class="text-xs bg-indigo-500 px-3 py-1 rounded-full">Хакатон MVP</span>
        </div>
    </header>

    <!-- Main Container -->
    <main class="max-w-2xl mx-auto p-4 sm:p-6 w-full flex-grow">
        
        <div class="bg-white rounded-2xl shadow-xl p-6 mb-6 border border-slate-100">
            <h2 class="text-lg font-semibold text-slate-700 mb-4">Өглөөний хичээл болон маршрутаа сонгоно уу</h2>
            
            <!-- Route Selection -->
            <div class="mb-4">
                <label class="block text-sm font-medium text-slate-600 mb-1">Гэр хорооллын чиглэл:</label>
                <select id="routeSelect" class="w-full p-3 border border-slate-300 rounded-xl focus:ring-2 focus:ring-indigo-500 outline-none">
                    <option value="25">Ч:1-Ч:2 (Их Залуу – Шанд) ~ 25 мин</option>
                    <option value="20">Ч:3 (Баян Тал) ~ 20 мин</option>
                    <option value="30">Ч:4 (Сагсай) ~ 30 мин</option>
                    <option value="35">Ч:5 (Говил) ~ 35 мин</option>
                    <option value="20">Ч:6 (Тосгон – Пирамид – Зээл) ~ 20 мин</option>
                    <option value="25">Ч:7 (Вокзал – Төгөл) ~ 25 мин</option>
                    <option value="40" selected>Ч:8 (Урд Хабитат – Дэнж – Уртытын гол) ~ 40 мин</option>
                    <option value="30">Ч:9 (Яргуйт – Автовокзал) ~ 30 мин</option>
                </select>
            </div>

            <!-- School Start Time -->
            <div class="mb-4">
                <label class="block text-sm font-medium text-slate-600 mb-1">Сургуулийн эхлэх цаг (Хостай цаг):</label>
                <input type="time" id="schoolTime" value="08:00" class="w-full p-3 border border-slate-300 rounded-xl focus:ring-2 focus:ring-indigo-500 outline-none">
            </div>

            <!-- Walking & Buffer Time -->
            <div class="mb-6">
                <label class="block text-sm font-medium text-slate-600 mb-1">Буудал хүртэл алхах хугацаа (минут):</label>
                <input type="number" id="walkTime" value="10" class="w-full p-3 border border-slate-300 rounded-xl focus:ring-2 focus:ring-indigo-500 outline-none">
            </div>

            <!-- Weather / Traffic Condition -->
            <div class="mb-6">
                <label class="block text-sm font-medium text-slate-600 mb-1">Замын нөхцөл / Цаг агаар:</label>
                <select id="trafficCondition" class="w-full p-3 border border-slate-300 rounded-xl focus:ring-2 focus:ring-indigo-500 outline-none">
                    <option value="0">Энгийн өдөр (+0 мин)</option>
                    <option value="15" selected>Өглөөний ачаалал (+15 мин)</option>
                    <option value="30">Цас / Хүйтэн / Хальтиргаа (+30 мин)</option>
                </select>
            </div>

            <button onclick="calculateCommute()" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-semibold py-3.5 rounded-xl shadow-lg transition duration-200">
                Яг хэдэн цагт гарахаа тооцоолох
            </button>
        </div>

        <!-- Result Card -->
        <div id="resultCard" class="hidden bg-emerald-50 border border-emerald-200 rounded-2xl p-6 shadow-md transition-all duration-300">
            <h3 class="text-emerald-800 font-bold text-lg mb-2">📌 Таны гарах оновчтой цаг:</h3>
            <div class="text-3xl font-extrabold text-emerald-600 mb-3" id="departureTimeOutput">07:05 AM</div>
            <p class="text-sm text-emerald-700 mb-4" id="recommendationText">Автобусны хуваарь болон замын ачааллыг тооцож үзэхэд энэ цагт гэрээсээ гарвал хичээлээсээ хоцрохгүй.</p>
            
            <div id="taxiWarning" class="hidden bg-amber-50 border border-amber-200 p-3 rounded-xl text-amber-800 text-xs mt-3">
                ⚠️ <strong>Анхааруулга:</strong> Дараагийн автобус оройтож магадгүй тул таксины мөнгөө хувааж суух сурагчдын групп рүү холбогдох эсвэл эрт гараарай!
            </div>
        </div>

    </main>

    <!-- Footer -->
    <footer class="text-center py-4 text-xs text-slate-400">
        Orkhon Province Student Transit Hackathon Project &copy; 2026
    </footer>

    <!-- JavaScript Logic -->
    <script>
        function calculateCommute() {
            const routeMinutes = parseInt(document.getElementById('routeSelect').value);
            const schoolTimeString = document.getElementById('schoolTime').value; // e.g. "08:00"
            const walkMinutes = parseInt(document.getElementById('walkTime').value) || 0;
            const trafficBuffer = parseInt(document.getElementById('trafficCondition').value) || 0;

            if (!schoolTimeString) {
                alert("Сургуулийн цагаа оруулна уу!");
                return;
            }

            // Convert school time to total minutes from midnight
            const [hours, minutes] = schoolTimeString.split(':').map(Number);
            const schoolTotalMinutes = hours * 60 + minutes;

            // Total required time = walk + bus route + traffic/weather buffer + 10 min safe arrival buffer
            const totalTripMinutes = walkMinutes + routeMinutes + trafficBuffer + 10;
            const departureTotalMinutes = schoolTotalMinutes - totalTripMinutes;

            // Format back to HH:MM
            let depHours = Math.floor(departureTotalMinutes / 60);
            let depMins = departureTotalMinutes % 60;

            if (depHours < 0) depHours += 24; // safety handle

            const formattedHours = String(depHours).padStart(2, '0');
            const formattedMins = String(depMins).padStart(2, '0');
            const finalDepartureTime = `${formattedHours}:${formattedMins}`;

            // Show Result Card
            const resultCard = document.getElementById('resultCard');
            resultCard.classList.remove('hidden');
            
            document.getElementById('departureTimeOutputinnerText', document.getElementById('departureTimeOutput').innerText = finalDepartureTime);

            // Logic for taxi warning if buffer is high
            const taxiWarning = document.getElementById('taxiWarning');
            if (trafficBuffer >= 20 || routeMinutes >= 35) {
                taxiWarning.classList.remove('hidden');
            } else {
                taxiWarning.classList.add('hidden');
            }
        }
    </script>
</body>
</html>
