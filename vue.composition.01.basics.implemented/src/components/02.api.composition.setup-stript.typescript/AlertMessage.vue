<template>
  <div class="alert" :class="[`alert-${type}`, { dismissible }]" role="alert">
    <div>
      <b>SCRIPT SETUP:</b> {{ text }}
      <div v-if="description">
        <a href="#" @click="toggleDesc">
          <template v-if="!expanded">show more » </template>
          <template v-else>« hide more</template>
        </a>
        <div v-if="expanded">
          <hr />
          {{ description }}
        </div>
      </div>
    </div>

    <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close" v-if="dismissible"
      @click="handleDismiss"></button>
  </div>
</template>

<script setup lang="ts">
export type AlertMessageProps = {
  text?: string
  description?: string,
  type: 'primary' | 'secondary' | 'success' | 'danger' | 'warning' | 'info' | 'light' | 'dark',
  dismissible?: boolean,
}

const props = withDefaults(defineProps<AlertMessageProps>(), {
  type: 'primary',
  dismissible: false
})

const expanded = defineModel('expanded')

const $emit = defineEmits<{
  (e: 'dismissed'): void
}>()

// methods.toggleDesc
function toggleDesc() {
  // synchronizacja obustronna
  expanded.value = !expanded.value
  // synchronizacja inner => external
}

// methods.handleDismiss
function handleDismiss() {
  $emit('dismissed')
}
</script>
