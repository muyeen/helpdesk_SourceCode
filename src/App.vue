<template>
  <div id="app">
    <Search v-on:search-run="search"/>
    <Result v-bind:searchResult="searchResult" v-if="keyWord.length"/>
 
  </div>
</template>

<script>
import Result from './components/Result';
import Search from './components/Search';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Result,
    Search
  }, 
  data() {
    return {
      keyWord: '',
      data : {
        users: [],
        organizations: [],
        tickets: []
      },
      searchResult : {
        users: [],
        organizations: [],
        tickets: []
      }

    }
  },
  created() {
    
      axios.get('https://muyeen.github.io/GoBot/users.json')
      .then(res => this.data.users = res.data)
      .catch(err => console.log(err));

      axios.get('https://muyeen.github.io/GoBot/organizations.json')
      .then(res => this.data.organizations = res.data)
      .catch(err => console.log(err));

      axios.get('https://muyeen.github.io/GoBot/tickets.json')
      .then(res => this.data.tickets = res.data)
      .catch(err => console.log(err));

     // this.searchAll();

    },
   methods: {
    search(keyWord){
      this.keyWord = keyWord;
      this.getUserDetails();
      this.getOrganizationDetails();
      this.getTicketDetails();

    },

    getOrganizationDetails(){
        this.searchResult.organizations = this.data.organizations
        .filter(organization => organization._id.toString() == this.keyWord)
        .map((organization) => {
        
          const  orgTickets = this.data.tickets.filter(ticket => ticket.organization_id == organization._id).map((ticket) => {
            return {
            id:ticket._id,
            subject: ticket.subject,
            user: this.data.users.filter(user => user._id === ticket.submitter_id)[0]
            }
          })
          
          return {
            orgData: organization,
            orgTickets: orgTickets
            };
          
        })
    },
    getUserDetails(){
      this.searchResult.users = this.data.users
      .filter(user => user._id.toString() === this.keyWord)
      .map((user) => {
        return {
          userData : user,
          orgData: this.data.organizations.filter(organization => organization._id === user.organization_id)[0],
          ticketsData:{
            assigneeTickets : this.data.tickets.filter(ticket => ticket.assignee_id === user._id),
            submittedTickets : this.data.tickets.filter(ticket => ticket.submitter_id === user._id)
          }
        }
      })
    },

    getTicketDetails(){
       this.searchResult.tickets = this.data.tickets
       .filter(ticket => ticket._id == this.keyWord)
       .map((ticket) => {
         return {
           ticketData: ticket,
           ticketAssignee : this.data.users.filter(user => user._id === ticket.assignee_id)[0],
           ticketSubmitter : this.data.users.filter(user => user._id === ticket.submitter_id)[0],
           ticketOrganization : this.data.organizations.filter(organization => organization._id === ticket.organization_id)[0]
         }
       });
    }
  }
    
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}
</style>


