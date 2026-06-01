<script lang="ts">
	import AppSidebar from '$lib/components/app-sidebar.svelte';
	import * as Breadcrumb from '$lib/components/ui/breadcrumb/index.js';
	import { Separator } from '$lib/components/ui/separator/index.js';
	import * as Sidebar from '$lib/components/ui/sidebar/index.js';
	import Card from '$lib/components/ui/card/card.svelte';
	import Badge from '$lib/components/ui/badge/badge.svelte';
	import Button from '$lib/components/ui/button/button.svelte';
	import * as Table from '$lib/components/ui/table/index.js';
	import Calendar20 from '$lib/components/calendar-20.svelte';

	// Données du patient
	const patient = {
		nom: 'Laurent',
		prenom: 'Dupont',
		dateNaissance: '15/05/1985',
		groupeSanguin: 'A-',
		taille: '1.70 m',
		poids: '75 kg',
		telephone: '+33 6 12 34 56 78',
		email: 'marie.dupont@email.fr',
		adresse: '123 Rue de la Santé, 75013 Paris'
	};

	// Date actuelle
	const today = new Date();
	const currentMonth = today.getMonth();
	const currentYear = today.getFullYear();
	const currentDay = today.getDate();

	// Jours de la semaine
	const daysOfWeek = ['Lun', 'Mar', 'Mer', 'Jeu', 'Ven', 'Sam', 'Dim'];

	// Mois
	const monthNames = [
		'Janvier',
		'Février',
		'Mars',
		'Avril',
		'Mai',
		'Juin',
		'Juillet',
		'Août',
		'Septembre',
		'Octobre',
		'Novembre',
		'Décembre'
	];

	// Générer les jours du mois
	function getDaysInMonth(month: number, year: number) {
		const firstDay = new Date(year, month, 1).getDay();
		const daysInMonth = new Date(year, month + 1, 0).getDate();
		const adjustedFirstDay = firstDay === 0 ? 6 : firstDay - 1; // Lundi = 0

		const days = [];
		// Jours vides avant le début du mois
		for (let i = 0; i < adjustedFirstDay; i++) {
			days.push({ day: null, isCurrentMonth: false });
		}
		// Jours du mois
		for (let i = 1; i <= daysInMonth; i++) {
			days.push({ day: i, isCurrentMonth: true });
		}
		return days;
	}

	const calendarDays = getDaysInMonth(currentMonth, currentYear);

	// Rendez-vous médicaux
	const rendezvous = [
		{
			id: 1,
			date: '15 Mai 2026',
			heure: '10:00',
			medecin: 'Dr. Laurent Bernard',
			specialite: 'Cardiologie',
			type: 'Consultation de suivi',
			lieu: 'Cabinet Médical, 45 Rue de la Santé, Paris',
			statut: 'Confirmé',
			rappel: '1 jour avant',
			notes: 'Apporter les résultats des analyses sanguines'
		},
		{
			id: 2,
			date: '20 Mai 2026',
			heure: '14:30',
			medecin: 'Dr. Sophie Martin',
			specialite: 'Médecine Générale',
			type: 'Contrôle annuel',
			lieu: 'Centre Médical Central, 12 Avenue de la République',
			statut: 'À confirmer',
			rappel: '2 jours avant',
			notes: ''
		},
		{
			id: 3,
			date: '25 Mai 2026',
			heure: '09:00',
			medecin: 'Dr. Ahmed El Kadi',
			specialite: 'Ophtalmologie',
			type: 'Examen de la vue',
			lieu: 'Clinique Vision, 78 Boulevard Saint-Michel',
			statut: 'Confirmé',
			rappel: '1 jour avant',
			notes: 'Prévoir 1h30 pour dilatation pupille'
		},
		{
			id: 4,
			date: '2 Juin 2026',
			heure: '16:00',
			medecin: 'Dr. Marie Leclerc',
			specialite: 'Kinésithérapie',
			type: 'Séance de rééducation',
			lieu: 'Cabinet Kiné Plus, 23 Rue Victor Hugo',
			statut: 'Confirmé',
			rappel: '1 jour avant',
			notes: 'Apporter une serviette'
		}
	];

	// Rappels de médicaments (agenda de prise)
	const medicaments = [
		{
			nom: 'Metformine',
			dosage: '500mg',
			frequence: '2 fois par jour',
			horaires: ['08:00', '20:00'],
			priseAvecRepas: true,
			instructions: 'À prendre pendant les repas',
			dateDebut: '01/01/2024',
			dateFin: 'Traitement continu',
			couleur: 'bg-blue-100 text-blue-800 border-blue-200'
		},
		{
			nom: 'Ramipril',
			dosage: '5mg',
			frequence: '1 fois par jour',
			horaires: ['08:00'],
			priseAvecRepas: false,
			instructions: 'Le matin à jeun',
			dateDebut: '15/03/2024',
			dateFin: 'Traitement continu',
			couleur: 'bg-green-100 text-green-800 border-green-200'
		},
		{
			nom: 'Aspirine',
			dosage: '100mg',
			frequence: '1 fois par jour',
			horaires: ['20:00'],
			priseAvecRepas: true,
			instructions: 'Le soir pendant le dîner',
			dateDebut: '01/02/2024',
			dateFin: 'Traitement continu',
			couleur: 'bg-purple-100 text-purple-800 border-purple-200'
		},
		{
			nom: 'Vitamine D',
			dosage: '2000 UI',
			frequence: '1 fois par jour',
			horaires: ['12:00'],
			priseAvecRepas: true,
			instructions: 'À midi avec le repas',
			dateDebut: '10/01/2024',
			dateFin: '31/12/2026',
			couleur: 'bg-orange-100 text-orange-800 border-orange-200'
		}
	];

	// Prochaines prises aujourd'hui
	const prochainePrises = [
		{
			medicament: 'Metformine 500mg',
			heure: '20:00',
			statut: 'À venir',
			instructions: 'Pendant le dîner'
		}
	];

	// Historique des prises (aujourd'hui)
	const historiquePrises = [
		{
			medicament: 'Metformine 500mg',
			heurePrevue: '08:00',
			heurePrise: '08:15',
			statut: 'Pris',
			retard: '15 min'
		},
		{
			medicament: 'Ramipril 5mg',
			heurePrevue: '08:00',
			heurePrise: '08:05',
			statut: 'Pris',
			retard: '5 min'
		},
		{
			medicament: 'Vitamine D 2000 UI',
			heurePrevue: '12:00',
			heurePrise: '12:00',
			statut: 'Pris',
			retard: 'À l\'heure'
		}
	];

	function getStatutColor(statut: string) {
		const colors: Record<string, string> = {
			Confirmé: 'bg-green-100 text-green-800 border-green-200',
			'À confirmer': 'bg-orange-100 text-orange-800 border-orange-200',
			Annulé: 'bg-red-100 text-red-800 border-red-200',
			Terminé: 'bg-slate-100 text-slate-800 border-slate-200',
			Pris: 'bg-green-100 text-green-800 border-green-200',
			'À venir': 'bg-blue-100 text-blue-800 border-blue-200',
			Manqué: 'bg-red-100 text-red-800 border-red-200'
		};
		return colors[statut] || 'bg-slate-100 text-slate-800 border-slate-200';
	}

	// Jours avec événements (pour le calendrier)
	const eventDays = [15, 20, 25];
</script>

<Sidebar.Provider>
	<AppSidebar />
	<Sidebar.Inset>
		<header
			class="flex h-16 shrink-0 items-center gap-2 border-b transition-[width,height] ease-linear group-has-data-[collapsible=icon]/sidebar-wrapper:h-12"
		>
			<div class="flex items-center gap-2 px-4">
				<Sidebar.Trigger class="-ms-1" />
				<Separator orientation="vertical" class="me-2 data-[orientation=vertical]:h-4" />
				<Breadcrumb.Root>
					<Breadcrumb.List>
						<Breadcrumb.Item class="hidden md:block">
							<Breadcrumb.Link href="/dashboard">Tableau de bord</Breadcrumb.Link>
						</Breadcrumb.Item>
						<Breadcrumb.Separator class="hidden md:block" />
						<Breadcrumb.Item>
							<Breadcrumb.Page>Agenda</Breadcrumb.Page>
						</Breadcrumb.Item>
					</Breadcrumb.List>
				</Breadcrumb.Root>
			</div>
		</header>

		<div class="flex flex-1 flex-col gap-6 p-6 pt-6">
			<!-- Header avec salutation -->
			<div class="flex items-center justify-between">
				<h1 class="flex items-center gap-2 text-3xl font-bold text-slate-900">
					Mon Agenda 
				</h1>
				<div class="flex gap-2">
					
					<Button variant="outline" class="border-teal-700 text-teal-800 hover:bg-teal-50">
						<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
							/>
						</svg>
						Planning du jour
					</Button>
					<Button variant="outline" class="border-teal-700 text-teal-800 hover:bg-teal-50">
						<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M12 4v16m8-8H4"
							/>
						</svg>
						Nouvel évènement
					</Button>
					<Button class="bg-teal-800 hover:bg-teal-700">
						<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
							/>
						</svg>
						Mes rappels
					</Button>
				</div>
			</div>

			<!-- Layout : Calendrier + Sections -->
			<div class="grid gap-6 lg:grid-cols-5">
				<!-- Colonne gauche : Calendrier + Prochaines prises -->
				<div class="space-y-6 lg:col-span-3">
					<!-- Calendrier du mois -->
                         <Card class="p-6">
						<div class="mb-4 flex items-center justify-between">
							<h2 class="text-lg font-bold text-slate-900">
								{monthNames[currentMonth]} {currentYear}
							</h2>
							<div class="flex gap-2">
								<Button size="sm" variant="ghost">
									<svg class="h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path
											stroke-linecap="round"
											stroke-linejoin="round"
											stroke-width="2"
											d="M15 19l-7-7 7-7"
										/>
									</svg>
								</Button>
								<Button size="sm" variant="ghost">
									<svg class="h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path
											stroke-linecap="round"
											stroke-linejoin="round"
											stroke-width="2"
											d="M9 5l7 7-7 7"
										/>
									</svg>
								</Button>
							</div>
						</div>

						<!-- Grille du calendrier -->
						<div class="grid grid-cols-7 gap-2">
							<!-- En-têtes des jours -->
							{#each daysOfWeek as day}
								<div class="text-center text-xs font-semibold text-slate-600">
									{day}
								</div>
							{/each}

							<!-- Jours du mois -->
							{#each calendarDays as { day, isCurrentMonth }}
								<div
									class="relative aspect-square rounded-lg border {isCurrentMonth
										? 'border-slate-200 bg-white hover:bg-slate-50'
										: 'border-transparent bg-slate-50'} cursor-pointer transition"
								>
									{#if day}
										<div
											class="flex h-full w-full flex-col items-center justify-center {day ===
											currentDay
												? 'rounded-lg bg-teal-800 text-white font-bold'
												: 'text-slate-700'}"
										>
											<span class="text-sm">{day}</span>
											{#if eventDays.includes(day)}
												<div class="mt-1 h-1.5 w-1.5 rounded-full bg-orange-500"></div>
											{/if}
										</div>
									{/if}
								</div>
							{/each}
						</div>

						<div class="mt-4 flex items-center gap-4 text-xs text-slate-600">
							<div class="flex items-center gap-1">
								<div class="h-2 w-2 rounded-full bg-teal-800"></div>
								<span>Aujourd'hui</span>
							</div>
							<div class="flex items-center gap-1">
								<div class="h-2 w-2 rounded-full bg-orange-500"></div>
								<span>Rendez-vous</span>
							</div>
						</div>
					</Card>
                         <Calendar20 />
				</div>

				<!-- Colonne droite : Rendez-vous + Médicaments -->
				<div class="space-y-6 lg:col-span-2">
					<!-- Rendez-vous médicaux à venir -->
					<Card class="p-6">
						<div class="mb-6 flex items-center justify-between">
							<div class="flex items-center gap-2 text-teal-700">
								<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
									/>
								</svg>
								<h2 class="text-xl font-bold text-slate-900">Rendez-vous Médicaux</h2>
							</div>
							<Badge class="bg-orange-100 text-orange-800 border-orange-200">
								{rendezvous.length} rendez-vous
							</Badge>
						</div>

						<div class="space-y-4">
							{#each rendezvous as rdv}
								<div class="rounded-lg border-2 border-slate-200 p-5 transition hover:border-teal-300 hover:shadow-md">
									<div class="flex items-start justify-between">
										<div class="flex-1">
											<div class="flex items-center gap-3">
												<div class="rounded-lg bg-teal-100 p-3 text-teal-800">
													<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
														<path
															stroke-linecap="round"
															stroke-linejoin="round"
															stroke-width="2"
															d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
														/>
													</svg>
												</div>
												<div>
													<h3 class="font-bold text-lg text-slate-900">{rdv.medecin}</h3>
													<div class="text-sm text-teal-700">{rdv.specialite}</div>
												</div>
											</div>

											<div class="mt-4 grid gap-3 md:grid-cols-2">
												<div>
													<div class="text-sm text-slate-500">Date & Heure</div>
													<div class="font-semibold text-slate-900">
														{rdv.date} à {rdv.heure}
													</div>
												</div>
												<div>
													<div class="text-sm text-slate-500">Type</div>
													<div class="font-semibold text-slate-900">{rdv.type}</div>
												</div>
												<div class="md:col-span-2">
													<div class="text-sm text-slate-500">Lieu</div>
													<div class="text-sm text-slate-700">{rdv.lieu}</div>
												</div>
												{#if rdv.notes}
													<div class="md:col-span-2">
														<div class="text-sm text-slate-500">Notes</div>
														<div class="text-sm text-orange-700 italic">📌 {rdv.notes}</div>
													</div>
												{/if}
											</div>
										</div>

										<div class="ml-4 text-right">
											<Badge class={getStatutColor(rdv.statut)}>{rdv.statut}</Badge>
											<div class="mt-2 text-xs text-slate-500">
												🔔 Rappel: {rdv.rappel}
											</div>
										</div>
									</div>

									<div class="mt-4 flex gap-2 border-t pt-4">
										<Button size="sm" variant="outline" class="flex-1">
											<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
												<path
													stroke-linecap="round"
													stroke-linejoin="round"
													stroke-width="2"
													d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"
												/>
											</svg>
											Modifier
										</Button>
										<Button size="sm" variant="outline" class="flex-1 text-red-600 hover:bg-red-50">
											<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
												<path
													stroke-linecap="round"
													stroke-linejoin="round"
													stroke-width="2"
													d="M6 18L18 6M6 6l12 12"
												/>
											</svg>
											Annuler
										</Button>
										<Button size="sm" class="flex-1 bg-teal-700 hover:bg-teal-800">
											<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
												<path
													stroke-linecap="round"
													stroke-linejoin="round"
													stroke-width="2"
													d="M9 5l7 7-7 7"
												/>
											</svg>
											Itinéraire
										</Button>
									</div>
								</div>
							{/each}
						</div>
					</Card>
				</div>
			</div>
		</div>
	</Sidebar.Inset>
</Sidebar.Provider>