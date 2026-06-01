<script lang="ts">
  import { cn } from "$lib/utils.js";
  import { Button } from "$lib/components/ui/button/index.js";
  import * as Card from "$lib/components/ui/card/index.js";
  import * as Field from "$lib/components/ui/field/index.js";
  import { Input } from "$lib/components/ui/input/index.js";
  import type { HTMLAttributes } from "svelte/elements";
  let { class: className, ...restProps }: HTMLAttributes<HTMLDivElement> = $props();
</script>
<div class={cn("flex flex-col gap-6", className)} {...restProps}>
  <Card.Root>
    <Card.Header class="text-center">
      <Card.Title class="text-2xl font-bold">Créez votre compte</Card.Title>
      <Card.Description>Entrez votre adresse e-mail ci-dessous pour créer votre compte.</Card.Description>
    </Card.Header>
    <Card.Content>
      <form>
        <Field.Group>
          <Field.Field>
            <Field.Label for="name">Nom complet</Field.Label>
            <Input id="name" type="text" placeholder="John Doe" required />
          </Field.Field>
          <Field.Field>
            <Field.Label for="email">Email</Field.Label>
            <Input id="email" type="email" placeholder="m@example.com" required />
          </Field.Field>
          <Field.Field>
            <Field.Field class="grid grid-cols-2 gap-4">
              <Field.Field>
                <Field.Label for="password">Mot de passe</Field.Label>
                <Input id="password" type="password" required />
              </Field.Field>
              <Field.Field>
                <Field.Label for="confirm-password">Confirmer le mot de passe</Field.Label>
                <Input id="confirm-password" type="password" required />
              </Field.Field>
            </Field.Field>
            <Field.Description>Doit contenir au moins 8 caractères.</Field.Description>
          </Field.Field>
          <Field.Field>
            <Button type="submit" class="px-4 py-6 bg-teal-950 text-white hover:bg-teal-800 hover:text-white">Créer un compte</Button>
            <Field.Description class="text-center">
              Vous avez déjà un compte? <a href="/auth/login">Se connecter</a>
            </Field.Description>
          </Field.Field>
        </Field.Group>
      </form>
    </Card.Content>
  </Card.Root>
  <Field.Description class="px-6 text-center">
    En cliquant sur continuer, vous acceptez nos <a href="#/">Conditions d'utilisation</a>
    et notre <a href="#/">Politique de confidentialité</a>.
  </Field.Description>
</div>