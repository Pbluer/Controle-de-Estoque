<template>
  <v-app>
    <v-app-bar app dark>
      <div class="d-flex align-center">
        <v-img alt="Vuetify Logo" class="shrink mr-2" contain src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png" transition="scale-transition" width="40"/>
        <v-img alt="Vuetify Name" class="shrink mt-1 hidden-sm-and-down" contain min-width="100" src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png" width="100"/>
      </div>

      <v-spacer></v-spacer>

      <v-btn text @click="dialog = true"> CADASTRO </v-btn>
      <v-btn color="red" :to="'/'"> SAIR </v-btn>
    </v-app-bar>

    <v-main>
      <div class="text-center">
        <v-dialog v-model="dialog" width="500" dark>
          <v-card>    

            <v-divider></v-divider>

            <v-card-text >
              <v-text-field label="Produto:" type="text" v-model="cadastro.produto" class="mt-5" ></v-text-field>
              <v-text-field label="Descrição:" type="text"  v-model="cadastro.descricao" ></v-text-field>
              <v-row>
                 <v-spacer></v-spacer>
                 <v-text-field label="Preço:" style="width:100px" type="number" v-model="cadastro.preco" ></v-text-field>
                 <v-spacer></v-spacer>
                <v-text-field label="Peso:" style="width:100px" type="number" v-model="cadastro.peso" ></v-text-field>
                 <v-spacer></v-spacer>
                <v-text-field label="Entrada:" style="width:100px" type="date" v-model="cadastro.entrada" ></v-text-field>
                 <v-spacer></v-spacer>
              </v-row>
            </v-card-text>

            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn dark @click="finalizarCadastro()" color="blue" > FINALIZAR </v-btn>
            </v-card-actions>

          </v-card>
        </v-dialog>
      </div> 
      <div class="d-sm-flex flex-comlumn">
        <v-container>
          <h1 class="ml-3">Comida</h1>
          <Tabela :comida="comida" @delet="excluirProduto(value)" />
        </v-container>
        <v-spacer></v-spacer>
        <v-container>
           <h1 class="ml-3">Bebida</h1>
          <Tabela :bebida="bebida"/>
        </v-container>
      </div>
    </v-main>
  </v-app>
</template>
<script>

import Axios from "axios"
import Tabela from "@/components/Tabela"
import Produto from "@/models/Produto.js"

export default {
  components: {    
    Tabela
  },
  async created(){    
    try{
      this.comida = await this.getTabela()
    }catch(error){
      console.log(error)
    }    
  },
  async updated(){
    this.comida = await this.getTabela()
  },
  data(){    
      return({
        dialog:false,
        cadastro: new Produto(),
        bebida:[],
        comida:[]
      })   
  },
  methods:{
    async getTabela(){        
      const { data } = await Axios.get("http://localhost:3000/comida")
      return data;
    },
    async finalizarCadastro(){
      this.dialog = false;
      Axios.post("http://localhost:3000/comida/",this.cadastro)
      this.cadastro = new Produto()           
    },
    excluirProduto(value){
      this.comida.splice(value,1)
    },
  }
}
</script>
