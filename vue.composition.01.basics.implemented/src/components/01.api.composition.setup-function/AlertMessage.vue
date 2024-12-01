<template>
    <div class="alert" :class="[`alert-${type}`, { dismissible }]" role="alert">
        <div>
            <b>SETUP FUNCTION:</b> {{ text }}
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
import { onMounted, watch, ref } from 'vue';

export default {
    props: {
        text: { type: String },
        description: { type: String },
        type: { type: String, default: 'primary' },
        dismissible: { type: Boolean, default: false },
        expanded: { type: Boolean, default: false }
    },
    emits: [, 'update:expanded', 'dismissed'],
    setup(props) {
        // data.expandedState
        const expandedState = ref(props.expanded)

        // mounted
        onMounted(() => {
            // synchronizacja inner => external
            this.expandedState = props.expanded
        })

        // methods.toggleDesc
        function toggleDesc() {
            expandedState.value = !expandedState.value
            // synchronizacja inner => external
            this.$emit('update:expanded', expandedState.value)
            // this.expanded = !this.expanded
        }

        // methods.handleDismiss
        function handleDismiss() {
            this.$emit('dismissed')
        }

        // watch.expaned
        watch(() => props.expaned, (val) => {
            // synchronizacja external => inner
            this.expandedState = val
        })

        return {
            expandedState,
            toggleDesc,
            handleDismiss
        }
    }
    //   props: {
    //     text: { type: String },
    //     description: { type: String },
    //     type: { type: String, default: 'primary' },
    //     dismissible: { type: Boolean, default: false },
    //     expanded: { type: Boolean, default: false },
    //   },
    //   mounted() {
    //     this.expandedState = this.expanded
    //   },
    //   data() {
    //     return {
    //       expandedState: false,
    //     }
    //   },
    //   emits: [, 'update:expanded', 'dismissed'],
    //   methods: {
    //     handleDismiss() {
    //       this.$emit('dismissed')
    //     },
    //     toggleDesc() {
    //       this.expandedState = !this.expandedState
    //       // synchronizacja inner => external
    //       this.$emit('update:expanded', this.expandedState)
    //       // this.expanded = !this.expanded
    //     },
    //   },
    //   watch: {
    //     expanded(val) {
    //       // synchronizacja external => inner
    //       this.expandedState = val
    //     },

    //     // expanded: {
    //     //   handler(val) {
    //     //     // synchronizacja external => inner
    //     //     this.expandedState = val
    //     //   },
    //     //   immediate: true
    //     // },
    //   },
}
</script>
