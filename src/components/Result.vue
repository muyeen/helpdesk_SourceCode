<template>
<div>
  <Users  v-bind:users="searchResult.users"/>
  <Organizations v-bind:organizations="searchResult.organizations" />
  <Tickets v-bind:tickets="searchResult.tickets" />

  <div v-if="(searchResult.users.length + searchResult.organizations.length + searchResult.tickets.length) == 0">
    <p>No Result Found</p>
  </div>
</div>
</template>

<script>
import Organizations from "./Organizations";
import Users from "./Users";
import Tickets from "./Tickets";

export default {
  name: "Result",
  components: {
    Organizations,
    Users,
    Tickets
  },
  props: [ "searchResult" ]
}
</script>

<style scoped>

</style>

