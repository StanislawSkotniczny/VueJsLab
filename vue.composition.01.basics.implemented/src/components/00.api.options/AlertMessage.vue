<template>
  <div class="alert" :class="[`alert-${type}`, { dismissible }]" role="alert">
    <div>
      <b>OPTIONS:</b> {{ text }}
      <div v-if="description">
        <a href="#" @click="toggleDesc">
          <template v-if="!expandedState">show more » </template>
          <template v-else>« hide more</template>
        </a>
        <div v-if="expandedState">
          <hr />
          {{ description }}
        </div>
      </div>
    </div>

    <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close" v-if="dismissible"
      @click="handleDismiss"></button>
  </div>
</template>

<script>
export default {
  mounted() {
    this.expandedState = this.expanded
  },
  props: {
    text: { type: String },
    description: { type: String },
    type: { type: String, default: 'primary' },
    dismissible: { type: Boolean, default: false },
    // holds component external state
    expanded: { type: Boolean, default: false },
  },
  emits: [, 'update:expanded', 'dismissed'],
  data() {
    return {
      // holds component inner state
      expandedState: false,
    }
  },
  methods: {
    handleDismiss() {
      this.$emit('dismissed')
    },
    toggleDesc() {
      this.expandedState = !this.expandedState
      // synchronizacja inner => external
      this.$emit('update:expanded', this.expandedState)
      // this.expanded = !this.expanded
    },
  },
  watch: {
    expanded(val) {
      // synchronizacja external => inner
      this.expandedState = val
    },

    // expanded: {
    //   handler(val) {
    //     // synchronizacja external => inner
    //     this.expandedState = val
    //   },
    //   immediate: true
    // },
  },
}
</script>
