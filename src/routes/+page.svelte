<script lang="ts">
	import Icon from '@iconify/svelte';
	import { onMount } from 'svelte';

	let isMenuOpen = false;

	onMount(() => {
		initParticles();
		initScrollReveal();
		initSmoothScroll();
	});

	function initParticles() {
		const container = document.getElementById('particles');
		if (!container) return;

		function createParticle() {
			const particle = document.createElement('div');
			particle.className = 'particle';
			particle.style.left = Math.random() * 100 + 'vw';
			particle.style.animationDelay = Math.random() * 8 + 's';
			particle.style.animationDuration = Math.random() * 3 + 5 + 's';
			particle.setAttribute('aria-hidden', 'true');
			container?.appendChild(particle);

			setTimeout(() => {
				if (particle.parentNode) {
					particle.remove();
				}
			}, 8000);
		}

		const intervalId = setInterval(createParticle, 300);

		// Cleanup function
		return () => clearInterval(intervalId);
	}

	function initScrollReveal() {
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						entry.target.classList.add('revealed');
					} else {
						entry.target.classList.remove('revealed');
					}
				});
			},
			{ threshold: 0.1, rootMargin: '50px' }
		);

		document.querySelectorAll('.scroll-reveal').forEach((el) => {
			observer.observe(el);
		});
	}

	function initSmoothScroll() {
		document.querySelectorAll('a[href^="#"]').forEach((anchor) => {
			anchor.addEventListener('click', function (e) {
				e.preventDefault();
				///@ts-expect-error
				const href = (this as HTMLAnchorElement).getAttribute('href');
				if (href) {
					const target = document.querySelector(href);
					if (target) {
						target.scrollIntoView({
							behavior: 'smooth',
							block: 'start'
						});
					}
				}
			});
		});
	}

	function toggleMenu() {
		isMenuOpen = !isMenuOpen;
	}
</script>

<svelte:head>
	<title>Noverna - High Quality Open Source Components</title>
	<meta name="description" content="Discover the power of Noverna - high quality open source components, tools and designs for modern developers." />
	<meta name="viewport" content="width=device-width, initial-scale=1" />
</svelte:head>

<main class="gradient-bg overflow-x-hidden text-white">
	<!-- Floating Background Elements -->
	<div class="pointer-events-none fixed inset-0 z-0" aria-hidden="true">
		<div class="floating-orb"></div>
		<div class="floating-orb"></div>
		<div class="floating-orb"></div>
	</div>

	<!-- Particle Effects -->
	<div id="particles" class="pointer-events-none fixed inset-0 z-10" aria-hidden="true"></div>

	<!-- Navigation -->
	<nav class="glass fixed top-0 z-50 w-full" role="navigation" aria-label="Main navigation">
		<div class="container mx-auto px-6 py-4">
			<div class="flex items-center justify-between">
				<a
					href="/"
					class="rounded-lg bg-gradient-to-r from-teal-400 to-emerald-400 bg-clip-text px-2 py-1 text-2xl font-bold text-transparent transition-transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-teal-400 focus:ring-offset-2 focus:ring-offset-slate-900"
					aria-label="Noverna - Go to homepage"
				>
					Noverna
				</a>

				<!-- Desktop Navigation -->
				<div class="hidden items-center space-x-8 md:flex">
					<a
						href="/docs"
						class="rounded px-2 py-1 text-slate-300 transition-all duration-300 hover:scale-110 hover:text-white focus:outline-none focus:ring-2 focus:ring-teal-400 focus:ring-offset-2 focus:ring-offset-slate-900"
					>
						Documentation
					</a>
					<a
						href="https://github.com/noverna"
						class="rounded px-2 py-1 text-slate-300 transition-all duration-300 hover:scale-110 hover:text-white focus:outline-none focus:ring-2 focus:ring-teal-400 focus:ring-offset-2 focus:ring-offset-slate-900"
						target="_blank"
						rel="noopener noreferrer"
						aria-label="Visit our GitHub repository (opens in new tab)"
					>
						GitHub
					</a>
					<a
						href="/docs"
						class="pulse-on-hover rounded-lg bg-gradient-to-r from-teal-500 to-emerald-500 px-4 py-2 text-sm font-medium transition-transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-teal-400 focus:ring-offset-2 focus:ring-offset-slate-900"
					>
						Get Started
					</a>
				</div>

				<!-- Mobile Menu Button -->
				<button
					class="rounded p-2 focus:outline-none focus:ring-2 focus:ring-teal-400 focus:ring-offset-2 focus:ring-offset-slate-900 md:hidden"
					on:click={toggleMenu}
					aria-expanded={isMenuOpen}
					aria-label="Toggle mobile menu"
				>
					<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d={isMenuOpen ? 'M6 18L18 6M6 6l12 12' : 'M4 6h16M4 12h16M4 18h16'} />
					</svg>
				</button>
			</div>

			<!-- Mobile Menu -->
			{#if isMenuOpen}
				<div class="mt-4 border-t border-slate-700 pb-4 md:hidden">
					<div class="flex flex-col space-y-4 pt-4">
						<a href="/docs" class="text-slate-300 transition-colors hover:text-white">Documentation</a>
						<a href="https://github.com/noverna" class="text-slate-300 transition-colors hover:text-white" target="_blank" rel="noopener noreferrer">GitHub</a>
						<a href="/docs" class="rounded-lg bg-gradient-to-r from-teal-500 to-emerald-500 px-4 py-2 text-center text-sm font-medium">Get Started</a>
					</div>
				</div>
			{/if}
		</div>
	</nav>

	<div class="relative z-20">
		<!-- Hero Section -->
		<section class="relative flex min-h-screen items-center justify-center px-6 text-center">
			<div class="mx-auto max-w-6xl">
				<div class="mb-6">
					<span class="mb-8 inline-block rounded-full border border-teal-500/30 bg-gradient-to-r from-teal-500/20 to-emerald-500/20 px-4 py-2 text-sm font-medium text-teal-300">
						🚀 Open Source Excellence
					</span>
				</div>

				<h1 class="mb-8 text-4xl font-black leading-tight sm:text-5xl md:text-7xl lg:text-8xl">
					<span class="block">High Quality.</span>
					<span class="glitch block bg-gradient-to-r from-teal-400 via-emerald-400 to-cyan-400 bg-clip-text text-transparent"> Fully Open Source. </span>
				</h1>

				<p class="mx-auto mb-12 max-w-4xl text-lg leading-relaxed text-slate-300 sm:text-xl md:text-2xl">
					Discover the power of <strong>Noverna</strong> - where quality and innovation converge. <br class="hidden sm:block" />
					High quality components, tools and designs, all at your fingertips.
				</p>

				<div class="flex flex-col items-center justify-center gap-6 sm:flex-row">
					<a
						href="/docs"
						class="pulse-on-hover group relative rounded-xl bg-gradient-to-r from-teal-500 to-emerald-500 px-10 py-4 text-lg font-bold shadow-2xl transition-all duration-300 hover:scale-110 focus:outline-none focus:ring-2 focus:ring-teal-400 focus:ring-offset-2 focus:ring-offset-slate-900"
					>
						<span class="relative z-10">Start Now</span>
						<div class="absolute inset-0 rounded-xl bg-gradient-to-r from-teal-600 to-emerald-600 opacity-0 transition-opacity group-hover:opacity-100"></div>
					</a>

					<a
						href="https://github.com/noverna"
						class="group rounded-xl border-2 border-slate-600 px-10 py-4 text-lg font-bold transition-all duration-300 hover:scale-110 hover:border-teal-400 hover:bg-teal-400/10 focus:outline-none focus:ring-2 focus:ring-teal-400 focus:ring-offset-2 focus:ring-offset-slate-900"
						target="_blank"
						rel="noopener noreferrer"
					>
						<span class="flex items-center">
							Discover on GitHub
							<svg class="ml-2 h-5 w-5 transition-transform group-hover:translate-x-1" fill="none" stroke="currentColor" viewBox="0 0 24 24" aria-hidden="true">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
							</svg>
						</span>
					</a>
				</div>

				<div class="mt-16">
					<div class="flex flex-col items-center justify-center space-y-6 text-slate-400 sm:flex-row sm:space-x-8 sm:space-y-0">
						<div class="text-center">
							<div class="text-2xl font-bold text-teal-400">3+</div>
							<div class="text-sm">Components</div>
						</div>
						<div class="hidden h-12 w-px bg-slate-600 sm:block"></div>
						<div class="text-center">
							<div class="text-2xl font-bold text-emerald-400">100%</div>
							<div class="text-sm">Open Source</div>
						</div>
						<div class="hidden h-12 w-px bg-slate-600 sm:block"></div>
						<div class="text-center">
							<div class="text-2xl font-bold text-cyan-400">AGPL 3.0</div>
							<div class="text-sm">License</div>
						</div>
					</div>
				</div>
			</div>
		</section>

		<!-- Features Section -->
		<section class="px-6 py-32" id="features">
			<div class="container mx-auto">
				<div class="scroll-reveal revealed mb-20 text-center">
					<h2 class="mb-6 text-3xl font-black sm:text-4xl md:text-5xl">
						Why <span class="bg-gradient-to-r from-teal-400 to-emerald-400 bg-clip-text text-transparent">Noverna</span>?
					</h2>
					<p class="mx-auto text-lg text-slate-400 sm:text-xl">
						The reason why you should choose Noverna is simple: we are truly <span class="font-bold text-emerald-400">open source</span>.
					</p>
				</div>

				<div class="grid grid-cols-1 gap-8 md:grid-cols-3">
					<div class="glass hover-lift scroll-reveal group rounded-2xl p-8">
						<div class="mb-6 flex h-16 w-16 items-center justify-center rounded-2xl bg-gradient-to-br from-teal-500 to-teal-600 transition-transform group-hover:scale-110">
							<svg class="h-8 w-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24" aria-hidden="true">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
							</svg>
						</div>
						<h3 class="mb-4 text-2xl font-bold text-teal-400">100% Open</h3>
						<p class="leading-relaxed text-slate-300">No hidden fees, no hidden licenses, no hidden costs. Just quality software as it should be.</p>
					</div>

					<div class="glass hover-lift scroll-reveal group rounded-2xl p-8">
						<div class="mb-6 flex h-16 w-16 items-center justify-center rounded-2xl bg-gradient-to-br from-emerald-500 to-emerald-600 transition-transform group-hover:scale-110">
							<svg class="h-8 w-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24" aria-hidden="true">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
							</svg>
						</div>
						<h3 class="mb-4 text-2xl font-bold text-emerald-400">Enterprise Ready</h3>
						<p class="leading-relaxed text-slate-300">Sophisticatedly developed, extensively tested and documented. Ready for critical production environments.</p>
					</div>

					<div class="glass hover-lift scroll-reveal group rounded-2xl p-8">
						<div class="mb-6 flex h-16 w-16 items-center justify-center rounded-2xl bg-gradient-to-br from-purple-500 to-purple-600 transition-transform group-hover:scale-110">
							<svg class="h-8 w-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24" aria-hidden="true">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M7 21a4 4 0 01-4-4V5a2 2 0 012-2h4a2 2 0 012 2v12a4 4 0 01-4 4zM21 5a2 2 0 00-2-2h-4a2 2 0 00-2 2v12a4 4 0 004 4h4a2 2 0 002-2V5z"
								/>
							</svg>
						</div>
						<h3 class="mb-4 text-2xl font-bold text-purple-400">Modern Design</h3>
						<p class="leading-relaxed text-slate-300">Contemporary, elegant and user-friendly. Developed with a focus on accessibility and performance.</p>
					</div>
				</div>
			</div>
		</section>

		<!-- Technologies Section -->
		<section class="px-6 py-32" id="technologies">
			<div class="container mx-auto">
				<div class="scroll-reveal mb-20 text-center">
					<h2 class="mb-6 text-3xl font-black sm:text-4xl md:text-5xl">
						Built for <span class="bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-transparent">Developers</span>
					</h2>
					<p class="mx-auto text-lg text-slate-400 sm:text-xl">We only use modern frameworks and cutting-edge tools</p>
				</div>

				<div class="grid grid-cols-2 gap-6 md:grid-cols-4">
					<div class="glass hover-lift scroll-reveal flex flex-col items-center justify-center rounded-xl p-6 transition-all duration-300 hover:border-orange-400/50">
						<Icon icon="skill-icons:typescript" class="mb-4 text-4xl" aria-hidden="true" />
						<h4 class="text-lg font-bold">TypeScript</h4>
					</div>
					<div class="glass hover-lift scroll-reveal flex flex-col items-center justify-center rounded-xl p-6 transition-all duration-300 hover:border-orange-400/50">
						<Icon icon="skill-icons:svelte" class="mb-4 text-4xl" aria-hidden="true" />
						<h4 class="text-lg font-bold">Svelte</h4>
					</div>
					<div class="glass hover-lift scroll-reveal flex flex-col items-center justify-center rounded-xl p-6 transition-all duration-300 hover:border-orange-400/50">
						<Icon icon="simple-icons:fivem" class="mb-4 text-4xl" style="color: #ae6f07" aria-hidden="true" />
						<h4 class="text-lg font-bold">Cfx.re</h4>
					</div>
					<div class="glass hover-lift scroll-reveal flex flex-col items-center justify-center rounded-xl p-6 transition-all duration-300 hover:border-blue-400/50">
						<Icon icon="simple-icons:netcup" class="mb-4 text-4xl" style="color: #114a66" aria-hidden="true" />
						<h4 class="text-lg font-bold">NetCup</h4>
					</div>
				</div>
			</div>
		</section>

		<!-- CTA Section -->
		<section class="px-6 py-32" id="cta">
			<div class="container mx-auto">
				<div class="glass hover-lift scroll-reveal rounded-3xl p-8 text-center sm:p-12">
					<h2 class="mb-6 text-3xl font-black sm:text-4xl md:text-5xl">
						Ready to <span class="bg-gradient-to-r from-teal-400 to-emerald-400 bg-clip-text text-transparent">innovate</span>?
					</h2>
					<p class="mx-auto mb-10 text-lg text-slate-300 sm:text-xl">Become part of the community and start your next project with the best open source tools.</p>

					<div class="flex flex-col justify-center gap-6 sm:flex-row">
						<a
							href="/docs"
							class="pulse-on-hover rounded-xl bg-gradient-to-r from-teal-500 to-emerald-500 px-10 py-4 text-lg font-bold shadow-2xl transition-all duration-300 hover:scale-110 focus:outline-none focus:ring-2 focus:ring-teal-400 focus:ring-offset-2 focus:ring-offset-slate-900"
						>
							Start Documentation
						</a>
						<a
							href="https://github.com/noverna"
							class="rounded-xl border-2 border-slate-600 px-10 py-4 text-lg font-bold transition-all duration-300 hover:scale-110 hover:border-teal-400 hover:bg-teal-400/10 focus:outline-none focus:ring-2 focus:ring-teal-400 focus:ring-offset-2 focus:ring-offset-slate-900"
							target="_blank"
							rel="noopener noreferrer"
						>
							View Code on GitHub
						</a>
					</div>
				</div>
			</div>
		</section>
	</div>

	<!-- Footer -->
	<footer class="glass border-t border-slate-700/50 py-12" role="contentinfo">
		<div class="container mx-auto px-6 text-center">
			<div class="mb-8">
				<h3 class="mb-4 bg-gradient-to-r from-teal-400 to-emerald-400 bg-clip-text text-2xl font-bold text-transparent">Noverna</h3>
				<p class="mx-auto text-slate-400">Building the future of open-source development, one component at a time.</p>
			</div>

			<div class="mb-8 flex flex-col justify-center space-y-4 sm:flex-row sm:space-x-8 sm:space-y-0">
				<a
					href="https://github.com/noverna"
					class="rounded px-2 py-1 text-slate-400 transition-colors hover:text-white focus:outline-none focus:ring-2 focus:ring-teal-400 focus:ring-offset-2 focus:ring-offset-slate-900"
					target="_blank"
					rel="noopener noreferrer"
				>
					GitHub
				</a>
				<a href="/docs" class="rounded px-2 py-1 text-slate-400 transition-colors hover:text-white focus:outline-none focus:ring-2 focus:ring-teal-400 focus:ring-offset-2 focus:ring-offset-slate-900">
					Documentation
				</a>
				<a
					href="/community"
					class="rounded px-2 py-1 text-slate-400 transition-colors hover:text-white focus:outline-none focus:ring-2 focus:ring-teal-400 focus:ring-offset-2 focus:ring-offset-slate-900"
				>
					Community
				</a>
			</div>

			<div class="border-t border-slate-700/50 pt-8">
				<p class="text-slate-500">
					Made with
					<span class="animate-pulse text-emerald-400" aria-label="love">💚</span>
					by the Noverna Team © 2025
				</p>
			</div>
		</div>
	</footer>
</main>

<style>
	/* Animated gradient background */
	.gradient-bg {
		background: linear-gradient(-45deg, #0f172a, #1e293b, #0c4a6e, #164e63);
		background-size: 400% 400%;
		animation: gradientShift 15s ease infinite;
	}

	@keyframes gradientShift {
		0% {
			background-position: 0% 50%;
		}
		50% {
			background-position: 100% 50%;
		}
		100% {
			background-position: 0% 50%;
		}
	}

	/* Floating orbs animation */
	.floating-orb {
		position: absolute;
		border-radius: 50%;
		background: linear-gradient(45deg, rgba(20, 184, 166, 0.3), rgba(16, 185, 129, 0.2));
		filter: blur(40px);
		animation: float 20s infinite linear;
	}

	.floating-orb:nth-child(1) {
		width: 300px;
		height: 300px;
		top: 10%;
		left: 10%;
		animation-delay: 0s;
	}

	.floating-orb:nth-child(2) {
		width: 200px;
		height: 200px;
		top: 60%;
		right: 15%;
		animation-delay: -7s;
	}

	.floating-orb:nth-child(3) {
		width: 250px;
		height: 250px;
		bottom: 20%;
		left: 50%;
		animation-delay: -14s;
	}

	@keyframes float {
		0%,
		100% {
			transform: translateY(0px) rotate(0deg);
		}
		33% {
			transform: translateY(-30px) rotate(120deg);
		}
		66% {
			transform: translateY(20px) rotate(240deg);
		}
	}

	/* Glass morphism effect */
	.glass {
		background: rgba(15, 23, 42, 0.7);
		backdrop-filter: blur(20px);
		border: 1px solid rgba(255, 255, 255, 0.1);
	}

	/* Smooth hover animations */
	.hover-lift {
		transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.hover-lift:hover {
		transform: translateY(-8px) scale(1.02);
		box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
	}

	/* Glitch effect for hero text */
	.glitch {
		position: relative;
		animation: glitch 3s infinite;
	}

	@keyframes glitch {
		0%,
		100% {
			transform: translate(0);
		}
		20% {
			transform: translate(-2px, 2px);
		}
		40% {
			transform: translate(-2px, -2px);
		}
		60% {
			transform: translate(2px, 2px);
		}
		80% {
			transform: translate(2px, -2px);
		}
	}

	/* Pulse animation for buttons */
	.pulse-on-hover:hover {
		animation: pulse 2s infinite;
	}

	@keyframes pulse {
		0% {
			box-shadow: 0 0 0 0 rgba(20, 184, 166, 0.7);
		}
		70% {
			box-shadow: 0 0 0 10px rgba(20, 184, 166, 0);
		}
		100% {
			box-shadow: 0 0 0 0 rgba(20, 184, 166, 0);
		}
	}

	/* Particle effect */
	.particle {
		position: absolute;
		width: 2px;
		height: 2px;
		background: rgba(20, 184, 166, 0.8);
		border-radius: 50%;
		animation: particle-float 8s infinite linear;
	}

	@keyframes particle-float {
		0% {
			transform: translateY(100vh) translateX(0);
			opacity: 0;
		}
		10% {
			opacity: 1;
		}
		90% {
			opacity: 1;
		}
		100% {
			transform: translateY(-100px) translateX(100px);
			opacity: 0;
		}
	}

	/* Scroll reveal animation */
	.scroll-reveal {
		opacity: 0;
		transform: translateY(50px);
		transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
	}

	.scroll-reveal.revealed {
		opacity: 1;
		transform: translateY(0);
	}

	/* Reduced motion for accessibility */
	@media (prefers-reduced-motion: reduce) {
		.gradient-bg {
			animation: none;
		}

		.floating-orb {
			animation: none;
		}

		.glitch {
			animation: none;
		}

		.particle {
			animation: none;
		}

		.scroll-reveal {
			opacity: 1;
			transform: none;
		}

		.hover-lift:hover {
			transform: none;
		}

		.pulse-on-hover:hover {
			animation: none;
		}
	}

	/* Responsive improvements */
	@media (max-width: 640px) {
		.hero-title {
			font-size: 2.5rem;
			line-height: 1.1;
		}

		.hero-subtitle {
			font-size: 1.125rem;
		}
	}
</style>
