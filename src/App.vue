<template>
  <v-app>
    <v-main>
      <User/>
    </v-main>
  </v-app>
</template>

<script>
import User from "./components/User"

export default {
  name: "App",
  components: {
    User
  }
}
</script>
