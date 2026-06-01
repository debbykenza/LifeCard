<!-- 
 document d'ordonnances
 document de chiruriges
 document de radiologie
 document de laboratoire
 document de consultation
 document de vaccination
 document de soins
 document de hospitalisation
 document de prescription
 document de certificat médical
 document de compte rendu médical
 document de résultat d'examen
 document de suivi médical
 document de diagnostic
 document de traitement
 certificat de santé
 -->

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
							<Breadcrumb.Page>Documents</Breadcrumb.Page>
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

		</div>
	</Sidebar.Inset>
</Sidebar.Provider>
