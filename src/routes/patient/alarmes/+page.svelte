<script lang="ts">
	import AppSidebar from '$lib/components/app-sidebar.svelte';
	import * as Breadcrumb from '$lib/components/ui/breadcrumb/index.js';
	import { Separator } from '$lib/components/ui/separator/index.js';
	import * as Sidebar from '$lib/components/ui/sidebar/index.js';
	import Card from '$lib/components/ui/card/card.svelte';
	import Badge from '$lib/components/ui/badge/badge.svelte';
	import Button from '$lib/components/ui/button/button.svelte';
	import * as Table from '$lib/components/ui/table/index.js';


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

	// Alarmes actives
	const alarmesActives = [
		{
			id: 1,
			medicament: 'Metformine 500mg',
			heure: '08:00',
			jours: ['Lun', 'Mar', 'Mer', 'Jeu', 'Ven', 'Sam', 'Dim'],
			type: 'Médicament',
			message: 'Prendre Metformine 500mg pendant le petit-déjeuner',
			sonnerie: 'Douce',
			vibration: true,
			repas: 'Pendant le repas',
			active: true
		},
		{
			id: 2,
			medicament: 'Ramipril 5mg',
			heure: '08:00',
			jours: ['Lun', 'Mar', 'Mer', 'Jeu', 'Ven', 'Sam', 'Dim'],
			type: 'Médicament',
			message: 'Prendre Ramipril 5mg le matin à jeun',
			sonnerie: 'Standard',
			vibration: true,
			repas: 'À jeun',
			active: true
		},
		{
			id: 3,
			medicament: 'Vitamine D 2000 UI',
			heure: '12:00',
			jours: ['Lun', 'Mar', 'Mer', 'Jeu', 'Ven', 'Sam', 'Dim'],
			type: 'Médicament',
			message: 'Prendre Vitamine D 2000 UI avec le déjeuner',
			sonnerie: 'Douce',
			vibration: false,
			repas: 'Pendant le repas',
			active: true
		},
		{
			id: 4,
			medicament: 'Aspirine 100mg',
			heure: '20:00',
			jours: ['Lun', 'Mar', 'Mer', 'Jeu', 'Ven', 'Sam', 'Dim'],
			type: 'Médicament',
			message: 'Prendre Aspirine 100mg pendant le dîner',
			sonnerie: 'Standard',
			vibration: true,
			repas: 'Pendant le repas',
			active: true
		},
		{
			id: 5,
			medicament: 'Rendez-vous Dr. Bernard',
			heure: '09:30',
			jours: ['Lun'],
			type: 'Rendez-vous',
			message: 'Consultation cardiologie - Apporter analyses sanguines',
			sonnerie: 'Forte',
			vibration: true,
			repas: '-',
			active: false
		}
	];

	// Historique des alarmes
	const historiqueAlarmes = [
		{
			id: 1,
			medicament: 'Metformine 500mg',
			heure: '08:00',
			date: '15/05/2026',
			statut: 'Pris',
			retard: 'À l\'heure'
		},
		{
			id: 2,
			medicament: 'Ramipril 5mg',
			heure: '08:00',
			date: '15/05/2026',
			statut: 'Pris',
			retard: '5 min'
		},
		{
			id: 3,
			medicament: 'Vitamine D 2000 UI',
			heure: '12:00',
			date: '15/05/2026',
			statut: 'Pris',
			retard: 'À l\'heure'
		},
		{
			id: 4,
			medicament: 'Aspirine 100mg',
			heure: '20:00',
			date: '14/05/2026',
			statut: 'Manqué',
			retard: '-'
		},
		{
			id: 5,
			medicament: 'Metformine 500mg',
			heure: '08:00',
			date: '14/05/2026',
			statut: 'Pris',
			retard: '15 min'
		}
	];

	// Statistiques
	const statistiques = {
		totalAlarmes: 5,
		alarmesActives: 4,
		prisesAujourdhui: 3,
		prisesManquees: 1,
		tauxAdherence: '95%'
	};

	function getStatutColor(statut: string) {
		const colors: Record<string, string> = {
			'Pris': 'bg-green-100 text-green-800 border-green-200',
			'Manqué': 'bg-red-100 text-red-800 border-red-200',
			'En attente': 'bg-orange-100 text-orange-800 border-orange-200',
			'À venir': 'bg-blue-100 text-blue-800 border-blue-200'
		};
		return colors[statut] || 'bg-slate-100 text-slate-800 border-slate-200';
	}

	function getTypeColor(type: string) {
		const colors: Record<string, string> = {
			'Médicament': 'bg-teal-100 text-teal-800 border-teal-200',
			'Rendez-vous': 'bg-purple-100 text-purple-800 border-purple-200',
			'Rappel': 'bg-orange-100 text-orange-800 border-orange-200'
		};
		return colors[type] || 'bg-slate-100 text-slate-800 border-slate-200';
	}
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
							<Breadcrumb.Page>Alarmes</Breadcrumb.Page>
						</Breadcrumb.Item>
					</Breadcrumb.List>
				</Breadcrumb.Root>
			</div>
		</header>

		<div class="flex flex-1 flex-col gap-6 p-6 pt-6">
			<!-- Header avec titre et actions -->
			<div class="flex items-center justify-between">
				<div>
					<h1 class="flex items-center gap-2 text-3xl font-bold text-slate-900">
						<svg class="h-8 w-8 text-teal-700" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
							/>
						</svg>
						Mes Alarmes
					</h1>
					<p class="mt-1 text-slate-600">Gérez vos rappels de médicaments et rendez-vous</p>
				</div>
				<div class="flex gap-2">
					<Button class="bg-teal-800 hover:bg-teal-700">
						<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M12 4v16m8-8H4"
							/>
						</svg>
						Nouvelle alarme
					</Button>
				</div>
			</div>

			<!-- Statistiques -->
			<div class="grid gap-4 md:grid-cols-5">
				<Card class="p-4">
					<div class="flex items-center gap-3">
						<div class="rounded-lg bg-teal-100 p-3 text-teal-800">
							<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
								/>
							</svg>
						</div>
						<div>
							<div class="text-2xl font-bold text-slate-900">{statistiques.totalAlarmes}</div>
							<div class="text-sm text-slate-600">Total alarmes</div>
						</div>
					</div>
				</Card>

				<Card class="p-4">
					<div class="flex items-center gap-3">
						<div class="rounded-lg bg-green-100 p-3 text-green-800">
							<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"
								/>
							</svg>
						</div>
						<div>
							<div class="text-2xl font-bold text-slate-900">{statistiques.alarmesActives}</div>
							<div class="text-sm text-slate-600">Alarmes actives</div>
						</div>
					</div>
				</Card>

				<Card class="p-4">
					<div class="flex items-center gap-3">
						<div class="rounded-lg bg-blue-100 p-3 text-blue-800">
							<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M5 13l4 4L19 7"
								/>
							</svg>
						</div>
						<div>
							<div class="text-2xl font-bold text-slate-900">{statistiques.prisesAujourdhui}</div>
							<div class="text-sm text-slate-600">Prises aujourd'hui</div>
						</div>
					</div>
				</Card>

				<Card class="p-4">
					<div class="flex items-center gap-3">
						<div class="rounded-lg bg-red-100 p-3 text-red-800">
							<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M6 18L18 6M6 6l12 12"
								/>
							</svg>
						</div>
						<div>
							<div class="text-2xl font-bold text-slate-900">{statistiques.prisesManquees}</div>
							<div class="text-sm text-slate-600">Prises manquées</div>
						</div>
					</div>
				</Card>

				<Card class="p-4">
					<div class="flex items-center gap-3">
						<div class="rounded-lg bg-purple-100 p-3 text-purple-800">
							<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"
								/>
							</svg>
						</div>
						<div>
							<div class="text-2xl font-bold text-slate-900">{statistiques.tauxAdherence}</div>
							<div class="text-sm text-slate-600">Taux d'adhérence</div>
						</div>
					</div>
				</Card>
			</div>

			<!-- Layout principal -->
			<div class="grid gap-6 lg:grid-cols-3">
				<!-- Colonne gauche : Alarmes actives -->
				<div class="lg:col-span-2 space-y-6">
					<Card class="p-6">
						<div class="mb-6 flex items-center justify-between">
							<div class="flex items-center gap-2">
								<svg class="h-6 w-6 text-teal-700" fill="none" stroke="currentColor" viewBox="0 0 24 24">
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
									/>
								</svg>
								<h2 class="text-xl font-bold text-slate-900">Alarmes Configurées</h2>
							</div>
							<Badge class="bg-teal-100 text-teal-800 border-teal-200">
								{statistiques.alarmesActives} actives
							</Badge>
						</div>

						<div class="space-y-4">
							{#each alarmesActives as alarme}
								<div class="rounded-lg border-2 {alarme.active ? 'border-teal-200 bg-white' : 'border-slate-200 bg-slate-50'} p-5 transition hover:shadow-md">
									<div class="flex items-start justify-between">
										<div class="flex-1">
											<div class="flex items-center gap-3">
												<div class="rounded-lg {alarme.active ? 'bg-teal-100 text-teal-800' : 'bg-slate-200 text-slate-600'} p-3">
													<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
														<path
															stroke-linecap="round"
															stroke-linejoin="round"
															stroke-width="2"
															d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
														/>
													</svg>
												</div>
												<div>
													<h3 class="font-bold text-lg text-slate-900">{alarme.medicament}</h3>
													<div class="flex items-center gap-2">
														<Badge class={getTypeColor(alarme.type)}>{alarme.type}</Badge>
														<span class="text-sm text-slate-500">{alarme.repas}</span>
													</div>
												</div>
											</div>

											<div class="mt-4 grid gap-3 md:grid-cols-2">
												<div>
													<div class="text-sm text-slate-500">Heure</div>
													<div class="font-semibold text-2xl text-teal-800">{alarme.heure}</div>
												</div>
												<div>
													<div class="text-sm text-slate-500">Sonnerie</div>
													<div class="font-semibold text-slate-900">{alarme.sonnerie}</div>
													<div class="text-xs text-slate-500">
														Vibration: {alarme.vibration ? 'Oui' : 'Non'}
													</div>
												</div>
												<div class="md:col-span-2">
													<div class="text-sm text-slate-500">Message</div>
													<div class="text-sm text-slate-700">{alarme.message}</div>
												</div>
												<div class="md:col-span-2">
													<div class="text-sm text-slate-500">Jours</div>
													<div class="flex flex-wrap gap-1 mt-1">
														{#each alarme.jours as jour}
															<span class="px-2 py-1 text-xs font-medium rounded bg-slate-100 text-slate-700">
																{jour}
															</span>
														{/each}
													</div>
												</div>
											</div>
										</div>

										<div class="ml-4 flex flex-col items-end gap-2">
											<!-- Toggle switch -->
											<button
												class="relative inline-flex h-6 w-11 items-center rounded-full transition {alarme.active ? 'bg-teal-600' : 'bg-slate-300'}"
											>
												<span
													class="inline-block h-4 w-4 transform rounded-full bg-white transition {alarme.active ? 'translate-x-6' : 'translate-x-1'}"
												></span>
											</button>
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
													d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
												/>
											</svg>
											Supprimer
										</Button>
									</div>
								</div>
							{/each}
						</div>
					</Card>
				</div>

				<!-- Colonne droite : Historique et conseils -->
				<div class="space-y-6">
					<!-- Prochaine alarme -->
					<Card class="p-6 bg-gradient-to-br from-teal-50 to-white border-2 border-teal-200">
						<div class="flex items-center gap-2 mb-4">
							<svg class="h-6 w-6 text-teal-700" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"
								/>
							</svg>
							<h3 class="font-bold text-slate-900">Prochaine alarme</h3>
						</div>
						<div class="text-center">
							<div class="text-5xl font-bold text-teal-800 mb-2">20:00</div>
							<div class="text-lg font-semibold text-slate-900">Aspirine 100mg</div>
							<div class="text-sm text-slate-600 mt-1">Pendant le dîner</div>
							<div class="mt-4 text-sm text-slate-500">
								Dans 4 heures et 30 minutes
							</div>
						</div>
					</Card>

					<!-- Historique des alarmes -->
					<Card class="p-6">
						<div class="mb-4 flex items-center gap-2">
							<svg class="h-5 w-5 text-teal-700" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"
								/>
							</svg>
							<h3 class="font-bold text-slate-900">Historique récent</h3>
						</div>

						<div class="space-y-3">
							{#each historiqueAlarmes as historique}
								<div class="flex items-center justify-between rounded-lg bg-slate-50 p-3">
									<div class="flex-1">
										<div class="text-sm font-semibold text-slate-900">{historique.medicament}</div>
										<div class="text-xs text-slate-600">
											{historique.date} à {historique.heure}
										</div>
									</div>
									<div class="text-right">
										<Badge class={getStatutColor(historique.statut)}>{historique.statut}</Badge>
										<div class="text-xs text-slate-500 mt-1">{historique.retard}</div>
									</div>
								</div>
							{/each}
						</div>

						<Button variant="outline" class="mt-4 w-full text-teal-700 hover:bg-teal-50">
							Voir tout l'historique
						</Button>
					</Card>

					<!-- Conseils -->
					<Card class="p-6 bg-amber-50 border-amber-200">
						<div class="flex items-start gap-3">
							<div class="text-2xl">💡</div>
							<div>
								<h3 class="font-bold text-slate-900 mb-2">Conseil</h3>
								<p class="text-sm text-slate-700">
									Activez les vibrations pour ne pas manquer vos prises de médicaments même en mode silencieux.
								</p>
							</div>
						</div>
					</Card>
				</div>
			</div>
		</div>
	</Sidebar.Inset>
</Sidebar.Provider>