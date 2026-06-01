<script lang="ts">
  import { Button } from "$lib/components/ui/button";
  import { Card } from "$lib/components/ui/card";
  import { Badge } from "$lib/components/ui/badge";
  
  // Features data
  const features = [
    {
      title: "Accès d'urgence",
      description: "Les secouristes accèdent instantanément à vos informations vitales en cas d'accident, sans connexion internet.",
      icon: "🚨"
    },
    {
      title: "Sécurité maximale",
      description: "Chiffrement AES-256 et contrôle d'accès à 4 niveaux pour protéger vos données médicales.",
      icon: "🔐"
    },
    {
      title: "Compatible mondial",
      description: "Utilisable dans n'importe quel pays, même dans les zones reculées sans infrastructure.",
      icon: "🌍"
    }
  ];
  
  // Access levels
  const accessLevels = [
    {
      level: "Urgence",
      icon: "🚨",
      color: "bg-red-50 border-red-200",
      title: "Accès instantané vital",
      description: "Groupe sanguin, allergies, traitements en cours"
    },
    {
      level: "Médecin",
      icon: "👨‍⚕️",
      color: "bg-blue-50 border-blue-200",
      title: "Dossier médical complet",
      description: "Historique, diagnostics, prescriptions"
    },
    {
      level: "Personnel Soignant",
      icon: "👩‍⚕️",
      color: "bg-green-50 border-green-200",
      title: "Suivi des soins",
      description: "Constantes, administrations, notes"
    },
    {
      level: "Patient",
      icon: "🙋",
      color: "bg-purple-50 border-purple-200",
      title: "Contrôle total",
      description: "Gérer médicaments, rappels, autorisations"
    }
  ];
  
  // Testimonials
  const testimonials = [
    {
      name: "Dr. Amina Touré",
      role: "Médecin urgentiste",
      image: "👩‍⚕️",
      text: "LifeCard a sauvé la vie d'un patient allergique. En 10 secondes, j'ai eu toutes les infos nécessaires pour agir sans risque.",
      rating: 5
    },
    {
      name: "Marc Dubois",
      role: "Patient diabétique",
      image: "👨",
      text: "Je voyage beaucoup pour le travail. Avec LifeCard, je suis rassuré : mon traitement est accessible partout dans le monde.",
      rating: 5
    },
    {
      name: "Infirmière Sarah K.",
      role: "Hôpital rural - Bénin",
      image: "👩",
      text: "Même sans internet, nous pouvons consulter les dossiers. C'est une révolution pour nos zones reculées.",
      rating: 5
    }
  ];
</script>

<!-- Hero Section -->
<section class="relative min-h-screen flex items-center bg-gradient-to-br from-slate-900 via-slate-800 to-slate-900 text-white overflow-hidden">
  <!-- Background decoration -->
  <div class="absolute inset-0 opacity-10">
    <div class="absolute top-20 right-20 w-72 h-72 bg-blue-500 rounded-full blur-3xl"></div>
    <div class="absolute bottom-20 left-20 w-96 h-96 bg-purple-500 rounded-full blur-3xl"></div>
  </div>
  
  <div class="container mx-auto px-6 lg:px-20 relative z-10">
    <div class="grid lg:grid-cols-2 gap-12 items-center">
      <!-- Left content -->
      <div class="space-y-8">
        <Badge class="bg-blue-500/20 text-blue-300 border-blue-500/30 px-4 py-2">
          🚀 La santé connectée pour tous
        </Badge>
        
        <h1 class="text-5xl lg:text-7xl font-bold leading-tight">
          Votre Dossier Médical,
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-purple-400">
            Toujours Avec Vous
          </span>
        </h1>
        
        <p class="text-xl text-slate-300 leading-relaxed">
          Avec LifeCard, vos informations de santé sont accessibles en quelques secondes, 
          partout dans le monde. Une carte intelligente NFC + QR Code pour une prise en charge rapide et efficace.
        </p>
        
        <div class="flex flex-wrap gap-4">
          <Button size="lg" class="bg-gradient-to-r from-blue-500 to-purple-500 hover:from-blue-600 hover:to-purple-600 text-white px-8 py-6 text-lg rounded-full">
            Commencer Maintenant
            <span class="ml-2">→</span>
          </Button>
          <Button size="lg" variant="outline" class="border-white/20 text-white hover:bg-white/10 px-8 py-6 text-lg rounded-full">
            En Savoir Plus
          </Button>
        </div>
        
        <!-- Stats -->
        <div class="flex gap-8 pt-8">
          <div>
            <div class="text-3xl font-bold text-blue-400">99.9%</div>
            <div class="text-sm text-slate-400">Disponibilité</div>
          </div>
          <div>
            <div class="text-3xl font-bold text-purple-400">4 Niveaux</div>
            <div class="text-sm text-slate-400">De sécurité</div>
          </div>
          <div>
            <div class="text-3xl font-bold text-green-400">Offline</div>
            <div class="text-sm text-slate-400">Mode hors-ligne</div>
          </div>
        </div>
      </div>
      
      <!-- Right image/illustration -->
      <div class="relative">
        <div class="relative bg-gradient-to-br from-blue-500/20 to-purple-500/20 backdrop-blur-sm rounded-3xl p-8 border border-white/10">
          <!-- Card mockup -->
          <div class="bg-white rounded-2xl shadow-2xl p-8 space-y-6">
            <div class="flex items-center justify-between">
              <div>
                <h3 class="text-2xl font-bold text-slate-800">LifeCard</h3>
                <p class="text-slate-500">Carte Nationale de Santé Universelle</p>
              </div>
              <div class="text-4xl">💳</div>
            </div>
            
            <div class="space-y-4 text-slate-700">
              <div class="flex items-center gap-3 bg-slate-50 p-4 rounded-lg">
                <span class="text-2xl">👤</span>
                <div>
                  <div class="font-semibold">Jean Dupont</div>
                  <div class="text-sm text-slate-500">Né le 15/03/1985</div>
                </div>
              </div>
              
              <div class="flex items-center gap-3 bg-slate-50 p-4 rounded-lg">
                <span class="text-2xl">🩸</span>
                <div>
                  <div class="font-semibold">Groupe sanguin: A+</div>
                  <div class="text-sm text-slate-500">Allergie: Pénicilline</div>
                </div>
              </div>
              
              <div class="bg-slate-100 h-32 rounded-lg flex items-center justify-center">
                <div class="text-6xl">📱</div>
              </div>
              <p class="text-center text-sm text-slate-500">Scannez pour accéder au dossier complet</p>
            </div>
          </div>
          
          <!-- Floating elements -->
          <div class="absolute -top-6 -right-6 bg-green-500 text-white px-4 py-2 rounded-full text-sm font-semibold shadow-lg animate-bounce">
            ✓ Sécurisé
          </div>
          <div class="absolute -bottom-6 -left-6 bg-blue-500 text-white px-4 py-2 rounded-full text-sm font-semibold shadow-lg animate-pulse">
            🌍 Mondial
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Why Choosing Us -->
<section class="py-20 bg-white">
  <div class="container mx-auto px-6 lg:px-20">
    <div class="text-center mb-16">
      <Badge class="mb-4 bg-blue-50 text-blue-600 border-blue-200">Pourquoi LifeCard</Badge>
      <h2 class="text-4xl lg:text-5xl font-bold text-slate-900 mb-4">
        Une Technologie au Service de Votre Santé
      </h2>
      <p class="text-xl text-slate-600 max-w-2xl mx-auto">
        Conçu pour fonctionner partout, même dans les conditions les plus difficiles
      </p>
    </div>
    
    <div class="grid md:grid-cols-3 gap-8">
      {#each features as feature}
        <Card class="p-8 hover:shadow-xl transition-shadow border-slate-200">
          <div class="text-5xl mb-4">{feature.icon}</div>
          <h3 class="text-2xl font-bold text-slate-900 mb-3">{feature.title}</h3>
          <p class="text-slate-600 leading-relaxed">{feature.description}</p>
        </Card>
      {/each}
    </div>
  </div>
</section>

<!-- Access Levels (Best Selling Product equivalent) -->
<section class="py-20 bg-slate-50">
  <div class="container mx-auto px-6 lg:px-20">
    <div class="text-center mb-16">
      <Badge class="mb-4 bg-purple-50 text-purple-600 border-purple-200">Sécurité</Badge>
      <h2 class="text-4xl lg:text-5xl font-bold text-slate-900 mb-4">
        4 Niveaux d'Accès Pour Votre Protection
      </h2>
      <p class="text-xl text-slate-600 max-w-2xl mx-auto">
        Chaque professionnel accède uniquement aux informations nécessaires
      </p>
    </div>
    
    <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
      {#each accessLevels as access}
        <Card class="p-6 hover:shadow-xl transition-all hover:-translate-y-2 border-2 {access.color}">
          <div class="text-center space-y-4">
            <div class="text-5xl">{access.icon}</div>
            <Badge class="bg-white border">{access.level}</Badge>
            <h3 class="text-xl font-bold text-slate-900">{access.title}</h3>
            <p class="text-slate-600 text-sm">{access.description}</p>
          </div>
        </Card>
      {/each}
    </div>
  </div>
</section>

<!-- Experience Section -->
<section class="py-20 bg-white">
  <div class="container mx-auto px-6 lg:px-20">
    <div class="grid lg:grid-cols-2 gap-12 items-center">
      <!-- Image -->
      <div class="relative">
        <div class="bg-gradient-to-br from-slate-100 to-slate-200 rounded-3xl p-12 aspect-video flex items-center justify-center">
          <div class="text-9xl">🏥</div>
        </div>
        <div class="absolute -bottom-6 -right-6 bg-blue-500 text-white p-6 rounded-2xl shadow-xl">
          <div class="text-3xl font-bold">24/7</div>
          <div class="text-sm">Disponible partout</div>
        </div>
      </div>
      
      <!-- Content -->
      <div class="space-y-6">
        <Badge class="bg-orange-50 text-orange-600 border-orange-200">EXPÉRIENCE</Badge>
        <h2 class="text-4xl lg:text-5xl font-bold text-slate-900">
          Nous Vous Offrons La Meilleure Expérience
        </h2>
        <p class="text-lg text-slate-600 leading-relaxed">
          LifeCard a été conçu en collaboration avec des médecins, des urgentistes et des patients 
          du monde entier. Notre mission : rendre les soins de santé accessibles à tous, partout, 
          avec élégance et simplicité.
        </p>
        <ul class="space-y-3">
          <li class="flex items-center gap-3 text-slate-700">
            <span class="bg-green-100 text-green-600 rounded-full p-1">✓</span>
            Interface intuitive, aucune formation nécessaire
          </li>
          <li class="flex items-center gap-3 text-slate-700">
            <span class="bg-green-100 text-green-600 rounded-full p-1">✓</span>
            Fonctionne hors ligne dans les zones reculées
          </li>
          <li class="flex items-center gap-3 text-slate-700">
            <span class="bg-green-100 text-green-600 rounded-full p-1">✓</span>
            Compatible avec tous les systèmes de santé
          </li>
        </ul>
        <Button class="bg-orange-500 hover:bg-orange-600 text-white px-8 py-6 rounded-full">
          Découvrir Plus →
        </Button>
      </div>
    </div>
  </div>
</section>

<!-- Materials Section (adapted for technology) -->
<section class="py-20 bg-slate-50">
  <div class="container mx-auto px-6 lg:px-20">
    <div class="grid lg:grid-cols-2 gap-12 items-center">
      <div class="space-y-6">
        <Badge class="bg-blue-50 text-blue-600 border-blue-200">TECHNOLOGIE</Badge>
        <h2 class="text-4xl lg:text-5xl font-bold text-slate-900">
          Des Standards de Sécurité Militaire
        </h2>
        <p class="text-lg text-slate-600 leading-relaxed">
          Nous utilisons les technologies les plus avancées pour protéger vos données de santé. 
          Chiffrement de bout en bout, authentification biométrique et blockchain décentralisée 
          garantissent l'intégrité de vos informations.
        </p>
        <div class="space-y-3">
          <div class="flex items-center gap-3">
            <div class="bg-blue-500 text-white rounded-lg p-3 text-xl">🔐</div>
            <div>
              <div class="font-semibold text-slate-900">Chiffrement AES-256</div>
              <div class="text-sm text-slate-600">Standard militaire et bancaire</div>
            </div>
          </div>
          <div class="flex items-center gap-3">
            <div class="bg-purple-500 text-white rounded-lg p-3 text-xl">🔗</div>
            <div>
              <div class="font-semibold text-slate-900">Blockchain décentralisée</div>
              <div class="text-sm text-slate-600">Traçabilité et inviolabilité</div>
            </div>
          </div>
          <div class="flex items-center gap-3">
            <div class="bg-green-500 text-white rounded-lg p-3 text-xl">📱</div>
            <div>
              <div class="font-semibold text-slate-900">Progressive Web App</div>
              <div class="text-sm text-slate-600">Fonctionne même hors ligne</div>
            </div>
          </div>
        </div>
        <Button variant="outline" class="border-slate-300 rounded-full px-8 py-6">
          En Savoir Plus →
        </Button>
      </div>
      
      <!-- Images grid -->
      <div class="grid grid-cols-2 gap-4">
        <div class="space-y-4">
          <div class="bg-gradient-to-br from-blue-100 to-blue-200 rounded-2xl aspect-square flex items-center justify-center text-6xl">
            📲
          </div>
          <div class="bg-gradient-to-br from-purple-100 to-purple-200 rounded-2xl aspect-video flex items-center justify-center text-6xl">
            💳
          </div>
        </div>
        <div class="space-y-4 pt-8">
          <div class="bg-gradient-to-br from-green-100 to-green-200 rounded-2xl aspect-video flex items-center justify-center text-6xl">
            🏥
          </div>
          <div class="bg-gradient-to-br from-orange-100 to-orange-200 rounded-2xl aspect-square flex items-center justify-center text-6xl">
            🌍
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Testimonials -->
<section class="py-20 bg-white">
  <div class="container mx-auto px-6 lg:px-20">
    <div class="text-center mb-16">
      <Badge class="mb-4 bg-yellow-50 text-yellow-600 border-yellow-200">TÉMOIGNAGES</Badge>
      <h2 class="text-4xl lg:text-5xl font-bold text-slate-900 mb-4">
        Ce Que Disent Nos Utilisateurs
      </h2>
      <p class="text-xl text-slate-600 max-w-2xl mx-auto">
        Des milliers de professionnels et patients nous font confiance
      </p>
    </div>
    
    <div class="grid md:grid-cols-3 gap-8">
      {#each testimonials as testimonial}
        <Card class="p-8 hover:shadow-xl transition-all hover:-translate-y-2 border-slate-200">
          <div class="space-y-4">
            <div class="flex gap-1">
              {#each Array(testimonial.rating) as _}
                <span class="text-yellow-400 text-xl">⭐</span>
              {/each}
            </div>
            <p class="text-slate-700 leading-relaxed italic">"{testimonial.text}"</p>
            <div class="flex items-center gap-4 pt-4 border-t">
              <div class="text-4xl">{testimonial.image}</div>
              <div>
                <div class="font-semibold text-slate-900">{testimonial.name}</div>
                <div class="text-sm text-slate-500">{testimonial.role}</div>
              </div>
            </div>
          </div>
        </Card>
      {/each}
    </div>
  </div>
</section>

<!-- CTA Section -->
<section class="py-20 bg-gradient-to-br from-blue-600 via-purple-600 to-blue-700 text-white">
  <div class="container mx-auto px-6 lg:px-20 text-center">
    <h2 class="text-4xl lg:text-6xl font-bold mb-6">
      Prêt à Révolutionner Votre Accès aux Soins ?
    </h2>
    <p class="text-xl mb-10 text-blue-100 max-w-2xl mx-auto">
      Rejoignez des milliers d'utilisateurs qui ont déjà fait le choix de la sécurité et de la simplicité
    </p>
    <div class="flex flex-wrap gap-4 justify-center">
      <Button size="lg" class="bg-white text-blue-600 hover:bg-slate-100 px-10 py-6 text-lg rounded-full">
        Commander Ma LifeCard
      </Button>
      <Button size="lg" variant="outline" class="border-white text-white hover:bg-white/10 px-10 py-6 text-lg rounded-full">
        Parler à Un Expert
      </Button>
    </div>
  </div>
</section>

<!-- Footer -->
<footer class="bg-slate-900 text-white py-16">
  <div class="container mx-auto px-6 lg:px-20">
    <div class="grid md:grid-cols-4 gap-8 mb-12">
      <div>
        <h3 class="text-2xl font-bold mb-4">LifeCard</h3>
        <p class="text-slate-400">
          La carte de santé universelle pour un accès aux soins partout dans le monde.
        </p>
      </div>
      
      <div>
        <h4 class="font-semibold mb-4">Solutions</h4>
        <ul class="space-y-2 text-slate-400">
          <li><a href="#" class="hover:text-white transition">Pour Patients</a></li>
          <li><a href="#" class="hover:text-white transition">Pour Médecins</a></li>
          <li><a href="#" class="hover:text-white transition">Pour Hôpitaux</a></li>
          <li><a href="#" class="hover:text-white transition">Pour Gouvernements</a></li>
        </ul>
      </div>
      
      <div>
        <h4 class="font-semibold mb-4">Entreprise</h4>
        <ul class="space-y-2 text-slate-400">
          <li><a href="#" class="hover:text-white transition">À Propos</a></li>
          <li><a href="#" class="hover:text-white transition">Blog</a></li>
          <li><a href="#" class="hover:text-white transition">Carrières</a></li>
          <li><a href="#" class="hover:text-white transition">Contact</a></li>
        </ul>
      </div>
      
      <div>
        <h4 class="font-semibold mb-4">Suivez-nous</h4>
        <div class="flex gap-4">
          <a href="#" class="bg-slate-800 hover:bg-slate-700 w-10 h-10 rounded-full flex items-center justify-center transition">
            F
          </a>
          <a href="#" class="bg-slate-800 hover:bg-slate-700 w-10 h-10 rounded-full flex items-center justify-center transition">
            T
          </a>
          <a href="#" class="bg-slate-800 hover:bg-slate-700 w-10 h-10 rounded-full flex items-center justify-center transition">
            I
          </a>
        </div>
      </div>
    </div>
    
    <div class="border-t border-slate-800 pt-8 flex flex-col md:flex-row justify-between items-center text-slate-400 text-sm">
      <p>© 2026 LifeCard CNSU. Tous droits réservés.</p>
      <div class="flex gap-6 mt-4 md:mt-0">
        <a href="#" class="hover:text-white transition">Conditions d'utilisation</a>
        <a href="#" class="hover:text-white transition">Politique de confidentialité</a>
      </div>
    </div>
  </div>
</footer>