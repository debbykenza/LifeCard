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
							<Breadcrumb.Page>Historique des visites</Breadcrumb.Page>
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
		</div>
	</Sidebar.Inset>
</Sidebar.Provider>
