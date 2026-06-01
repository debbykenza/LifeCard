<script lang="ts">
	import Button  from '$lib/components/ui/button/button.svelte';
	import  Card  from '$lib/components/ui/card/card.svelte';
	import Badge  from '$lib/components/ui/badge/badge.svelte';
	import type { Url } from 'url';
	import { onMount } from 'svelte';

					

	// Features data
	const features = [
		{
			title: "Accès d'urgence",
			description:
				"Les secouristes accèdent instantanément à vos informations vitales en cas d'accident, sans connexion internet.",
			icon: '🚨',
			image: '/images/sapeur_pompier3.svg'
		},
		{
			title: 'Sécurité maximale',
			description:
				"Chiffrement AES-256 et contrôle d'accès à 4 niveaux pour protéger vos données médicales.",
			icon: '🔐',
			image: '/images/secure_data2.svg'
		},
		{
			title: 'Compatible mondial',
			description:
				"Utilisable dans n'importe quel pays, même dans les zones reculées sans infrastructure.",
			icon: '🌍',
			image: '/images/utilisation_mondiale4.svg'
		}
	];

	// Access levels : Type pour les niveaux d'accès
	type AccessLevel = {
		id: string;
		level: string;
		icon: string;
		color: string;
		title: string;
		textColor: string;
		bgbadgecolor: string;
		textbadgecolor: string;
		description: string;
		image: string; // Emoji ou URL d'image représentant la catégorie
		actors: string[]; // Liste des acteurs de cette catégorie
		accessInfo: string[]; // Informations auxquelles ils ont accès
	};

	// Données des niveaux d'accès
	const accessLevels: AccessLevel[] = [
		{
			id: 'medecin',
			level: 'Médecins',
			icon: '👨‍⚕️',
			color: 'bg-teal-900 border-white',
			title: 'Dossier médical complet',
			textColor: 'text-white',
			bgbadgecolor: 'bg-white',
			textbadgecolor: 'text-teal-800',
			description: 'Accès total avec authentification professionnelle',
			image: '/images/medecin2.svg',
			actors: [
				'Médecin généraliste',
				'Médecin spécialiste',
				'Chirurgien',
				'Psychiatre',
				'Pédiatre'
			],
			accessInfo: [
				'Historique médical complet',
				"Résultats d'examens et analyses",
				'Imagerie médicale (radios, IRM, scanners)',
				'Diagnostics antérieurs',
				'Prescriptions et ordonnances',
				'Compte-rendus de consultation',
				'Modifications du dossier médical'
			]
		},
		{
			id: 'urgence',
			level: 'Urgentistes',
			icon: '🚨',
			color: 'bg-neutral',
			textColor: 'text-teal-950',
			bgbadgecolor: 'bg-teal-700',
			textbadgecolor: 'text-white',
			title: 'Accès instantané vital',
			description: "Interviennent en cas d'urgence sans authentification",
			image: '/images/sapeur_pompier3.svg',
			actors: [
				'Sapeurs-pompiers',
				'Ambulanciers',
				'Secouristes SAMU',
				'Équipes de sauvetage',
				'Personnel de premiers secours'
			],
			accessInfo: [
				'Groupe sanguin',
				'Allergies médicamenteuses',
				'Traitements en cours',
				'Maladies chroniques',
				"Contacts d'urgence",
				'Directives anticipées'
			]
		},

		{
			id: 'paramedical',
			level: 'Paramédical',
			icon: '👩‍⚕️',
			color: 'bg-teal-900',
			textColor: 'text-white',
			bgbadgecolor: 'bg-white',
			textbadgecolor: 'text-teal-800',
			title: 'Suivi des soins',
			description: 'Accès limité aux informations de suivi',
			image: '/images/paramedical3.svg',
			actors: [
				'Infirmier / Infirmière',
				'Aide-soignant(e)',
				'Kinésithérapeute',
				'Sage-femme',
				'Ergothérapeute',
				'Radiologues',
				'Techniciens de laboratoire'
			],
			accessInfo: [
				'Constantes vitales (tension, température, poids)',
				'Prescriptions médicales en cours',
				'Planning de soins',
				'Traçabilité des actes infirmiers',
				'Prise de médicaments',
				'Notes de surveillance'
			]
		},
		{
			id: 'patient',
			level: 'Patient',
			icon: '🙋',
			color: 'bg-neutral',
			textColor: 'text-teal-950',
			bgbadgecolor: 'bg-teal-800',
			textbadgecolor: 'text-white',
			title: 'Contrôle total',
			description: 'Gestion complète de votre dossier médical',
			image: '/images/patient2.svg',
			actors: ['Vous-même (titulaire)', 'Représentant légal', 'Personne de confiance désignée'],
			accessInfo: [
				"Consultation de l'historique complet",
				"Gestion des autorisations d'accès",
				'Ajout de documents personnels',
				'Configuration des rappels de médicaments',
				'Historique des accès au dossier',
				"Gestion des contacts d'urgence",
				'Export et partage de données',
				'Suppression de données personnelles'
			]
		}
	];

	// État pour l'onglet sélectionné
	let selectedLevel = $state(accessLevels[0]);

	// Testimonials
	const testimonials = [
		{
			name: 'Dr. Amina Touré',
			role: 'Médecin urgentiste',
			image: '/images/landing_page.png',
			text: "LifeCard a sauvé la vie d'un patient allergique. En 10 secondes, j'ai eu toutes les infos nécessaires pour agir sans risque.",
			rating: 5
		},
		{
			name: 'Marc Dubois',
			role: 'Patient diabétique',
			image: '/images/landing_page.png',
			text: 'Je voyage beaucoup pour le travail. Avec LifeCard, je suis rassuré : mon traitement est accessible partout dans le monde.',
			rating: 5
		},
		{
			name: 'Infirmière Sarah K.',
			role: 'Hôpital rural - Bénin',
			image: '/images/landing_page.png',
			text: "Même sans internet, nous pouvons consulter les dossiers. C'est une révolution pour nos zones reculées.",
			rating: 5
		}
	];

	// Variable pour le menu mobile
	let mobileMenuOpen = $state(false);

	// Variable pour la section active
	let activeSection = $state('accueil');

	// Détection de la section active au scroll (version alternative)
	onMount(() => {
		const sections = [
			'accueil',
			'pourquoi',
			'securite',
			'experience',
			'technologie',
			'temoignages'
		];

		function updateActiveSection() {
			const scrollPosition = window.scrollY + 150; // Offset pour le header

			for (const id of sections) {
				const element = document.getElementById(id);
				if (element) {
					const top = element.offsetTop;
					const bottom = top + element.offsetHeight;

					if (scrollPosition >= top && scrollPosition < bottom) {
						activeSection = id;
						break;
					}
				}
			}
		}

		// Détection au scroll
		window.addEventListener('scroll', updateActiveSection);
		// Détection au chargement
		updateActiveSection();

		return () => {
			window.removeEventListener('scroll', updateActiveSection);
		};
	});
</script>


<!-- Header / Navbar -->
<header
	class="fixed top-0 right-0 left-0 z-50 border-b border-slate-200 bg-white/95 shadow-sm backdrop-blur-md"
>
	<nav class="container mx-auto px-6 lg:px-20">
		<div class="flex items-center justify-between py-4">
			<!-- Logo -->
			<a href="/" class="flex items-center gap-2">
				<div class="rounded-lg bg-teal-700 p-2 text-xl font-bold text-white">LC</div>
				<span class="text-2xl font-bold text-teal-950">LifeCard</span>
			</a>

			<!-- Desktop Navigation -->
			<div class="hidden items-center gap-8 md:flex">
				<a
					href="#accueil"
					class="relative pb-1 font-medium text-slate-700 transition hover:text-teal-700
					       {activeSection === 'accueil' ? 'text-teal-800' : ''}"
				>
					Accueil
					{#if activeSection === 'accueil'}
						<span class="absolute right-0 bottom-0 left-0 h-0.5 bg-teal-800"></span>
					{/if}
				</a>
				<a
					href="#pourquoi"
					class="relative pb-1 font-medium text-slate-700 transition hover:text-teal-700
					       {activeSection === 'pourquoi' ? 'text-teal-800' : ''}"
				>
					Pourquoi LifeCard
					{#if activeSection === 'pourquoi'}
						<span class="absolute right-0 bottom-0 left-0 h-0.5 bg-teal-800"></span>
					{/if}
				</a>
				<a
					href="#securite"
					class="relative pb-1 font-medium text-slate-700 transition hover:text-teal-700
					       {activeSection === 'securite' ? 'text-teal-800' : ''}"
				>
					Sécurité
					{#if activeSection === 'securite'}
						<span class="absolute right-0 bottom-0 left-0 h-0.5 bg-teal-800"></span>
					{/if}
				</a>
				<a
					href="#experience"
					class="relative pb-1 font-medium text-slate-700 transition hover:text-teal-700
					       {activeSection === 'experience' ? 'text-teal-800' : ''}"
				>
					Expérience
					{#if activeSection === 'experience'}
						<span class="absolute right-0 bottom-0 left-0 h-0.5 bg-teal-800"></span>
					{/if}
				</a>
				<a
					href="#technologie"
					class="relative pb-1 font-medium text-slate-700 transition hover:text-teal-700
					       {activeSection === 'technologie' ? 'text-teal-800' : ''}"
				>
					Technologie
					{#if activeSection === 'technologie'}
						<span class="absolute right-0 bottom-0 left-0 h-0.5 bg-teal-800"></span>
					{/if}
				</a>
				<a
					href="#temoignages"
					class="relative pb-1 font-medium text-slate-700 transition hover:text-teal-700
					       {activeSection === 'temoignages' ? 'text-teal-800' : ''}"
				>
					Témoignages
					{#if activeSection === 'temoignages'}
						<span class="absolute right-0 bottom-0 left-0 h-0.5 bg-teal-800"></span>
					{/if}
				</a>
			</div>

			<!-- Auth Buttons Desktop -->
			<div class="hidden items-center gap-3 md:flex">
				<Button
					variant="outline"
					class="border-teal-700 px-4 py-4 text-teal-800 hover:bg-teal-50"
					onclick={() => (window.location.href = '/auth/login')}
				>
					Connexion
				</Button>
				<Button
					class="bg-teal-800 px-4 py-4 text-white hover:bg-teal-800"
					onclick={() => (window.location.href = '/auth/register')}
				>
					Inscription
				</Button>
			</div>

			<!-- Mobile Menu Button -->
			<button
				class="p-2 text-slate-700 md:hidden"
				onclick={() => (mobileMenuOpen = !mobileMenuOpen)}
				aria-label="Toggle menu"
			>
				<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					{#if mobileMenuOpen}
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M6 18L18 6M6 6l12 12"
						/>
					{:else}
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M4 6h16M4 12h16M4 18h16"
						/>
					{/if}
				</svg>
			</button>
		</div>

		<!-- Mobile Menu -->
		{#if mobileMenuOpen}
			<div class="animate-in space-y-3 pb-4 slide-in-from-top md:hidden">
				<a
					href="#accueil"
					class="block py-2 font-medium text-slate-700 transition hover:text-teal-700
					       {activeSection === 'accueil' ? 'border-l-4 border-teal-800 pl-3 text-teal-800' : ''}"
					onclick={() => (mobileMenuOpen = false)}
				>
					Accueil
				</a>
				<a
					href="#pourquoi"
					class="block py-2 font-medium text-slate-700 transition hover:text-teal-700
					       {activeSection === 'pourquoi' ? 'border-l-4 border-teal-800 pl-3 text-teal-800' : ''}"
					onclick={() => (mobileMenuOpen = false)}
				>
					Pourquoi LifeCard
				</a>
				<a
					href="#securite"
					class="block py-2 font-medium text-slate-700 transition hover:text-teal-700
					       {activeSection === 'securite' ? 'border-l-4 border-teal-800 pl-3 text-teal-800' : ''}"
					onclick={() => (mobileMenuOpen = false)}
				>
					Sécurité
				</a>
				<a
					href="#experience"
					class="block py-2 font-medium text-slate-700 transition hover:text-teal-700
					       {activeSection === 'experience' ? 'border-l-4 border-teal-800 pl-3 text-teal-800' : ''}"
					onclick={() => (mobileMenuOpen = false)}
				>
					Expérience
				</a>
				<a
					href="#technologie"
					class="block py-2 font-medium text-slate-700 transition hover:text-teal-700
					       {activeSection === 'technologie' ? 'border-l-4 border-teal-800 pl-3 text-teal-800' : ''}"
					onclick={() => (mobileMenuOpen = false)}
				>
					Technologie
				</a>
				<a
					href="#temoignages"
					class="block py-2 font-medium text-slate-700 transition hover:text-teal-700
					       {activeSection === 'temoignages' ? 'border-l-4 border-teal-800 pl-3 text-teal-800' : ''}"
					onclick={() => (mobileMenuOpen = false)}
				>
					Témoignages
				</a>

				<div class="flex flex-col gap-2 border-t border-slate-200 pt-4">
					<Button
						variant="outline"
						class="w-full border-teal-700 text-teal-700 hover:bg-teal-50"
						onclick={() => {
							mobileMenuOpen = false;
							window.location.href = '/auth/login';
						}}
					>
						Connexion
					</Button>
					<Button
						class="w-full bg-teal-700 text-white hover:bg-teal-800"
						onclick={() => {
							mobileMenuOpen = false;
							window.location.href = '/auth/register';
						}}
					>
						Inscription
					</Button>
				</div>
			</div>
		{/if}
	</nav>
</header>

<!-- Spacer pour compenser le header fixe -->
<!-- <div class="h-20"></div> -->

<!-- Hero Section -->
<section class=" relative flex min-h-screen items-center overflow-hidden" id="accueil">
	<!-- Background decoration -->
	<div class="absolute inset-0 opacity-10">
		<div class="absolute top-20 right-20 h-72 w-72 rounded-full bg-green-500 blur-3xl"></div>
		<div class="absolute bottom-20 left-20 h-96 w-96 rounded-full bg-green-500 blur-3xl"></div>
	</div>

	<div class="relative z-10 container mx-auto px-6 lg:px-20">
		<div class="grid items-center gap-12 lg:grid-cols-2">
			<!-- Left content -->
			<div class="space-y-8">
				<!-- <h1 class="text-5xl lg:text-5xl font-bold leading-tight">LifeCard</h1> -->
				<h1 class="mb-4 text-3xl font-bold text-slate-900 lg:text-5xl">
					LifeCard,
					<span class="bg-teal-700 bg-clip-text text-transparent">
						La carte de santé universelle
					</span>
				</h1>

				<p class="text-md leading-relaxed">
					Imaginez un monde où votre dossier médical vous suit partout. LifeCard est bien plus
					qu'une carte de santé : c'est votre compagnon médical qui garantit une prise
					en charge rapide et efficace, que vous soyez en consultation, en voyage ou en situation
					d'urgence. 
				</p>

				<!-- <p>Grâce à la technologie NFC et QR Code, vos informations vitales sont
					accessibles instantanément par les professionnels de santé autorisés.</p> -->

				<div class="flex flex-wrap gap-2 grid grid-cols-2 md:grid-cols-2 lg:grid-cols-2 items-center">
					<Button
						size="xs"
						class="rounded-full bg-teal-950 py-6 text-sm text-white hover:bg-white hover:text-cyan-950"
					>
						Commander la carte
						<span class="ml-2">→</span>
					</Button>
					<Button
						size="xs"
						variant="outline"
						class="rounded-full border-teal-950 py-5 text-sm hover:bg-teal-950 hover:text-white"
					>
						Télécharger l'application 
						
						
					</Button>
					
				</div>

				<!-- Stats -->
				<div class="flex gap-8 pt-8">
					<div>
						<div class="text-3xl font-bold text-teal-950">99.9%</div>
						<div class="text-sm text-slate-400">Disponibilité</div>
					</div>
					<div>
						<div class="text-3xl font-bold text-teal-950">4 Niveaux</div>
						<div class="text-sm text-slate-400">De sécurité</div>
					</div>
					<div>
						<div class="text-3xl font-bold text-teal-950">Offline</div>
						<div class="text-sm text-slate-400">Mode hors-ligne</div>
					</div>
				</div>
			</div>

			<!-- Right image/illustration -->
			<div class="relative">
				<div class="relative rounded-3xl border border-white/10 bg-teal-950 p-8">
					<!-- Card mockup -->

					<img
						src="/images/landing_page.png"
						alt="LifeCard Illustration"
						class="rounded-2xl shadow-lg"
					/>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- Why Choosing Us -->
<section class="bg-white py-20" id="pourquoi">
	<div class="container mx-auto px-6 lg:px-20">
		<div class="mb-16 text-center">
			<Badge class="mb-4 border-teal-200 bg-blue-50 text-teal-950">Pourquoi LifeCard</Badge>
			<h2 class="mb-4 text-4xl font-bold text-slate-900 lg:text-5xl">
				Une Technologie au Service de Votre Santé
			</h2>
			<p class="mx-auto max-w-2xl text-xl text-slate-600">
				Conçu pour fonctionner partout, même dans les conditions les plus difficiles
			</p>
		</div>

		<div class="grid gap-8 md:grid-cols-3">
			{#each features as feature}
				<Card class="border-slate-200 p-8 transition-shadow hover:shadow-xl">
					<!-- <div class="text-xl mb-4">{feature.icon}</div> -->
					<img src={feature.image} alt={feature.title} class="mb-6 w-full" />
					<h3 class="mb-3 text-2xl font-bold text-slate-900">{feature.title}</h3>
					<p class="leading-relaxed text-slate-600">{feature.description}</p>
				</Card>
			{/each}
		</div>
	</div>
</section>



<!-- Access Levels Section -->
<section class="bg-slate-50 py-20" id="securite">
	<div class="container mx-auto px-6 lg:px-20">
		<div class="mb-16 text-center">
			<Badge class="mb-4 border-teal-200 bg-blue-50 text-teal-950">Sécurité</Badge>
			<h2 class="mb-4 text-4xl font-bold text-slate-900 lg:text-5xl">
				4 Niveaux d'Accès Pour Votre Protection
			</h2>
			<p class="mx-auto max-w-2xl text-xl text-slate-600">
				Chaque professionnel de santé accède uniquement aux informations nécessaires
			</p>
		</div>

		<!-- Tabs Navigation -->
		<div class="mb-8 flex flex-wrap justify-center gap-4">
			{#each accessLevels as access}
				<Button
					variant={selectedLevel.id === access.id ? 'default' : 'default'}
					class="rounded-full px-6 py-3 text-base font-semibold transition-all
                 {selectedLevel.id === access.id
						? 'scale-105 bg-teal-800 text-white shadow-lg hover:border-slate-400 hover:bg-teal-700 hover:text-white'
						: 'border-slate-300 bg-white text-slate-700 hover:border-slate-400 hover:bg-teal-700 hover:text-white'}"
					onclick={() => (selectedLevel = access)}
				>
					{access.level}
				</Button>
			{/each}
		</div>

		<!-- Content Display -->
		<Card class="border-1 p-8 shadow-xl lg:p-12 {selectedLevel.color}">
			<div class="grid gap-8 lg:grid-cols-2 lg:gap-12">
				<!-- Left: Actors & Access Info -->
				<div class="space-y-8">
					<!-- Titre et description -->
					<div class="space-y-3">
						<!-- <Badge class="border-2 bg-teal-700 px-4 py-2 text-base font-semibold">
							{selectedLevel.level}
						</Badge> -->
						<h3 class="text-3xl font-bold {selectedLevel.textColor}">{selectedLevel.title}</h3>
						<p class="text-lg {selectedLevel.textColor}">{selectedLevel.description}</p>
					</div>

					<!-- Liste des acteurs -->
					<div class="space-y-4">
						<h4
							class="flex items-center gap-2 text-xl font-bold text-slate-900 {selectedLevel.textColor}"
						>
							Qui peut accéder ?
						</h4>
						<div class="space-y-2">
							<!-- {#each selectedLevel.actors as actor} -->
							<!-- <div
									class="flex items-center gap-3 rounded-lg bg-white/70 px-4 py-3 backdrop-blur-sm"
								>
									<span class="text-green-600">✓</span>
									<span class="font-medium text-slate-800">{actor}</span>
								</div> -->
							<div class="flex flex-wrap gap-3">
								{#each selectedLevel.actors as actor}
									<Badge
										class="border-2  {selectedLevel.bgbadgecolor}  {selectedLevel.textbadgecolor} px-4 py-4 text-base font-semibold "
									>
										{actor}
									</Badge>
								{/each}
							</div>
							<!-- {/each} -->
						</div>
					</div>

					<!-- Informations accessibles -->
					<div class="space-y-4">
						<h4
							class="flex items-center gap-2 text-xl font-bold text-slate-900 {selectedLevel.textColor}"
						>
							Informations accessibles
						</h4>
						<div class="flex flex-wrap gap-3">
							{#each selectedLevel.accessInfo as info}
								<Badge
									class="border-2  {selectedLevel.bgbadgecolor}  {selectedLevel.textbadgecolor} px-4 py-4 text-base font-semibold"
								>
									{info}
								</Badge>
							{/each}
						</div>
					</div>
				</div>

				<!-- Right: Image -->
				<div class="flex items-center justify-center">
					<div
						class="flex h-full w-full items-center justify-center rounded-2xl bg-teal-50 p-8 backdrop-blur-xl"
					>
						<img
							src={selectedLevel.image}
							alt={selectedLevel.level}
							class="h-full w-full object-contain"
						/>
					</div>
				</div>
			</div>
		</Card>
	</div>
</section>

<!-- Experience Section -->
<section class="bg-white py-20" id="experience">
	<div class="container mx-auto px-6 lg:px-20">
		<div class="grid items-center gap-12 lg:grid-cols-2">
			<!-- Image -->
			<div class="relative">
				<!-- <div
					class="flex aspect-video items-center justify-center rounded-3xl bg-gradient-to-br from-slate-100 to-slate-200 p-12"
				> -->
				<img src="/images/carte_nfc.png" alt="carte nfc" class="rounded-2xl shadow-lg" />

				<!-- </div> -->
				<div class="absolute -right-6 -bottom-6 rounded-2xl bg-teal-900 p-6 text-white shadow-xl">
					<div class="text-3xl font-bold">24/7</div>
					<div class="text-sm">Disponible partout</div>
				</div>
			</div>

			<!-- Content -->
			<div class="space-y-6">
				<Badge class="bg-teal-50 text-teal-950">EXPÉRIENCE</Badge>
				<h2 class="text-4xl font-bold text-slate-900 lg:text-5xl">
					Nous Vous Offrons La Meilleure Expérience
				</h2>
				<p class="text-lg leading-relaxed text-slate-600">
					LifeCard a été conçu en collaboration avec des médecins, des urgentistes et des patients
					du monde entier. Notre mission : rendre les soins de santé accessibles à tous, partout,
					avec élégance et simplicité.
				</p>
				<ul class="space-y-3">
					<li class="flex items-center gap-3 text-slate-700">
						<span class="rounded-full bg-green-100 p-1 text-green-600">✓</span>
						Interface intuitive, aucune formation nécessaire
					</li>
					<li class="flex items-center gap-3 text-slate-700">
						<span class="rounded-full bg-green-100 p-1 text-green-600">✓</span>
						Fonctionne hors ligne dans les zones reculées
					</li>
					<li class="flex items-center gap-3 text-slate-700">
						<span class="rounded-full bg-green-100 p-1 text-green-600">✓</span>
						Compatible avec tous les systèmes de santé
					</li>
				</ul>
				<!-- <Button class="rounded-full bg-orange-500 px-8 py-6 text-white hover:bg-orange-600">
					Découvrir Plus →
				</Button> -->
			</div>
		</div>
	</div>
</section>

<!-- Materials Section (adapted for technology) -->
<section class="bg-slate-50 py-20" id="technologie">
	<div class="container mx-auto px-6 lg:px-20">
		<div class="grid items-center gap-12 lg:grid-cols-2">
			<div class="space-y-6">
				<Badge class="bg-teal-50 text-teal-950">TECHNOLOGIE</Badge>
				<h2 class="text-4xl font-bold text-slate-900 lg:text-5xl">
					Des Standards de Sécurité Militaire
				</h2>
				<p class="text-lg leading-relaxed text-slate-600">
					Nous utilisons les technologies les plus avancées pour protéger vos données de santé.
					Chiffrement de bout en bout, authentification biométrique et blockchain décentralisée
					garantissent l'intégrité de vos informations.
				</p>
				<div class="space-y-3">
					<div class="flex items-center gap-3">
						<div class="rounded-lg bg-green-100 p-1 p-3 text-xl text-green-600 text-teal-950">
							01.
						</div>

						<div>
							<div class="font-semibold text-slate-900">Chiffrement AES-256</div>
							<div class="text-sm text-slate-600">Standard militaire et bancaire</div>
						</div>
					</div>
					<div class="flex items-center gap-3">
						<div class="rounded-lg bg-green-100 p-1 p-3 text-xl text-green-600 text-teal-950">
							02.
						</div>
						<div>
							<div class="font-semibold text-slate-900">Blockchain décentralisée</div>
							<div class="text-sm text-slate-600">Traçabilité et inviolabilité</div>
						</div>
					</div>
					<div class="flex items-center gap-3">
						<div class="rounded-lg bg-green-100 p-1 p-3 text-xl text-green-600 text-teal-950">
							03.
						</div>
						<div>
							<div class="font-semibold text-slate-900">Progressive Web App</div>
							<div class="text-sm text-slate-600">Fonctionne même hors ligne</div>
						</div>
					</div>
				</div>
				<Button variant="outline" class="rounded-full border-slate-300 px-8 py-6">
					En Savoir Plus →
				</Button>
			</div>

			<!-- Images grid -->
			<div class="grid grid-cols-2 gap-4">
				<div class="space-y-4">
					<div
						class="flex aspect-square items-center justify-center rounded-2xl bg-teal-900 text-6xl"
					>
						<img src="/images/chiffrement_aes.svg" alt="Médecin" />
					</div>
					<div
						class="flex aspect-video items-center justify-center rounded-2xl bg-teal-50 text-6xl"
					>
						<img src="/images/connexion_compte.svg" alt="Médecin" />
					</div>
				</div>
				<div class="space-y-4 pt-8">
					<div
						class="flex aspect-video items-center justify-center rounded-2xl bg-teal-50 text-3xl"
					>
						<img src="/images/chiffrement.svg" alt="Médecin" />
					</div>
					<div
						class="flex aspect-square items-center justify-center rounded-2xl bg-teal-900 text-6xl"
					>
						<img src="/images/blockchain.svg" alt="Médecin" />
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- Testimonials -->
<section class="bg-white py-20" id="temoignages">
	<div class="container mx-auto px-6 lg:px-20">
		<div class="mb-16 text-center">
			<Badge class="bg-teal-50 text-teal-950">TÉMOIGNAGES</Badge>
			<h2 class="mb-4 text-4xl font-bold text-slate-900 lg:text-5xl">
				Ce Que Disent Nos Utilisateurs
			</h2>
			<p class="mx-auto max-w-2xl text-xl text-slate-600">
				Des milliers de professionnels et patients nous font confiance
			</p>
		</div>

		<div class="grid gap-8 md:grid-cols-3">
			{#each testimonials as testimonial}
				<Card
					class="border-slate-200 bg-teal-900 p-8 text-white transition-all hover:-translate-y-2 hover:shadow-xl"
				>
					<div class="space-y-4">
						<div class="flex items-center gap-4 pt-4">
							<div class="text-4xl">
								<img
									src={testimonial.image}
									alt={testimonial.name}
									class="h-12 w-12 rounded-2xl object-cover shadow-lg"
								/>
							</div>
							<div>
								<div class="font-semibold">{testimonial.name}</div>
								<div class="text-sm">{testimonial.role}</div>
							</div>
						</div>
						<!-- <div class="flex gap-1">
							{#each Array(testimonial.rating) as _}
								<span class="text-xl text-yellow-400">⭐</span>
							{/each}
						</div> -->
						<p class="leading-relaxed italic">"{testimonial.text}"</p>
					</div>
				</Card>
			{/each}
		</div>
	</div>
</section>

<!-- FAQ Section -->
<section class="bg-slate-50" id="faq">
	<div class="container mx-auto px-6 lg:px-20">
		<div class="mb-16 text-center">
			<Badge class="mb-4 bg-teal-50 text-teal-950">FAQ</Badge>
			<h2 class="mb-4 text-4xl font-bold text-slate-900 lg:text-5xl">
				Questions Fréquemment Posées
			</h2>
			<p class="mx-auto max-w-2xl text-xl text-slate-600">
				Trouvez des réponses aux questions les plus courantes sur LifeCard
			</p>
		</div>

		<div class="mx-auto max-w-4xl space-y-4">
			{#each [
				{
					question: "Qu'est-ce que LifeCard et comment fonctionne-t-elle ?",
					answer: "LifeCard est une carte de santé intelligente avec technologie NFC et QR Code qui stocke vos informations médicales vitales. Elle permet aux professionnels de santé d'accéder instantanément à votre dossier médical, même sans connexion internet."
				},
				{
					question: "Comment obtenir ma LifeCard ?",
					answer: "Vous pouvez commander votre LifeCard directement sur notre site web. Après votre commande, vous recevrez votre carte sous 5 à 7 jours ouvrables. Vous devrez ensuite créer votre compte et remplir votre dossier médical via notre application."
				},
				{
					question: "Mes données médicales sont-elles sécurisées ?",
					answer: "Absolument. Nous utilisons un chiffrement AES-256 de niveau militaire et une blockchain décentralisée pour garantir la sécurité et l'intégrité de vos données. Seuls les professionnels autorisés peuvent accéder à vos informations selon 4 niveaux d'accès stricts."
				},
				{
					question: "La carte fonctionne-t-elle sans connexion internet ?",
					answer: "Oui ! C'est l'un des principaux avantages de LifeCard. Les informations vitales (groupe sanguin, allergies, traitements) sont accessibles via NFC même sans connexion. L'application fonctionne également en mode hors-ligne grâce à la technologie PWA."
				},
				{
					question: "Puis-je utiliser LifeCard dans d'autres pays ?",
					answer: "Oui, LifeCard est conçue pour être utilisable partout dans le monde. Le système respecte les standards internationaux de santé (HL7 FHIR) et fonctionne dans n'importe quel pays, même dans les zones reculées."
				},
				{
					question: "Comment puis-je mettre à jour mes informations médicales ?",
					answer: "Vous pouvez mettre à jour vos informations à tout moment via l'application mobile ou web. Les médecins peuvent également ajouter des informations après chaque consultation. Toutes les modifications sont synchronisées automatiquement."
				}
			] as faq, i}
				<details class="group rounded-xl border-2 border-slate-200 bg-white p-6 transition-all hover:border-teal-600 hover:bg-teal-50 hover:shadow-lg hover:cursor-pointer">
					<summary class="flex cursor-pointer items-center justify-between font-semibold text-slate-900">
						<span class="text-lg">{faq.question}</span>
						<svg 
							class="h-5 w-5 text-teal-700 transition-transform group-open:rotate-180" 
							fill="none" 
							stroke="currentColor" 
							viewBox="0 0 24 24"
						>
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/>
						</svg>
					</summary>
					<p class="mt-4 text-slate-600 leading-relaxed">
						{faq.answer}
					</p>
				</details>
			{/each}
		</div>

		<!-- CTA vers contact -->
		<div class="mt-12 text-center">
			<p class="mb-4 text-slate-600">Vous ne trouvez pas la réponse à votre question ?</p>
			<Button variant="outline" class="rounded-full border-teal-700 text-teal-800 hover:bg-teal-50 px-6 py-3">
				Contactez-nous
			</Button>
		</div>
	</div>
</section>

<!-- App Download Section -->
<section class="bg-white py-20" id="application">
	<div class="container mx-auto px-6 lg:px-20">
		<div class="grid items-center gap-12 lg:grid-cols-2">
			<!-- Left: Content -->
			<div class="space-y-6">
				<Badge class="bg-teal-50 text-teal-950">APPLICATION MOBILE</Badge>
				<h2 class="text-4xl font-bold text-slate-900 lg:text-5xl">
					Gérez Votre Santé du Bout des Doigts
				</h2>
				<p class="text-lg leading-relaxed text-slate-600">
					Téléchargez l'application LifeCard pour accéder à votre dossier médical, gérer vos médicaments, 
					programmer des rappels et partager vos informations avec vos professionnels de santé en toute sécurité.
				</p>

				<!-- Features list -->
				<ul class="space-y-3">
					<li class="flex items-center gap-3 text-slate-700">
						<div class="flex h-8 w-8 items-center justify-center rounded-full bg-teal-100 text-teal-700">
							<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/>
							</svg>
						</div>
						Accès instantané à votre dossier médical complet
					</li>
					<li class="flex items-center gap-3 text-slate-700">
						<div class="flex h-8 w-8 items-center justify-center rounded-full bg-teal-100 text-teal-700">
							<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/>
							</svg>
						</div>
						Rappels automatiques pour vos médicaments
					</li>
					<li class="flex items-center gap-3 text-slate-700">
						<div class="flex h-8 w-8 items-center justify-center rounded-full bg-teal-100 text-teal-700">
							<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/>
							</svg>
						</div>
						Partage sécurisé avec vos médecins
					</li>
					<li class="flex items-center gap-3 text-slate-700">
						<div class="flex h-8 w-8 items-center justify-center rounded-full bg-teal-100 text-teal-700">
							<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/>
							</svg>
						</div>
						Fonctionne hors ligne - vos données toujours accessibles
					</li>
				</ul>

				<!-- Download buttons -->
				<div class="flex flex-wrap gap-4 pt-4">
					<a 
						href="#" 
						class="flex items-center gap-3 rounded-xl bg-black px-6 py-3 text-white transition hover:bg-gray-800"
					>
						<svg class="h-8 w-8" viewBox="0 0 24 24" fill="currentColor">
							<path d="M17.05 20.28c-.98.95-2.05.8-3.08.35-1.09-.46-2.09-.48-3.24 0-1.44.62-2.2.44-3.06-.35C2.79 15.25 3.51 7.59 9.05 7.31c1.35.07 2.29.74 3.08.8 1.18-.24 2.31-.93 3.57-.84 1.51.12 2.65.72 3.4 1.8-3.12 1.87-2.38 5.98.48 7.13-.57 1.5-1.31 2.99-2.54 4.09l.01-.01zM12.03 7.25c-.15-2.23 1.66-4.07 3.74-4.25.29 2.58-2.34 4.5-3.74 4.25z"/>
						</svg>
						<div class="text-left">
							<div class="text-xs">Télécharger sur</div>
							<div class="text-lg font-semibold">App Store</div>
						</div>
					</a>

					<a 
						href="#" 
						class="flex items-center gap-3 rounded-xl bg-black px-6 py-3 text-white transition hover:bg-gray-800"
					>
						<svg class="h-8 w-8" viewBox="0 0 24 24" fill="currentColor">
							<path d="M3,20.5V3.5C3,2.91 3.34,2.39 3.84,2.15L13.69,12L3.84,21.85C3.34,21.6 3,21.09 3,20.5M16.81,15.12L6.05,21.34L14.54,12.85L16.81,15.12M20.16,10.81C20.5,11.08 20.75,11.5 20.75,12C20.75,12.5 20.53,12.9 20.18,13.18L17.89,14.5L15.39,12L17.89,9.5L20.16,10.81M6.05,2.66L16.81,8.88L14.54,11.15L6.05,2.66Z"/>
						</svg>
						<div class="text-left">
							<div class="text-xs">Disponible sur</div>
							<div class="text-lg font-semibold">Google Play</div>
						</div>
					</a>
				</div>

				<!-- Stats -->
				<div class="flex gap-8 pt-6 border-t border-slate-200">
					<div>
						<div class="text-2xl font-bold text-teal-800">50K+</div>
						<div class="text-sm text-slate-600">Téléchargements</div>
					</div>
					<div>
						<div class="text-2xl font-bold text-teal-800">4.8/5</div>
						<div class="text-sm text-slate-600">Note moyenne</div>
					</div>
					<div>
						<div class="text-2xl font-bold text-teal-800">10K+</div>
						<div class="text-sm text-slate-600">Avis positifs</div>
					</div>
				</div>
			</div>

			<!-- Right: App mockup -->
			<div class="relative">
				<div class="relative">
					<!-- Phone mockup with gradient background -->
					<div class="absolute inset-0 rounded-3xl bg-gradient-to-br from-teal-100 to-teal-200 opacity-50 blur-3xl"></div>
					<div class="relative grid grid-cols-2 gap-4">
						<!-- Phone 1 -->
						<div class="transform transition hover:scale-105">
							<div class="overflow-hidden rounded-3xl border-8 border-slate-900 bg-white shadow-2xl">
								<div class="aspect-[10/19] bg-gradient-to-b from-teal-50 to-white p-4">
									<!-- Status bar -->
									<div class="mb-4 flex items-center justify-between text-xs">
										<span>9:41</span>
										<div class="flex gap-1">
											<div class="h-3 w-3 rounded-full bg-slate-300"></div>
											<div class="h-3 w-3 rounded-full bg-slate-300"></div>
											<div class="h-3 w-3 rounded-full bg-slate-300"></div>
										</div>
									</div>
									<!-- Content placeholder -->
									<img src="/images/carte_nfc.png" alt="écran1">
								</div>
							</div>
						</div>

						<!-- Phone 2 (slightly offset) -->
						<div class="transform pt-12 transition hover:scale-105">
							<div class="overflow-hidden rounded-3xl border-8 border-slate-900 bg-white shadow-2xl">
								<div class="aspect-[10/19] bg-gradient-to-b from-white to-teal-50 p-4">
									<!-- Status bar -->
									<div class="mb-4 flex items-center justify-between text-xs">
										<span>9:41</span>
										<div class="flex gap-1">
											<div class="h-3 w-3 rounded-full bg-slate-300"></div>
											<div class="h-3 w-3 rounded-full bg-slate-300"></div>
											<div class="h-3 w-3 rounded-full bg-slate-300"></div>
										</div>
									</div>
									<!-- Content placeholder -->
									<img src="/images/carte_nfc.png" alt="écran1">
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- CTA Section -->
<section class="bg-teal-950 py-20 text-white">
	<div class="container mx-auto px-6 text-center lg:px-20">
		<h2 class="mb-6 text-4xl font-bold lg:text-6xl">
			Prêt à Révolutionner Votre Accès aux Soins ?
		</h2>
		<p class="mx-auto mb-10 max-w-2xl text-xl text-blue-100">
			Rejoignez des milliers d'utilisateurs qui ont déjà fait le choix de la sécurité et de la
			simplicité
		</p>
		<div class="flex flex-wrap justify-center gap-4">
			<Button
				size="lg"
				class="rounded-full bg-white px-10 py-6 text-lg text-teal-800 hover:bg-slate-100"
			>
				Commander Ma LifeCard
			</Button>
			<Button
				size="lg"
				variant="outline"
				class="rounded-full border-white bg-teal-950 px-10 py-6 text-lg text-white hover:bg-white/10"
			>
				Parler à Un Expert
			</Button>
		</div>
	</div>
</section>

<!-- Footer -->
<footer class="bg-zinc-900 py-16 text-white">
	<div class="container mx-auto px-6 lg:px-20">
		<div class="mb-12 grid gap-8 md:grid-cols-4">
			<div>
				<h3 class="mb-4 text-2xl font-bold">LifeCard</h3>
				<p class="text-slate-400">
					La carte de santé universelle pour un accès aux soins partout dans le monde.
				</p>
			</div>

			<div>
				<h4 class="mb-4 font-semibold">Solutions</h4>
				<ul class="space-y-2 text-slate-400">
					<li><a href="#" class="transition hover:text-white">Pour Patients</a></li>
					<li><a href="#" class="transition hover:text-white">Pour Médecins</a></li>
					<li><a href="#" class="transition hover:text-white">Pour Hôpitaux</a></li>
					<li><a href="#" class="transition hover:text-white">Pour Gouvernements</a></li>
				</ul>
			</div>

			<div>
				<h4 class="mb-4 font-semibold">Entreprise</h4>
				<ul class="space-y-2 text-slate-400">
					<li><a href="#" class="transition hover:text-white">À Propos</a></li>
					<li><a href="#" class="transition hover:text-white">Blog</a></li>
					<li><a href="#" class="transition hover:text-white">Carrières</a></li>
					<li><a href="#" class="transition hover:text-white">Contact</a></li>
				</ul>
			</div>

			<div>
				<h4 class="mb-4 font-semibold">Suivez-nous</h4>
				<div class="flex gap-4">
					<a
						href="#"
						class="flex h-10 w-10 items-center justify-center rounded-full bg-slate-800 transition hover:bg-slate-700"
					>
						F
					</a>
					<a
						href="#"
						class="flex h-10 w-10 items-center justify-center rounded-full bg-slate-800 transition hover:bg-slate-700"
					>
						T
					</a>
					<a
						href="#"
						class="flex h-10 w-10 items-center justify-center rounded-full bg-slate-800 transition hover:bg-slate-700"
					>
						I
					</a>
				</div>
			</div>
		</div>

		<div
			class="flex flex-col items-center justify-between border-t border-slate-800 pt-8 text-sm text-slate-400 md:flex-row"
		>
			<p>© 2026 LifeCard CNSU. Tous droits réservés.</p>
			<div class="mt-4 flex gap-6 md:mt-0">
				<a href="#" class="transition hover:text-white">Conditions d'utilisation</a>
				<a href="#" class="transition hover:text-white">Politique de confidentialité</a>
			</div>
		</div>
	</div>
</footer>
