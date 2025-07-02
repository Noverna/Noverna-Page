<script lang="ts">
	import { onMount } from 'svelte';

	onMount(() => {
		document.title = 'Noverna - Coming Soon';
	});
</script>

<div class="relative flex min-h-screen flex-col items-center justify-center overflow-hidden bg-slate-900 px-4 text-white">
	<!-- Hintergrundverlauf -->
	<div class="absolute inset-0 -z-10 bg-gradient-to-r from-teal-400/10 via-emerald-400/10 to-slate-600/10 opacity-30 blur-3xl"></div>

	<!-- Dekorative Partikel (optional: ersetzen durch Canvas später) -->
	<div class="pointer-events-none absolute inset-0 -z-10">
		<div class="h-full w-full animate-pulse bg-[radial-gradient(ellipse_at_top_left,_var(--tw-gradient-stops))] from-teal-400/5 via-emerald-300/5 to-transparent blur-3xl"></div>
	</div>

	<div class="absolute left-4 top-4">
		<a href="/" class="text-2xl font-bold text-teal-400 hover:text-teal-500">Zurück</a>
	</div>

	<!-- Inhalt -->
	<div class="text-center">
		<h1 class="text-5xl font-bold text-teal-400 md:text-6xl">Noverna</h1>
		<p class="mt-4 text-lg text-slate-300 md:text-xl">Wir arbeiten gerade an etwas Großem. Bleib dran – unsere Open-Source-Plattform für hochwertige Ressourcen startet bald.</p>

		<!-- E-Mail-Benachrichtigung (optional) -->
		<form class="mt-8 flex flex-col items-center justify-center gap-4 sm:flex-row">
			<input
				type="email"
				placeholder="E-Mail-Adresse"
				class="w-full rounded-md border border-slate-700 bg-slate-800 px-4 py-2 text-white placeholder-slate-400 focus:outline-none focus:ring-2 focus:ring-teal-400 sm:w-auto"
			/>
			<button type="submit" class="rounded-md bg-gradient-to-r from-teal-400 to-emerald-400 px-6 py-2 font-semibold text-slate-900 shadow-lg transition-transform hover:scale-105">
				Benachrichtigen
			</button>
		</form>

		<!-- Footer -->
		<p class="mt-12 text-sm text-slate-500">© {new Date().getFullYear()} Noverna. Alle Rechte vorbehalten.</p>
	</div>
</div>
