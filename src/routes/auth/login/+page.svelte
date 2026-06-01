<script>
	import LoginForm from "$lib/components/login-form.svelte";
  import SignupForm from "$lib/components/signup-form.svelte";
  import Button  from "$lib/components/ui/button/button.svelte";

</script>

<div class="bg-muted relative flex min-h-svh flex-col items-center justify-center p-6 md:p-10">
  <!-- Bouton de retour vers la landing -->
  <Button
    variant="ghost"
    class="absolute bg-teal-950 top-4 left-4 md:top-6 md:left-6 flex items-center gap-2 text-white hover:text-white hover:bg-teal-800"
    onclick={() => window.location.href = '/landing'}
  >
    <svg 
      xmlns="http://www.w3.org/2000/svg" 
      width="20" 
      height="20" 
      viewBox="0 0 24 24" 
      fill="none" 
      stroke="currentColor" 
      stroke-width="2" 
      stroke-linecap="round" 
      stroke-linejoin="round"

      class="text-white"
    >
      <path d="M19 12H5M12 19l-7-7 7-7"/>
    </svg>
    Retour
  </Button>

  <div class="w-full max-w-md md:max-w-md border border-gray-200 rounded-lg bg-white p-6 md:p-10">
    <LoginForm />
  </div>
</div>