<template>
  <div>
    <h3 v-if="tickets.length">Ticket:</h3>
    <div v-bind:key="ticket.ticketData.id" v-for="ticket in tickets">
      <h4>{{ticket.ticketData.subject}}</h4>
      <div class="org-name">Organization: {{ticket.ticketOrganization.name}}</div>
      <div class="org-name">Assignee: {{ticket.ticketAssignee.name}}</div>
      <div class="org-name">Submitter: {{ticket.ticketSubmitter.name}}</div>
    </div>
  </div>
  
</template>

<script>
export default {
    name: "Tickets",
    props: ["tickets"]
}
</script>

<style>

</style>