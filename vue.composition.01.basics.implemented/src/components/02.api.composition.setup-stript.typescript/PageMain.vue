<template>
    <alert :type="a.type" :text="a.message" :key="a.id" :description="a.description" :expanded="true"
        v-for="a in alerts">
    </alert>
</template>
<script>
import AlertMessage from './AlertMessage.vue';

export default {
    data() {
        const types = ['primary', 'secondary', 'success', 'danger', 'warning', 'info', 'light', 'dark']

        function createAlerts(types) {
            return types.map((t, idx) => ({
                id: idx,
                type: t,
                message: `A simple ${t} alert is displayed here...`,
                description:
                    "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.",
            }))
        }

        return {
            alerts: createAlerts(types),
        }
    },
    components: {
        alert: AlertMessage,
    },
}
</script>
