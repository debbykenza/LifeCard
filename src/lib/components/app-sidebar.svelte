<script lang="ts" module>
	import AudioWaveformIcon from "@lucide/svelte/icons/audio-waveform";
	import BookOpenIcon from "@lucide/svelte/icons/book-open";
	import BotIcon from "@lucide/svelte/icons/bot";
	import ChartPieIcon from "@lucide/svelte/icons/chart-pie";
	import CommandIcon from "@lucide/svelte/icons/command";
	import FrameIcon from "@lucide/svelte/icons/frame";
	import GalleryVerticalEndIcon from "@lucide/svelte/icons/gallery-vertical-end";
	import MapIcon from "@lucide/svelte/icons/map";
	import Settings2Icon from "@lucide/svelte/icons/settings-2";
	import SquareTerminalIcon from "@lucide/svelte/icons/square-terminal";

	// This is sample data.
	const data = {
		user: {
			name: "shadcn",
			email: "m@example.com",
			avatar: "/avatars/shadcn.jpg",
		},
		teams: [
			{
				name: "Acme Inc",
				logo: GalleryVerticalEndIcon,
				plan: "Enterprise",
			},
			{
				name: "Acme Corp.",
				logo: AudioWaveformIcon,
				plan: "Startup",
			},
			{
				name: "Evil Corp.",
				logo: CommandIcon,
				plan: "Free",
			},
		],
		navMain: [
			{
				title: "Dossier médical",
				url: "/patient/dossier_medical",
				icon: SquareTerminalIcon,
				items: [
					{
						title: "Résumé",
						url: "/patient/dossier_medical/resume",
					},
					{
						title: "Allergies",
						url: "/patient/dossier_medical/allergies",
					},
					{
						title: "Maladies chroniques",
						url: "/patient/dossier_medical/maladies_chroniques",
					},
					{
						title: "Traitements",
						url: "/patient/dossier_medical/traitements",
					},
					{
						title: "Vaccinations",
						url: "/patient/dossier_medical/vaccinations",
					},
					{
						title: "Historique des visites",
						url: "/patient/dossier_medical/historique_des_visites",
					},
					{
						title: "Journal d'Accès",
						url: "/patient/dossier_medical/journal_d_acces",
					},
				],
			},
			{
				title: "Documents médicaux",
				url: "/patient/documents_medicaux",
				icon: BotIcon,
				items: [
					{
						title: "Documents",
						url: "/patient/documents_medicaux",
					},]
				
			},
			
			
			
		],
		Organisations: [
			{
				name: "Agenda",
				url: "/patient/agendas",
				icon: Settings2Icon,
				
			},

			{
				name: "Alarmes",
				url: "/patient/alarmes",
				icon: Settings2Icon,
				
			},
			
		],
		Visites: [
			{
				name: "Hospitalisation",
				url: "/patient/hospitalisations",
				icon: Settings2Icon,
				// items: [
				// 	{
				// 		title: "General",
				// 		url: "#",
				// 	},
				// 	{
				// 		title: "Team",
				// 		url: "#",
				// 	},
					
				// ],
			},

			// {
			// 	name: "Consultations",
			// 	url: "/patient/consultations",
			// 	icon: Settings2Icon,
			
			// },
			
		],
		Carte: [
			{
				name: "Configuration de la carte",
				url: "/patient/configuration_carte",
				icon: FrameIcon,
			},
			{
				name: "Fiche médicale",
				url: "/patient/fiche_medicale",
				icon: ChartPieIcon,
			},
			{
				name: "Commandes & Paiements",
				url: "/patient/commande_paiement",
				icon: MapIcon,
			},
		],

	};
</script>

<script lang="ts">
	import NavMain from "./nav-main.svelte";
	import NavProjects from "./nav-projects.svelte";
	import NavUser from "./nav-user.svelte";
	import TeamSwitcher from "./team-switcher.svelte";
	import * as Sidebar from "$lib/components/ui/sidebar/index.js";
	import type { ComponentProps } from "svelte";
	import NavVisites from "./nav-visites.svelte";
	import NavOrganisation from "./nav-organisation.svelte";

	let {
		ref = $bindable(null),
		collapsible = "icon",
		...restProps
	}: ComponentProps<typeof Sidebar.Root> = $props();
</script>

<Sidebar.Root bind:ref {collapsible} {...restProps}>
	<Sidebar.Header>
		<TeamSwitcher teams={data.teams} />
	</Sidebar.Header>
	
	<Sidebar.Content>
		<NavMain items={data.navMain} />
		<NavVisites visites={data.Visites} />
		<NavOrganisation organisation={data.Organisations} />
		<NavProjects projects={data.Carte} />
	</Sidebar.Content>
	<Sidebar.Footer>
		<NavUser user={data.user} />
	</Sidebar.Footer>
	<Sidebar.Rail />
</Sidebar.Root>
