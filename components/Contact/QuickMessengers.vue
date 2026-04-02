<script setup lang="ts">
import { siteConfig } from '~/config/site'

const channels = [
  {
    name: 'Viber',
    hint: 'Швидкі повідомлення',
    link: siteConfig.social.viber,
    iconBg: 'bg-purple-50',
    iconClass: 'text-[#675da9]',
  },
  {
    name: 'Telegram',
    hint: 'Оперативний зв\'язок',
    link: siteConfig.social.telegram,
    iconBg: 'bg-cyan-50',
    iconClass: 'text-[#1E96C8]',
  },
  {
    name: 'Facebook',
    hint: 'Спілкування в Facebook',
    link: siteConfig.social.facebook,
    iconBg: 'bg-blue-50',
    iconClass: 'text-[#0966ff]',
  },
] as const
</script>

<template>
  <div
    class="bg-white border border-slate-200 rounded-2xl p-5 transition-all duration-200 hover:shadow-md hover:-translate-y-0.5">
    <div class="mb-4">
      <h3 class="text-sm font-bold text-slate-900">
        Швидкий зв'язок
      </h3>
      <p class="text-xs text-slate-500 mt-1">
        Відповідаємо швидше, ніж по email
      </p>
    </div>
    <div class="grid gap-3">
      <NuxtLink
        v-for="ch in channels"
        :key="ch.name"
        :href="ch.link"
        target="_blank"
        rel="noopener noreferrer"
        :title="ch.hint"
        class="group flex items-center gap-3 rounded-xl border border-slate-100 bg-slate-50/60 px-2 py-2 hover:border-slate-200 hover:bg-white transition-colors">
        <div class="w-10 h-10 rounded-lg flex items-center justify-center shrink-0" :class="ch.iconBg">
          <BaseIconSocialTelegram v-if="ch.name === 'Telegram'" class="w-5 h-5" :class="ch.iconClass" />
          <BaseIconSocialViber v-else-if="ch.name === 'Viber'" class="w-5 h-5" :class="ch.iconClass" />
          <BaseIconSocialFacebook v-else class="w-5 h-5" :class="ch.iconClass" />
        </div>
        <div class="min-w-0 flex-1 text-left">
          <div class="text-sm leading-tight font-semibold text-slate-900 truncate">
            {{ ch.name }}
          </div>
          <div class="text-xs text-slate-500 mt-1">
            {{ ch.hint }}
          </div>
        </div>
        <UIcon 
          name="i-heroicons-arrow-top-right-on-square-20-solid"
          class="w-4 h-4 shrink-0 text-slate-300 group-hover:text-blue-600 transition-colors"
        />
      </NuxtLink>
    </div>
  </div>
</template>
