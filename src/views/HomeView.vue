<template>
  <v-main class="bg-transparent">
    <!-- HERO -->
    <section
        id="hero"
        class="relative min-h-[90vh] flex flex-col items-center text-center overflow-hidden"
    >
      <!-- ANIMAÇÃO DE FUNDO -->
      <div class="absolute inset-0 top-0">
        <canvas ref="canvas" class="w-full h-full"></canvas>
      </div>

      <div class="bg-transparent w-100 mt-4">
        <v-container class="flex items-center justify-between py-3">
          <div class="flex items-center gap-3 cursor-pointer" @click="scrollToSection('hero')">
            <div
                class="w-10 h-10 rounded-lg bg-gradient-to-br from-rose-600 to-amber-600 flex items-center justify-center text-white font-extrabold text-lg">
              MP
            </div>
            <h1 class="text-2xl md:text-3xl font-extrabold tracking-tight text-neutral-900">Maria Padilha</h1>
          </div>

          <nav class="hidden md:flex gap-1 text-[16px] font-medium">
            <v-btn variant="flat" rounded="xl" color="#FB1C54" class="hover:text-rose-600 transition text-none text-white" @click="scrollToSection('sobre')">Sobre</v-btn>
            <v-btn variant="flat" rounded="xl" color="#FB1C54" class="hover:text-rose-600 transition text-none text-white" @click="scrollToSection('planos')">Planos</v-btn>
            <v-btn variant="flat" rounded="xl" color="#FB1C54" class="hover:text-rose-600 transition text-none text-white" @click="scrollToSection('contato')">Contato</v-btn>
          </nav>
        </v-container>
      </div>

      <v-container class="relative z-10 px-6 py-5 mt-10">
        <h2
            class="text-4xl md:text-6xl font-black tracking-tight leading-tight mb-6 bg-clip-text text-transparent bg-gradient-to-r from-rose-700 via-rose-500 to-orange-500 drop-shadow-[0_2px_10px_rgba(244,63,94,0.3)]"
        >
          Desenvolvimento Web <br/> Responsivo
        </h2>

        <p
            class="text-lg md:text-xl text-neutral-600 max-w-2xl mx-auto mb-10"
        >
          Crie seu site moderno e eficiente. <br/>
          Soluções personalizadas para destacar sua presença online.
        </p>

        <div class="flex flex-col sm:flex-row justify-center gap-2">
          <v-btn
              class="text-none" rounded variant="flat"
              @click="scrollToSection('planos')"
          >
            Solicitar Orçamento
          </v-btn>
          <v-btn
              variant="outlined"
              class="text-none" rounded
              @click="scrollToSection('sobre')"
          >
            Saiba Mais
          </v-btn>
        </div>

        <div class="mt-10 text-sm text-neutral-500">
          🚀 +15 projetos entregues • Performance garantida • Design exclusivo
        </div>
      </v-container>
    </section>

    <!-- SOBRE -->
    <section id="sobre" class="py-24 bg-neutral-50 border-t border-neutral-200 z-10 py-5">
      <v-container class="px-6">
        <h3
            class="text-4xl md:text-5xl font-extrabold text-center mb-12 text-neutral-900"
        >
          Inovação com Estilo
        </h3>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
          <div data-aos="zoom-in-right" data-aos-duration="1100" class="flex justify-center">
            <img
                :src="require('@/assets/img/site.png')"
                alt="Equipe tecnológica" cover
                class="rounded-lg shadow-2xl border border-rose-100"
            />
          </div>

          <div data-aos="zoom-in-left" data-aos-duration="1300">
            <p
                class="text-lg md:text-xl text-neutral-700 leading-relaxed mb-6"
            >
              Criamos experiências digitais que unem estética e tecnologia.
              Sites rápidos, dinâmicos e responsivos — tudo feito com
              excelência e um toque moderno de design digital.
            </p>

            <ul class="grid grid-cols-1 lg:grid-cols-2 gap-6">
              <li
                  v-for="item in sobreItens"
                  :key="item.titulo"
                  class="flex items-start gap-4"
              >
                <v-btn
                    :icon="item.icone"
                    :color="item.cor"
                    variant="tonal"
                >
                </v-btn>
                <div>
                  <h4 class="font-semibold text-lg text-neutral-900">
                    {{ item.titulo }}
                  </h4>
                  <p class="text-sm text-neutral-600">
                    {{ item.descricao }}
                  </p>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </v-container>
    </section>

    <!-- PLANOS -->
    <section id="planos" class="py-5 bg-white">
      <v-container>
        <h3
            class="text-4xl md:text-5xl font-extrabold text-center mb-14 text-neutral-900"
        >
          Nossos <span class="text-rose-600">Planos</span>
        </h3>

        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
          <v-card
              v-for="plan in planos"
              :key="plan.slug"
              data-aos="zoom-in-right" data-aos-duration="1200"
              class="pa-5 bg-gradient-to-b from-white to-neutral-50 border border-neutral-200 card cursor-pointer"
          >
            <div class="flex items-center justify-between mb-4">
              <h4 class="text-2xl font-bold text-neutral-900">
                {{ plan.nome }}
              </h4>
              <span
                  class="text-sm text-rose-600 font-medium"
              >{{ plan.tag }}</span
              >
            </div>

            <p class="text-neutral-600 mb-6">{{ plan.descricao }}</p>

            <v-btn
                variant="tonal" color="#F80042" class="w-full text-none" rounded
                @click="contratar(plan)"
            >
              Contratar
            </v-btn>

            <div
                v-if="expandedIndex === i"
                class="mt-6 bg-neutral-50 border border-neutral-200 rounded-2xl pa-4 text-sm text-neutral-700 overflow-hidden"
            >
              <div v-html="plan.detalhes"/>
            </div>

          </v-card>
        </div>
      </v-container>
    </section>

    <!-- CONTATO -->
    <section
        id="contato"
        class="py-5 bg-neutral-50 border-t border-neutral-200 text-center"
    >
      <v-container data-aos="zoom-in-right" data-aos-duration="1500">
        <h3
            class="text-4xl md:text-5xl font-extrabold mb-6 text-neutral-900"
        >
          Vamos Conversar?
        </h3>
        <p
            class="text-lg text-neutral-600 max-w-2xl mx-auto mb-10"
        >
          Fale conosco e receba uma proposta personalizada para o seu projeto.
        </p>

        <div class="flex flex-col sm:flex-row justify-center gap-2">
          <v-btn
              rounded variant="flat" color="#25D366"
              @click="abrirWhatsApp" class="text-none"
          >
            Falar no WhatsApp
          </v-btn>
          <v-btn
              variant="outlined" rounded
              @click="mailto" class="text-none"
          >
            Enviar Email
          </v-btn>
        </div>
      </v-container>
    </section>

    <!-- FOOTER -->
    <footer
        class="py-8 text-center text-neutral-500 bg-white border-t border-neutral-200"
    >
      <v-container>
        © {{ new Date().getFullYear() }} Maria Padilha — Feito com ❤️ e tecnologia
      </v-container>
    </footer>
  </v-main>
</template>

<script setup>
import {onMounted, onUnmounted, ref} from 'vue'

const canvas = ref(null)

onMounted(() => {
  const c = canvas.value
  if (!c) return // segurança extra

  const ctx = c.getContext('2d')

  const resize = () => {
    if (!canvas.value) return
    canvas.value.width = window.innerWidth
    canvas.value.height = window.innerHeight
  }

  window.addEventListener('resize', resize)
  resize() // chama após garantir que existe

  const particles = Array.from({length: 60}).map(() => ({
    x: Math.random() * window.innerWidth,
    y: Math.random() * window.innerHeight,
    r: Math.random() * 2 + 1,
    dx: (Math.random() - 0.5) * 0.8,
    dy: (Math.random() - 0.5) * 0.8
  }))

  function animate() {
    if (!canvas.value) return
    ctx.clearRect(0, 0, c.width, c.height)

    const gradient = ctx.createLinearGradient(0, 0, c.width, c.height)
    gradient.addColorStop(0, 'rgba(244,63,94,0.15)')
    gradient.addColorStop(1, 'rgba(249,115,22,0.1)')
    ctx.fillStyle = gradient
    ctx.fillRect(0, 0, c.width, c.height)

    particles.forEach(p => {
      ctx.beginPath()
      ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2)
      ctx.fillStyle = 'rgba(244,63,94,0.4)'
      ctx.fill()
      p.x += p.dx
      p.y += p.dy
      if (p.x < 0 || p.x > c.width) p.dx *= -1
      if (p.y < 0 || p.y > c.height) p.dy *= -1
    })

    requestAnimationFrame(animate)
  }

  animate()

  // Limpa o listener ao desmontar
  onUnmounted(() => window.removeEventListener('resize', resize))
})

const sobreItens = [
  {
    icone: 'mdi-speedometer',
    titulo: 'Alta Performance',
    descricao: 'Sites rápidos e otimizados para qualquer dispositivo.',
    cor: '#E11D48', // vermelho intenso (rose-600)
  },
  {
    icone: 'mdi-cog-outline',
    titulo: 'Tecnologia Atual',
    descricao: 'Stacks modernas, seguras e de alta performance.',
    cor: '#d73760', // vinho profundo (rose-800)
  },
  {
    icone: 'mdi-cellphone-link',
    titulo: 'Design Responsivo',
    descricao: 'Experiência perfeita e adaptável em todos os tamanhos de tela.',
    cor: '#F43F5E', // magenta avermelhado (rose-500)
  },
  {
    icone: 'mdi-target',
    titulo: 'Conversão',
    descricao: 'Layouts pensados para gerar engajamento e resultados reais.',
    cor: '#ef5874', // laranja avermelhado (amber-600)
  },
]

const planos = [
  {
    slug: 'landing',
    nome: 'Plano Essencial (Landing Page)',
    tag: 'Essencial',
    descricao: 'Ideal para quem precisa de uma página de apresentação moderna e rápida.',
    detalhes: `
      <h4 class="font-semibold text-rose-600 mb-2">Inclui:</h4>
      <ul class="list-disc list-inside mb-2">
        <li>01 página (scroll único)</li>
        <li>Design personalizado conforme identidade visual</li>
        <li>Formulário de contato simples</li>
        <li>Integração com WhatsApp</li>
        <li>SEO básico</li>
      </ul>
      <p><b>Prazo médio:</b> 5 dias úteis</p>
    `,
  },
  {
    slug: 'pro',
    nome: 'Plano Profissional (Site Institucional)',
    tag: 'Negócios',
    descricao: 'Ideal para empresas que precisam apresentar serviços e portfólio completo.',
    detalhes: `
      <h4 class="font-semibold text-rose-600 mb-2">Inclui:</h4>
      <ul class="list-disc list-inside mb-2">
        <li>Até 5 páginas (Home, Sobre, Serviços, Contato e Extra)</li>
        <li>Design exclusivo e profissional</li>
        <li>Formulário com envio para e-mail</li>
        <li>Modo escuro/claro incluso</li>
        <li>SEO otimizado e Google Maps</li>
      </ul>
      <p><b>Prazo médio:</b> 10–15 dias úteis</p>
    `,
  },
  {
    slug: 'premium',
    nome: 'Plano Premium (Painel Admin)',
    tag: 'Painel',
    descricao: 'Para quem quer autonomia para editar textos, imagens e serviços.',
    detalhes: `
      <h4 class="font-semibold text-rose-600 mb-2">Inclui:</h4>
      <ul class="list-disc list-inside mb-2">
        <li>Até 7 páginas</li>
        <li>Painel administrativo para editar textos e fotos</li>
        <li>Integrações avançadas (Google Maps, redes sociais, formulários)</li>
        <li>SEO avançado + Google Search Console</li>
        <li>Suporte pós-entrega de 30 dias</li>
      </ul>
      <p><b>Prazo médio:</b> 20–30 dias úteis</p>
    `,
  },
]

const scrollToSection = id => document.getElementById(id)?.scrollIntoView({behavior: 'smooth'})
const contratar = plan => window.open(`https://wa.me/5565984391860?text=${encodeURIComponent(`Olá, vim pelo site! Tenho interesse no *${plan.nome}*. Poderia me passar mais informações?`)}`, '_blank')
const abrirWhatsApp = () => window.open('https://wa.me/5565984391860', '_blank')
const mailto = () => (window.location.href = 'mailto:padilhabarbosa23@gmail.com')
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800;900&display=swap');

html, body, #app {
  font-family: 'Inter', sans-serif;
  scroll-behavior: smooth;
}

canvas {
  position: absolute;
  inset: 0;
  z-index: 0;
  display: block;
}

.card:hover {
  transform: translateY(-4px) scale(1.1) !important;
  box-shadow: 0 15px 30px rgba(226, 29, 72, 0.25); /* tom do vinho/vermelho */
  filter: brightness(1.05);
  transition: all 0.2s ease;
}
</style>
