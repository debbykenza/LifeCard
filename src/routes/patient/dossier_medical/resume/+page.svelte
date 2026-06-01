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

	// Contact d'urgence
	const contactUrgence = {
		nom: 'Jean Dupont',
		relation: 'Époux',
		telephone: '+33 6 98 76 54 32',
		assurance: 'Sécurité Sociale + Mutuelle XYZ'
	};

	// Maladies chroniques
	const maladiesChroniques = [
		{
			nom: 'Diabète Type 2',
			diagnostique: 'Janvier 2024',
			statut: 'Contrôlé'
		},
		{
			nom: 'Hypertension artérielle',
			diagnostique: 'Mars 2025',
			statut: 'Sous traitement'
		},
		{
			nom: 'Asthme',
			diagnostique: 'Août 2023',
			statut: 'Intermittent'
		}
	];

	// Infomations médicales
	const InfoMedicaux = [
		{
			nom: 'Allergies',
			derniereDose: '15 Mars 2026',
			prochainRappel: 'Mars 2027'
		},
		{
			nom: 'Traitements en cours',
			derniereDose: '20 Oct 2025',
			prochainRappel: 'Oct 2026'
		},
		{
			nom: "Infos d'urgence",
			derniereDose: '10 Fév 2024',
			prochainRappel: 'Fév 2034'
		}
	];
	// Vaccinations
	const vaccinations = [
		{
			nom: 'COVID-19',
			derniereDose: '15 Mars 2026',
			prochainRappel: 'Mars 2027'
		},
		{
			nom: 'Grippe saisonnière',
			derniereDose: '20 Oct 2025',
			prochainRappel: 'Oct 2026'
		},
		{
			nom: 'Tétanos',
			derniereDose: '10 Fév 2024',
			prochainRappel: 'Fév 2034'
		}
	];

	// Historique des visites
	const visites = [
		{
			medecin: 'Dr. Laurent Bernard',
			specialite: 'Cardiologie',
			date: '20 Mars 2026',
			motif: 'Contrôle cardiaque régulier',
			notes: 'Tension artérielle normale (120/80). ECG normal. Continuer le traitement actuel.',
			prescriptions: ['Metformine 500mg']
		},
		{
			medecin: 'Dr. Sophie Martin',
			specialite: 'Médecine Générale',
			date: '15 Février 2026',
			motif: 'Consultation générale',
			notes: '',
			prescriptions: []
		}
	];

	// Documents médicaux
	const documents = [
		{
			nom: 'Ordonnance - Mars 2026',
			type: 'Ordonnance',
			date: '20/03/2026',
			medecin: 'Dr. Bernard'
		},
		{
			nom: 'Résultats analyses sanguines',
			type: 'Résultats',
			date: '15/03/2026',
			medecin: 'Dr. Martin'
		},
		{
			nom: 'IRM Cardiaque',
			type: 'Imagerie',
			date: '10/02/2026',
			medecin: 'Dr. Bernard'
		},
		{
			nom: 'Compte-rendu consultation',
			type: 'Rapport',
			date: '15/02/2026',
			medecin: 'Dr. Martin'
		}
	];

	// Journal d'accès RGPD
	const journalAcces = [
		{
			date: '30 Mars 2026 10:45',
			utilisateur: 'Dr. Laurent Bernard',
			action: 'Consultation dossier',
			ip: '192.168.1.45'
		},
		{
			date: '20 Mars 2026 14:30',
			utilisateur: 'Dr. Laurent Bernard',
			action: 'Ajout visite',
			ip: '192.168.1.45'
		},
		{
			date: '15 Février 2026 10:15',
			utilisateur: 'Dr. Sophie Martin',
			action: 'Modification ordonnance',
			ip: '192.168.1.89'
		}
	];
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
							<Breadcrumb.Page>Dossier médical</Breadcrumb.Page>
						</Breadcrumb.Item>
						<Breadcrumb.Separator class="hidden md:block" />
						<Breadcrumb.Item>
							<Breadcrumb.Page>Résumé</Breadcrumb.Page>
						</Breadcrumb.Item>
					</Breadcrumb.List>
				</Breadcrumb.Root>
			</div>
		</header>

		<div class="flex flex-1 flex-col gap-6 p-6 pt-6">
			<!-- Header avec salutation -->
			<div>
				<h1 class="flex items-center gap-2 text-3xl font-bold text-slate-900">
					Bonjour, {patient.prenom} 👋
				</h1>
			</div>

			<!-- Section informations principales -->
			<div class="grid gap-4 md:grid-cols-4">

                <!-- Informations médicales -->
				<Card class="p-6 border-teal-800 col-span-3">
					<div class="mb-4 flex items-center gap-2 text-teal-700">
						<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
							/>
						</svg>
						<h3 class="font-semibold text-slate-900 text-lg">Informations médicales</h3>
					</div>
					<div class="space-y-3 text-sm grid grid-cols-4 gap-4">
                        <!-- nom complet -->
                        <div class="flex items-start gap-2 text-slate-600">
							<svg
								class="mt-0.5 h-4 w-4 flex-shrink-0"
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
							<div>
								<div class="text-md text-slate-500">Nom Complet</div>
								<div class="font-medium text-slate-900 text-lg">{patient.nom} {patient.prenom}</div>
							</div>
						</div>

                        <!-- date de naissance -->
						<div class="flex items-start gap-2 text-slate-600">
							<svg
								class="mt-0.5 h-4 w-4 flex-shrink-0"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
								/>
							</svg>
							<div>
								<div class="text-md text-slate-500">Date de naissance</div>
								<div class="font-medium text-lg text-slate-900">{patient.dateNaissance}</div>
							</div>
						</div>

                        <!-- groupe sanguin -->
                         <div class="flex items-start gap-2 text-slate-600">
							<svg
								class="mt-0.5 h-4 w-4 flex-shrink-0"
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
							<div>
								<div class="text-md text-slate-500">Groupe sanguin</div>
								<div class="font-medium text-lg text-slate-900">{patient.groupeSanguin}</div>
							</div>
						</div>
                        <!-- Taille -->
                         <div class="flex items-start gap-2 text-slate-600">
							<svg
								class="mt-0.5 h-4 w-4 flex-shrink-0"
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
							<div>
								<div class="text-md text-slate-500">Taille</div>
								<div class="font-medium text-lg text-slate-900">{patient.taille}</div>
							</div>
						</div>
                        <!-- Poids -->
                         <div class="flex items-start gap-2 text-slate-600">
							<svg
								class="mt-0.5 h-4 w-4 flex-shrink-0"
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
							<div>
								<div class="text-md text-slate-500">Poids</div>
								<div class="font-medium text-lg text-slate-900">{patient.poids}</div>
							</div>
						</div>

                        <!-- téléphone -->
                        <div class="flex items-start gap-2 text-slate-600">
							<svg
								class="mt-0.5 h-4 w-4 flex-shrink-0"
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
							<div>
								<div class="text-md text-slate-500">Téléphone</div>
								<div class="font-medium text-lg text-slate-900">{patient.telephone}</div>
							</div>
						</div>

                        <!-- email -->
						<div class="flex items-start gap-2 text-slate-600">
							<svg
								class="mt-0.5 h-4 w-4 flex-shrink-0"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
								/>
							</svg>
							<div>
								<div class="text-md text-slate-500">Email</div>
								<div class="font-medium text-lg text-slate-900">{patient.email}</div>
							</div>
						</div>

                        <!-- adresse -->
						<div class="flex items-start gap-2 text-slate-600">
							<svg
								class="mt-0.5 h-4 w-4 flex-shrink-0"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
								/><path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
								/>
							</svg>
							<div>
								<div class="text-md text-slate-500">Adresse</div>
								<div class="font-medium text-lg text-slate-900">{patient.adresse}</div>
							</div>
						</div>
					</div>
				</Card>

				

				<!-- Contact d'Urgence -->
				<Card class="p-6 col-span-1 bg-red-50">
					<div class="mb-4 flex items-center  gap-2 text-teal-700 text-lg">
						<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"
							/>
						</svg>
						<h3 class="font-semibold text-lg text-slate-900">Contact d'Urgence</h3>
					</div>
					<div class="space-y-3">
						<div>
							<div class="font-semibold text-md text-slate-900">{contactUrgence.nom}</div>
							<div class="text-md text-slate-500">{contactUrgence.relation}</div>
						</div>
						<div>
                            <div class="font-semibold text-md text-slate-900">Téléphone</div>
							<div class="font-medium text-md text-orange-600">{contactUrgence.telephone}</div>
						</div>
						<!-- <div class="mt-4 border-t pt-4">
							<div class="mb-1 text-xs text-slate-500">Assurance</div>
							<div class="text-sm font-medium text-slate-900">{contactUrgence.assurance}</div>
						</div> -->
					</div>
				</Card>

                <!-- Informations de Contact -->
				<!-- <Card class="p-6">
					<div class="mb-4 flex items-center gap-2 text-teal-700">
						<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
							/>
						</svg>
						<h3 class="font-semibold text-slate-900">Informations de Contact</h3>
					</div>
					<div class="space-y-3 text-sm">
						<div class="flex items-start gap-2 text-slate-600">
							<svg
								class="mt-0.5 h-4 w-4 flex-shrink-0"
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
							<div>
								<div class="text-xs text-slate-500">Téléphone</div>
								<div class="font-medium text-slate-900">{patient.telephone}</div>
							</div>
						</div>
						<div class="flex items-start gap-2 text-slate-600">
							<svg
								class="mt-0.5 h-4 w-4 flex-shrink-0"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
								/>
							</svg>
							<div>
								<div class="text-xs text-slate-500">Email</div>
								<div class="font-medium text-slate-900">{patient.email}</div>
							</div>
						</div>
						<div class="flex items-start gap-2 text-slate-600">
							<svg
								class="mt-0.5 h-4 w-4 flex-shrink-0"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
								/><path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
								/>
							</svg>
							<div>
								<div class="text-xs text-slate-500">Adresse</div>
								<div class="font-medium text-slate-900">{patient.adresse}</div>
							</div>
						</div>
					</div>
				</Card> -->

				
			</div>

			<!-- Informations médicales -->
			<!-- <Card class="p-6">
        <div class="mb-6 flex items-center gap-2 text-teal-700">
          <svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"/>
          </svg>
          <h3 class="text-lg font-semibold text-slate-900">Informations médicales</h3>
        </div>
        <div class="grid gap-4 md:grid-cols-3">
        
          {#each InfoMedicaux as InfoMedical}
          
            <div class="rounded-lg border border-slate-200 bg-slate-50 p-4">
              <div class="font-semibold text-slate-900">{InfoMedical.nom}</div>
              <div class="mt-2 space-y-1 text-sm text-slate-600">
                <div>Dernière dose: {InfoMedical.derniereDose}</div>
                <div>Prochain rappel: {InfoMedical.prochainRappel}</div>
              </div>
            </div>
          {/each}
        </div>
      </Card> -->

			<!-- Allergies -->
			<Card class="p-6">
				<div class="mb-6 flex items-center justify-between gap-2 text-teal-700">
					<div class="flex items-center gap-2 text-teal-700">
						<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"
							/>
						</svg>
						<h3 class="text-lg font-semibold text-slate-900">Allergies</h3>
					</div>
					<Button
						variant="outline"
						class="border-slate-300 bg-teal-800 text-white hover:bg-teal-700 hover:text-white"
					>
						<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M12 4v16m8-8H4"
							/>
						</svg>
						Ajouter une allergie
					</Button>
				</div>
				<div class="grid gap-4 md:grid-cols-3">
					{#each maladiesChroniques as maladie}
						<div class="rounded-lg border border-slate-200 bg-slate-50 p-4">
							<div class="font-semibold text-slate-900">{maladie.nom}</div>
							<div class="mt-1 text-sm text-slate-600">
								Diagnostiqué: {maladie.diagnostique}
							</div>
							<Badge class="mt-2 border-green-200 bg-green-100 text-green-800">
								{maladie.statut}
							</Badge>
						</div>
					{/each}
				</div>
			</Card>

			<!-- Maladie chronique 2 -->
			<Card class="p-6">
				<div class="mb-6 flex items-center justify-between gap-2 text-teal-700">
					<div class="flex items-center gap-2 text-teal-700">
						<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"
							/>
						</svg>
						<h3 class="text-lg font-semibold text-slate-900">Maladies chroniques</h3>
					</div>
					<Button
						variant="outline"
						class="border-slate-300 bg-teal-800 text-white hover:bg-teal-700 hover:text-white"
					>
						<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M12 4v16m8-8H4"
							/>
						</svg>
						Ajouter une maladie chronique
					</Button>
				</div>
				<div class="grid gap-4 md:grid-cols-3">
					{#each maladiesChroniques as maladie}
						<div class="rounded-lg border border-slate-200 bg-slate-50 p-4">
							<div class="font-semibold text-slate-900">{maladie.nom}</div>
							<div class="mt-1 text-sm text-slate-600">
								Diagnostiqué: {maladie.diagnostique}
							</div>
							<Badge class="mt-2 border-green-200 bg-green-100 text-green-800">
								{maladie.statut}
							</Badge>
						</div>
					{/each}
				</div>
			</Card>

			<!-- Traitements -->
			<Card class="p-6">
				<div class="mb-6 flex items-center justify-between gap-2 text-teal-700">
					<div class="flex items-center gap-2 text-teal-700">
						<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"
							/>
						</svg>
						<h3 class="text-lg font-semibold text-slate-900">Traitements</h3>
					</div>
					<Button
						variant="outline"
						class="border-slate-300 bg-teal-800 text-white hover:bg-teal-700 hover:text-white"
					>
						<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M12 4v16m8-8H4"
							/>
						</svg>
						Ajouter un traitement
					</Button>
				</div>
				<div class="grid gap-4 md:grid-cols-3">
					{#each maladiesChroniques as maladie}
						<div class="rounded-lg border border-slate-200 bg-slate-50 p-4">
							<div class="font-semibold text-slate-900">{maladie.nom}</div>
							<div class="mt-1 text-sm text-slate-600">
								Diagnostiqué: {maladie.diagnostique}
							</div>
							<Badge class="mt-2 border-green-200 bg-green-100 text-green-800">
								{maladie.statut}
							</Badge>
						</div>
					{/each}
				</div>
			</Card>

			<!-- Vaccinations -->
			<Card class="p-6">
				<div class="mb-6 flex items-center justify-between gap-2 text-teal-700">
					<div class="flex items-center gap-2 text-teal-700">
						<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"
							/>
						</svg>
						<h3 class="text-lg font-semibold text-slate-900">Vaccinations</h3>
					</div>
					<Button
						variant="outline"
						class="border-slate-300 bg-teal-800 text-white hover:bg-teal-700 hover:text-white"
					>
						<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M12 4v16m8-8H4"
							/>
						</svg>
						Ajouter une vaccination
					</Button>
				</div>
				<div class="grid gap-4 md:grid-cols-3">
					{#each vaccinations as vaccin}
						<div class="rounded-lg border border-slate-200 bg-slate-50 p-4">
							<div class="font-semibold text-slate-900">{vaccin.nom}</div>
							<div class="mt-2 space-y-1 text-sm text-slate-600">
								<div>Dernière dose: {vaccin.derniereDose}</div>
								<div>Prochain rappel: {vaccin.prochainRappel}</div>
							</div>
						</div>
					{/each}
				</div>
			</Card>

			<!-- Historique des Visites -->
			<Card class="p-6">
				<div class="mb-6 flex items-center justify-between">
					<div class="flex items-center gap-2 text-teal-700">
						<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"
							/>
						</svg>
						<h3 class="text-lg font-semibold text-slate-900">Historique des Visites</h3>
					</div>
					<Button class="bg-teal-800 hover:bg-teal-700">
						<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M12 4v16m8-8H4"
							/>
						</svg>
						Ajouter une visite
					</Button>
				</div>

				<div class="space-y-6">
					{#each visites as visite}
						<div class="rounded-lg border border-slate-200 p-6">
							<div class="flex items-start justify-between">
								<div>
									<div class="text-lg font-semibold text-slate-900">{visite.medecin}</div>
									<div class="text-sm text-slate-500">{visite.specialite}</div>
								</div>
								<div class="text-sm text-slate-500">{visite.date}</div>
							</div>

							<div class="mt-4 space-y-3">
								<div>
									<div class="text-sm font-semibold text-slate-700">Motif de consultation:</div>
									<div class="text-sm text-slate-600">{visite.motif}</div>
								</div>

								{#if visite.notes}
									<div>
										<div class="text-sm font-semibold text-slate-700">Notes médicales:</div>
										<div class="text-sm text-slate-600">{visite.notes}</div>
									</div>
								{/if}

								{#if visite.prescriptions.length > 0}
									<div>
										<div class="mb-2 text-sm font-semibold text-slate-700">Prescriptions:</div>
										<div class="flex flex-wrap gap-2">
											{#each visite.prescriptions as prescription}
												<Badge class="border-blue-200 bg-blue-100 text-blue-800">
													{prescription}
												</Badge>
											{/each}
										</div>
									</div>
								{/if}
							</div>
						</div>
					{/each}
				</div>
			</Card>

			<!-- Documents Médicaux -->
			<Card class="p-6">
				<div class="mb-6 flex items-center justify-between">
					<div class="flex items-center gap-2 text-teal-700">
						<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"
							/>
						</svg>
						<h3 class="text-lg font-semibold text-slate-900">Documents Médicaux</h3>
					</div>
					<Button
						variant="outline"
						class="border-slate-300 bg-teal-800 text-white hover:bg-teal-700 hover:text-white"
					>
						<svg class="mr-2 h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M12 4v16m8-8H4"
							/>
						</svg>
						Ajouter un document
					</Button>
				</div>

				<div class="grid gap-4 md:grid-cols-4">
					{#each documents as doc}
						<div
							class="group relative rounded-lg border border-slate-200 p-4 transition hover:border-teal-300 hover:shadow-md"
						>
							<button class="absolute top-2 right-2 opacity-0 transition group-hover:opacity-100">
								<svg
									class="h-4 w-4 text-slate-400 hover:text-teal-600"
									fill="none"
									stroke="currentColor"
									viewBox="0 0 24 24"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"
									/>
								</svg>
							</button>
							<div class="mb-3 flex h-12">
								<svg
									class="h-10 w-10 text-teal-600"
									fill="none"
									stroke="currentColor"
									viewBox="0 0 24 24"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"
									/>
								</svg>
							</div>
							<div class="truncate text-sm font-semibold text-slate-900">{doc.nom}</div>
							<div class="mt-1 text-xs text-slate-500">{doc.type}</div>
							<div class="mt-1 text-xs text-slate-400">{doc.date}</div>
							<div class="text-xs text-slate-500">{doc.medecin}</div>
						</div>
					{/each}
				</div>
			</Card>

			<!-- Journal d'Accès (Traçabilité RGPD) -->
			<Card class="p-6">
				<div class="mb-6 flex items-center gap-2 text-teal-700">
					<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"
						/>
					</svg>
					<h3 class="text-lg font-semibold text-slate-900">Journal d'Accès (Traçabilité RGPD)</h3>
				</div>

				<div class="overflow-x-auto">
					<Table.Root>
						<Table.Header>
							<Table.Row>
								<Table.Head>Date & Heure</Table.Head>
								<Table.Head>Utilisateur</Table.Head>
								<Table.Head>Action</Table.Head>
								<Table.Head>Adresse IP</Table.Head>
							</Table.Row>
						</Table.Header>
						<Table.Body>
							{#each journalAcces as log}
								<Table.Row>
									<Table.Cell class="font-medium">{log.date}</Table.Cell>
									<Table.Cell>{log.utilisateur}</Table.Cell>
									<Table.Cell class="text-slate-600">{log.action}</Table.Cell>
									<Table.Cell class="font-mono text-sm text-slate-500">{log.ip}</Table.Cell>
								</Table.Row>
							{/each}
						</Table.Body>
					</Table.Root>
				</div>
			</Card>
		</div>
	</Sidebar.Inset>
</Sidebar.Provider>
