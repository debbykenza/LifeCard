<script lang="ts">
	import AppSidebar from '$lib/components/app-sidebar.svelte';
	import * as Breadcrumb from '$lib/components/ui/breadcrumb/index.js';
	import { Separator } from '$lib/components/ui/separator/index.js';
	import * as Sidebar from '$lib/components/ui/sidebar/index.js';
	import Card from '$lib/components/ui/card/card.svelte';
	import Badge from '$lib/components/ui/badge/badge.svelte';
	import Button from '$lib/components/ui/button/button.svelte';

	// Données du patient
	const patient = {
		nom: 'Laurent',
		prenom: 'Dupont',
		dateNaissance: '15/05/1985',
		age: 41,
		groupeSanguin: 'A-',
		taille: '1.70 m',
		poids: '75 kg',
		imc: '25.9 kg/m²',
		telephone: '+33 6 12 34 56 78',
		email: 'marie.dupont@email.fr',
		adresse: '123 Rue de la Santé, 75013 Paris',
		numeroSecu: '1 85 05 75 123 456 78',
		medecinTraitant: 'Dr. Sophie Martin - +33 1 98 76 54 32'
	};

	// Contact d'urgence
	const contactUrgence = {
		nom: 'Jean Dupont',
		relation: 'Époux',
		telephone: '+33 6 98 76 54 32'
	};

	// Allergies
	const allergies = [
		{ nom: 'Pénicilline', severite: 'Sévère', reaction: 'Choc anaphylactique' },
		{ nom: 'Arachides', severite: 'Modérée', reaction: 'Urticaire, œdème' },
		{ nom: 'Latex', severite: 'Légère', reaction: 'Irritation cutanée' },
		{ nom: 'Iode', severite: 'Modérée', reaction: 'Éruption cutanée' }
	];

	// Maladies chroniques
	const maladiesChroniques = [
		{ nom: 'Diabète Type 2', diagnostique: 'Janvier 2024', statut: 'Contrôlé' },
		{ nom: 'Hypertension artérielle', diagnostique: 'Mars 2025', statut: 'Sous traitement' },
		{ nom: 'Asthme', diagnostique: 'Août 2023', statut: 'Intermittent' }
	];

	// Traitements en cours
	const traitements = [
		{ nom: 'Metformine', dosage: '500mg', frequence: '2x/jour', horaires: '08:00, 20:00' },
		{ nom: 'Ramipril', dosage: '5mg', frequence: '1x/jour', horaires: '08:00' },
		{ nom: 'Aspirine', dosage: '100mg', frequence: '1x/jour', horaires: '20:00' },
		{ nom: 'Ventoline', dosage: '100µg', frequence: 'Si besoin', horaires: 'En cas de crise' }
	];

	// Antécédents chirurgicaux
	const antecedentsChirurgicaux = [
		{ intervention: 'Appendicectomie', date: '2010', lieu: 'Hôpital Saint-Louis, Paris' },
		{ intervention: 'Fracture poignet droit', date: '2018', lieu: 'Clinique du Sport, Paris' }
	];

	// Vaccinations importantes
	const vaccinations = [
		{ nom: 'COVID-19', derniereDose: '15 Mars 2026' },
		{ nom: 'Grippe', derniereDose: '20 Oct 2025' },
		{ nom: 'Tétanos', derniereDose: '10 Fév 2024' }
	];

	// Constantes vitales récentes
	const constantesVitales = {
		tension: '120/80 mmHg',
		frequenceCardiaque: '72 bpm',
		saturation: '98%',
		temperature: '37.1°C',
		date: '20 Mars 2026'
	};

	function getSeveriteColor(severite: string) {
		const colors: Record<string, string> = {
			Sévère: 'bg-red-100 text-red-800 border-red-200',
			Modérée: 'bg-orange-100 text-orange-800 border-orange-200',
			Légère: 'bg-yellow-100 text-yellow-800 border-yellow-200'
		};
		return colors[severite] || 'bg-slate-100 text-slate-800 border-slate-200';
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
							<Breadcrumb.Page>Fiche médicale d'urgence</Breadcrumb.Page>
						</Breadcrumb.Item>
					</Breadcrumb.List>
				</Breadcrumb.Root>
			</div>
		</header>

		<div class="flex flex-1 flex-col items-center justify-center p-6 pt-6">
			<!-- Fiche Médicale d'Urgence - Card Centrée -->
			<Card class="w-full max-w-6xl overflow-hidden shadow-2xl">
				<!-- Bandeau d'urgence -->
				<div class="bg-teal-700 px-8 py-4">
					<div class="flex items-center justify-between">
						<div class="flex items-center gap-3">
							<svg class="h-8 w-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4.5c-.77-.833-2.694-.833-3.464 0L3.34 16.5c-.77.833.192 2.5 1.732 2.5z"
								/>
							</svg>
							<h1 class="text-2xl font-bold text-white">FICHE MÉDICALE D'URGENCE</h1>
						</div>
						<!-- <Badge class="border-red-200 bg-white px-4 py-2 text-lg text-red-800">
							{patient.groupeSanguin}
						</Badge> -->
					</div>
				</div>

				<div class="p-8">
					<!-- Section Identité -->
					<div class="mb-8 rounded-lg bg-slate-50 p-6">
						<div class="mb-4 flex items-center gap-2">
							<svg
								class="h-6 w-6 text-slate-700"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
								/>
							</svg>
							<h2 class="text-xl font-bold text-slate-900">Identité du Patient</h2>
						</div>
						<div class="grid gap-4 md:grid-cols-3">
							<div>
								<div class="text-sm text-slate-500">Nom complet</div>
								<div class="text-lg font-bold text-slate-900">{patient.nom} {patient.prenom}</div>
							</div>
							<div>
								<div class="text-sm text-slate-500">Date de naissance</div>
								<div class="text-lg font-bold text-slate-900">
									{patient.dateNaissance} ({patient.age} ans)
								</div>
							</div>
							<div>
								<div class="text-sm text-slate-500">Groupe sanguin</div>
								<div class="text-lg font-bold text-slate-900">{patient.groupeSanguin}</div>
							</div>
							<div>
								<div class="text-sm text-slate-500">Taille / Poids</div>
								<div class="text-lg font-bold text-slate-900">
									{patient.taille} / {patient.poids}
								</div>
							</div>
							<div>
								<div class="text-sm text-slate-500">IMC</div>
								<div class="text-lg font-bold text-slate-900">{patient.imc}</div>
							</div>
							<div>
								<div class="text-sm text-slate-500">Adresse</div>
								<div class="text-md font-semibold text-slate-900">{patient.adresse}</div>
							</div>
						</div>
					</div>

					<!-- Contact d'Urgence + Médecin Traitant -->
					<div class="mb-8 grid gap-6 md:grid-cols-2">
						<div class="rounded-lg bg-teal-50 p-3">
							<div class="mb-2 flex items-center gap-2">
								<svg
									class="h-5 w-5 text-teal-700"
									fill="none"
									stroke="currentColor"
									viewBox="0 0 24 24"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"
									/>
								</svg>
								<h3 class="font-bold text-xl text-teal-700">Contact d'Urgence</h3>
							</div>
							<div class="text-lg">Nom complet : {contactUrgence.nom}</div>
							<div class="text-lg"> Relation : {contactUrgence.relation}</div>
							<div class="text-lg">Téléphone : {contactUrgence.telephone}</div>
						</div>

						<div class="rounded-lg  bg-teal-50 p-3">
							<div class="mb-2 flex items-center gap-2">
								<svg
									class="h-5 w-5 text-teal-700"
									fill="none"
									stroke="currentColor"
									viewBox="0 0 24 24"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
									/>
								</svg>
								<h3 class="font-bold text-xl text-teal-700">Médecin Traitant</h3>
							</div>
							<div class="text-slate-900 text-lg">{patient.medecinTraitant}</div>
						</div>
					</div>

					<!-- Section Critique : Allergies -->
					<div class="mb-8">
						<div class="mb-4 flex items-center gap-2">
							<svg
								class="h-6 w-6 text-teal-600"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4.5c-.77-.833-2.694-.833-3.464 0L3.34 16.5c-.77.833.192 2.5 1.732 2.5z"
								/>
							</svg>
							<h2 class="text-xl font-bold text-teal-900">Allergies</h2>
						</div>
						<div class="flex flex-wrap gap-3">
							{#each allergies as allergie}
								<div class="rounded-lg bg-teal-50 px-4 py-2">
									<span class="font-semibold text-teal-900">{allergie.nom}</span>
									<span class="ml-2 text-sm text-teal-700">({allergie.reaction})</span>
									<Badge class="ml-2 {getSeveriteColor(allergie.severite)} text-xs">
										{allergie.severite}
									</Badge>
								</div>
							{/each}
						</div>
					</div>

					<!-- Maladies Chroniques -->
					<div class="mb-8">
						<div class="mb-4 flex items-center gap-2">
							<svg
								class="h-6 w-6 text-orange-600"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"
								/>
							</svg>
							<h2 class="text-xl font-bold text-slate-900">Maladies Chroniques</h2>
						</div>
						<div class="grid gap-3 md:grid-cols-3">
							{#each maladiesChroniques as maladie}
								<div class="rounded-lg border border-slate-200 bg-slate-50 p-4">
									<div class="font-bold text-slate-900">{maladie.nom}</div>
									<div class="mt-1 text-sm text-slate-600">Depuis {maladie.diagnostique}</div>
									<Badge class="mt-2 border-green-200 bg-green-100 text-green-800">
										{maladie.statut}
									</Badge>
								</div>
							{/each}
						</div>
					</div>

					<!-- Traitements en cours -->
					<div class="mb-8">
						<div class="mb-4 flex items-center gap-2">
							<svg
								class="h-6 w-6 text-teal-600"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"
								/>
							</svg>
							<h2 class="text-xl font-bold text-slate-900">Traitements en Cours</h2>
						</div>
						<div class="overflow-x-auto">
							<table class="w-full text-left">
								<thead>
									<tr class="border-b-2 border-slate-200">
										<th class="pb-2 font-semibold text-slate-700">Médicament</th>
										<th class="pb-2 font-semibold text-slate-700">Dosage</th>
										<th class="pb-2 font-semibold text-slate-700">Fréquence</th>
										<th class="pb-2 font-semibold text-slate-700">Horaires</th>
									</tr>
								</thead>
								<tbody>
									{#each traitements as traitement}
										<tr class="border-b border-slate-100">
											<td class="py-3 font-semibold text-slate-900">{traitement.nom}</td>
											<td class="py-3 text-slate-700">{traitement.dosage}</td>
											<td class="py-3 text-slate-700">{traitement.frequence}</td>
											<td class="py-3 text-slate-700">{traitement.horaires}</td>
										</tr>
									{/each}
								</tbody>
							</table>
						</div>
					</div>

					<!-- Antécédents + Constantes -->
					<div class="mb-8 grid gap-6 md:grid-cols-2">
						<div>
							<div class="mb-4 flex items-center gap-2">
								<svg
									class="h-6 w-6 text-slate-600"
									fill="none"
									stroke="currentColor"
									viewBox="0 0 24 24"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"
									/>
								</svg>
								<h2 class="text-xl font-bold text-slate-900">Antécédents Chirurgicaux</h2>
							</div>
							<div class="space-y-3">
								{#each antecedentsChirurgicaux as antecedent}
									<div class="rounded-lg border border-slate-200 p-4">
										<div class="font-bold text-slate-900">{antecedent.intervention}</div>
										<div class="text-sm text-slate-600">{antecedent.date} - {antecedent.lieu}</div>
									</div>
								{/each}
							</div>
						</div>

						<div>
							<div class="mb-4 flex items-center gap-2">
								<svg
									class="h-6 w-6 text-slate-600"
									fill="none"
									stroke="currentColor"
									viewBox="0 0 24 24"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"
									/>
								</svg>
								<h2 class="text-xl font-bold text-slate-900">Constantes Vitales Récentes</h2>
								<div class="text-sm text-slate-500">({constantesVitales.date})</div>
							</div>
							<div class="grid grid-cols-2 gap-3">
								<div class="rounded-lg bg-green-50 p-4">
									<div class="text-sm text-slate-600">Tension</div>
									<div class="text-xl font-bold text-green-900">{constantesVitales.tension}</div>
								</div>
								<div class="rounded-lg bg-blue-50 p-4">
									<div class="text-sm text-slate-600">FC</div>
									<div class="text-xl font-bold text-blue-900">
										{constantesVitales.frequenceCardiaque}
									</div>
								</div>
								<div class="rounded-lg bg-purple-50 p-4">
									<div class="text-sm text-slate-600">SpO2</div>
									<div class="text-xl font-bold text-purple-900">
										{constantesVitales.saturation}
									</div>
								</div>
								<div class="rounded-lg bg-orange-50 p-4">
									<div class="text-sm text-slate-600">Température</div>
									<div class="text-xl font-bold text-orange-900">
										{constantesVitales.temperature}
									</div>
								</div>
							</div>
						</div>
					</div>

					<!-- Vaccinations -->
					<div class="mb-8">
						<div class="mb-4 flex items-center gap-2">
							<svg
								class="h-6 w-6 text-teal-600"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"
								/>
							</svg>
							<h2 class="text-xl font-bold text-slate-900">Vaccinations</h2>
						</div>
						<div class="flex flex-wrap gap-3">
							{#each vaccinations as vaccin}
								<div class="rounded-lg border border-teal-200 bg-teal-50 px-4 py-2">
									<span class="font-semibold text-teal-900">{vaccin.nom}</span>
									<span class="ml-2 text-sm text-teal-700">({vaccin.derniereDose})</span>
								</div>
							{/each}
						</div>
					</div>

					<!-- Pied de page -->
					<div class="mt-8 border-t-2 border-slate-200 pt-6 text-center">
						<div class="flex items-center justify-center gap-4">
							<svg
								class="h-6 w-6 text-slate-400"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"
								/>
							</svg>
							<p class="text-sm text-slate-500">
								Dernière mise à jour : 20 Mars 2026 | Document confidentiel - Usage médical
								uniquement
							</p>
						</div>
					</div>
				</div>
			</Card>
		</div>
	</Sidebar.Inset>
</Sidebar.Provider>
