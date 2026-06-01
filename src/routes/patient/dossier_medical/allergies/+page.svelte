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


	// Allergies
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
		},
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
							<Breadcrumb.Page>Allergies</Breadcrumb.Page>
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

		</div>
	</Sidebar.Inset>
</Sidebar.Provider>
