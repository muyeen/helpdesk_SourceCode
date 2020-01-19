<template>
    <div>
        <h3 v-if="users.length">User:</h3>
        <div v-bind:key="user.userData.id"  v-for="user in users">
            <h4 class="user-name">{{user.userData.name}}</h4>
            <div class="org-name">Organization: {{user.orgData.name}}</div>

             <h5 v-if="user.ticketsData.assigneeTickets.length">Assignee Tickets:</h5>
            <ul>
                <li v-bind:key="ticket.id" v-for="ticket in user.ticketsData.assigneeTickets">
                    {{ticket.subject}}
                </li>
            </ul>

            <h5 v-if="user.ticketsData.submittedTickets.length">Submitted Tickets:</h5>
            <ul>
                <li v-bind:key="ticket.id" v-for="ticket in user.ticketsData.submittedTickets">
                    {{ticket.subject}}
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: "Users",
    props:[ "users" ]
}
</script>

<style>

</style>