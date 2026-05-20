<!DOCTYPE html>
<html lang="nl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dossier: De Verloren Oppervlaktematen</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Special+Elite&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #a855f7;
            --secondary: #0f172a;
            --accent: #eab308;
            --success: #22c55e;
            --error: #ef4444;
            --terminal: #22c55e;
        }

        body {
            font-family: 'Share Tech Mono', monospace;
            background-color: var(--secondary);
            background-image: radial-gradient(circle, #1e1b4b 0%, #0f172a 100%);
            background-attachment: fixed;
        }

        .detective-font {
            font-family: 'Special Elite', cursive;
        }

        .custom-glow {
            box-shadow: 0 0 15px rgba(168, 85, 247, 0.4);
        }

        .terminal-glow {
            box-shadow: 0 0 15px rgba(34, 197, 94, 0.2);
        }

        .quiz-input {
            background-color: #0f172a !important;
            color: #eab308 !important;
        }

        /* Custom scrollbar for terminal vibes */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #1e293b;
        }
        ::-webkit-scrollbar-thumb {
            background: #475569;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #a855f7;
        }
    </style>
</head>
<body class="text-slate-200 min-h-screen p-4 md:p-8">

<div class="max-w-6xl mx-auto bg-slate-900/90 border-2 border-slate-700 rounded-xl shadow-2xl overflow-hidden relative custom-glow">
    
    <!-- Stamp: CONFIDENTIAL -->
    <div class="absolute top-6 right-6 pointer-events-none z-10 select-none opacity-20 md:opacity-40">
        <div class="detective-font border-4 border-red-500 text-red-500 text-2xl md:text-3xl font-bold uppercase tracking-wider px-4 py-2 rotate-12">
            STRIKT GEHEIM
        </div>
    </div>

    <!-- Header Section -->
    <header class="border-b-2 border-slate-700 p-6 bg-slate-950/80">
        <h1 class="text-3xl md:text-4xl text-yellow-500 font-bold uppercase tracking-widest text-center detective-font mb-2">
            Case File: De Verloren Oppervlaktematen
        </h1>
        <p class="text-center text-slate-400 text-sm md:text-base tracking-widest uppercase">
            [ Systeemstatus: Actief | AI Integratie ingeschakeld ]
        </p>
    </header>

    <section class="bg-slate-950 border-b border-slate-700 p-4">
        <div class="flex flex-col md:flex-row items-center justify-between gap-4">
            <div class="flex items-center gap-3">
                <span class="flex h-3 w-3 relative">
                    <span id="keyStatusPulse" class="animate-ping absolute inline-flex h-full w-full rounded-full bg-red-400 opacity-75"></span>
                    <span id="keyStatusIndicator" class="relative inline-flex rounded-full h-3 w-3 bg-red-500"></span>
                </span>
                <p class="text-sm font-semibold tracking-wide" id="apiStatusText">Gemini AI Offline (Geen Sleutel)</p>
            </div>
            <div class="w-full md:w-auto flex items-center gap-2">
                <input type="password" id="apiKeyInput" placeholder="Voer Gemini API Key in..." class="bg-slate-900 border border-slate-600 rounded px-3 py-1 text-sm text-yellow-500 focus:outline-none focus:border-purple-500 w-full md:w-64" />
                <button onclick="saveApiKey()" class="bg-purple-600 hover:bg-purple-700 text-white text-sm font-bold px-4 py-1.5 rounded transition uppercase tracking-wider shrink-0">
                    Koppel
                </button>
            </div>
        </div>
        <p class="text-[11px] text-slate-500 mt-2 text-center md:text-left">
            * Je API-sleutel wordt veilig lokaal bewaard. Heb je geen sleutel? De app draait automatisch op een geavanceerde lokale wiskunde-simulator!
        </p>
    </section>

    <!-- Interactive Map & Video Section -->
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 p-6">
        
        <!-- Left column: Evidence and schema -->
        <div class="lg:col-span-7 space-y-6">
            
            <div class="flex flex-col sm:flex-row gap-4 justify-between items-center bg-slate-950/50 p-4 rounded-lg border border-slate-800">
                <button class="bg-slate-800 hover:bg-slate-700 text-yellow-500 border border-yellow-500/50 px-4 py-2 rounded font-bold uppercase text-xs tracking-wider transition w-full sm:w-auto" onclick="toggleVideo()">
                    [ GEGEVENS-TAPE AFSPELEN ]
                </button>
                <div class="text-xs text-slate-400 uppercase text-center sm:text-right">
                    Case ID: <span class="text-purple-400 font-bold">#OPP-30-2026</span>
                </div>
            </div>

            <div class="video-wrapper hidden" id="videoWrapper">
                <iframe id="youtubeIframe" class="w-full aspect-video rounded-lg border border-slate-700" src="https://www.youtube.com/embed/tRvaALumlW0" frameborder="0" allowfullscreen></iframe>
            </div>

            <!-- Mystery Image Frame -->
            <div class="bg-slate-950 p-4 rounded-lg border-2 border-slate-800 relative">
                <h3 class="text-center text-yellow-500 font-bold uppercase tracking-wider mb-3 detective-font">Het Geheime Bewijsstuk</h3>
                <div class="relative w-full aspect-video bg-black rounded overflow-hidden max-w-md mx-auto border border-slate-800">
                    <img id="evidenceImage" src="https://images.unsplash.com/photo-1502134249126-9f3755a50d78?q=80&w=1000&auto=format&fit=crop" alt="Geheim Bewijsstuk" onerror="this.src='https://placehold.co/500x375/111111/f1c40f?text=GEHEIM+BEWIJSSTUK'" class="w-full h-full object-cover">
                    <div class="overlay-grid absolute inset-0 grid grid-cols-6 grid-rows-5 gap-[1px]" id="overlayGrid">
                        <!-- Tiles dynamically injected -->
                    </div>
                </div>
                <p class="text-center text-[11px] text-slate-500 mt-2">Los de cases hieronder op om puzzelstukken van het gecensureerde bewijsmateriaal te verwijderen.</p>
            </div>

            <div class="bg-slate-950/80 p-4 rounded-lg border border-slate-800 flex flex-col gap-3">
                <!-- Ladder Schema Container (optimised for full visibility on all screens) -->
                <div class="w-full flex items-center justify-between text-center select-none">
                    <!-- Unit Box km² -->
                    <div class="flex flex-col items-center flex-shrink">
                        <div class="w-7 h-7 sm:w-10 sm:h-10 md:w-12 md:h-12 bg-slate-900 border border-slate-700 rounded-lg flex items-center justify-center font-bold text-yellow-500 text-[10px] sm:text-xs md:text-base">km²</div>
                    </div>
                    <!-- Arrow -->
                    <div class="flex-grow flex flex-col items-center justify-center text-[7px] sm:text-[9px] md:text-[10px] text-slate-600 min-w-0 px-0.5 relative">
                        <span class="text-emerald-500 font-bold leading-none">x100</span>
                        <div class="w-full h-[1px] bg-slate-700 my-1 relative after:content-['▶'] after:absolute after:right-0 after:-top-[5px] after:text-[6px] sm:after:text-[8px]"></div>
                        <span class="text-red-500 font-bold leading-none">:100</span>
                    </div>

                    <!-- Unit Box hm² -->
                    <div class="flex flex-col items-center flex-shrink">
                        <div class="w-7 h-7 sm:w-10 sm:h-10 md:w-12 md:h-12 bg-slate-900 border border-slate-700 rounded-lg flex items-center justify-center font-bold text-yellow-500 text-[10px] sm:text-xs md:text-base">hm²</div>
                    </div>
                    <!-- Arrow -->
                    <div class="flex-grow flex flex-col items-center justify-center text-[7px] sm:text-[9px] md:text-[10px] text-slate-600 min-w-0 px-0.5 relative">
                        <span class="text-emerald-500 font-bold leading-none">x100</span>
                        <div class="w-full h-[1px] bg-slate-700 my-1 relative after:content-['▶'] after:absolute after:right-0 after:-top-[5px] after:text-[6px] sm:after:text-[8px]"></div>
                        <span class="text-red-500 font-bold leading-none">:100</span>
                    </div>

                    <!-- Unit Box dam² -->
                    <div class="flex flex-col items-center flex-shrink">
                        <div class="w-7 h-7 sm:w-10 sm:h-10 md:w-12 md:h-12 bg-slate-900 border border-slate-700 rounded-lg flex items-center justify-center font-bold text-yellow-500 text-[10px] sm:text-xs md:text-base">dam²</div>
                    </div>
                    <!-- Arrow -->
                    <div class="flex-grow flex flex-col items-center justify-center text-[7px] sm:text-[9px] md:text-[10px] text-slate-600 min-w-0 px-0.5 relative">
                        <span class="text-emerald-500 font-bold leading-none">x100</span>
                        <div class="w-full h-[1px] bg-slate-700 my-1 relative after:content-['▶'] after:absolute after:right-0 after:-top-[5px] after:text-[6px] sm:after:text-[8px]"></div>
                        <span class="text-red-500 font-bold leading-none">:100</span>
                    </div>

                    <!-- Unit Box m² -->
                    <div class="flex flex-col items-center flex-shrink">
                        <div class="w-7 h-7 sm:w-10 sm:h-10 md:w-12 md:h-12 bg-slate-900 border-2 border-purple-500 rounded-lg flex items-center justify-center font-bold text-yellow-500 text-[10px] sm:text-xs md:text-base">m²</div>
                    </div>
                    <!-- Arrow -->
                    <div class="flex-grow flex flex-col items-center justify-center text-[7px] sm:text-[9px] md:text-[10px] text-slate-600 min-w-0 px-0.5 relative">
                        <span class="text-emerald-500 font-bold leading-none">x100</span>
                        <div class="w-full h-[1px] bg-slate-700 my-1 relative after:content-['▶'] after:absolute after:right-0 after:-top-[5px] after:text-[6px] sm:after:text-[8px]"></div>
                        <span class="text-red-500 font-bold leading-none">:100</span>
                    </div>

                    <!-- Unit Box dm² -->
                    <div class="flex flex-col items-center flex-shrink">
                        <div class="w-7 h-7 sm:w-10 sm:h-10 md:w-12 md:h-12 bg-slate-900 border border-slate-700 rounded-lg flex items-center justify-center font-bold text-yellow-500 text-[10px] sm:text-xs md:text-base">dm²</div>
                    </div>
                    <!-- Arrow -->
                    <div class="flex-grow flex flex-col items-center justify-center text-[7px] sm:text-[9px] md:text-[10px] text-slate-600 min-w-0 px-0.5 relative">
                        <span class="text-emerald-500 font-bold leading-none">x100</span>
                        <div class="w-full h-[1px] bg-slate-700 my-1 relative after:content-['▶'] after:absolute after:right-0 after:-top-[5px] after:text-[6px] sm:after:text-[8px]"></div>
                        <span class="text-red-500 font-bold leading-none">:100</span>
                    </div>

                    <!-- Unit Box cm² -->
                    <div class="flex flex-col items-center flex-shrink">
                        <div class="w-7 h-7 sm:w-10 sm:h-10 md:w-12 md:h-12 bg-slate-900 border border-slate-700 rounded-lg flex items-center justify-center font-bold text-yellow-500 text-[10px] sm:text-xs md:text-base">cm²</div>
                    </div>
                    <!-- Arrow -->
                    <div class="flex-grow flex flex-col items-center justify-center text-[7px] sm:text-[9px] md:text-[10px] text-slate-600 min-w-0 px-0.5 relative">
                        <span class="text-emerald-500 font-bold leading-none">x100</span>
                        <div class="w-full h-[1px] bg-slate-700 my-1 relative after:content-['▶'] after:absolute after:right-0 after:-top-[5px] after:text-[6px] sm:after:text-[8px]"></div>
                        <span class="text-red-500 font-bold leading-none">:100</span>
                    </div>

                    <!-- Unit Box mm² -->
                    <div class="flex flex-col items-center flex-shrink">
                        <div class="w-7 h-7 sm:w-10 sm:h-10 md:w-12 md:h-12 bg-slate-900 border border-slate-700 rounded-lg flex items-center justify-center font-bold text-yellow-500 text-[10px] sm:text-xs md:text-base">mm²</div>
                    </div>
                </div>

                <!-- Mnemonic text placed beautifully directly under the entire schema -->
                <div class="text-center bg-slate-900/40 p-2.5 rounded border border-slate-800 mt-1">
                    <span class="text-[9px] text-slate-500 uppercase tracking-widest block mb-0.5">Ezelsbruggetje</span>
                    <div class="text-xs sm:text-sm md:text-base text-yellow-500 font-bold uppercase tracking-wider font-mono">
                        <span class="text-purple-400 underline decoration-purple-500/50">K</span>rijgt 
                        <span class="text-purple-400 underline decoration-purple-500/50">H</span>ij 
                        <span class="text-purple-400 underline decoration-purple-500/50">D</span>an 
                        <span class="text-purple-400 underline decoration-purple-500/50">M</span>aar 
                        <span class="text-purple-400 underline decoration-purple-500/50">D</span>rie 
                        <span class="text-purple-400 underline decoration-purple-500/50">C</span>akejes 
                        <span class="text-purple-400 underline decoration-purple-500/50">M</span>ee?
                    </div>
                    <span class="text-[9px] text-slate-400 block mt-1">
                        Elke stap naar rechts is <span class="text-emerald-400 font-bold">x100</span> • Elke stap naar links is <span class="text-red-400 font-bold">:100</span>
                    </span>
                </div>
            </div>

        </div>

        <!-- Right column: Interactive AI Control Panel -->
        <div class="lg:col-span-5 space-y-6">
            
            <div class="bg-slate-950 p-4 rounded-lg border border-purple-500/50 relative overflow-hidden bg-gradient-to-br from-slate-950 to-slate-900">
                <div class="absolute -top-10 -right-10 w-24 h-24 bg-purple-600/10 rounded-full blur-xl"></div>
                
                <h3 class="text-purple-400 font-bold uppercase text-sm tracking-widest mb-2 flex items-center gap-2">
                    <span>📡</span> AI Grounded Case Generator
                </h3>
                <p class="text-xs text-slate-400 mb-4 leading-relaxed">
                    Gebruik Google Search via de Gemini-intelligentie om direct cases te maken over echte plekken of onderwerpen op aarde!
                </p>

                <div class="space-y-3">
                    <label class="block text-[11px] text-slate-400 uppercase tracking-wider">Thema of Locatie:</label>
                    <div class="flex gap-2">
                        <input type="text" id="groundedThemeInput" placeholder="Bijv: Nederlandse meren, Formule 1 circuits, Efteling..." class="bg-slate-900 border border-slate-700 rounded px-3 py-1.5 text-xs text-yellow-500 focus:outline-none focus:border-purple-500 flex-grow" />
                        <button onclick="generateGroundedCases()" id="btnGroundedCase" class="bg-purple-600 hover:bg-purple-700 text-white text-xs font-bold px-4 py-1.5 rounded uppercase tracking-wider transition flex items-center gap-1">
                            <span id="groundedLoader" class="hidden animate-spin h-3.5 w-3.5 border-2 border-white border-t-transparent rounded-full"></span>
                            <span>Zoek & Bouw</span>
                        </button>
                    </div>
                    <div id="searchCitationPanel" class="hidden text-[11px] bg-slate-900 p-2 rounded border border-slate-800 text-slate-400">
                        <span class="text-yellow-500 font-bold">Gebruikte bronnen:</span>
                        <ul id="citationList" class="list-disc list-inside mt-1 space-y-1"></ul>
                    </div>
                </div>
            </div>

            <div class="bg-slate-950 border border-emerald-500/30 rounded-lg overflow-hidden terminal-glow flex flex-col h-[320px]">
                <div class="bg-slate-900 px-4 py-2 border-b border-emerald-500/20 flex items-center justify-between">
                    <span class="text-emerald-400 text-xs tracking-widest uppercase font-bold flex items-center gap-1.5">
                        <span class="h-2 w-2 rounded-full bg-emerald-500 animate-pulse"></span> Terminal: Rechercheur Pi
                    </span>
                    <button onclick="clearTerminalChat()" class="text-slate-500 hover:text-red-400 text-[10px] uppercase tracking-wider">Wis log</button>
                </div>
                
                <!-- Chat log -->
                <div id="terminalChatLog" class="p-4 flex-grow overflow-y-auto space-y-3 text-xs font-mono">
                    <div class="text-emerald-500">
                        &gt; [Systeem] Welkom bij het wiskunde-detective netwerk. Ik ben Rechercheur Pi. Stel me gerust al je vragen over het decoderen van oppervlaktes!
                    </div>
                </div>

                <!-- Quick buttons -->
                <div class="p-2 border-t border-slate-800 bg-slate-950 flex gap-1 overflow-x-auto text-[10px]">
                    <button onclick="askTerminal('Hoe werkt dam² naar cm²?')" class="bg-slate-900 hover:bg-slate-800 text-yellow-500/80 hover:text-yellow-500 border border-slate-800 hover:border-slate-700 px-2.5 py-1 rounded whitespace-nowrap">
                        Hoe werkt dam²?
                    </button>
                    <button onclick="askTerminal('Geef me een ezelsbruggetje tip!')" class="bg-slate-900 hover:bg-slate-800 text-yellow-500/80 hover:text-yellow-500 border border-slate-800 hover:border-slate-700 px-2.5 py-1 rounded whitespace-nowrap">
                        Ezelsbruggetje tip
                    </button>
                    <button onclick="askTerminal('Vertel me een flauwe detective grap over wiskunde')" class="bg-slate-900 hover:bg-slate-800 text-yellow-500/80 hover:text-yellow-500 border border-slate-800 hover:border-slate-700 px-2.5 py-1 rounded whitespace-nowrap">
                        Wiskunde-grap
                    </button>
                </div>

                <!-- Chat inputs -->
                <div class="p-2 border-t border-slate-800 bg-slate-900 flex gap-2">
                    <input type="text" id="terminalInput" placeholder="Stel een vraag aan Rechercheur Pi..." onkeydown="handleTerminalKey(event)" class="bg-slate-950 border border-slate-700 rounded px-3 py-1.5 text-xs text-yellow-500 focus:outline-none focus:border-emerald-500 flex-grow" />
                    <button onclick="sendTerminalMessage()" class="bg-emerald-600 hover:bg-emerald-700 text-white font-bold px-4 rounded text-xs transition uppercase">Verstuur</button>
                </div>
            </div>

        </div>

    </div>

    <main class="p-6 border-t-2 border-slate-700">
        
        <div class="flex flex-col sm:flex-row justify-between items-center gap-4 mb-6">
            <div>
                <h2 class="text-xl text-yellow-500 font-bold uppercase tracking-wider detective-font">Actief Onderzoeks Dossier</h2>
                <p class="text-xs text-slate-400">Vul het juiste antwoord in en druk op <span class="text-emerald-400 font-bold">ENTER</span> of klik erbuiten.</p>
            </div>
            
            <div class="flex gap-2">
                <button id="btnGenQuestions" class="bg-slate-800 hover:bg-slate-700 text-purple-400 hover:text-purple-300 border border-purple-500/30 px-4 py-2 rounded text-xs font-bold uppercase tracking-wider transition flex items-center gap-2" onclick="generateNewQuestions()">
                    <span>[ GENEREEER STANDAARD CASES ]</span>
                    <span id="standardLoader" class="hidden animate-spin h-3.5 w-3.5 border-2 border-purple-400 border-t-transparent rounded-full"></span>
                </button>
            </div>
        </div>

        <!-- Scores and coins -->
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-6">
            <div class="bg-slate-950 p-4 rounded-lg border border-slate-800 text-center flex flex-col justify-center">
                <span class="text-xs text-slate-400 uppercase tracking-wider">Opgeloste Cases</span>
                <span id="scoreBoard" class="text-2xl font-bold text-slate-100 mt-1">OPGELOST: 0 / 30</span>
            </div>
            <div class="bg-slate-950 p-4 rounded-lg border border-slate-800 flex items-center justify-center gap-4">
                <div id="coinIcon" class="w-12 h-12 bg-yellow-500 rounded-full flex items-center justify-center border-4 border-yellow-700 text-slate-950 font-bold text-2xl shadow-lg shadow-yellow-500/20 select-none">★</div>
                <div class="text-left">
                    <span class="text-xs text-slate-400 uppercase tracking-wider">Gouden Bewijsstukken</span>
                    <h4 id="coinCount" class="text-xl font-bold text-yellow-500">0 GOUDEN BEWIJZEN</h4>
                </div>
            </div>
        </div>

        <!-- Grid with dynamic question modules -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6" id="quizGrid">
            <!-- Injected dynamically via JavaScript -->
        </div>

    </main>

    <!-- Custom Dialog / Toast alert -->
    <div id="toastNotification" class="fixed bottom-6 right-6 bg-slate-950 border-2 border-purple-500 text-slate-100 text-xs font-mono p-4 rounded-lg shadow-2xl z-50 max-w-sm hidden transition-all duration-300">
        <!-- Injected via helper -->
    </div>

</div>

<script>
    // Load and manage API key from local storage
    let localApiKey = localStorage.getItem("GEMINI_API_KEY") || "";
    document.getElementById("apiKeyInput").value = localApiKey;

    function saveApiKey() {
        const inputVal = document.getElementById("apiKeyInput").value.trim();
        localStorage.setItem("GEMINI_API_KEY", inputVal);
        localApiKey = inputVal;
        updateKeyStatus();
        showToast("Gemini API sleutel succesvol gekoppeld en bewaard!");
    }

    function updateKeyStatus() {
        const pulse = document.getElementById("keyStatusPulse");
        const dot = document.getElementById("keyStatusIndicator");
        const label = document.getElementById("apiStatusText");
        if (localApiKey) {
            pulse.classList.remove("bg-red-400");
            pulse.classList.add("bg-emerald-400");
            dot.classList.remove("bg-red-500");
            dot.classList.add("bg-emerald-500");
            label.textContent = "Gemini AI Gekoppeld (Online)";
            label.classList.add("text-emerald-400");
        } else {
            pulse.classList.remove("bg-emerald-400");
            pulse.classList.add("bg-red-400");
            dot.classList.remove("bg-emerald-500");
            dot.classList.add("bg-red-500");
            label.textContent = "Gemini AI Offline (Geen Sleutel)";
            label.classList.remove("text-emerald-400");
        }
    }

    let currentQuestions = [
        { q: "65 cm² = ... dm²", a: "0.65", u: "dm²" },
        { q: "4650 cm² = ... m²", a: "0.465", u: "m²" },
        { q: "3450 dm² = ... m²", a: "34.5", u: "m²" },
        { q: "0,35 km² = ... hm²", a: "35", u: "hm²" },
        { q: "4,5 hm² = ... dam²", a: "450", u: "dam²" },
        { q: "2,6 dam² = ... m²", a: "260", u: "m²" },
        { q: "1,2 m² = ... cm²", a: "12000", u: "cm²" },
        { q: "800 mm² = ... cm²", a: "8", u: "cm²" },
        { q: "0,5 m² = ... dm²", a: "50", u: "dm²" },
        { q: "75 dam² = ... hm²", a: "0.75", u: "hm²" },
        { q: "12,5 dm² = ... mm²", a: "125000", u: "mm²" },
        { q: "0,02 km² = ... m²", a: "20000", u: "m²" },
        { q: "950 m² = ... dam²", a: "9.5", u: "dam²" },
        { q: "4,8 hm² = ... m²", a: "48000", u: "m²" },
        { q: "32 mm² = ... cm²", a: "0.32", u: "cm²" },
        { q: "0,005 m² = ... cm²", a: "50", u: "cm²" },
        { q: "125 m² = ... hm²", a: "0.0125", u: "hm²" },
        { q: "0,9 dm² = ... cm²", a: "90", u: "cm²" },
        { q: "5500 mm² = ... cm²", a: "55", u: "cm²" },
        { q: "0,3 dam² = ... dm²", a: "3000", u: "dm²" },
        { q: "15 cm² = ... mm²", a: "1500", u: "mm²" },
        { q: "0,15 km² = ... m²", a: "150000", u: "m²" },
        { q: "720 dm² = ... m²", a: "7.2", u: "m²" },
        { q: "1,5 hm² = ... dam²", a: "150", u: "dam²" },
        { q: "40 cm² = ... m²", a: "0.004", u: "m²" },
        { q: "0,06 dam² = ... cm²", a: "600000", u: "cm²" },
        { q: "90000 mm² = ... dm²", a: "9", u: "dm²" },
        { q: "0,8 m² = ... dm²", a: "80", u: "dm²" },
        { q: "2,5 km² = ... hm²", a: "250", u: "hm²" },
        { q: "3000 cm² = ... m²", a: "0.3", u: "m²" }
    ];

    const quizGrid = document.getElementById('quizGrid');
    const overlayGrid = document.getElementById('overlayGrid');
    const scoreBoard = document.getElementById('scoreBoard');
    const coinCount = document.getElementById('coinCount');
    const coinIcon = document.getElementById('coinIcon');

    function showToast(message) {
        const toast = document.getElementById('toastNotification');
        toast.innerHTML = `<span class="text-purple-400 font-bold">INFO DECYPHER:</span> <p class="mt-1">${message}</p>`;
        toast.classList.remove('hidden');
        setTimeout(() => {
            toast.classList.add('hidden');
        }, 5000);
    }

    // Dynamic fetch caller to the Gemini API
    async function fetchGemini(prompt, systemInstruction, enableGrounding = false) {
        if (!localApiKey) {
            throw new Error("Geen API key gevonden.");
        }
        
        const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${localApiKey}`;
        const payload = {
            contents: [{ parts: [{ text: prompt }] }]
        };

        if (enableGrounding) {
            payload.tools = [{ "google_search": {} }];
        }

        if (systemInstruction) {
            payload.systemInstruction = {
                parts: [{ text: systemInstruction }]
            };
        }

        let retries = 3;
        let delay = 1000;
        
        for (let i = 0; i < retries; i++) {
            try {
                const response = await fetch(url, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });
                
                if (!response.ok) {
                    throw new Error(`API Status Error: ${response.status}`);
                }
                
                const result = await response.json();
                const candidate = result.candidates?.[0];
                const text = candidate?.content?.parts?.[0]?.text;
                
                // Extract search grounding metadata if present
                let sources = [];
                if (enableGrounding && candidate?.groundingMetadata?.groundingAttributions) {
                    sources = candidate.groundingMetadata.groundingAttributions
                        .map(attr => ({
                            uri: attr.web?.uri,
                            title: attr.web?.title,
                        }))
                        .filter(s => s.uri && s.title);
                }
                
                return { text, sources };
            } catch (err) {
                if (i === retries - 1) throw err;
                await new Promise(res => setTimeout(res, delay));
                delay *= 2;
            }
        }
    }

    async function generateGroundedCases() {
        const themeInput = document.getElementById('groundedThemeInput').value.trim();
        if (!themeInput) {
            showToast("Typ eerst een thema of locatie in om real-world cases te bouwen!");
            return;
        }

        const btn = document.getElementById('btnGroundedCase');
        const loader = document.getElementById('groundedLoader');
        btn.disabled = true;
        loader.classList.remove('hidden');

        // Check if API key is present
        if (!localApiKey) {
            // Simulated local real-world content for fallback
            setTimeout(() => {
                generateMockGrounded(themeInput);
                btn.disabled = false;
                loader.classList.add('hidden');
            }, 2000);
            return;
        }

        const systemPrompt = "Je bent een wiskundige detective. Je MOET echte wereldfacten en oppervlaktematen opzoeken (met de zoektool) over het gevraagde thema. Bouw exact 5 unieke en interessante wiskundeomrekenpuzzels in een spannend detectiveverhaal. Bijvoorbeeld: De oppervlakte van de Eiffeltoren, een sportveld, provincie, etc. Geef de output ENKEL en ALLEEN als een JSON array van objecten met de velden: q (de somtekst inclusief context, bijv 'Het circuit van Spa-Francorchamps beslaat 1,4 km². Reken om: 1.4 km² = ... hm²'), a (het antwoord als string met punt decimalen, bijv '140'), u (de doeleenheid, bijv 'hm²'), story (een kort, grappig detective-mysterieverhaal van 1 à 2 zinnen waarom deze berekening nodig is).";
        const prompt = `Genereer 5 unieke oppervlaktematen puzzels gebaseerd op werkelijke opzoekbare feiten over het thema: "${themeInput}".`;

        try {
            const { text, sources } = await fetchGemini(prompt, systemPrompt, true);
            const cleanJson = text.replace(/```json/g, '').replace(/```/g, '').trim();
            const newQuestions = JSON.parse(cleanJson);
            
            if (Array.isArray(newQuestions)) {
                // Prepend or replace the current question list
                currentQuestions = newQuestions;
                renderQuiz();
                renderOverlay(newQuestions.length);
                
                // Show source citations
                const citationPanel = document.getElementById('searchCitationPanel');
                const citationList = document.getElementById('citationList');
                citationList.innerHTML = '';
                
                if (sources && sources.length > 0) {
                    sources.slice(0, 3).forEach(src => {
                        const li = document.createElement('li');
                        li.innerHTML = `<a href="${src.uri}" target="_blank" class="text-purple-400 hover:underline font-semibold">${src.title}</a>`;
                        citationList.appendChild(li);
                    });
                    citationPanel.classList.remove('hidden');
                } else {
                    citationPanel.classList.add('hidden');
                }
                
                showToast(`Succesvol 5 real-world cases gegenereerd over "${themeInput}"!`);
            }
        } catch (error) {
            console.error(error);
            showToast("Fout bij het laden via de Gemini Search-grounding. We starten de lokale simulator...");
            generateMockGrounded(themeInput);
        } finally {
            btn.disabled = false;
            loader.classList.add('hidden');
        }
    }

    // Local Mock Generator in case of missing key or API issues
    function generateMockGrounded(theme) {
        const generated = [
            {
                q: `De hoofdlocatie van "${theme}" is geschat op een oppervlakte van 12,5 hm². Rechercheur, we moeten dit weten in dam². Omrekenen: 12,5 hm² = ... dam²`,
                a: "1250",
                u: "dam²",
                story: "De bende van de Gecensureerde Cirkel heeft documenten begraven op exact 10 meter van de rand. Bereken de perimeter!"
            },
            {
                q: `De dader ontsnapte in een helikopter en wierp bewijs af boven een sector van 0,45 km². Reken om naar m²: 0,45 km² = ... m²`,
                a: "450000",
                u: "m²",
                story: "Onze zoekhonden hebben een specifiek gebied nodig om de modderige laarzen van de dader op te sporen."
            },
            {
                q: `Er is een geheime code verborgen op een microfilm van 800 mm². Hoe groot is dit in cm²? 800 mm² = ... cm²`,
                a: "8",
                u: "cm²",
                story: "De vergrootlens van de forensische afdeling kan enkel bewijsmateriaal groter dan 5 cm² focussen."
            },
            {
                q: `We vonden een platplattegrond van "${theme}" met een verdacht gemarkeerde zone van 3200 dm². Reken dit om naar m²: 3200 dm² = ... m²`,
                a: "32",
                u: "m²",
                story: "We vermoeden dat de verborgen kluis zich exact onder een vloerkleed van deze afmetingen bevindt."
            },
            {
                q: `De perimeterbeveiliging van de kluis bestrijkt een oppervlakte van 0,05 hm². Reken om naar dm²: 0,05 hm² = ... dm²`,
                a: "50000",
                u: "dm²",
                story: "Als we de sensoren verkeerd instellen, gaat het alarm direct af en ontsnappen de schurken via de riolering!"
            }
        ];
        currentQuestions = generated;
        renderQuiz();
        renderOverlay(generated.length);
        document.getElementById('searchCitationPanel').classList.add('hidden');
        showToast(`Lokale simulator heeft 5 fictieve mysteries gebouwd rondom "${theme}"!`);
    }

    async function askTerminal(text) {
        document.getElementById('terminalInput').value = text;
        sendTerminalMessage();
    }

    function handleTerminalKey(event) {
        if (event.key === 'Enter') {
            sendTerminalMessage();
        }
    }

    async function sendTerminalMessage() {
        const input = document.getElementById('terminalInput');
        const text = input.value.trim();
        if (!text) return;

        const chatLog = document.getElementById('terminalChatLog');
        
        // Render user message
        chatLog.innerHTML += `<div class="text-yellow-500 font-bold">&gt; Jij: ${text}</div>`;
        input.value = '';
        chatLog.scrollTop = chatLog.scrollHeight;

        // Render loading state
        const loadingId = "loader-" + Date.now();
        chatLog.innerHTML += `<div id="${loadingId}" class="text-emerald-500 italic animate-pulse">&gt; Rechercheur Pi is aan het typen...</div>`;
        chatLog.scrollTop = chatLog.scrollHeight;

        if (!localApiKey) {
            // Fast simulated responses for Rechercheur Pi
            setTimeout(() => {
                document.getElementById(loadingId).remove();
                let answer = "Interessante vraag! Mijn data-terminals tonen aan dat elke stap op onze trap (van 'Krijgt Hij Dan Maar Drie Cakejes Mee') een factor 100 is. Dus m² naar dm² is 1 stap naar rechts, dus vermenigvuldigen met 100! Koppel je Gemini API key om live te praten.";
                if (text.toLowerCase().includes("grap")) {
                    answer = "Waarom hebben wiskunde-detectives altijd een liniaal bij zich? Om de oppervlakte van de misdaad op te meten, centimeter voor centimeter! 🔍";
                }
                chatLog.innerHTML += `<div class="text-emerald-400">&gt; Rechercheur Pi: ${answer}</div>`;
                chatLog.scrollTop = chatLog.scrollHeight;
            }, 1000);
            return;
        }

        const systemPrompt = "Je bent Rechercheur Pi, een doorgewinterde detective-rechercheur die gespecialiseerd is in wiskunde-misdaden. Je bent droog, houdt van detective-slang en praat uiterst enthousiast over het omrekenen van oppervlaktematen met het ezelsbruggetje 'Krijgt Hij Dan Maar Drie Cakejes Mee'. Leg concepten simpel en humoristisch uit aan leerlingen.";
        
        try {
            const { text: responseText } = await fetchGemini(text, systemPrompt);
            document.getElementById(loadingId).remove();
            chatLog.innerHTML += `<div class="text-emerald-400">&gt; Rechercheur Pi: ${responseText}</div>`;
        } catch (error) {
            document.getElementById(loadingId).remove();
            chatLog.innerHTML += `<div class="text-red-400">&gt; Fout: Verbinding met AI-database mislukt. Probeer het opnieuw.</div>`;
        }
        chatLog.scrollTop = chatLog.scrollHeight;
    }

    function clearTerminalChat() {
        document.getElementById('terminalChatLog').innerHTML = `
            <div class="text-emerald-500">
                &gt; [Systeem] Terminal-geschiedenis gewist. Misdaadnetwerk gereed.
            </div>
        `;
    }

    async function generateNewQuestions() {
        const btn = document.getElementById('btnGenQuestions');
        const loader = document.getElementById('standardLoader');
        btn.disabled = true;
        loader.classList.remove('hidden');

        if (!localApiKey) {
            // Mock generate 30 default standard conversions
            setTimeout(() => {
                const units = ['mm²', 'cm²', 'dm²', 'm²', 'dam²', 'hm²', 'km²'];
                const generated = [];
                for(let i=0; i<30; i++) {
                    const fromIdx = Math.floor(Math.random() * units.length);
                    let toIdx = Math.floor(Math.random() * units.length);
                    while(toIdx === fromIdx) { toIdx = Math.floor(Math.random() * units.length); }
                    
                    const fromUnit = units[fromIdx];
                    const toUnit = units[toIdx];
                    
                    const diff = toIdx - fromIdx;
                    const baseVal = (Math.random() * 20 + 1).toFixed(Math.random() > 0.5 ? 1 : 0);
                    const mathVal = parseFloat(baseVal);
                    const factor = Math.pow(100, Math.abs(diff));
                    const calculatedAns = diff > 0 ? mathVal / factor : mathVal * factor;
                    
                    let formattedAns = calculatedAns.toString();
                    if (calculatedAns < 0.000001) {
                        formattedAns = calculatedAns.toFixed(10).replace(/\.?0+$/, "");
                    }
                    
                    generated.push({
                        q: `${baseVal.replace('.', ',')} ${fromUnit} = ... ${toUnit}`,
                        a: formattedAns,
                        u: toUnit,
                        story: "Een verdacht voertuig heeft sporen achtergelaten op dit terrein."
                    });
                }
                currentQuestions = generated;
                renderQuiz();
                renderOverlay(30);
                showToast("Succesvol 30 nieuwe standaard cases geladen!");
                btn.disabled = false;
                loader.classList.add('hidden');
            }, 1000);
            return;
        }

        const system = "Je bent een wiskunde leraar in een detective game. Genereer 30 unieke oefenvragen voor het omrekenen van OPPORVLAKTEMATEN (dus km², hm², dam², m², dm², cm², mm²). Denk eraan: elke stap op de trap is een factor 100 (x100 of :100). Geef de output ENKEL als een JSON array van objecten met de velden: q (bijv '5 m² = ... cm²'), a (het antwoord als string met een punt voor decimalen bijv '50000'), u (de doeleenheid bijv 'cm²'), story (een kort zinnetje met detective-sfeer).";
        const prompt = "Genereer 30 nieuwe onderzoeksvragen voor oppervlaktematen.";

        try {
            const { text } = await fetchGemini(prompt, system);
            const cleanJson = text.replace(/```json/g, '').replace(/```/g, '').trim();
            const newQuestions = JSON.parse(cleanJson);
            if (Array.isArray(newQuestions)) {
                currentQuestions = newQuestions;
                renderQuiz();
                renderOverlay(newQuestions.length); 
                showToast("Nieuwe cases succesvol gedownload via Gemini AI!");
            }
        } catch (error) {
            console.error(error);
            showToast("Kon geen AI-verbinding maken. Gebruik een geldige Gemini API key.");
        } finally {
            btn.disabled = false;
            loader.classList.add('hidden');
        }
    }

    async function helpWithQuestionStory(index) {
        const question = currentQuestions[index];
        const storyDiv = document.getElementById(`story-${index}`);
        const btn = document.getElementById(`storyBtn-${index}`);
        
        if (!storyDiv.classList.contains('hidden')) {
            storyDiv.classList.add('hidden');
            return;
        }

        storyDiv.classList.remove('hidden');
        storyDiv.innerHTML = `<span class="animate-pulse text-purple-400">Database doorspitten...</span>`;

        if (!localApiKey) {
            setTimeout(() => {
                storyDiv.innerHTML = `<div class="bg-slate-900 p-2.5 rounded border border-slate-700 text-[11px] text-slate-300">
                    <span class="text-purple-400 font-bold uppercase">CASE HISTORIE:</span> ${question.story || 'Dit kavel werd doorzocht door rechercheurs na een anonieme tip over verborgen documenten.'}
                </div>`;
            }, 800);
            return;
        }

        const systemPrompt = "Je bent een doorgewinterde detective. Schrijf een super meeslepend en grappig mini-misdaadscenario (maximaal 2 zinnen) waarom de speler deze specifieke oppervlaktemaat moet omrekenen. Gebruik hardcore detective jargon (zoals 'het lab', 'de hoofdverdachte', 'vingerafdrukken').";
        const prompt = `Bouw een verhaal rondom de som: "${question.q}"`;

        try {
            const { text } = await fetchGemini(prompt, systemPrompt);
            storyDiv.innerHTML = `<div class="bg-slate-900 p-2.5 rounded border border-slate-700 text-[11px] text-slate-300">
                <span class="text-purple-400 font-bold uppercase">CASE HISTORIE:</span> ${text}
            </div>`;
        } catch (error) {
            storyDiv.innerHTML = `<span class="text-red-400">Fout bij ophalen dossiergegevens.</span>`;
        }
    }

    function renderOverlay(totalTiles = 30) {
        overlayGrid.innerHTML = '';
        overlayGrid.style.gridTemplateColumns = `repeat(${Math.ceil(Math.sqrt(totalTiles))}, 1fr)`;
        
        for (let i = 0; i < totalTiles; i++) {
            const tile = document.createElement('div');
            tile.className = 'tile bg-slate-950/95 border border-slate-800 text-slate-500 flex items-center justify-center text-xs transition-all duration-700 ease-out select-none cursor-pointer hover:bg-slate-900';
            tile.id = `tile-${i}`;
            tile.innerText = i + 1;
            overlayGrid.appendChild(tile);
        }
    }

    function renderQuiz() {
        quizGrid.innerHTML = '';
        currentQuestions.forEach((item, index) => {
            const div = document.createElement('div');
            div.className = 'quiz-item bg-slate-950 p-4 rounded-lg border-l-4 border-slate-700 flex flex-col gap-3 transition-all duration-300 shadow-md';
            div.id = `item-${index}`;
            const label = item.q.split('=')[0].trim() + ' =';
            
            div.innerHTML = `
                <div class="flex justify-between items-center gap-2">
                    <span class="text-xs font-semibold uppercase tracking-wider text-slate-400">Case #${index+1}</span>
                    <button id="storyBtn-${index}" onclick="helpWithQuestionStory(${index})" class="text-[10px] bg-purple-950/50 text-purple-400 border border-purple-800/50 rounded px-2 py-0.5 hover:bg-purple-900 hover:text-white transition uppercase font-mono">
                        Dossier 🔍
                    </button>
                </div>
                <div class="text-sm font-semibold text-slate-200 leading-relaxed">${label}</div>
                <div class="input-wrapper">
                    <input type="text" class="quiz-input bg-slate-900 text-yellow-500 w-32 rounded border border-slate-700 px-3 py-1.5 focus:outline-none focus:border-purple-500" placeholder="Antwoord..." onkeydown="handleKeyDown(event, this, '${item.a}', ${index})" onblur="checkAnswer(this, '${item.a}', ${index})" oninput="clearFeedback(${index})">
                    <span class="text-xs font-bold text-slate-400 whitespace-nowrap">${item.u}</span>
                    <span class="feedback-icon ml-auto" id="feedback-${index}"></span>
                </div>
                <div id="story-${index}" class="hidden mt-2"></div>
            `;
            quizGrid.appendChild(div);
        });
        updateScore();
    }

    function handleKeyDown(event, input, correctAnswer, index) {
        if (event.key === 'Enter') {
            checkAnswer(input, correctAnswer, index);
        }
    }

    function clearFeedback(index) {
        const container = document.getElementById(`item-${index}`);
        const feedback = document.getElementById(`feedback-${index}`);
        if (container.classList.contains('border-emerald-500') || container.classList.contains('border-red-500')) {
            container.className = 'quiz-item bg-slate-950 p-4 rounded-lg border-l-4 border-slate-700 flex flex-col gap-3 transition-all duration-300 shadow-md';
            feedback.innerHTML = '';
            updateScore();
        }
    }

    function checkAnswer(input, correctAnswer, index) {
        const val = input.value.replace(',', '.').trim();
        const feedback = document.getElementById(`feedback-${index}`);
        const container = document.getElementById(`item-${index}`);
        const tile = document.getElementById(`tile-${index}`);
        const wasCorrect = container.classList.contains('border-emerald-500');
        
        if (val === "") {
            container.className = 'quiz-item bg-slate-950 p-4 rounded-lg border-l-4 border-slate-700 flex flex-col gap-3 transition-all duration-300 shadow-md';
            feedback.innerHTML = '';
        } else if (parseFloat(val) === parseFloat(correctAnswer)) {
            if (!wasCorrect) {
                coinIcon.classList.remove('collect-anim');
                void coinIcon.offsetWidth; 
                coinIcon.classList.add('collect-anim');
                
                // Animate and reveal evidence tile
                if (tile) {
                    tile.classList.add('opacity-0', 'scale-50', 'translate-y-[-50px]', 'rotate-45');
                    tile.style.pointerEvents = 'none';
                }
            }
            container.className = 'quiz-item bg-slate-900 p-4 rounded-lg border-l-4 border-emerald-500 flex flex-col gap-3 transition-all duration-300 shadow-md shadow-emerald-950/20';
            feedback.innerHTML = '<span class="text-emerald-500 font-bold">✔ CORRECT</span>';
        } else {
            container.className = 'quiz-item bg-slate-900 p-4 rounded-lg border-l-4 border-red-500 flex flex-col gap-3 transition-all duration-300 shadow-md shadow-red-950/20';
            feedback.innerHTML = '<span class="text-red-500 font-bold">✖ FOUT</span>';
        }
        updateScore();
    }

    function updateScore() {
        const corrects = document.querySelectorAll('.quiz-item.border-emerald-500').length;
        scoreBoard.textContent = `OPGELOST: ${corrects} / ${currentQuestions.length}`;
        coinCount.textContent = `${corrects} GOUDEN BEWIJZEN`;
    }

    function toggleVideo() {
        const wrapper = document.getElementById('videoWrapper');
        if (wrapper.classList.contains('hidden')) {
            wrapper.classList.remove('hidden');
        } else {
            wrapper.classList.add('hidden');
        }
    }

    // Initialize gameplay
    window.onload = function() {
        updateKeyStatus();
        renderOverlay(30);
        renderQuiz();
    };
</script>

</body>
</html>
