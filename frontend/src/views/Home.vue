<template>
  <v-app>
    <v-app-bar app dark>
      <h1>Estoque</h1>
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
              <v-text-field label="Preço:"  type="number" v-model="cadastro.preco" ></v-text-field>
              <v-text-field label="Peso:"  type="number" v-model="cadastro.peso" ></v-text-field>
              <v-text-field label="Entrada:"  type="date" v-model="cadastro.entrada" ></v-text-field>
              <v-select  v-model="select" :items="items" :rules="[v => !!v || 'Item is required']" label="Item" required></v-select>
            </v-card-text>
            <v-divider></v-divider>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn dark @click="finalizarCadastro(select)" color="blue" > FINALIZAR </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </div> 
      <div class="d-sm-flex flex-comlumn">
        <v-container>
          <h1 class="ml-3">Comida</h1>
          <TabelaComida :comida="comida" @delet="excluirProduto(value)" />
        </v-container>
        <v-spacer></v-spacer>
        <v-container>
           <h1 class="ml-3">Bebida</h1>
          <TabelaBebida :bebida="bebida"  @delet="excluirProduto(value)" />
        </v-container>
      </div>
    </v-main>
  </v-app>
</template>
<script>

import Axios from "axios"
import TabelaComida from "@/components/TabelaComida"
import TabelaBebida from "@/components/TabelaBebida"
import Produto from "@/models/Produto.js"

export default {
  components: {    
    TabelaComida,
    TabelaBebida
  },
  async created(){    
    try{
      this.comida = await this.getTabela("comida")
      this.bebida = await this.getTabela("bebida")
    }catch(error){
      console.log(error)
    }    
  },
  async updated(){
    //this.comida = await this.getTabela("comida");
    //this.bebida = await this.getTabela("bebida");
  },
  data(){    
      return({
        dialog:false,
        cadastro: new Produto(),
        bebida:[],
        comida:[],
        select:null,
        items:[
          "Comida",
          "Bebida"
        ]
      })   
  },
  methods:{
    async getTabela(option){        
      const { data } = await Axios.get("http://localhost:3000/"+ option).catch( ( err)=>{ console.log(err)} )
      return data;
    },
    async finalizarCadastro(option){
      this.dialog = false;
      Axios.post("http://localhost:3000/"+ option +"/",this.cadastro)
      this.$forceUpdate()
      this.cadastro = new Produto()           
    },
    excluirProduto(value){
      if(this.select == "Comida"){
        this.comida.splice(value,1)
      }
        this.bebida.splice(value,1)
    },
  }
}
</script>
