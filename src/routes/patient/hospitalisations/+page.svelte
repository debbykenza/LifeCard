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

	// Informations d'hospitalisation
	const hospitalisation = {
		numero: 'H-2026-00234',
		service: 'Cardiologie',
		chambre: '204',
		lit: 'A',
		dateAdmission: '10 Mai 2026',
		dateSortiePrevue: '17 Mai 2026',
		duree: '7 jours',
		statut: 'En cours',
		medecinResponsable: 'Dr. Laurent Bernard',
		priorite: 'Moyenne'
	};

	// Motif d'hospitalisation
	const motif = {
		raisonPrincipale: 'Douleurs thoraciques et hypertension sévère',
		diagnostic: 'Insuffisance cardiaque décompensée',
		symptomes: 'Dyspnée, œdème des membres inférieurs, fatigue intense',
		complications: 'Risque d\'arythmie cardiaque',
		antecedents: 'Diabète Type 2, Hypertension artérielle'
	};

	// État actuel
	const etatActuel = {
		etatGeneral: 'Stable',
		douleur: '3/10',
		mobilite: 'Réduite',
		conscience: 'Alerte',
		alimentation: 'Normale',
		respiration: 'Assistée',
		observations: 'Patient sous surveillance continue. Amélioration progressive.'
	};

	const badges = [
		{ label: 'Stable', color: 'bg-green-100 text-green-800 border-green-200' },
		{ label: 'Sous surveillance', color: 'bg-orange-100 text-orange-800 border-orange-200' },
		{ label: 'Diabétique', color: 'bg-blue-100 text-blue-800 border-blue-200' },
		{ label: 'Sous oxygène', color: 'bg-purple-100 text-purple-800 border-purple-200' }
	];

	// Constantes vitales
	const dernieresConstantes = {
		temperature: '37.2°C',
		tension: '130/85 mmHg',
		frequenceCardiaque: '78 bpm',
		saturationOxygene: '96%',
		glycemie: '1.20 g/L',
		poids: '75 kg',
		frequenceRespiratoire: '16/min'
	};

	const historiqueConstantes = [
		{
			heure: '14:00',
			temperature: '37.2°C',
			tension: '130/85',
			pouls: '78',
			oxygene: '96%'
		},
		{
			heure: '10:00',
			temperature: '37.5°C',
			tension: '135/90',
			pouls: '82',
			oxygene: '95%'
		},
		{
			heure: '06:00',
			temperature: '37.8°C',
			tension: '140/92',
			pouls: '85',
			oxygene: '94%'
		}
	];

	// Soins et actes médicaux
	const soins = [
		{
			type: 'Injection d\'insuline',
			heurePrevue: '13:00',
			frequence: 'Quotidienne',
			statut: 'Effectué',
			effectuePar: 'Infirmière Kenza',
			notes: 'Injection sous-cutanée sans incident'
		},
		{
			type: 'Prise de tension',
			heurePrevue: '18:00',
			frequence: 'Toutes les 4h',
			statut: 'En attente',
			effectuePar: '',
			notes: ''
		},
		{
			type: 'Perfusion',
			heurePrevue: '08:00',
			frequence: 'Continue',
			statut: 'Effectué',
			effectuePar: 'Infirmier Marc',
			notes: 'Perfusion de sérum physiologique'
		},
		{
			type: 'Kinésithérapie respiratoire',
			heurePrevue: '15:00',
			frequence: '2x/jour',
			statut: 'Retardé',
			effectuePar: 'Kiné Sophie',
			notes: 'Patient fatigué, reporté à 16h'
		}
	];

	// Personnel médical
	const personnel = [
		{
			nom: 'Dr. Laurent Bernard',
			role: 'Cardiologue',
			horaires: '08h - 16h',
			taches: 'Suivi cardiaque quotidien'
		},
		{
			nom: 'Kenza Beglah',
			role: 'Infirmière',
			horaires: '07h - 15h',
			taches: 'Injections, constantes, soins'
		},
		{
			nom: 'Marc Dubois',
			role: 'Infirmier',
			horaires: '15h - 23h',
			taches: 'Surveillance nocturne'
		},
		{
			nom: 'Sophie Martin',
			role: 'Kinésithérapeute',
			horaires: '10h - 14h',
			taches: 'Rééducation respiratoire'
		}
	];

	// Médicaments administrés
	const medicaments = [
		{
			medicament: 'Ramipril',
			dosage: '5mg',
			frequence: '1x/jour',
			heure: '08:00',
			voie: 'Orale',
			administrePar: 'Inf. Kenza',
			statut: 'Effectué'
		},
		{
			medicament: 'Metformine',
			dosage: '500mg',
			frequence: '2x/jour',
			heure: '08:00 - 20:00',
			voie: 'Orale',
			administrePar: 'Inf. Marc',
			statut: 'Effectué'
		},
		{
			medicament: 'Furosémide',
			dosage: '40mg',
			frequence: '1x/jour',
			heure: '12:00',
			voie: 'Intraveineuse',
			administrePar: 'Inf. Kenza',
			statut: 'En attente'
		}
	];

	// Examens médicaux
	const examens = [
		{
			type: 'ECG',
			date: '10 Mai 2026',
			resultat: 'Rythme sinusal normal',
			medecin: 'Dr. Bernard'
		},
		{
			type: 'Prise de sang',
			date: '11 Mai 2026',
			resultat: 'En attente',
			medecin: 'Dr. Martin'
		},
		{
			type: 'Radiographie thoracique',
			date: '10 Mai 2026',
			resultat: 'Cardiomégalie modérée',
			medecin: 'Dr. Bernard'
		}
	];

	// Notes et observations
	const notes = [
		{
			date: '13 Mai 2026 - 14:00',
			auteur: 'Inf. Kenza',
			note: 'Patient plus stable. Température en baisse. Bonne réponse au traitement diurétique.'
		},
		{
			date: '12 Mai 2026 - 22:00',
			auteur: 'Inf. Marc',
			note: 'Nuit calme. Patient a bien dormi. Aucun incident à signaler.'
		},
		{
			date: '12 Mai 2026 - 10:00',
			auteur: 'Dr. Bernard',
			note: 'Amélioration de l\'état général. Réduction des œdèmes des membres inférieurs. Maintien du traitement actuel.'
		}
	];

	// Planning journalier
	const planning = [
		{ heure: '08:00', activite: 'Médicaments du matin', statut: 'Effectué' },
		{ heure: '10:00', activite: 'Prise de constantes', statut: 'Effectué' },
		{ heure: '12:00', activite: 'Perfusion diurétique', statut: 'En attente' },
		{ heure: '13:00', activite: 'Injection insuline', statut: 'Effectué' },
		{ heure: '15:00', activite: 'Kinésithérapie', statut: 'En attente' },
		{ heure: '16:00', activite: 'Visite médecin', statut: 'Programmé' },
		{ heure: '18:00', activite: 'Prise de tension', statut: 'Programmé' },
		{ heure: '20:00', activite: 'Médicaments du soir', statut: 'Programmé' }
	];

	function getStatutColor(statut: string) {
		const colors: Record<string, string> = {
			'En cours': 'bg-blue-100 text-blue-800 border-blue-200',
			'Effectué': 'bg-green-100 text-green-800 border-green-200',
			'En attente': 'bg-orange-100 text-orange-800 border-orange-200',
			'Retardé': 'bg-red-100 text-red-800 border-red-200',
			'Programmé': 'bg-purple-100 text-purple-800 border-purple-200'
		};
		return colors[statut] || 'bg-slate-100 text-slate-800 border-slate-200';
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
							<Breadcrumb.Page>Hospitalisations</Breadcrumb.Page>
						</Breadcrumb.Item>
					</Breadcrumb.List>
				</Breadcrumb.Root>
			</div>
		</header>

		<div class="flex flex-1 flex-col gap-6 p-6 pt-6">
			<!-- Header avec salutation -->
			<div class="flex items-center justify-between">
				<h1 class="flex items-center gap-2 text-3xl font-bold text-slate-900">
					Bonjour, {patient.prenom} 👋
				</h1>
				<Badge class={getStatutColor(hospitalisation.statut)}>
					{hospitalisation.statut}
				</Badge>
			</div>

			<!-- Layout principal : 2 colonnes -->
			<div class="grid gap-6 lg:grid-cols-3">
				<!-- Colonne principale (gauche - 2/3) -->
				<div class="space-y-6 lg:col-span-2">
					<!-- 1. Informations générales de l'hospitalisation -->
					<Card class="p-6">
						<div class="mb-4 flex items-center gap-2 text-teal-700">
							<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4"
								/>
							</svg>
							<h2 class="text-xl font-bold text-slate-900">Informations Générales</h2>
						</div>

						<div class="grid gap-4 md:grid-cols-2">
							<div class="space-y-3">
								<div>
									<span class="text-sm text-slate-500">Numéro d'hospitalisation</span>
									<div class="font-semibold text-slate-900">{hospitalisation.numero}</div>
								</div>
								<div>
									<span class="text-sm text-slate-500">Service / Unité</span>
									<div class="font-semibold text-slate-900">{hospitalisation.service}</div>
								</div>
								<div class="flex gap-4">
									<div>
										<span class="text-sm text-slate-500">Chambre</span>
										<div class="font-semibold text-slate-900">{hospitalisation.chambre}</div>
									</div>
									<div>
										<span class="text-sm text-slate-500">Lit</span>
										<div class="font-semibold text-slate-900">{hospitalisation.lit}</div>
									</div>
								</div>
							</div>

							<div class="space-y-3">
								<div>
									<span class="text-sm text-slate-500">Date d'admission</span>
									<div class="font-semibold text-slate-900">{hospitalisation.dateAdmission}</div>
								</div>
								<div>
									<span class="text-sm text-slate-500">Date prévue de sortie</span>
									<div class="font-semibold text-slate-900">{hospitalisation.dateSortiePrevue}</div>
								</div>
								<div>
									<span class="text-sm text-slate-500">Durée d'hospitalisation</span>
									<div class="font-semibold text-slate-900">{hospitalisation.duree}</div>
								</div>
							</div>
						</div>

						<div class="mt-4 flex items-center justify-between border-t pt-4">
							<div>
								<span class="text-sm text-slate-500">Médecin responsable</span>
								<div class="font-semibold text-slate-900">{hospitalisation.medecinResponsable}</div>
							</div>
							<Badge class="bg-yellow-100 text-yellow-800 border-yellow-200">
								Priorité: {hospitalisation.priorite}
							</Badge>
						</div>
					</Card>

					<!-- 2. Motif d'hospitalisation -->
					<Card class="p-6">
						<div class="mb-4 flex items-center gap-2 text-teal-700">
							<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"
								/>
							</svg>
							<h2 class="text-xl font-bold text-slate-900">Motif d'Hospitalisation</h2>
						</div>

						<div class="space-y-3">
							<div>
								<span class="text-sm font-semibold text-slate-700">Raison principale:</span>
								<p class="text-slate-900">{motif.raisonPrincipale}</p>
							</div>
							<div>
								<span class="text-sm font-semibold text-slate-700">Diagnostic:</span>
								<p class="text-slate-900">{motif.diagnostic}</p>
							</div>
							<div>
								<span class="text-sm font-semibold text-slate-700">Symptômes observés:</span>
								<p class="text-slate-600">{motif.symptomes}</p>
							</div>
							<div>
								<span class="text-sm font-semibold text-slate-700">Complications possibles:</span>
								<p class="text-orange-700">{motif.complications}</p>
							</div>
							<div>
								<span class="text-sm font-semibold text-slate-700">Antécédents liés:</span>
								<p class="text-slate-600">{motif.antecedents}</p>
							</div>
						</div>
					</Card>

					<!-- 5. Soins et actes médicaux -->
					<Card class="p-6">
						<div class="mb-4 flex items-center justify-between">
							<div class="flex items-center gap-2 text-teal-700">
								<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-6 9l2 2 4-4"
									/>
								</svg>
								<h2 class="text-xl font-bold text-slate-900">Soins & Actes Médicaux</h2>
							</div>
							<Button size="sm" class="bg-teal-600 hover:bg-teal-700">
								<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M12 4v16m8-8H4"
									/>
								</svg>
								Ajouter un soin
							</Button>
						</div>

						<div class="space-y-4">
							{#each soins as soin}
								<div class="rounded-lg border border-slate-200 p-4">
									<div class="flex items-start justify-between">
										<div class="flex-1">
											<div class="flex items-center gap-3">
												<h3 class="font-semibold text-slate-900">{soin.type}</h3>
												<Badge class={getStatutColor(soin.statut)}>{soin.statut}</Badge>
											</div>
											<div class="mt-2 grid gap-2 text-sm md:grid-cols-3">
												<div>
													<span class="text-slate-500">Heure prévue:</span>
													<span class="ml-1 font-medium">{soin.heurePrevue}</span>
												</div>
												<div>
													<span class="text-slate-500">Fréquence:</span>
													<span class="ml-1 font-medium">{soin.frequence}</span>
												</div>
												{#if soin.effectuePar}
													<div>
														<span class="text-slate-500">Par:</span>
														<span class="ml-1 font-medium">{soin.effectuePar}</span>
													</div>
												{/if}
											</div>
											{#if soin.notes}
												<p class="mt-2 text-sm text-slate-600 italic">{soin.notes}</p>
											{/if}
										</div>
									</div>
								</div>
							{/each}
						</div>
					</Card>

					<!-- 7. Médicaments administrés -->
					<Card class="p-6">
						<div class="mb-4 flex items-center gap-2 text-teal-700">
							<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"
								/>
							</svg>
							<h2 class="text-xl font-bold text-slate-900">Médicaments Administrés</h2>
						</div>

						<div class="overflow-x-auto">
							<Table.Root>
								<Table.Header>
									<Table.Row>
										<Table.Head>Médicament</Table.Head>
										<Table.Head>Dosage</Table.Head>
										<Table.Head>Fréquence</Table.Head>
										<Table.Head>Heure</Table.Head>
										<Table.Head>Voie</Table.Head>
										<Table.Head>Administré par</Table.Head>
										<Table.Head>Statut</Table.Head>
									</Table.Row>
								</Table.Header>
								<Table.Body>
									{#each medicaments as med}
										<Table.Row>
											<Table.Cell class="font-medium">{med.medicament}</Table.Cell>
											<Table.Cell>{med.dosage}</Table.Cell>
											<Table.Cell>{med.frequence}</Table.Cell>
											<Table.Cell>{med.heure}</Table.Cell>
											<Table.Cell>{med.voie}</Table.Cell>
											<Table.Cell class="text-sm">{med.administrePar}</Table.Cell>
											<Table.Cell>
												<Badge class={getStatutColor(med.statut)}>{med.statut}</Badge>
											</Table.Cell>
										</Table.Row>
									{/each}
								</Table.Body>
							</Table.Root>
						</div>
					</Card>

					<!-- 9. Notes et observations -->
					<Card class="p-6">
						<div class="mb-4 flex items-center justify-between">
							<div class="flex items-center gap-2 text-teal-700">
								<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"
									/>
								</svg>
								<h2 class="text-xl font-bold text-slate-900">Notes & Observations</h2>
							</div>
							<Button size="sm" variant="outline">
								<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M12 4v16m8-8H4"
									/>
								</svg>
								Ajouter une note
							</Button>
						</div>

						<div class="space-y-4">
							{#each notes as note}
								<div class="rounded-lg border-l-4 border-teal-500 bg-slate-50 p-4">
									<div class="mb-2 flex items-center justify-between">
										<span class="text-sm font-semibold text-teal-700">{note.auteur}</span>
										<span class="text-xs text-slate-500">{note.date}</span>
									</div>
									<p class="text-slate-700">{note.note}</p>
								</div>
							{/each}
						</div>
					</Card>

					<!-- 8. Examens médicaux -->
					<Card class="p-6">
						<div class="mb-4 flex items-center gap-2 text-teal-700">
							<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"
								/>
							</svg>
							<h2 class="text-xl font-bold text-slate-900">Examens & Résultats</h2>
						</div>

						<div class="space-y-3">
							{#each examens as examen}
								<div class="flex items-center justify-between rounded-lg border border-slate-200 p-4">
									<div class="flex-1">
										<div class="font-semibold text-slate-900">{examen.type}</div>
										<div class="mt-1 text-sm text-slate-600">{examen.resultat}</div>
									</div>
									<div class="text-right">
										<div class="text-sm text-slate-500">{examen.date}</div>
										<div class="text-xs text-slate-400">{examen.medecin}</div>
									</div>
								</div>
							{/each}
						</div>
					</Card>
				</div>

				<!-- Colonne de droite (1/3) -->
				<div class="space-y-6">
					<!-- 3. État actuel du patient -->
					<Card class="p-6">
						<div class="mb-4 flex items-center gap-2 text-teal-700">
							<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"
								/>
							</svg>
							<h2 class="text-lg font-bold text-slate-900">État Actuel</h2>
						</div>

						<div class="mb-4 flex flex-wrap gap-2">
							{#each badges as badge}
								<Badge class={badge.color}>{badge.label}</Badge>
							{/each}
						</div>

						<div class="space-y-2 text-sm">
							<div class="flex justify-between">
								<span class="text-slate-600">État général:</span>
								<span class="font-semibold text-slate-900">{etatActuel.etatGeneral}</span>
							</div>
							<div class="flex justify-between">
								<span class="text-slate-600">Douleur:</span>
								<span class="font-semibold">{etatActuel.douleur}</span>
							</div>
							<div class="flex justify-between">
								<span class="text-slate-600">Mobilité:</span>
								<span class="font-semibold">{etatActuel.mobilite}</span>
							</div>
							<div class="flex justify-between">
								<span class="text-slate-600">Conscience:</span>
								<span class="font-semibold">{etatActuel.conscience}</span>
							</div>
							<div class="flex justify-between">
								<span class="text-slate-600">Alimentation:</span>
								<span class="font-semibold">{etatActuel.alimentation}</span>
							</div>
							<div class="flex justify-between">
								<span class="text-slate-600">Respiration:</span>
								<span class="font-semibold">{etatActuel.respiration}</span>
							</div>
						</div>

						<div class="mt-4 rounded-lg bg-blue-50 p-3 text-sm text-blue-900">
							<p>{etatActuel.observations}</p>
						</div>
					</Card>

					<!-- 4. Constantes vitales -->
					<Card class="p-6">
						<div class="mb-4 flex items-center gap-2 text-teal-700">
							<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"
								/>
							</svg>
							<h2 class="text-lg font-bold text-slate-900">Constantes Vitales</h2>
						</div>

						<div class="mb-4 space-y-3">
							<div class="rounded-lg bg-gradient-to-r from-red-50 to-red-100 p-3">
								<div class="text-xs text-red-700">Température</div>
								<div class="text-2xl font-bold text-red-900">
									{dernieresConstantes.temperature}
								</div>
							</div>

							<div class="rounded-lg bg-gradient-to-r from-blue-50 to-blue-100 p-3">
								<div class="text-xs text-blue-700">Tension Artérielle</div>
								<div class="text-2xl font-bold text-blue-900">{dernieresConstantes.tension}</div>
							</div>

							<div class="grid grid-cols-2 gap-3">
								<div class="rounded-lg bg-gradient-to-r from-purple-50 to-purple-100 p-3">
									<div class="text-xs text-purple-700">Pouls</div>
									<div class="text-xl font-bold text-purple-900">
										{dernieresConstantes.frequenceCardiaque}
									</div>
								</div>

								<div class="rounded-lg bg-gradient-to-r from-green-50 to-green-100 p-3">
									<div class="text-xs text-green-700">SpO2</div>
									<div class="text-xl font-bold text-green-900">
										{dernieresConstantes.saturationOxygene}
									</div>
								</div>
							</div>

							<div class="grid grid-cols-2 gap-3">
								<div class="rounded-lg bg-gradient-to-r from-orange-50 to-orange-100 p-3">
									<div class="text-xs text-orange-700">Glycémie</div>
									<div class="text-lg font-bold text-orange-900">
										{dernieresConstantes.glycemie}
									</div>
								</div>

								<div class="rounded-lg bg-gradient-to-r from-teal-50 to-teal-100 p-3">
									<div class="text-xs text-teal-700">Poids</div>
									<div class="text-lg font-bold text-teal-900">{dernieresConstantes.poids}</div>
								</div>
							</div>
						</div>

						<!-- Historique -->
						<div class="mt-6">
							<h3 class="mb-3 text-sm font-semibold text-slate-700">Historique (Aujourd'hui)</h3>
							<div class="overflow-x-auto">
								<Table.Root>
									<Table.Header>
										<Table.Row class="text-xs">
											<Table.Head class="p-2">Heure</Table.Head>
											<Table.Head class="p-2">T°</Table.Head>
											<Table.Head class="p-2">TA</Table.Head>
											<Table.Head class="p-2">Pouls</Table.Head>
											<Table.Head class="p-2">SpO2</Table.Head>
										</Table.Row>
									</Table.Header>
									<Table.Body>
										{#each historiqueConstantes as constante}
											<Table.Row class="text-xs">
												<Table.Cell class="p-2 font-medium">{constante.heure}</Table.Cell>
												<Table.Cell class="p-2">{constante.temperature}</Table.Cell>
												<Table.Cell class="p-2">{constante.tension}</Table.Cell>
												<Table.Cell class="p-2">{constante.pouls}</Table.Cell>
												<Table.Cell class="p-2">{constante.oxygene}</Table.Cell>
											</Table.Row>
										{/each}
									</Table.Body>
								</Table.Root>
							</div>
						</div>
					</Card>

					<!-- 6. Personnel médical affecté -->
					<Card class="p-6">
						<div class="mb-4 flex items-center gap-2 text-teal-700">
							<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"
								/>
							</svg>
							<h2 class="text-lg font-bold text-slate-900">Personnel Affecté</h2>
						</div>

						<div class="space-y-3">
							{#each personnel as personne}
								<div class="rounded-lg border border-slate-200 p-3">
									<div class="font-semibold text-slate-900">{personne.nom}</div>
									<div class="text-sm text-teal-700">{personne.role}</div>
									<div class="mt-2 text-xs text-slate-600">
										<div>🕐 {personne.horaires}</div>
										<div class="mt-1">📋 {personne.taches}</div>
									</div>
								</div>
							{/each}
						</div>
					</Card>

					<!-- 10. Planning journalier -->
					<Card class="p-6">
						<div class="mb-4 flex items-center gap-2 text-teal-700">
							<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"
								/>
							</svg>
							<h2 class="text-lg font-bold text-slate-900">Planning du Jour</h2>
						</div>

						<div class="space-y-2">
							{#each planning as activite}
								<div class="flex items-center gap-3 rounded-lg border-l-4 {getStatutColor(activite.statut).includes('green') ? 'border-green-500 bg-green-50' : getStatutColor(activite.statut).includes('orange') ? 'border-orange-500 bg-orange-50' : 'border-purple-500 bg-purple-50'} p-3">
									<div class="font-mono text-sm font-semibold text-slate-700">
										{activite.heure}
									</div>
									<div class="flex-1">
										<div class="text-sm font-medium text-slate-900">{activite.activite}</div>
										<Badge class="{getStatutColor(activite.statut)} mt-1 text-xs">
											{activite.statut}
										</Badge>
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