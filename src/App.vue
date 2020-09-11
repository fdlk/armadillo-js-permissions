<template>
  <div id="app">
    <h1>Search users</h1>
    <input type="text" v-model.lazy="searchQuery"/>
    <ul>
      <li v-for="user in users" :key="user.id">{{user.email}}
        Registrations:
        <ul>
          <li v-for="registration in user.registrations" :key="registration.id">{{registration}}</li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'app',
  data: () => ({
    searchQuery: ''
  }),
  apollo: {
    users: {
      query: gql`query SearchUsers($searchQuery: String!) {
        users(searchQuery: $searchQuery){
          id
          email
          registrations {
            id
            roles
          }
        }
      }`,
      variables () {
        return {
          searchQuery: this.searchQuery
        }
      }
    },
    registrations: gql`query {
      registrations {
        id
        email
      }
    }`
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
