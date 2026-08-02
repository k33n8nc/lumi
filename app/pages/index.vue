<template>
  <div class="p-6 md:p-10 min-h-screen bg-lumi-white flex flex-col gap-10">

    <!-- Grid Test -->
    <section class="p-6 bg-white rounded-xl shadow-sm border border-slate-200">
      <span class="text-xs uppercase tracking-wider text-slate-500 font-semibold">3. Responsive Grid Test</span>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mt-4">
        <div class="p-4 bg-lumi-navy text-lumi-white rounded-lg shadow font-medium">Card 1 (Col 1)</div>
        <div class="p-4 bg-lumi-yellow text-lumi-navy rounded-lg shadow font-medium">Card 2 (Col 2)</div>
        <div class="p-4 bg-slate-100 text-lumi-navy border border-slate-300 rounded-lg shadow font-medium">Card 3 (Col 3)</div>
      </div>
    </section>

    <!-- Global Plain Headings Test (@layer base) -->
    <section class="p-6 bg-white rounded-xl shadow-sm border border-slate-200">
      <span class="text-xs uppercase tracking-wider text-slate-500 font-semibold">4. Global Plain Headings (@layer base - no utility classes applied)</span>
      <div class="mt-4 flex flex-col gap-4 text-lumi-navy">
        <h1>Plain Global Step Sizing</h1>
        <h2>Plain Global Step Sizing</h2>
        <h3>Plain Global Step Sizing</h3>
      </div>
    </section>

  </div>
</template>
