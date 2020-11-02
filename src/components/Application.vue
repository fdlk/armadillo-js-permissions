<template>
  <div class="application" v-if="application">
    <h1>{{ application.name }}</h1>
    <code>{{ application.id }}</code>
    <div v-if="application.roles">
      <h2>Roles</h2>
      <ul>
        <li v-for="role in application.roles" :key="role.id">
          <span :class="{super: role.isSuperRole, default: role.isDefault}">{{role.name}}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  apollo: {
    application: gql`query {
      application {
        id
        name
      }
    }`
  }
}
</script>
<style scoped>
  span.default {
    font-style: italic;
  }
  span.super {
    font-weight: bold;
  }
</style>
