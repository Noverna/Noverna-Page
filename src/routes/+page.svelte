<script lang="ts">
	import Icon from '@iconify/svelte';
	import { onMount } from 'svelte';
	import { fade, fly, scale } from 'svelte/transition';

	let mounted = false;
	let scrollY = 0;
	let heroRef: HTMLElement;

	onMount(() => {
		mounted = true;

		// Warte bis alle Elemente gerendert sind
		setTimeout(() => {
			// Smooth reveal animations
			const observer = new IntersectionObserver(
				(entries) => {
					entries.forEach((entry) => {
						console.log('Entry:', entry.target.className, 'isIntersecting:', entry.isIntersecting);
						if (entry.isIntersecting) {
							console.log('Adding animate-in to:', entry.target.className);
							entry.target.classList.add('animate-in');
						}
					});
				},
				{ threshold: 0.1 }
			);

			const elements = document.querySelectorAll('.animate-on-scroll');
			console.log('Found elements:', elements.length);
			elements.forEach((el) => {
				console.log('Observing:', el.className);
				observer.observe(el);
			});

			// Clean up function
			return () => {
				observer.disconnect();
			};
		}, 100);

		// Parallax scrolling
		const handleScroll = () => {
			scrollY = window.scrollY;
		};

		window.addEventListener('scroll', handleScroll);
		return () => window.removeEventListener('scroll', handleScroll);
	});

	let stats = {
		// Later create an API for requesting this stats
		projects: 5,
		contributors: 0,
		stars: 0
	};

	let features = [
		{
			icon: 'lucide:rocket',
			title: 'Lightning-Fast Development',
			description: 'From idea to deployment in minutes with modern tooling'
		},
		{
			icon: 'lucide:shield-check',
			title: 'Enterprise-Grade Security',
			description: 'Top-tier security standards with 99.9% guaranteed uptime'
		},
		{
			icon: 'lucide:puzzle',
			title: 'Modular Architecture',
			description: 'Flexible building blocks for any application and use case'
		},
		{
			icon: 'lucide:heart',
			title: 'Developer First',
			description: 'Built by the community, for the community — fully open source'
		}
	];

	let projects = [
		{
			name: 'Noverna Core',
			description: 'A modern modular core for a TypeScript-based game framework',
			tech: ['Svelte', 'TypeScript', 'Tailwind', 'Inversify'],
			stars: 0,
			color: 'from-blue-500 to-cyan-500',
			status: 'active'
		},
		{
			// TODO: Planned
			name: 'NovAPI',
			description: 'Scalable microservice starter built for games and live servers',
			tech: ['Go', 'Docker', 'Kubernetes', 'Postgres', 'Redis'],
			stars: 0,
			color: 'from-purple-500 to-pink-500',
			status: 'planned'
		},
		{
			// TODO: Planned
			name: 'DevTools Pro',
			description: 'CLI tools for scaffolding, building and managing modded game resources',
			tech: ['TypeScript', 'Bun', 'CLI'],
			stars: 0,
			color: 'from-green-500 to-emerald-500',
			status: 'planned'
		},
		{
			// TODO: Planned
			name: 'NoveCache',
			description: 'Game-specific cache and asset layer for low-latency multiplayer experiences',
			tech: ['Go', 'TypeScript', 'Redis', 'CLI'],
			stars: 0,
			color: 'from-red-500 to-rose-500',
			status: 'planned'
		}
	];
</script>

<svelte:window bind:scrollY />

{#if mounted}
	<main class="bg-primary relative min-h-screen overflow-hidden text-white">
		<!-- Animated Background -->
		<div class="pointer-events-none fixed inset-0">
			<div class="absolute inset-0 bg-gradient-to-br from-blue-900/10 via-purple-900/10 to-pink-900/10"></div>
			<div class="absolute left-1/4 top-1/4 h-96 w-96 animate-pulse rounded-full bg-blue-500/5 blur-3xl"></div>
			<div class="absolute right-1/4 top-3/4 h-96 w-96 animate-pulse rounded-full bg-purple-500/5 blur-3xl delay-1000"></div>
			<div class="delay-2000 absolute bottom-1/4 left-1/2 h-96 w-96 animate-pulse rounded-full bg-pink-500/5 blur-3xl"></div>
		</div>

		<!-- Navigation -->
		<header class="fixed top-0 z-50 w-full">
			<nav class="glass-nav border-b border-white/10 bg-black/20 backdrop-blur-xl">
				<div class="container mx-auto flex h-20 items-center justify-between px-6">
					<div class="flex items-center gap-3" in:fly={{ x: -50, duration: 800 }}>
						<img src="/logo_finish.png" alt="Noverna Logo" class="h-12" />
					</div>

					<div class="flex gap-8 font-medium" in:fly={{ x: 50, duration: 800 }}>
						<a href="#home" class="nav-link group">
							<span>Home</span>
							<div class="nav-underline"></div>
						</a>
						<a href="#projects" class="nav-link group">
							<span>Projects</span>
							<div class="nav-underline"></div>
						</a>
						<a href="#docs" class="nav-link group">
							<span>Docs</span>
							<div class="nav-underline"></div>
						</a>
						<a href="#contact" class="nav-link group">
							<span>Contact</span>
							<div class="nav-underline"></div>
						</a>
					</div>

					<!-- Later navigate to the login Page or Member Page -->
					<div class="btn-member">
						<button class="">Member</button>
					</div>
				</div>
			</nav>
		</header>

		<!-- Hero Section -->
		<section class="relative flex min-h-screen items-center justify-center pt-20" bind:this={heroRef}>
			<div class="container relative z-10 mx-auto px-6 text-center">
				<div class="mx-auto">
					{#if mounted}
						<h1 class="hero-title mb-8 text-6xl font-bold leading-tight md:text-8xl" in:fade={{ duration: 1000 }} style="transform: translateY({scrollY * 0.2}px)">
							<span class="bg-gradient-to-r from-blue-400 via-purple-400 to-pink-400 bg-clip-text text-transparent"> Open Source. </span>
							<br />
							<span class="text-white">Newly Designed.</span>
						</h1>

						<p class="mb-12 text-xl leading-relaxed text-gray-300 md:text-2xl" in:fade={{ delay: 300, duration: 1000 }}>
							We're building the next generation of open-source tools.<br />
							Modern technology. Intuitive APIs. A flawless developer experience.
						</p>

						<div class="mb-16 flex flex-col justify-center gap-6 sm:flex-row" in:fade={{ delay: 600, duration: 1000 }}>
							<button class="btn-primary group">
								<Icon icon="lucide:rocket" class="mr-2 transition-transform group-hover:rotate-12" />
								Get Started
							</button>
							<button class="btn-secondary group">
								<Icon icon="lucide:github" class="mr-2 transition-transform group-hover:scale-110" />
								Explore on GitHub
							</button>
						</div>
					{/if}

					<!-- Stats -->
					<div class="mt-16 grid grid-cols-1 gap-8 md:grid-cols-3">
						{#each Object.entries(stats) as [key, value], i}
							<div class="stat-card animate-on-scroll" style="animation-delay: {i * 100}ms">
								<div class="stat-number mb-2 bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-4xl font-bold text-transparent">
									{value}+
								</div>
								<div class="stat-label capitalize text-gray-400">
									{key === 'projects' ? 'Projects' : key === 'contributors' ? 'Contributors' : 'GitHub Stars'}
								</div>
							</div>
						{/each}
					</div>
				</div>
			</div>
		</section>

		<!-- Projects Section -->
		<section class="relative py-24" id="projects">
			<div class="container mx-auto px-6">
				<div class="animate-on-scroll mb-16 text-center">
					<h2 class="mb-6 bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-5xl font-bold text-transparent">Our Projects</h2>
					<p class="mx-auto text-xl text-gray-300">High quality open source projects including Planned ones</p>
				</div>

				<div class="grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-3">
					{#each projects as project, i}
						<div class="project-card animate-on-scroll" style="animation-delay: {i * 150}ms">
							<div class="project-header bg-gradient-to-r {project.color} rounded-t-2xl p-6">
								<h3 class="mb-2 text-2xl font-bold text-white">{project.name}</h3>
								<p class="text-white/90">{project.description}</p>
							</div>
							<div class="project-body p-6">
								<div class="mb-4 flex flex-wrap gap-2">
									{#each project.tech as tech}
										<span class="rounded-full bg-white/10 px-3 py-1 text-sm text-gray-300">
											{tech}
										</span>
									{/each}
								</div>
								<div class="flex items-center justify-between">
									<div class="flex items-center gap-2 text-gray-400">
										<Icon icon="lucide:star" class="text-yellow-400" />
										<span>{project.stars}</span>
									</div>
									<button class="project-link">
										<Icon icon="lucide:external-link" />
									</button>
								</div>
							</div>
						</div>
					{/each}
				</div>
			</div>
		</section>

		<!-- Features Section -->
		<section class="relative py-24">
			<div class="container mx-auto px-6">
				<div class="animate-on-scroll mb-16 text-center">
					<h2 class="mb-6 text-5xl font-bold text-white">
						Why <span class="bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-transparent">Noverna?</span>
					</h2>
					<p class="mx-auto text-xl text-gray-300">We are using the latest technologies and best practices.</p>
				</div>

				<div class="grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-4">
					{#each features as feature, i}
						<div class="feature-card animate-on-scroll" style="animation-delay: {i * 100}ms">
							<div class="feature-icon mb-8">
								<Icon icon={feature.icon} class="text-4xl" />
							</div>
							<h3 class="mb-3 mt-4 text-xl font-bold text-white">{feature.title}</h3>
							<p class="text-gray-300">{feature.description}</p>
						</div>
					{/each}
				</div>
			</div>
		</section>

		<!-- Getting Started Section -->
		<section class="relative py-24">
			<div class="container mx-auto px-6">
				<div class="glass-container rounded-3xl p-12">
					<div class="animate-on-scroll mb-16 text-center">
						<h2 class="mb-6 text-5xl font-bold text-white">
							How to <span class="bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-transparent">Start?</span>
						</h2>
						<p class="text-xl text-gray-300">In just a few steps you can start using Noverna Resources.</p>
					</div>

					<div class="grid grid-cols-1 gap-8 md:grid-cols-3">
						{#each [{ icon: 'lucide:search', title: 'Find a Project', desc: 'Find the perfect project for your desire' }, { icon: 'lucide:download', title: 'Easy Install', desc: 'Mostly a few resources and you are ready to go' }, { icon: 'lucide:zap', title: 'Starting', desc: 'All that with a few Steps, to start your Journey' }] as step, i}
							<div class="step-card animate-on-scroll" style="animation-delay: {i * 150}ms">
								<div class="step-number">
									<span>{i + 1}</span>
								</div>
								<Icon icon={step.icon} class="mb-4 text-3xl text-blue-400" />
								<h3 class="mb-2 text-xl font-bold text-white">{step.title}</h3>
								<p class="text-gray-300">{step.desc}</p>
							</div>
						{/each}
					</div>
				</div>
			</div>
		</section>

		<!-- Community Section -->
		<section class="relative py-24">
			<div class="container mx-auto px-6">
				<div class="community-cta text-center">
					<div class="animate-on-scroll">
						<h2 class="mb-6 text-5xl font-bold text-white">
							Join the <span class="bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-transparent">Community</span>
						</h2>
						<p class="mx-auto mb-12 text-xl text-gray-300">Join the Noverna Community and share your knowledge with other members.</p>

						<div class="flex flex-col justify-center gap-6 sm:flex-row">
							<button class="btn-discord group">
								<Icon icon="lucide:message-circle" class="mr-2 transition-transform group-hover:scale-110" />
								Our Discord
							</button>
							<button class="btn-github group">
								<Icon icon="lucide:github" class="mr-2 transition-transform group-hover:rotate-12" />
								Our Github
							</button>
						</div>
					</div>
				</div>
			</div>
		</section>

		<!-- Footer -->
		<footer class="border-t border-white/10 bg-black/20 backdrop-blur-xl">
			<div class="container mx-auto px-6 py-16">
				<div class="grid grid-cols-1 gap-8 md:grid-cols-4">
					<div class="footer-brand">
						<div class="mb-4 flex items-center gap-3">
							<div class="flex h-10 w-10 items-center justify-center rounded-xl bg-gradient-to-r from-blue-500 to-purple-500">
								<Icon icon="lucide:code" class="text-lg text-white" />
							</div>
							<span class="text-xl font-bold">Noverna</span>
						</div>
						<p class="leading-relaxed text-gray-400">The Next generation of Open Source Tools, all completly free and Open for all, here will history be written.</p>
					</div>

					{#each [{ title: 'Projekte', links: ['Alle Projekte', 'Featured', 'Neueste'] }, { title: 'Community', links: ['Discord', 'GitHub', 'Discussions'] }, { title: 'Support', links: ['Dokumentation', 'Tutorials', 'Kontakt'] }] as section}
						<div class="footer-section">
							<h3 class="mb-4 font-semibold text-white">{section.title}</h3>
							<ul class="space-y-2">
								{#each section.links as link}
									<li>
										<a href="#" class="text-gray-400 transition-colors hover:text-white">{link}</a>
									</li>
								{/each}
							</ul>
						</div>
					{/each}
				</div>

				<div class="mt-12 border-t border-white/10 pt-8 text-center text-gray-400">
					<p>&copy; {new Date().getFullYear()} Noverna. Crafted with ❤️ for the Open Source Community.</p>
				</div>
			</div>
		</footer>
	</main>
{/if}

<style>
	:global(body) {
		font-family:
			'Inter',
			-apple-system,
			BlinkMacSystemFont,
			sans-serif;
		background: #0a0a0a;
		overflow-x: hidden;
	}

	/* Glass Effects */
	.glass-nav {
		background: rgba(0, 0, 0, 0.2);
		backdrop-filter: blur(20px);
		border: 1px solid rgba(255, 255, 255, 0.1);
	}

	.glass-container {
		background: rgba(255, 255, 255, 0.02);
		backdrop-filter: blur(20px);
		border: 1px solid rgba(255, 255, 255, 0.1);
	}

	/* Navigation */
	.nav-link {
		position: relative;
		color: #e5e7eb;
		text-decoration: none;
		transition: all 0.3s ease;
		padding: 0.5rem 0;
	}

	.nav-underline {
		position: absolute;
		bottom: 0;
		left: 0;
		width: 0;
		height: 2px;
		background: linear-gradient(90deg, #3b82f6, #8b5cf6);
		transition: width 0.3s ease;
	}

	.nav-link:hover .nav-underline,
	.nav-link:focus .nav-underline {
		width: 100%;
	}

	.nav-link:hover {
		color: #ffffff;
	}

	/* Buttons */
	.btn-primary {
		background: linear-gradient(135deg, #3b82f6, #8b5cf6);
		padding: 1rem 2rem;
		border-radius: 1rem;
		font-weight: 600;
		color: white;
		border: none;
		cursor: pointer;
		transition: all 0.3s ease;
		display: flex;
		align-items: center;
		justify-content: center;
		text-decoration: none;
		box-shadow: 0 10px 30px rgba(59, 130, 246, 0.3);
	}

	.btn-primary:hover {
		transform: translateY(-2px);
		box-shadow: 0 15px 40px rgba(59, 130, 246, 0.4);
	}

	.btn-secondary {
		background: rgba(255, 255, 255, 0.05);
		backdrop-filter: blur(10px);
		padding: 1rem 2rem;
		border-radius: 1rem;
		font-weight: 600;
		color: white;
		border: 1px solid rgba(255, 255, 255, 0.1);
		cursor: pointer;
		transition: all 0.3s ease;
		display: flex;
		align-items: center;
		justify-content: center;
		text-decoration: none;
	}

	.btn-secondary:hover {
		background: rgba(255, 255, 255, 0.1);
		transform: translateY(-2px);
		border-color: rgba(255, 255, 255, 0.2);
	}

	.btn-member {
		background: linear-gradient(135deg, #3b82f6, #8b5cf6);
		padding: 0.5rem 1.25rem;
		border-radius: 1rem;
		font-weight: 600;
		color: white;
		border: none;
		cursor: pointer;
		transition: all 0.3s ease;
		display: flex;
		align-items: center;
		justify-content: center;
		text-decoration: none;
		box-shadow: 0 10px 30px rgba(59, 130, 246, 0.3);
	}

	.btn-member:hover {
		transform: translateY(-2px);
		box-shadow: 0 15px 40px rgba(59, 130, 246, 0.4);
	}

	.btn-discord {
		background: linear-gradient(135deg, #5865f2, #7289da);
		padding: 1rem 2rem;
		border-radius: 1rem;
		font-weight: 600;
		color: white;
		border: none;
		cursor: pointer;
		transition: all 0.3s ease;
		display: flex;
		align-items: center;
		justify-content: center;
		text-decoration: none;
		box-shadow: 0 10px 30px rgba(88, 101, 242, 0.3);
	}

	.btn-discord:hover {
		transform: translateY(-2px);
		box-shadow: 0 15px 40px rgba(88, 101, 242, 0.4);
	}

	.btn-github {
		background: rgba(255, 255, 255, 0.05);
		backdrop-filter: blur(10px);
		padding: 1rem 2rem;
		border-radius: 1rem;
		font-weight: 600;
		color: white;
		border: 1px solid rgba(255, 255, 255, 0.1);
		cursor: pointer;
		transition: all 0.3s ease;
		display: flex;
		align-items: center;
		justify-content: center;
		text-decoration: none;
	}

	.btn-github:hover {
		background: rgba(255, 255, 255, 0.1);
		transform: translateY(-2px);
		border-color: rgba(255, 255, 255, 0.2);
	}

	/* Cards */
	.stat-card {
		background: rgba(255, 255, 255, 0.02);
		backdrop-filter: blur(10px);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 1.5rem;
		padding: 2rem;
		text-align: center;
		transition: all 0.3s ease;
		opacity: 0;
		transform: translateY(30px);
	}

	.stat-card.animate-in {
		opacity: 1;
		transform: translateY(0);
	}

	.stat-card:hover {
		transform: translateY(-5px);
		border-color: rgba(255, 255, 255, 0.2);
		box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
	}

	.project-card {
		background: rgba(255, 255, 255, 0.02);
		backdrop-filter: blur(10px);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 1.5rem;
		overflow: hidden;
		transition: all 0.3s ease;
		opacity: 0;
		transform: translateY(30px);
	}

	.project-card.animate-in {
		opacity: 1;
		transform: translateY(0);
	}

	.project-card:hover {
		transform: translateY(-10px);
		border-color: rgba(255, 255, 255, 0.2);
		box-shadow: 0 25px 50px rgba(0, 0, 0, 0.3);
	}

	.project-body {
		background: rgba(255, 255, 255, 0.02);
	}

	.project-link {
		background: rgba(255, 255, 255, 0.1);
		border: none;
		border-radius: 0.5rem;
		width: 2.5rem;
		height: 2.5rem;
		display: flex;
		align-items: center;
		justify-content: center;
		color: white;
		cursor: pointer;
		transition: all 0.3s ease;
	}

	.project-link:hover {
		background: rgba(255, 255, 255, 0.2);
		transform: scale(1.1);
	}

	.feature-card {
		background: rgba(255, 255, 255, 0.02);
		backdrop-filter: blur(10px);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 1.5rem;
		padding: 2rem;
		text-align: center;
		transition: all 0.3s ease;
		opacity: 0;
		transform: translateY(30px);
	}

	.feature-card.animate-in {
		opacity: 1;
		transform: translateY(0);
	}

	.feature-card:hover {
		transform: translateY(-5px);
		border-color: rgba(255, 255, 255, 0.2);
		box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
	}

	.feature-icon {
		background: linear-gradient(135deg, #3b82f6, #8b5cf6);
		width: 4rem;
		height: 4rem;
		border-radius: 1rem;
		display: flex;
		align-items: center;
		justify-content: center;
		margin: 0 auto;
		color: white;
	}

	.step-card {
		background: rgba(255, 255, 255, 0.02);
		backdrop-filter: blur(10px);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 1.5rem;
		padding: 2rem;
		text-align: center;
		transition: all 0.3s ease;
		opacity: 0;
		transform: translateY(30px);
		position: relative;
	}

	.step-card.animate-in {
		opacity: 1;
		transform: translateY(0);
	}

	.step-card:hover {
		transform: translateY(-5px);
		border-color: rgba(255, 255, 255, 0.2);
		box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
	}

	.step-number {
		position: absolute;
		top: -1rem;
		left: 50%;
		transform: translateX(-50%);
		background: linear-gradient(135deg, #3b82f6, #8b5cf6);
		width: 2rem;
		height: 2rem;
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
		color: white;
		font-weight: bold;
		font-size: 0.875rem;
	}

	/* Animations */
	/* Animations */
	@keyframes fadeInUp {
		from {
			opacity: 0;
			transform: translateY(50px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	.animate-on-scroll {
		opacity: 0;
		transform: translateY(50px);
		transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
	}

	.animate-on-scroll.animate-in {
		opacity: 1;
		transform: translateY(0);
	}

	/* Staggered animations for better effect */
	.animate-on-scroll:nth-child(1) {
		transition-delay: 0ms;
	}
	.animate-on-scroll:nth-child(2) {
		transition-delay: 100ms;
	}
	.animate-on-scroll:nth-child(3) {
		transition-delay: 200ms;
	}
	.animate-on-scroll:nth-child(4) {
		transition-delay: 300ms;
	}

	.animate-on-scroll {
		opacity: 0;
		transform: translateY(30px);
		transition: all 0.6s ease;
	}

	.animate-on-scroll.animate-in {
		opacity: 1;
		transform: translateY(0);
	}
</style>
