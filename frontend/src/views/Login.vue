<template>
  <v-app id="fundo">
    <v-container id="container">
      <v-card id="login" class="p-2 d-flex flex-column text-center" dark>
        <h1>Login</h1>
        <v-text-field label="Login:" type="text"></v-text-field>
        <v-text-field label="Senha:" type="text"></v-text-field>
        <v-btn dark :to="'/inicio'">Login</v-btn>
      </v-card>
    </v-container>
  </v-app>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
#fundo {
  background: url("../assets/fundo.jpg");
  background-size: 100%;
}

#login {
  padding: 10px 20px 15px 20px;
}

#container {
  display: flex;
  justify-content: center;
  margin: auto;
}
</style>