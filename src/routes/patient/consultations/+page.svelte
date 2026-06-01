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
							<Breadcrumb.Page>Consultations</Breadcrumb.Page>
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
		</div>
	</Sidebar.Inset>
</Sidebar.Provider>
