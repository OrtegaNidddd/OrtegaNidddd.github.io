<script setup>
import { ref } from "vue";
import emailjs from "@emailjs/browser";

const EMAILJS_SERVICE_ID  = import.meta.env.VITE_EMAILJS_SERVICE_ID 
const EMAILJS_TEMPLATE_ID = import.meta.env.VITE_EMAILJS_TEMPLATE_ID
const EMAILJS_PUBLIC_KEY  = import.meta.env.VITE_EMAILJS_PUBLIC_KEY

defineProps({
  linkGithub: String,
  linkInstagram: String,
});

const formData = ref({
  nombre: "",
  email: "",    
  asunto: "",
  mensaje: "",
});

const isSubmitting = ref(false);
const showSuccess = ref(false);
const showCopied = ref(false);

const contactSectionStyle = {
  background: 'var(--section-surface)',
  color: 'var(--text-primary)'
};

const mutedTextStyle = {
  color: 'var(--text-muted)'
};

const handleSubmit = async () => {
  isSubmitting.value = true;
  try {
    // Los nombres de las keys deben coincidir con las variables del Template en EmailJS
    await emailjs.send(
      EMAILJS_SERVICE_ID,
      EMAILJS_TEMPLATE_ID,
      {
        nombre:  formData.value.nombre,
        email:   formData.value.email,
        asunto:  formData.value.asunto,
        mensaje: formData.value.mensaje,
      },
      { publicKey: EMAILJS_PUBLIC_KEY }
    );

    showSuccess.value = true;
    formData.value = { nombre:'', email:'', asunto:'', mensaje:'' };
    setTimeout(() => (showSuccess.value = false), 5000);
  } catch (err) {
    alert('No se pudo enviar el mensaje. Intenta de nuevo.');
    // console.error(err);
  } finally {
    isSubmitting.value = false;
  }
};

const copyToClipboard = (text) => {
  navigator.clipboard.writeText(text);

  // Mostrar notificación
  showCopied.value = true;

  // Ocultar después de 2 segundos
  setTimeout(() => {
    showCopied.value = false;
  }, 2000);
};
</script>

<template>
  <section
    id="contacto"
    class="py-20 px-4 relative transition-colors duration-300"
    :style="contactSectionStyle"
  >
    <!-- Toast de copiado -->
    <transition
      enter-active-class="transition duration-300 ease-out"
      enter-from-class="translate-y-2 opacity-0"
      enter-to-class="translate-y-0 opacity-100"
      leave-active-class="transition duration-200 ease-in"
      leave-from-class="translate-y-0 opacity-100"
      leave-to-class="translate-y-2 opacity-0"
    >
      <div
        v-if="showCopied"
        class="fixed top-8 right-8 bg-green-500 text-white px-6 py-3 rounded-xl shadow-2xl flex items-center gap-3 z-50 border border-green-400"
      >
        <svg
          class="w-5 h-5"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-6 9l2 2 4-4"
          />
        </svg>
        <span class="font-semibold">¡Email copiado al portapapeles!</span>
      </div>
    </transition>

    <div class="max-w-6xl mx-auto">
      <!-- Header -->
      <div class="text-center mb-16">
        <div
          class="inline-flex items-center justify-center w-16 h-16 rounded-2xl bg-gradient-to-br from-indigo-600/20 to-purple-600/20 border border-indigo-600/30 mb-6"
        >
          <svg
            class="w-8 h-8 text-indigo-500/90"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
            />
          </svg>
        </div>
        <h2
          class="text-4xl font-bold mb-4 bg-gradient-to-r from-sky-500 to-pink-600 bg-clip-text text-transparent"
        >
          ¿Hablamos?
        </h2>
        <p class="text-lg max-w-2xl mx-auto" :style="mutedTextStyle">
          Estoy disponible para nuevos proyectos y oportunidades. No dudes en
          contactarme.
        </p>
      </div>

      <div class="grid md:grid-cols-2 gap-8">
        <!-- Información de contacto -->
        <div class="space-y-6">
          <!-- Tarjeta de información -->
          <div
            class="rounded-2xl border backdrop-blur-sm p-8 shadow-xl"
            style="border-color: var(--dark-color)"
          >
            <h3 class="text-2xl font-bold mb-6">Información de Contacto</h3>

            <div class="space-y-6">
              <!-- Email -->
              <div
                class="flex items-start gap-4 group cursor-pointer"
                @click="copyToClipboard('orteganid@gmail.com')"
              >
                <div
                  class="w-12 h-12 rounded-xl bg-indigo-600/20 flex items-center justify-center border border-indigo-600/40 group-hover:bg-indigo-600/30 transition-colors"
                >
                  <svg
                    class="w-6 h-6 text-indigo-600/90"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                    />
                  </svg>
                </div>
                <div class="flex-1">
                  <p class="text-sm text-gray-500 mb-1">Email</p>
                  <p
                    class="font-medium group-hover:text-indigo-400 transition-colors"
                  >
                    orteganid@gmail.com
                  </p>
                  <p class="text-xs text-gray-500 mt-1">Click para copiar</p>
                </div>
              </div>

              <!-- Instagram -->
              <a
                :href="linkInstagram"
                target="_blank"
                class="flex items-start gap-4 group"
              >
                <div
                  class="w-12 h-12 rounded-xl bg-gradient-to-br from-purple-600 via-pink-500 to-orange-400 flex items-center justify-center group-hover:shadow-lg transition-all"
                >
                  <svg
                    class="w-6 h-6 text-white"
                    fill="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      d="M7.75 2h8.5A5.75 5.75 0 0122 7.75v8.5A5.75 5.75 0 0116.25 22h-8.5A5.75 5.75 0 012 16.25v-8.5A5.75 5.75 0 017.75 2zm0 1.5A4.25 4.25 0 003.5 7.75v8.5A4.25 4.25 0 007.75 20.5h8.5a4.25 4.25 0 004.25-4.25v-8.5A4.25 4.25 0 0016.25 3.5h-8.5zM12 7a5 5 0 110 10 5 5 0 010-10zm0 1.5a3.5 3.5 0 100 7 3.5 3.5 0 000-7zm4.75-.88a1.12 1.12 0 110 2.24 1.12 1.12 0 010-2.24z"
                    />
                  </svg>
                </div>
                <div class="flex-1">
                  <p class="text-sm text-gray-500 mb-1">Instagram</p>
                  <p
                    class="font-medium group-hover:text-pink-500 transition-colors"
                  >
                    @nick._.ortega
                  </p>
                </div>
              </a>

              <!-- GitHub -->
              <a
                :href="linkGithub"
                target="_blank"
                class="flex items-start gap-4 group"
              >
                <div
                  class="w-12 h-12 rounded-xl bg-gray-500/30 flex items-center justify-center border border-gray-500/50 group-hover:bg-gray-500/40 transition-colors"
                >
                  <svg
                    class="w-6 h-6 "
                    fill="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
                    />
                  </svg>
                </div>
                <div class="flex-1">
                  <p class="text-sm text-gray-500 mb-1">GitHub</p>
                  <p
                    class="font-medium group-hover:text-gray-300 transition-colors"
                  >
                    github.com/OrtegaNidddd
                  </p>
                </div>
              </a>

              <!-- Ubicación -->
              <div class="flex items-start gap-4">
                <div
                  class="w-12 h-12 rounded-xl bg-green-500/20 flex items-center justify-center border border-green-500/40"
                >
                  <svg
                    class="w-6 h-6 text-green-500"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
                    />
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
                    />
                  </svg>
                </div>
                <div class="flex-1">
                  <p class="text-sm text-gray-500 mb-1">Ubicación</p>
                  <p class="font-medium">Cúcuta, Colombia</p>
                </div>
              </div>
            </div>
          </div>

          <!-- Disponibilidad -->
          <div
            class="rounded-2xl border backdrop-blur-sm p-6 shadow-xl bg-gradient-to-br from-green-600/40 to-emerald-600/50 border-green-500/30"
          >
            <div class="flex items-center gap-3">
              <div class="relative">
                <div class="w-3 h-3 bg-green-600 rounded-full"></div>
                <div
                  class="absolute inset-0 w-3 h-3 bg-green-600 rounded-full animate-ping"
                ></div>
              </div>
              <div>
                <p class="font-semibold ">Disponible para trabajar</p>
                <p class="text-sm">
                  Respondo en menos de 24 horas
                </p>
              </div>
            </div>
          </div>
        </div>

        <!-- Formulario de contacto -->
        <div
          class="rounded-2xl border backdrop-blur-sm p-8 shadow-xl"
          style="border-color: var(--dark-color)"
        >
          <h3 class="text-2xl font-bold mb-6">Envíame un mensaje</h3>

          <form @submit.prevent="handleSubmit" class="space-y-6">
            <!-- Nombre -->
            <div>
              <label
                for="nombre"
                class="block text-sm font-medium text-gray-400 mb-2"
              >
                Nombre
              </label>
              <input
                id="nombre"
                v-model="formData.nombre"
                type="text"
                required
                class="w-full px-4 py-3 rounded-xl border border-gray-400/30 focus:border-indigo-500 focus:ring-1 focus:ring-indigo-500/50 outline-none transition-all placeholder-gray-500"
                style="background-color: var(--dark-color);"
                placeholder="Tu nombre"
              />
            </div>

            <!-- Email -->
            <div>
              <label
                for="email"
                class="block text-sm font-medium text-gray-400 mb-2"
              >
                Email
              </label>
              <input
                id="email"
                v-model="formData.email"
                type="email"
                required
                class="w-full px-4 py-3 rounded-xl border border-gray-400/30 focus:border-indigo-500 focus:ring-1 focus:ring-indigo-500/50 outline-none transition-all placeholder-gray-500"
                style="background-color: var(--dark-color);"
                placeholder="tu@email.com"
              />
            </div>

            <!-- Asunto -->
            <div>
              <label
                for="asunto"
                class="block text-sm font-medium text-gray-400 mb-2"
              >
                Asunto
              </label>
              <input
                id="asunto"
                v-model="formData.asunto"
                type="text"
                required
                class="w-full px-4 py-3 rounded-xl border border-gray-400/30 focus:border-indigo-500 focus:ring-1 focus:ring-indigo-500/50 outline-none transition-all placeholder-gray-500"
                style="background-color: var(--dark-color);"
                placeholder="¿Sobre qué quieres hablar?"
              />
            </div>

            <!-- Mensaje -->
            <div>
              <label
                for="mensaje"
                class="block text-sm font-medium text-gray-400 mb-2"
              >
                Mensaje
              </label>
              <textarea
                id="mensaje"
                v-model="formData.mensaje"
                rows="5"
                required
                class="w-full px-4 py-3 rounded-xl border border-gray-400/30 focus:border-indigo-500 focus:ring-1 focus:ring-indigo-500/50 outline-none transition-all placeholder-gray-500 resize-none"
                style="background-color: var(--dark-color);"
                placeholder="Cuéntame sobre tu proyecto o idea..."
              ></textarea>
            </div>

            <!-- Botón de envío -->
            <button
              type="submit"
              :disabled="isSubmitting"
              class="w-full bg-gradient-to-r from-indigo-500 to-purple-600 hover:from-indigo-600 hover:to-purple-700 text-white font-bold py-3 px-6 rounded-xl transition-all duration-200 transform hover:scale-105 disabled:opacity-50 disabled:cursor-not-allowed disabled:hover:scale-100 flex items-center justify-center gap-2"
            >
              <span v-if="!isSubmitting">Enviar mensaje</span>
              <span v-else>Enviando...</span>
              <svg
                v-if="!isSubmitting"
                class="w-5 h-5"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M14 5l7 7m0 0l-7 7m7-7H3"
                />
              </svg>
            </button>

            <!-- Mensaje de éxito -->
            <div
              v-if="showSuccess"
              class="bg-green-500/10 border border-green-500/30 rounded-xl p-4 flex items-start gap-3"
            >
              <svg
                class="w-6 h-6 text-green-400 flex-shrink-0"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"
                />
              </svg>
              <div>
                <p class="font-semibold text-green-400">¡Mensaje enviado!</p>
                <p class="text-sm text-gray-400">
                  Te responderé lo antes posible.
                </p>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>
