<script lang="ts">
  import {
    FieldGroup,
    Field,
    FieldLabel,
    FieldDescription,
    FieldSeparator,
   
  } from "$lib/components/ui/field/index.js";
  import { Input } from "$lib/components/ui/input/index.js";
  import { Button } from "$lib/components/ui/button/index.js";
  import { cn, type WithElementRef } from "$lib/utils.js";
  import type { HTMLFormAttributes } from "svelte/elements";
  import * as Card from "$lib/components/ui/card/index.js";
  let {
    ref = $bindable(null),
    class: className,
    ...restProps
  }: WithElementRef<HTMLFormAttributes> = $props();
  const id = $props.id();
</script>
<form class={cn("flex flex-col gap-6", className)} bind:this={ref} {...restProps}>
  <FieldGroup>
    <div class="flex flex-col items-center gap-1 text-center">
      <h1 class="text-2xl font-bold">Connectez-vous</h1>
      <p class="text-muted-foreground text-sm text-balance">
       Entrez votre adresse e-mail ci-dessous pour vous connecter à votre compte.
      </p>
    </div>
    <Field>
      <FieldLabel for="email-{id}">Email</FieldLabel>
      <Input id="email-{id}" type="email" placeholder="m@example.com" required />
    </Field>
    <Field>
      <div class="flex items-center">
        <FieldLabel for="password-{id}">Mot de passe</FieldLabel>
        <a href="##" class="ms-auto text-sm underline-offset-4 hover:underline">
         Mot de passe oublié?
        </a>
      </div>
      <Input id="password-{id}" type="password" required />
    </Field>
    <Field>
      <Button type="submit" class="px-4 py-6 bg-teal-950 text-white hover:bg-teal-800 hover:text-white">
      <a href="/patient/dossier_medical/resume">Se connecter</a>
      
      </Button>
    </Field>
  
    <Field>
      <FieldDescription class="text-center">
       Vous n'avez pas de compte ?
        <a href="/auth/register" class="underline underline-offset-4">S'inscrire</a>
      </FieldDescription>
    </Field>
  </FieldGroup>
 
</form>