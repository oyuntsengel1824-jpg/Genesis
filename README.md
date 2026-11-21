#Genesis
<!DOCTYPE html>
<html lang="mn" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Эрдэнэт Сурагч Транзит - Ухаалаг Цаг Тооцоолуур & Төлөвлөгч</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@500;700&family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <style>
        body {
            font-family: 'Plus Jakarta Sans', system-ui, -apple-system, sans-serif;
        }
        .font-mono-time {
            font-family: 'JetBrains Mono', monospace;
        }
        @keyframes slideUp {
            0% {
                opacity: 0;
                transform: translateY(18px);
            }
            100% {
                opacity: 1;
                transform: translateY(0);
            }
        }
        .animate-slideUp {
            animation: slideUp 0.45s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }
        .planner-surface {
            background-color: #0b1120;
            background-image:
                radial-gradient(circle at 85% 10%, rgba(99, 102, 241, 0.22), transparent 48%),
                radial-gradient(circle at 15% 90%, rgba(34, 211, 238, 0.14), transparent 45%),
                radial-gradient(rgba(148, 163, 184, 0.14) 1px, transparent 1px);
            background-size: 100% 100%, 100% 100%, 18px 18px;
        }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen flex flex-col justify-between selection:bg-indigo-500 selection:text-white">

    <!-- Header -->
    <header class="sticky top-0 z-30 bg-slate-950/90 backdrop-blur border-b border-slate-800 py-3.5 px-4 sm:px-6">
        <div class="max-w-5xl mx-auto flex flex-wrap justify-between items-center gap-3">
            <a href="#" class="text-lg sm:text-xl font-bold text-white flex items-center gap-2 tracking-tight">
                <span>🚍</span>
                <span>Erdenet Student Commute</span>
            </a>
            <div class="flex items-center gap-2 sm:gap-3 text-xs sm:text-sm">
                <span class="hidden sm:inline-block bg-indigo-500/15 text-indigo-300 border border-indigo-500/30 px-3 py-1 rounded-full text-xs">Хакатон MVP</span>
                <a href="#planner" class="px-3.5 py-1.5 rounded-lg bg-indigo-600 hover:bg-indigo-500 text-white font-semibold transition">Daily Planner</a>
            </div>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="relative overflow-hidden border-b border-slate-800 bg-gradient-to-b from-indigo-950/45 via-slate-950 to-slate-950 py-12 px-4 sm:px-6">
        <div class="max-w-4xl mx-auto text-center">
            <span class="inline-block text-xs font-semibold tracking-wider uppercase px-3 py-1 rounded-full bg-indigo-500/15 text-indigo-300 border border-indigo-500/30 mb-3">
                Эрдэнэт • Автобус, Сургууль & Өдрийн Төлөвлөгөө
            </span>
            <h1 class="text-3xl sm:text-5xl font-extrabold tracking-tight text-white leading-tight">
                <span class="block">Хичээлдээ яг цагтаа.</span>
                <span class="block mt-2 h-[1.25em] overflow-hidden">
                    <span id="kineticWord" class="inline-block bg-gradient-to-r from-indigo-400 via-cyan-300 to-emerald-400 bg-clip-text text-transparent animate-slideUp">
                        Автобусаа тооцоол.
                    </span>
                </span>
            </h1>
        </div>
    </section>

    <!-- Main Container -->
    <main class="max-w-5xl mx-auto p-4 sm:p-6 w-full flex-grow grid grid-cols-1 lg:grid-cols-12 gap-6">

        <!-- ЗҮҮН ТАЛ: АВТОБУС, СУРГУУЛЬ & ХОЦРОЛТЫН ШИЙДЭЛ -->
        <div class="lg:col-span-7 space-y-6">

            <section class="relative rounded-2xl overflow-hidden border border-slate-800 shadow-xl">
                <div
                    class="absolute inset-0 bg-cover bg-center opacity-25 scale-105"
                    style="background-image: url('https://images.unsplash.com/photo-1570125909232-eb263c188f7e?auto=format&fit=crop&w=1400&q=80');"
                ></div>
                <div class="absolute inset-0 bg-gradient-to-b from-slate-950/85 via-slate-950/90 to-slate-950"></div>

                <div class="relative p-5 sm:p-6 space-y-5">
                    <h2 class="text-lg font-bold text-white tracking-tight">Өглөөний хичээл болон маршрутаа сонгоно уу</h2>

                    <!-- Сургууль сонгох -->
                    <div>
                        <label for="schoolSelect" class="block text-sm font-medium text-slate-300 mb-1.5">Сургууль (Эрдэнэт):</label>
                        <select id="schoolSelect" onchange="syncSchoolLocation(true)" class="w-full p-3 bg-slate-900/90 border border-slate-700 text-white rounded-xl focus:ring-2 focus:ring-indigo-500 outline-none">
                            <option value="1" data-stop="Төв" data-walk="5" selected>1-р сургууль (Буудал: Төв • ~5 мин)</option>
                            <option value="2" data-stop="7-р хороолол" data-walk="6">2-р сургууль (Буудал: 7-р хороолол • ~6 мин)</option>
                            <option value="3" data-stop="Дэнж" data-walk="7">3-р сургууль (Буудал: Дэнж • ~7 мин)</option>
                            <option value="4" data-stop="Төв" data-walk="6">4-р сургууль (Буудал: Төв • ~6 мин)</option>
                            <option value="8" data-stop="Төв" data-walk="8">8-р сургууль (Буудал: Төв • ~8 мин)</option>
                            <option value="14" data-stop="Зээл" data-walk="5">14-р сургууль (Буудал: Зээл • ~5 мин)</option>
                            <option value="15" data-stop="Төгөл" data-walk="6">15-р сургууль (Буудал: Төгөл • ~6 мин)</option>
                            <option value="17" data-stop="Шанд" data-walk="7">17-р сургууль (Буудал: Шанд • ~7 мин)</option>
                            <option value="18" data-stop="Баян Тал" data-walk="6">18-р сургууль (Буудал: Баян Тал • ~6 мин)</option>
                        </select>
                        <div class="mt-2.5 flex flex-wrap items-center gap-2" id="recommendedRoutesContainer"></div>
                    </div>

                    <!-- Route Selection -->
                    <div>
                        <label for="routeSelect" class="block text-sm font-medium text-slate-300 mb-1.5">Гэр хорооллын чиглэл:</label>
                        <select id="routeSelect" onchange="syncRouteStops()" class="w-full p-3 bg-slate-900/90 border border-slate-700 text-white rounded-xl focus:ring-2 focus:ring-indigo-500 outline-none">
                            <option value="25" data-code="Ч:1–Ч:2" data-stops="Их Залуу,Төв,Шанд">Ч:1–Ч:2 (Их Залуу – Шанд) ~ 25 мин</option>
                            <option value="20" data-code="Ч:3" data-stops="Баян Тал,Үйлдвэр,Төв">Ч:3 (Баян Тал) ~ 20 мин</option>
                            <option value="30" data-code="Ч:4" data-stops="Сагсай,Дэнж,Төв">Ч:4 (Сагсай) ~ 30 мин</option>
                            <option value="35" data-code="Ч:5" data-stops="Говил,7-р хороолол,Төв">Ч:5 (Говил) ~ 35 мин</option>
                            <option value="20" data-code="Ч:6" data-stops="Тосгон,Пирамид,Зээл">Ч:6 (Тосгон – Пирамид – Зээл) ~ 20 мин</option>
                            <option value="25" data-code="Ч:7" data-stops="Вокзал,Төв,Төгөл">Ч:7 (Вокзал – Төгөл) ~ 25 мин</option>
                            <option value="40" data-code="Ч:8" data-stops="Урд Хабитат,Дэнж,Уртын гол" selected>Ч:8 (Урд Хабитат – Дэнж – Уртын гол) ~ 40 мин</option>
                            <option value="30" data-code="Ч:9" data-stops="Яргуйт,Төв,Автовокзал">Ч:9 (Яргуйт – Автовокзал) ~ 30 мин</option>
                        </select>
                    </div>

                    <!-- Автобусны байршил -->
                    <div class="bg-slate-900/90 border border-slate-800 rounded-xl p-4">
                        <div class="flex items-center justify-between gap-2 mb-4">
                            <span id="busLocationLabel" class="text-xs font-semibold text-cyan-300">
                                Автобус яг одоо: Төв орчимд явж байна
                            </span>
                            <button type="button" onclick="moveBusPosition()" class="text-xs bg-slate-800 hover:bg-slate-700 text-slate-200 px-3 py-1 rounded-lg transition cursor-pointer">
                                Байршил шинэчлэх
                            </button>
                        </div>

                        <div class="relative pt-6 pb-1">
                            <div class="h-1.5 w-full bg-slate-800 rounded-full overflow-hidden">
                                <div id="busProgressBar" class="h-full bg-gradient-to-r from-indigo-500 to-cyan-400 transition-all duration-500" style="width: 50%;"></div>
                            </div>
                            <div id="busMarker" class="absolute top-0 -translate-x-1/2 transition-all duration-500" style="left: 50%;">
                                <span class="inline-flex items-center justify-center w-7 h-7 rounded-full bg-cyan-400 text-slate-950 text-sm font-bold shadow-lg">
                                    🚍
                                </span>
                            </div>
                            <div id="busStopsRow" class="flex justify-between mt-3 text-[11px] text-slate-400"></div>
                        </div>
                    </div>

                    <!-- School Start Time -->
                    <div>
                        <label for="schoolTime" class="block text-sm font-medium text-slate-300 mb-1.5">Сургуулийн эхлэх цаг:</label>
                        <input type="time" id="schoolTime" value="08:00" class="w-full p-3 bg-slate-900/90 border border-slate-700 text-white rounded-xl focus:ring-2 focus:ring-indigo-500 outline-none">
                    </div>

                    <!-- Walking Times -->
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label for="walkTime" class="block text-sm font-medium text-slate-300 mb-1.5">Гэрээс буудал алхах (мин):</label>
                            <input type="number" id="walkTime" value="10" min="0" class="w-full p-3 bg-slate-900/90 border border-slate-700 text-white rounded-xl focus:ring-2 focus:ring-indigo-500 outline-none">
                        </div>
                        <div>
                            <label for="stopToSchoolWalk" class="block text-sm font-medium text-slate-300 mb-1.5">Буудлаас сургууль алхах (мин):</label>
                            <input type="number" id="stopToSchoolWalk" value="5" min="0" class="w-full p-3 bg-slate-900/90 border border-slate-700 text-white rounded-xl focus:ring-2 focus:ring-indigo-500 outline-none">
                        </div>
                    </div>

                    <!-- Weather / Traffic Condition -->
                    <div>
                        <label for="trafficCondition" class="block text-sm font-medium text-slate-300 mb-1.5">Замын нөхцөл / Цаг агаар:</label>
                        <select id="trafficCondition" class="w-full p-3 bg-slate-900/90 border border-slate-700 text-white rounded-xl focus:ring-2 focus:ring-indigo-500 outline-none">
                            <option value="0">Энгийн өдөр (+0 мин)</option>
                            <option value="15" selected>Өглөөний ачаалал (+15 мин)</option>
                            <option value="30">Цас / Хүйтэн / Хальтиргаа (+30 мин)</option>
                        </select>
                    </div>

                    <button type="button" onclick="calculateCommute()" class="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-semibold py-3.5 rounded-xl shadow-lg transition duration-200 cursor-pointer">
                        Яг хэдэн цагт гарахаа тооцоолох
                    </button>
                </div>
            </section>

            <!-- Result Card + Саатлын ойлгомжтой шийдэл -->
            <section id="resultCard" class="hidden bg-slate-900 border border-slate-800 rounded-2xl p-5 sm:p-6 shadow-lg space-y-4">
                <div class="p-4 rounded-xl bg-emerald-500/10 border border-emerald-500/30">
                    <h3 class="text-emerald-300 font-bold text-base mb-1">📌 Таны гарах оновчтой цаг:</h3>
                    <div class="text-3xl font-extrabold font-mono-time text-emerald-400 mb-2" id="departureTimeOutput">07:05</div>
                    <p class="text-xs sm:text-sm text-slate-300" id="recommendationText"></p>
                </div>

                <div id="taxiWarning" class="hidden bg-amber-500/10 border border-amber-500/30 p-4 rounded-xl text-amber-200 text-xs sm:text-sm space-y-2">
                    <div>
                        ⚠️ <strong>Автобус хоцорсон / ачаалалтай үеийн шийдэл:</strong>
                        <span id="delayDetailText"></span>
                    </div>
                    <button type="button" onclick="shiftPlannerTasks(15)" class="bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-xs px-3 py-1.5 rounded-lg transition cursor-pointer">
                        Planner-ийн цагийг +15 мин хойшлуулах
                    </button>
                </div>
            </section>

        </div>

        <!-- БАРУУН ТАЛ: DAILY PLANNER (#planner) -->
        <aside id="planner" class="lg:col-span-5">
            <div class="planner-surface border border-indigo-500/25 ring-1 ring-white/5 rounded-3xl p-5 sm:p-6 shadow-2xl shadow-indigo-950/50 sticky top-20">
                <div class="flex items-center justify-between mb-5 pb-3.5 border-b border-white/10">
                    <div>
                        <span class="block text-[10px] font-bold uppercase tracking-[0.18em] text-cyan-300/90">Ухаалаг Төлөвлөгч</span>
                        <h2 class="text-xl font-extrabold tracking-tight text-white mt-0.5">Daily Planner</h2>
                    </div>
                    <span id="taskCount" class="font-mono-time text-xs font-bold bg-indigo-500/20 text-indigo-200 border border-indigo-400/30 px-3 py-1 rounded-full">3</span>
                </div>

                <form onsubmit="addPlannerTask(event)" class="flex gap-2 mb-4">
                    <input type="time" id="plannerTimeInput" value="08:00" class="font-mono-time bg-slate-900/90 border border-slate-700/80 text-cyan-200 text-xs sm:text-sm rounded-xl px-2.5 py-2.5 outline-none focus:ring-2 focus:ring-cyan-400/70">
                    <input type="text" id="plannerTitleInput" placeholder="Ажил нэмэх..." class="flex-1 min-w-0 bg-slate-900/90 border border-slate-700/80 text-white text-sm placeholder:text-slate-400 rounded-xl px-3.5 py-2.5 outline-none focus:ring-2 focus:ring-indigo-400/70">
                    <button type="submit" class="bg-gradient-to-r from-indigo-500 to-cyan-500 hover:from-indigo-400 hover:to-cyan-400 text-slate-950 text-base font-extrabold px-4 py-2 rounded-xl shadow-md shadow-cyan-500/20 transition cursor-pointer shrink-0">
                        +
                    </button>
                </form>

                <ul id="plannerList" class="space-y-2.5"></ul>
            </div>
        </aside>

    </main>

    <!-- Footer -->
    <footer class="text-center py-4 text-xs text-slate-500 border-t border-slate-900">
        Orkhon Province Student Transit Hackathon Project &copy; 2026
    </footer>

    <script>
        const words = [
            "Автобусаа тооцоол.",
            "Өдрөө төлөвлө.",
            "Хоцролтгүй яв."
        ];
        let wIdx = 0;
        const kineticEl = document.getElementById("kineticWord");
        setInterval(() => {
            wIdx = (wIdx + 1) % words.length;
            kineticEl.classList.remove("animate-slideUp");
            void kineticEl.offsetWidth;
            kineticEl.textContent = words[wIdx];
            kineticEl.classList.add("animate-slideUp");
        }, 2300);

        let currentStopIndex = 0;

        function suggestRoutesForSchool(autoSelectFirst = false) {
            const schoolSel = document.getElementById("schoolSelect");
            const targetStop = schoolSel.options[schoolSel.selectedIndex].dataset.stop || "Төв";
            const routeSel = document.getElementById("routeSelect");
            const container = document.getElementById("recommendedRoutesContainer");
            const matchingIndices = [];

            Array.from(routeSel.options).forEach((opt, idx) => {
                const stops = (opt.dataset.stops || "").split(",").map(s => s.trim());
                if (stops.includes(targetStop)) matchingIndices.push(idx);
            });

            if (autoSelectFirst && matchingIndices.length > 0) {
                routeSel.selectedIndex = matchingIndices[0];
                currentStopIndex = 0;
            }

            container.innerHTML = matchingIndices.map(idx => {
                const opt = routeSel.options[idx];
                const active = routeSel.selectedIndex === idx;
                return `
                    <button type="button" onclick="selectRecommendedRoute(${idx})" class="text-xs px-2.5 py-1 rounded-lg transition cursor-pointer ${
                        active ? "bg-indigo-600 text-white font-semibold" : "bg-slate-800 hover:bg-slate-700 text-slate-300"
                    }">
                        ${opt.dataset.code} (${opt.value} мин)
                    </button>
                `;
            }).join("");

            renderBusLocation();
        }

        function selectRecommendedRoute(idx) {
            document.getElementById("routeSelect").selectedIndex = idx;
            currentStopIndex = 0;
            suggestRoutesForSchool(false);
        }

        function syncSchoolLocation(autoSelectFirst = false) {
            const opt = document.getElementById("schoolSelect").selectedOptions[0];
            document.getElementById("stopToSchoolWalk").value = parseInt(opt.dataset.walk) || 5;
            suggestRoutesForSchool(autoSelectFirst);
        }

        function getCurrentStops() {
            const opt = document.getElementById("routeSelect").selectedOptions[0];
            return (opt.dataset.stops || "Эхлэл,Дунд,Төгсгөл").split(",");
        }

        function renderBusLocation() {
            const stops = getCurrentStops();
            if (currentStopIndex >= stops.length) currentStopIndex = 0;
            const percent = stops.length > 1 ? (currentStopIndex / (stops.length - 1)) * 100 : 0;

            document.getElementById("busProgressBar").style.width = `${percent}%`;
            document.getElementById("busMarker").style.left = `${percent}%`;
            document.getElementById("busLocationLabel").textContent =
                `Автобус яг одоо: ${stops[currentStopIndex]} орчимд явж байна`;
            document.getElementById("busStopsRow").innerHTML = stops.map((stop, idx) =>
                `<span class="${idx === currentStopIndex ? "text-cyan-300 font-semibold" : ""}">${stop}</span>`
            ).join("");
        }

        function syncRouteStops() {
            currentStopIndex = 0;
            renderBusLocation();
        }

        function moveBusPosition() {
            const stops = getCurrentStops();
            currentStopIndex = (currentStopIndex + 1) % stops.length;
            renderBusLocation();
        }

        syncSchoolLocation(true);

        function calculateCommute() {
            const routeMinutes = parseInt(document.getElementById("routeSelect").value);
            const schoolTimeString = document.getElementById("schoolTime").value;
            const walkToBusMinutes = parseInt(document.getElementById("walkTime").value) || 0;
            const walkToSchoolMinutes = parseInt(document.getElementById("stopToSchoolWalk").value) || 0;
            const trafficBuffer = parseInt(document.getElementById("trafficCondition").value) || 0;

            if (!schoolTimeString) {
                alert("Сургуулийн цагаа оруулна уу!");
                return;
            }

            const [hours, minutes] = schoolTimeString.split(":").map(Number);
            const schoolTotalMinutes = hours * 60 + minutes;
            const totalTripMinutes = walkToBusMinutes + routeMinutes + walkToSchoolMinutes + trafficBuffer + 10;

            let departureTotalMinutes = schoolTotalMinutes - totalTripMinutes;
            if (departureTotalMinutes < 0) departureTotalMinutes += 24 * 60;

            const depHours = Math.floor(departureTotalMinutes / 60) % 24;
            const depMins = departureTotalMinutes % 60;
            const finalDepartureTime = `${String(depHours).padStart(2, "0")}:${String(depMins).padStart(2, "0")}`;

            document.getElementById("resultCard").classList.remove("hidden");
            document.getElementById("departureTimeOutput").textContent = finalDepartureTime;
            document.getElementById("recommendationText").textContent =
                `Автобусны зам (${routeMinutes} мин) + алхалт (${walkToBusMinutes + walkToSchoolMinutes} мин) + нөхцөл (+${trafficBuffer} мин) + нөөц (10 мин) нийлээд энэ цагт гарвал хичээлээсээ хоцрохгүй.`;

            const taxiWarning = document.getElementById("taxiWarning");
            if (trafficBuffer >= 15 || routeMinutes >= 35) {
                taxiWarning.classList.remove("hidden");
                document.getElementById("delayDetailText").textContent =
                    " Дараагийн автобус оройтож магадгүй тул эрт гарах, зэрэгцээ чиглэл харах эсвэл сурагчдын группээр такси хувааж суугаарай.";
            } else {
                taxiWarning.classList.add("hidden");
            }
        }

        let plannerTasks = [
            { id: 1, time: "07:05", title: "Гэрээс гарах", done: false },
            { id: 2, time: "08:00", title: "Хичээл эхлэх", done: false },
            { id: 3, time: "13:30", title: "Даалгавар хийх", done: false }
        ];

        function renderPlanner() {
            const list = document.getElementById("plannerList");
            document.getElementById("taskCount").textContent = plannerTasks.length;

            if (plannerTasks.length === 0) {
                list.innerHTML = `<li class="text-center text-xs text-slate-400 py-7 bg-slate-900/50 rounded-2xl border border-dashed border-slate-700/70">Төлөвлөсөн ажил алга.</li>`;
                return;
            }

            list.innerHTML = plannerTasks.map(task => `
                <li class="flex items-center justify-between gap-2.5 p-3 rounded-2xl bg-slate-900/75 hover:bg-slate-900 border border-white/10 transition">
                    <button type="button" onclick="toggleTask(${task.id})" class="flex items-center gap-3 text-left flex-1 min-w-0 cursor-pointer">
                        <span class="font-mono-time text-xs font-bold text-cyan-300 bg-cyan-500/10 border border-cyan-400/20 px-2.5 py-1 rounded-lg shrink-0">${task.time}</span>
                        <span class="text-sm font-medium truncate ${task.done ? "line-through text-slate-500" : "text-slate-100"}">${escapeHtml(task.title)}</span>
                    </button>
                    <button type="button" onclick="deleteTask(${task.id})" title="Хасах" class="text-xs font-semibold text-slate-400 hover:text-rose-400 px-2.5 py-1 rounded-lg hover:bg-rose-500/10 transition cursor-pointer shrink-0">
                        ✕
                    </button>
                </li>
            `).join("");
        }

        function addPlannerTask(e) {
            e.preventDefault();
            const timeVal = document.getElementById("plannerTimeInput").value || "08:00";
            const titleInput = document.getElementById("plannerTitleInput");
            const titleVal = titleInput.value.trim();
            if (!titleVal) return;

            plannerTasks.push({ id: Date.now(), time: timeVal, title: titleVal, done: false });
            titleInput.value = "";
            renderPlanner();
        }

        function deleteTask(id) {
            plannerTasks = plannerTasks.filter(t => t.id !== id);
            renderPlanner();
        }

        function toggleTask(id) {
            plannerTasks = plannerTasks.map(t => t.id === id ? { ...t, done: !t.done } : t);
            renderPlanner();
        }

        function shiftPlannerTasks(mins) {
            plannerTasks = plannerTasks.map(t => {
                if (t.done) return t;
                const [h, m] = t.time.split(":").map(Number);
                const total = (h * 60 + m + mins) % (24 * 60);
                return {
                    ...t,
                    time: `${String(Math.floor(total / 60)).padStart(2, "0")}:${String(total % 60).padStart(2, "0")}`
                };
            });
            renderPlanner();
        }

        function escapeHtml(str) {
            return str.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;");
        }

        renderPlanner();
    </script>
</body>
</html>
