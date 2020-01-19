<template>
  <div>
    <h3 v-if="organizations.length">Organization:</h3>

    <div v-bind:key="organization.orgData.id" v-for="organization in organizations">

      <h4>{{organization.orgData.name}}</h4>
      <h5 v-if="organization.orgTickets.length">Tickets:</h5>
      <ul>
        <li v-bind:key="ticket.id" v-for="ticket in organization.orgTickets">
          {{ticket.subject}} - {{ticket.user.name}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
    name:"Organizations",
    props:[ "organizations" ]
}
</script>

<style>

</style>