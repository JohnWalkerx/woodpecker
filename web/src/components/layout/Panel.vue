<template>
  <div
    class="rounded-md w-full shadow overflow-hidden bg-wp-background-100 dark:bg-wp-background-200 border border-wp-background-400"
  >
    <component
      :is="collapsable ? 'button' : 'div'"
      v-if="title"
      type="button"
      class="flex w-full font-bold gap-2 text-wp-text-100 px-4 py-2 bg-wp-background-300"
      @click="_collapsed = !_collapsed"
    >
      <Icon
        v-if="collapsable"
        name="chevron-right"
        class="transition-transform duration-150 min-w-6 h-6"
        :class="{ 'transform rotate-90': !collapsed }"
      />
      {{ title }}
    </component>
    <div
      :class="{
        'max-h-auto': !collapsed,
        'max-h-0': collapsed,
      }"
      class="transition-height duration-150 overflow-hidden"
    >
      <div class="w-full p-4 text-wp-text-100">
        <slot />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { computed, ref } from 'vue';

import Icon from '~/components/atomic/Icon.vue';

const props = defineProps<{
  title?: string;
  collapsable?: boolean;
}>();

/**
 * _collapsed is used to store the internal state of the panel, but is
 * ignored if the panel is not collapsable.
 */
const _collapsed = ref(false);

const collapsed = computed(() => props.collapsable && _collapsed.value);
</script>
