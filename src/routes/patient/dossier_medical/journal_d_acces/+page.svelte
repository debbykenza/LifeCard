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
							<Breadcrumb.Page>Journal d'Accès</Breadcrumb.Page>
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
