<template>
  <v-app>
    <v-app-bar app dark>
      <div class="d-flex align-center">
        <v-img alt="Vuetify Logo" class="shrink mr-2" contain src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png" transition="scale-transition" width="40"/>
        <v-img alt="Vuetify Name" class="shrink mt-1 hidden-sm-and-down" contain min-width="100" src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png" width="100"/>
      </div>

      <v-spacer></v-spacer>

      <v-btn text @click="dialog = true"> CADASTRO </v-btn>
    </v-app-bar>

    <v-main>
      <div class="text-center" >
        <v-dialog v-model="dialog" width="500" dark>
          <v-card>    

            <v-divider></v-divider>

            <v-card-text >
              <v-text-field label="Produto" v-model="cadastro.produto" class="mt-5" ></v-text-field>
              <v-text-field label="Descrição" v-model="cadastro.descricao" ></v-text-field>
              <v-text-field label="Preço" type="number" v-model="cadastro.preco" ></v-text-field>
            </v-card-text>

            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn dark @click="finalizarCadastro()" color="blue" > FINALIZAR </v-btn>
            </v-card-actions>

          </v-card>
        </v-dialog>
      </div> 
      {{cadastro}}
    </v-main>
  </v-app>
</template>
<script>

//import Axios from "axios"
import Produto from "@/models/Produto.js"

export default {
  name: 'Home',
  components: {    
  },
  data(){
    return{
      dialog:false,
      cadastro: new Produto()
    }
  },methods:{
    finalizarCadastro(){
      this.dialog = false;
      this.cadastro = new Produto()
    }
  }
}
</script>
