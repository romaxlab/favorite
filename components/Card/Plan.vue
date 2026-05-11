<script setup lang="ts">
const props = defineProps<{
  name: string;
  category: string;
  description: string;
  price: string;
  speed?: string;
  features: string[];
  isRecommended?: boolean;
  isSelected?: boolean;
  badge?: string;
  priceUnit?: string;
}>()

const emit = defineEmits(['onCardClick'])

const isBadge = computed(() => !!props.badge)
const isRec = computed(() => props.isRecommended && !isBadge.value)
</script>

<template>
  <div
    class="relative w-full flex flex-col h-full rounded-2xl border transition-all duration-300 hover:-translate-y-1"
    :class="[
      isBadge
        ? 'bg-linear-to-b from-amber-50 to-white border-amber-400 shadow-lg shadow-amber-500/10 ring-1 ring-amber-400/30 hover:shadow-xl hover:shadow-amber-500/15'
        : isRec
          ? 'bg-linear-to-b from-white to-blue-50/40 border-blue-400 shadow-lg shadow-blue-500/10 ring-1 ring-blue-400/30 hover:shadow-xl hover:shadow-blue-500/15'
          : 'bg-white border-slate-200/80 shadow-sm hover:shadow-lg hover:border-slate-300',
    ]"
  >
    <div
      v-if="isBadge"
      class="absolute -top-3.5 left-1/2 -translate-x-1/2 flex items-center gap-1.5 px-4 py-1.5 text-xs font-bold text-white bg-linear-to-r from-amber-500 to-orange-500 rounded-full shadow-md shadow-amber-500/30 whitespace-nowrap uppercase tracking-wide"
    >
      <UIcon name="i-heroicons-fire-20-solid" class="w-3.5 h-3.5" />
      {{ props.badge }}
    </div>
    <div
      v-else-if="isRec"
      class="absolute -top-3.5 left-1/2 -translate-x-1/2 flex items-center gap-1.5 px-4 py-1.5 text-xs font-bold text-white bg-linear-to-r from-blue-600 to-blue-500 rounded-full shadow-md shadow-blue-500/30 whitespace-nowrap uppercase tracking-wide"
    >
      <UIcon name="i-heroicons-star-20-solid" class="w-3.5 h-3.5" />
      Рекомендовано
    </div>

    <div class="p-6 flex flex-col flex-1">
      <p
        class="text-xs font-semibold uppercase tracking-widest"
        :class="isBadge ? 'text-amber-600' : isRec ? 'text-blue-600' : 'text-slate-400'"
      >
        {{ props.name }}
      </p>

      <div class="mt-4">
        <span class="text-4xl font-extrabold" :class="isBadge || isRec ? 'text-slate-900' : 'text-slate-800'">{{ props.price }}</span>
        <span class="text-slate-400 ml-1 text-sm">{{ props.priceUnit ?? '/міс' }}</span>
      </div>

      <div v-if="props.speed" class="mt-3">
        <span
          class="inline-flex items-center gap-1.5 text-sm font-medium px-3 py-1.5 rounded-full"
          :class="isBadge
            ? 'text-amber-700 bg-amber-100/80'
            : isRec
              ? 'text-blue-700 bg-blue-100/80'
              : 'text-blue-600 bg-blue-50'"
        >
          <UIcon name="i-heroicons-bolt-20-solid" class="w-4 h-4" />
          {{ props.speed }}
        </span>
      </div>

      <p
        v-if="props.description"
        :title="props.description"
        class="mt-4 text-sm line-clamp-2"
        :class="isBadge || isRec ? 'text-slate-600' : 'text-slate-400'"
      >
        {{ props.description }}
      </p>

      <ul class="mt-6 space-y-2.5 flex-1">
        <li
          v-for="feature in props.features"
          :key="feature"
          class="flex items-start gap-2.5"
        >
          <UIcon
            name="i-heroicons-check-circle-20-solid"
            class="w-5 h-5 shrink-0 mt-0.5"
            :class="isBadge ? 'text-amber-500' : isRec ? 'text-blue-500' : 'text-green-500'"
          />
          <span class="text-sm" :class="isBadge || isRec ? 'text-slate-700' : 'text-slate-600'">{{ feature }}</span>
        </li>
      </ul>

      <UButton
        label="Підключити цей тариф"
        :size="isBadge || isRec ? 'xl' : 'lg'"
        class="mt-6 w-full justify-center font-semibold cursor-pointer transition-all duration-200"
        :class="isBadge
          ? 'bg-linear-to-r from-amber-500 to-orange-500 hover:from-amber-600 hover:to-orange-600 text-white hover:scale-[1.02]'
          : isRec
            ? 'bg-blue-600 hover:bg-blue-700 text-white hover:scale-[1.02]'
            : 'hover:border-slate-400'"
        :color="isBadge || isRec ? 'primary' : 'neutral'"
        :variant="isBadge || isRec ? 'solid' : 'outline'"
        @click.stop="emit('onCardClick')"
      />
    </div>
  </div>
</template>
