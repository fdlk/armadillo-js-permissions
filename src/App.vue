<template>
  <div id="app">
    <application></application>
    <h1>Add users</h1>
    <input type="text" v-model.lazy="searchQuery"/>
    <ul>
      <li v-for="user in users" :key="user.id">{{user.email}}
        <ul>
          <li v-for="role in user.roles" :key="role">{{role}}</li>
        </ul>
      </li>
    </ul>
    <h1>Registered users</h1>
    <ul>
      <li v-for="user in registeredUsers" :key="user.id">{{user.email}}
        <ul>
          <li v-for="role in user.roles" :key="role">{{role}}</li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
import gql from 'graphql-tag'
import Application from './components/Application'

export default {
  name: 'app',
  components: {
    Application
  },
  data () {
    return {
      searchQuery: 'Fleur'
    }
  },
  apollo: {
    users: {
      query: gql`query SearchUsers($searchQuery: String!) {
        users(searchQuery: $searchQuery){
          id
          email
          roles
        }
      }`,
      variables () {
        return {
          searchQuery: this.searchQuery
        }
      }
    },
    registeredUsers: gql`query {
      registeredUsers {
        id
        email
        roles
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
