<template>
  <div class="events-container">
    <h1>Event for {{ user.name }}</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
    <template v-if="page != 1">
      <router-link :to="{ name: 'EventList', query: { page: page -1 } }" rel="prev">Prev Page</router-link>
      <template v-if="hasNextPage"> | </template>
    </template>
    <router-link v-if="hasNextPage" :to="{ name: 'EventList', query: { page: page + 1 } }" rel="next">Next Page</router-link>
  </div>
</template>

<script>
// @ is an alias to /src
import EventCard from '../components/EventCard.vue'
import { mapState } from 'vuex'

export default {
  name: 'EventList',
  components: {
    EventCard,
  },
  created() {
    this.perPage = 3 //Not reactive 

    this.$store.dispatch('fetchEvents', {
      perPage: this.perPage,
      page: this.page
    })
  },
  computed: {
    page() {
      return parseInt(this.$route.query.page) || 1
    },
    hasNextPage() {
      return this.eventsTotal > this.page * this.perPage
    },
    ...mapState(['events', 'eventsTotal', 'user'])
  } 
}
</script>

<style scoped>
.events-container {
  display:flex;
  flex-direction: column;
  align-items: center;
}
</style>
