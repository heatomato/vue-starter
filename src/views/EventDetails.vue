<template>
    <div v-if="event">
        <h1>{{ event.title }}</h1>
        <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
        <p>{{ event.description }}</p>
    </div>
</template>

<script>
import { mapState }  from 'vuex'

export default {
    name: 'EventDetails',
    props: ['id'],
    data() {
        return {
            event: null
        }
    },
    created() {
        this.$store.dispatch('fetchEvent', this,id)
    },
    computed: mapState(['event'])
}
</script>