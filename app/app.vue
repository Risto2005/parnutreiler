
<script setup lang="ts">
import { onMounted, onUnmounted, ref, watch } from 'vue'

const selectedPhoto = ref<string | null>(null)
const menuOpen = ref(false)

function closePhoto() {
  selectedPhoto.value = null
}

function handleKeydown(event: KeyboardEvent) {
  if (event.key === 'Escape') {
    closePhoto()
    menuOpen.value = false
  }
}

watch(selectedPhoto, (photo) => {
  document.body.style.overflow = photo ? 'hidden' : ''
})

onMounted(() => window.addEventListener('keydown', handleKeydown))
onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
  document.body.style.overflow = ''
})

const contact = {
  phone: '+372 555 1234',
  email: 'info@parnutreiler.ee',
}

const prices = [
  { title: '1–3 tundi', price: 'XX €' },
  { title: '1–12 tundi', price: 'XX €' },
  { title: '1–24 tundi', price: 'XX €' },
]

const features = [
  {
    title: 'Elektriline vints',
    description:
      'Haagis on varustatud elektrilise vintsiga sõiduki haagisele laadimiseks.',
  },
  {
    title: 'Koormarihmad',
    description:
      'Sõiduki kinnitamiseks vajalikud koormarihmad kuuluvad rendihinna sisse.',
  },
  {
    title: 'Ööpäevaringne väljastamine ja tagastamine',
    description:
      'Haagist on võimalik kätte saada ja tagastada ööpäevaringselt.',
  },
]

const gallery = [
  {
    src: 'https://cdn.webshopapp.com/shops/255717/files/483538801/image.jpg',
    alt: 'Autoveohaagis külgvaates',
  },
  {
    src: 'https://www.aanhangcars.nl/media/catalog/product/cache/1f8a71b9d27ae7eadeedc4372aff9d47/a/h/ahc.02.211.606.65.01-i.jpg',
    alt: 'Autoveohaagise platvorm',
  },
  {
    src: 'https://b263dd3dd2.clvaw-cdnwnd.com/92b79db79c21796226422c04f061f2af/200003394-685be685c0/20231213_141042.jpeg?ph=b263dd3dd2',
    alt: 'Autoveohaagis pealesõidurampidega',
  },
  {
    src: 'https://gttowing.co.uk/uploads/cms/products/8217/image00011-image-preview.jpg',
    alt: 'Autoveohaagis eestvaates',
  },
]
</script>

<template>
  <main class="min-h-screen bg-[#101010] text-white">
    <!-- Navigatsioon -->
    <header class="absolute inset-x-0 top-0 z-20">
      <div
        class="mx-auto flex max-w-7xl items-center justify-between px-6 py-6 lg:px-10"
      >
        <a href="#" class="text-xl font-bold tracking-wide">
          PÄRNU <span class="text-red-700">TREILER</span>
        </a>

        <nav class="hidden items-center gap-8 text-sm text-gray-300 md:flex" aria-label="Peamenüü">
          <a href="#haagis" class="transition hover:text-white">Haagis</a>
          <a href="#lisavarustus" class="transition hover:text-white">Lisavarustus</a>
          <a href="#hinnakiri" class="transition hover:text-white">Hinnakiri</a>
          <a href="#galerii" class="transition hover:text-white">Galerii</a>
          <a href="#kontakt" class="transition hover:text-white">Kontakt</a>
        </nav>

        <div class="flex items-center gap-3">
          <a href="#kontakt" class="hidden rounded-md bg-red-900 px-5 py-3 text-sm font-semibold transition hover:bg-red-800 sm:inline-flex">
            Võta ühendust
          </a>
          <button
            type="button"
            class="inline-flex h-10 w-10 items-center justify-center rounded-md border border-white/20 text-white md:hidden"
            :aria-expanded="menuOpen"
            aria-label="Ava menüü"
            @click="menuOpen = !menuOpen"
          >
            <svg v-if="!menuOpen" viewBox="0 0 24 24" class="h-6 w-6" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true">
              <path d="M4 7h16M4 12h16M4 17h16" />
            </svg>
            <svg v-else viewBox="0 0 24 24" class="h-6 w-6" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true">
              <path d="m6 6 12 12M18 6 6 18" />
            </svg>
          </button>
        </div>
      </div>

      <nav v-if="menuOpen" class="border-t border-white/10 bg-[#101010] px-6 py-3 md:hidden" aria-label="Mobiilimenüü">
        <a v-for="item in [
          { label: 'Haagis', href: '#haagis' },
          { label: 'Lisavarustus', href: '#lisavarustus' },
          { label: 'Hinnakiri', href: '#hinnakiri' },
          { label: 'Galerii', href: '#galerii' },
          { label: 'Kontakt', href: '#kontakt' },
        ]" :key="item.href" :href="item.href" class="block py-3 text-sm text-gray-300 hover:text-white" @click="menuOpen = false">
          {{ item.label }}
        </a>
      </nav>
    </header>

    <!-- Avalehe päis -->
    <section
  class="relative flex min-h-[82svh] items-center bg-cover bg-center pt-24 sm:min-h-[90vh]"
  style="background-image: url('/images/trailer.jpg')"
>
      <div class="absolute inset-0"></div>
      <div
        class="absolute inset-0 bg-gradient-to-r from-black/90 via-black/65 to-black/60"
      ></div>

      <div class="relative mx-auto w-full max-w-7xl px-5 pb-14 pt-32 sm:px-6 sm:pb-16 sm:pt-36 lg:px-10">
        <div class="max-w-3xl">
          <h1 class="text-4xl font-bold leading-tight sm:text-5xl lg:text-7xl">
            Autoveohaagise rent Pärnus
          </h1>

          <p class="mt-6 max-w-2xl text-base leading-7 text-gray-300 sm:mt-7 sm:text-lg sm:leading-8">
            Rendime autoveohaagist sõiduautode transportimiseks. Haagis on
            varustatud elektrilise vintsi ja koormarihmadega.
          </p>

          <div class="mt-8 flex flex-wrap gap-3 sm:mt-10 sm:gap-4">
            <a
              href="#hinnakiri"
              class="rounded-md bg-red-900 px-6 py-3.5 font-semibold transition hover:bg-red-800 sm:px-7 sm:py-4"
            >
              Vaata hinnakirja
            </a>

            <a
              href="#kontakt"
              class="rounded-md border border-white/40 px-6 py-3.5 font-semibold transition hover:bg-white hover:text-black sm:px-7 sm:py-4"
            >
              Kontakt
            </a>
          </div>
        </div>
      </div>
    </section>

    <!-- Haagise tutvustus -->
    <section id="haagis" class="scroll-mt-20 px-5 py-16 sm:px-6 sm:py-20 lg:px-10 lg:py-24">
      <div
        class="mx-auto grid max-w-7xl gap-12 lg:grid-cols-2 lg:items-center"
      >
        <div>
          <p
            class="mb-4 text-sm font-semibold uppercase tracking-[0.2em] text-red-500"
          >
            Haagise info
          </p>

          <h2 class="text-3xl font-bold sm:text-4xl">
            Autoveohaagis sõidukite transportimiseks
          </h2>

          <p class="mt-6 leading-8 text-gray-400">
            Pakume autoveohaagist sõiduautode transportimiseks. Haagis sobib
            sõiduki ühest asukohast teise toimetamiseks. Tehnilised andmed ja
            lisavarustus on toodud allpool.
          </p>
        </div>

        <div class="rounded-lg border border-white/10 bg-[#191919] p-6 sm:p-8">
          <h3 class="mb-6 text-xl font-semibold">Tehnilised andmed</h3>

          <div class="space-y-5">
            <div
              class="flex items-center justify-between border-b border-white/10 pb-4"
            >
              <span class="text-gray-400">Haagise tüüp</span>
              <span class="font-medium">Autoveohaagis</span>
            </div>

            <div
              class="flex items-center justify-between border-b border-white/10 pb-4"
            >
              <span class="text-gray-400">Platvormi mõõdud</span>
              <span class="font-medium">2,5 × 1,3 m</span>
            </div>

            <div class="flex items-center justify-between">
              <span class="text-gray-400">Kandevõime</span>
              <span class="font-medium">750 kg</span>
            </div>
          </div>

          <p class="mt-6 text-xs leading-6 text-gray-500">
            Enne rentimist kontrolli, et haagise mõõdud, kandevõime ja
            täismass sobivad transporditava sõiduki ning vedukiga.
          </p>
        </div>
      </div>
    </section>

    <!-- Lisavarustus -->
    <section
      id="lisavarustus"
      class="scroll-mt-20 border-y border-white/10 bg-[#171717] px-5 py-16 sm:px-6 sm:py-20 lg:px-10 lg:py-24"
    >
      <div class="mx-auto max-w-7xl">
        <div class="max-w-2xl">
          <p
            class="mb-4 text-sm font-semibold uppercase tracking-[0.2em] text-red-500"
          >
            Lisavarustus ja teenindus
          </p>

          <h2 class="text-3xl font-bold sm:text-4xl">
            Haagise varustus ja kasutustingimused
          </h2>

          <p class="mt-5 leading-8 text-gray-400">
            Haagise kasutamiseks vajalik põhivarustus on rendihinna sees.
            Väljastamine ja tagastamine on korraldatud ööpäevaringselt.
          </p>
        </div>

        <div class="mt-12 grid gap-5 md:grid-cols-3">
          <article
            v-for="feature in features"
            :key="feature.title"
            class="rounded-lg border border-white/10 bg-[#101010] p-6 sm:p-7"
          >
            <div
              class="mb-6 flex h-12 w-12 items-center justify-center rounded-md bg-red-950 text-red-400"
            >
              <svg
                v-if="feature.title === 'Elektriline vints'"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="1.7"
                class="h-6 w-6"
              >
                <path d="M13 2 4 14h7l-1 8 10-13h-7l1-7Z" />
              </svg>

              <svg
                v-else-if="feature.title === 'Koormarihmad'"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="1.7"
                class="h-6 w-6"
              >
                <path d="M4 7h16M4 17h16M7 4v16m10-16v16" />
                <path d="m4 7 3-3 3 3m7 10 3 3 1-3" />
              </svg>

              <svg
                v-else
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="1.7"
                class="h-6 w-6"
              >
                <circle cx="12" cy="12" r="9" />
                <path d="M12 7v5l3 2" />
              </svg>
            </div>

            <h3 class="text-lg font-semibold">{{ feature.title }}</h3>
            <p class="mt-3 text-sm leading-7 text-gray-400">
              {{ feature.description }}
            </p>
          </article>
        </div>
      </div>
    </section>

    <!-- Hinnakiri -->
    <section id="hinnakiri" class="scroll-mt-20 px-5 py-16 sm:px-6 sm:py-20 lg:px-10 lg:py-24">
      <div class="mx-auto max-w-7xl">
        <div class="max-w-2xl">
          <p
            class="mb-4 text-sm font-semibold uppercase tracking-[0.2em] text-red-500"
          >
            Hinnakiri
          </p>

          <h2 class="text-3xl font-bold sm:text-4xl">
            Haagise rendihinnad
          </h2>

          <p class="mt-5 leading-8 text-gray-400">
            Rendihind sõltub rendiperioodi pikkusest. Elektrilise vintsi ja
            koormarihmade kasutamine sisaldub rendihinnas.
          </p>
        </div>

        <div class="mt-12 grid gap-5 md:grid-cols-3">
          <article
            v-for="(item, index) in prices"
            :key="item.title"
            class="rounded-lg border border-white/10 bg-[#191919] p-6 sm:p-8"
            :class="index === 1 ? 'border-red-900/80' : ''"
          >
            <p class="text-sm font-medium text-gray-400">Rendiperiood</p>

            <h3 class="mt-3 text-2xl font-bold">
              {{ item.title }}
            </h3>

            <div class="my-7 h-px bg-white/10"></div>

            <p class="text-3xl font-bold text-white">
              {{ item.price }}
            </p>

            <p class="mt-2 text-sm text-gray-500">Rendihind</p>
          </article>
        </div>
      </div>
    </section>

    <!-- Galerii -->
    <section
      id="galerii"
      class="scroll-mt-20 border-y border-white/10 bg-[#171717] px-5 py-16 sm:px-6 sm:py-20 lg:px-10 lg:py-24"
    >
      <div class="mx-auto max-w-7xl">
        <div class="max-w-2xl">
          <p
            class="mb-4 text-sm font-semibold uppercase tracking-[0.2em] text-red-500"
          >
            Fotod
          </p>

          <h2 class="text-3xl font-bold sm:text-4xl">
            Haagise galerii
          </h2>

          <p class="mt-5 leading-8 text-gray-400">
            Vaata autoveohaagiste näidisfotosid.
          </p>
        </div>

        <div class="mt-12 grid grid-cols-1 gap-5 sm:grid-cols-2 lg:grid-cols-4">
          <button
            v-for="photo in gallery"
            :key="photo.src"
            type="button"
            :aria-label="`Suurenda pilti: ${photo.alt}`"
            class="group relative block aspect-[4/3] overflow-hidden rounded-lg border border-white/10 bg-[#222] focus-visible:outline focus-visible:outline-2 focus-visible:outline-red-500"
            @click="selectedPhoto = photo.src"
          >
            <img
              :src="photo.src"
              :alt="photo.alt"
              loading="lazy"
              decoding="async"
              class="h-full w-full object-cover transition duration-500 group-hover:scale-105"
            />
            <span class="sr-only">Suurenda pilti</span>
          </button>
        </div>
      </div>
    </section>


    <!-- Pildi suurvaade -->
    <Teleport to="body">
      <div
        v-if="selectedPhoto"
        class="fixed inset-0 z-[100] flex items-center justify-center bg-black/95 p-4 sm:p-8"
        role="dialog"
        aria-modal="true"
        aria-label="Suurendatud haagise foto"
        @click.self="closePhoto"
      >
        <button
          type="button"
          class="absolute right-4 top-4 flex h-11 w-11 items-center justify-center rounded-full border border-white/20 bg-white/10 text-3xl text-white transition hover:bg-red-900"
          aria-label="Sulge pilt"
          @click="closePhoto"
        >
          &times;
        </button>
        <img
          :src="selectedPhoto"
          alt="Suurendatud haagise foto"
          class="max-h-[90vh] max-w-full rounded-lg object-contain"
          decoding="async"
          @click.stop
        />
      </div>
    </Teleport>

    <!-- Kontakt -->
    <section
      id="kontakt"
      class="scroll-mt-20 border-t border-white/10 bg-[#171717] px-5 py-16 sm:px-6 sm:py-20 lg:px-10 lg:py-24"
    >
      <div
        class="mx-auto grid max-w-7xl gap-12 lg:grid-cols-2 lg:items-center"
      >
        <div>
          <p
            class="mb-4 text-sm font-semibold uppercase tracking-[0.2em] text-red-500"
          >
            Kontakt
          </p>

          <h2 class="text-3xl font-bold sm:text-4xl">
            Haagise rentimiseks võtke ühendust
          </h2>

          <p class="mt-6 max-w-xl leading-8 text-gray-400">
            Renditingimuste, saadavuse ja täpsema info saamiseks võtke meiega
            ühendust telefoni või e-posti teel.
          </p>
        </div>

        <div class="rounded-lg border border-white/10 bg-[#101010] p-6 sm:p-8">
          <div class="space-y-7">
            <div>
              <p class="text-sm text-gray-500">Telefon</p>
              <a
                :href="`tel:${contact.phone.replaceAll(' ', '')}`"
                class="mt-2 block text-xl font-semibold transition hover:text-red-400"
              >
                {{ contact.phone }}
              </a>
            </div>

            <div class="h-px bg-white/10"></div>

            <div>
              <p class="text-sm text-gray-500">E-post</p>
              <a
                :href="`mailto:${contact.email}`"
                class="mt-2 block break-all text-xl font-semibold transition hover:text-red-400"
              >
                {{ contact.email }}
              </a>
            </div>
          </div>

          <div class="mt-8 flex flex-col gap-3 sm:flex-row">
            <a
              :href="`tel:${contact.phone.replaceAll(' ', '')}`"
              class="rounded-md bg-red-900 px-6 py-3 text-center text-sm font-semibold transition hover:bg-red-800"
            >
              Helista
            </a>

            <a
              :href="`mailto:${contact.email}`"
              class="rounded-md border border-white/20 px-6 py-3 text-center text-sm font-semibold transition hover:border-white hover:bg-white hover:text-black"
            >
              Saada e-kiri
            </a>
          </div>
        </div>
      </div>
    </section>

    <!-- Jalus -->
    <footer class="border-t border-white/10 bg-[#0b0b0b] px-6 py-8 lg:px-10">
      <div
        class="mx-auto flex max-w-7xl flex-col justify-between gap-4 text-sm text-gray-500 sm:flex-row"
      >
        <p>
          © {{ new Date().getFullYear() }} Pärnu Treiler. Kõik õigused kaitstud.
        </p>

        <p>Autoveohaagise rent Pärnus</p>
      </div>
    </footer>
  </main>
</template>

<style>
html {
  scroll-behavior: smooth;
}

@media (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto;
  }
}
</style>




