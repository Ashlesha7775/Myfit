# Myfit
html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>My Fit Journal</title>
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  <meta name="theme-color" content="#0d1117">
  
  <!-- Tailwind CSS CDN -->
  <script src="https://tailwindcss.com"></script>
  
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            brand: {
              green: '#1b4332',
              accent: '#00E676',
              coral: '#E07A5F',
              bgLight: '#F4F6F8',
              bgDark: '#0D1117',
              cardDark: '#161B22',
            }
          }
        }
      }
    }
  </script>

  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      -webkit-tap-highlight-color: transparent;
    }
    .glass-card {
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
    }
    .no-scrollbar::-webkit-scrollbar { display: none; }
    .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
  </style>
</head>
<body class="bg-brand-bgLight dark:bg-brand-bgDark text-slate-800 dark:text-slate-100 min-h-screen pb-24 transition-colors duration-300">

  <!-- TOP HEADER -->
  <header class="sticky top-0 z-30 px-5 py-4 bg-white/80 dark:bg-brand-cardDark/80 glass-card border-b border-slate-200 dark:border-slate-800 flex justify-between items-center">
    <div>
      <h1 class="text-xl font-extrabold tracking-tight bg-gradient-to-r from-emerald-600 to-teal-500 bg-clip-text text-transparent">My Fit Journal</h1>
      <p class="text-xs text-slate-500 dark:text-slate-400 font-medium">Elegant Indian Wellness Tracker</p>
    </div>
    <div class="flex items-center gap-2">
      <div class="flex items-center gap-1.5 px-3 py-1 bg-amber-500/10 text-amber-600 dark:text-amber-400 rounded-full text-xs font-bold border border-amber-500/20">
        <svg xmlns="http://w3.org" width="14" height="14" viewBox="0 0 24 24" fill="currentColor" class="text-amber-500"><path d="M12 2c1 3 2.5 3.5 3.5 4.5A5 5 0 0 1 17 10a5 5 0 1 1-10 0c0-.3 0-.6.1-.9a2 2 0 1 0 3.3-2C8 4.5 11 2 12 2Z"/></svg>
        <span id="streak-count">1</span> Day Streak
      </div>
      <button onclick="toggleTheme()" class="p-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300 hover:bg-slate-200 dark:hover:bg-slate-700 transition">
        <span class="dark:hidden">🌙</span>
        <span class="hidden dark:block">☀️</span>
      </button>
    </div>
  </header>

  <!-- MAIN DASHBOARD CONTENT -->
  <main class="max-w-md mx-auto px-4 pt-4 space-y-4">
    
    <!-- MOTIVATIONAL TOP ACCENT -->
    <div class="p-4 rounded-2xl bg-gradient-to-br from-emerald-900/10 to-teal-900/10 border border-emerald-500/10">
      <p id="quote-text" class="text-xs font-medium italic text-slate-600 dark:text-slate-300 text-center">"Consistency is the core of premium health."</p>
    </div>

    <!-- METRICS TARGET CALCULATOR & SUMMARY -->
    <div class="p-5 rounded-3xl bg-white dark:bg-brand-cardDark border border-slate-200/80 dark:border-slate-800 shadow-sm space-y-4">
      <div class="flex justify-between items-start">
        <div>
          <h3 class="text-xs font-bold text-slate-400 uppercase tracking-wider">Calorie Balance</h3>
          <div class="text-3xl font-black mt-1 tracking-tight flex items-baseline gap-1">
            <span id="net-cal">0</span>
            <span class="text-xs font-normal text-slate-400">kcal net</span>
          </div>
        </div>
        <button onclick="openSetupModal()" class="text-xs font-bold px-3 py-1.5 bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 rounded-xl transition">
          ⚙️ Setup Target
        </button>
      </div>

      <!-- DETAILED CALORIE MATH -->
      <div class="grid grid-cols-3 gap-2 text-center text-xs py-2 bg-slate-50 dark:bg-slate-800/40 rounded-xl border border-slate-100 dark:border-slate-800/40">
        <div>
          <span class="text-slate-400 block text-[10px] uppercase font-bold">Goal Target</span>
          <span id="target-cal" class="font-bold text-slate-700 dark:text-slate-200">2000</span>
        </div>
        <div>
          <span class="text-slate-400 block text-[10px] uppercase font-bold">Food Intake</span>
          <span id="consumed-cal" class="font-bold text-emerald-500">+0</span>
        </div>
        <div>
          <span class="text-slate-400 block text-[10px] uppercase font-bold">Workout Burn</span>
          <span id="burned-cal" class="font-bold text-rose-400">-0</span>
        </div>
      </div>

      <!-- PROGRESS TRACK BAR -->
      <div class="space-y-1.5">
        <div class="w-full bg-slate-100 dark:bg-slate-800 h-2.5 rounded-full overflow-hidden">
          <div id="cal-progress-bar" class="bg-gradient-to-r from-emerald-500 to-emerald-400 h-full w-0 transition-all duration-500"></div>
        </div>
        <div class="flex justify-between text-[11px] font-semibold text-slate-400">
          <span id="remaining-label">2000 kcal left</span>
          <span id="progress-percent">0%</span>
        </div>
      </div>

      <!-- MACRO DISTRIBUTION -->
      <div class="grid grid-cols-3 gap-3 pt-2 text-center">
        <div class="border-t border-slate-100 dark:border-slate-800/60 pt-2">
          <span class="text-[9px] font-bold text-slate-400 block tracking-wider">PROTEIN</span>
          <span class="text-sm font-black text-blue-500"><span id="protein-val">0</span> / <span id="target-protein">120</span>g</span>
        </div>
        <div class="border-t border-slate-100 dark:border-slate-800/60 pt-2">
          <span class="text-[9px] font-bold text-slate-400 block tracking-wider">CARBS</span>
          <span class="text-sm font-black text-amber-500"><span id="carbs-val">0</span> / <span id="target-carbs">230</span>g</span>
        </div>
        <div class="border-t border-slate-100 dark:border-slate-800/60 pt-2">
          <span class="text-[9px] font-bold text-slate-400 block tracking-wider">FATS</span>
          <span class="text-sm font-black text-rose-500"><span id="fats-val">0</span> / <span id="target-fats">65</span>g</span>
        </div>
      </div>
    </div>

    <!-- SEARCH & LOG INTERFACE -->
    <div class="p-4 rounded-3xl bg-white dark:bg-brand-cardDark border border-slate-200/80 dark:border-slate-800 shadow-sm space-y-4">
      <div class="flex border-b border-slate-100 dark:border-slate-800 pb-2 gap-4">
        <button onclick="switchLogTab('food')" id="btn-tab-food" class="text-sm font-bold text-emerald-500 pb-1 border-b-2 border-emerald-500 transition">Log Indian Diet</button>
        <button onclick="switchLogTab('workout')" id="btn-tab-workout" class="text-sm font-bold text-slate-400 pb-1 border-b-2 border-transparent transition">Log Workouts</button>
      </div>

      <!-- FOOD SEARCH PANEL -->
      <div id="panel-log-food" class="space-y-3">
        <div class="relative">
          <input type="text" id="food-search-input" oninput="filterFood()" placeholder="Search chicken, paneer, lassi, chai, dosa..." class="w-full pl-9 pr-4 py-2.5 rounded-xl bg-slate-50 dark:bg-slate-800/80 text-sm border border-slate-200 dark:border-slate-700/80 focus:outline-none focus:border-emerald-500 text-slate-800 dark:text-slate-100">
          <span class="absolute left-3 top-3 text-slate-400 text-sm">🔍</span>
        </div>

        <!-- SEARCH RESULTS CONTAINER -->
        <div id="food-search-results" class="max-h-48 overflow-y-auto divide-y divide-slate-100 dark:divide-slate-800 custom-scrollbar pr-1 hidden">
          <!-- Dynamically populated -->
        </div>
      </div>

      <!-- WORKOUT LOGGER PANEL -->
      <div id="panel-log-workout" class="space-y-3 hidden">
        <div class="grid grid-cols-2 gap-2">
          <select id="workout-select" class="p-2.5 rounded-xl bg-slate-50 dark:bg-slate-800 text-xs border border-slate-200 dark:border-slate-700 focus:outline-none">
            <option value="yoga">Yoga / Surya Namaskar</option>
            <option value="running">Running / Jogging</option>
            <option value="walking">Brisk Walking</option>
            <option value="gym">Weight Lifting / Gym</option>
            <option value="cycling">Cycling</option>
            <option value="cricket">Cricket / Sports</option>
          </select>
          <input type="number" id="workout-duration" placeholder="Duration (mins)" class="p-2.5 rounded-xl bg-slate-50 dark:bg-slate-800 text-xs border border-slate-200 dark:border-slate-700 focus:outline-none text-slate-800 dark:text-slate-100">
        </div>
        <button onclick="addWorkoutLog()" class="w-full py-2.5 rounded-xl bg-slate-900 dark:bg-slate-100 text-white dark:text-slate-900 font-bold text-xs hover:opacity-90 transition">
          Add Workout Burn
        </button>
      </div>
    </div>

    <!-- HYDRATION COUNTER -->
    <div class="p-4 rounded-2xl bg-white dark:bg-brand-cardDark border border-slate-200/80 dark:border-slate-800 shadow-sm flex items-center justify-between">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 rounded-xl bg-blue-500/10 flex items-center justify-center text-blue-500 font-bold text-lg">💧</div>
        <div>
          <h4 class="text-xs font-bold uppercase tracking-wider text-slate-400">Hydration Tracker</h4>
          <p class="text-sm font-black mt-0.5"><span id="water-count">0</span> / 8 <span class="text-xs font-medium text-slate-400">Glasses (250ml)</span></p>
        </div>
      </div>
      <div class="flex items-center gap-1.5">