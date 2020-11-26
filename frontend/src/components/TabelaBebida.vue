<template>
  <v-container>
    <v-simple-table dark>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-center">Produto</th>
            <th class="text-center">Descrição</th>
            <th class="text-center">Preço</th>
            <th class="text-center">Peso</th>
            <th class="text-center">Data</th>
          </tr>
        </thead>
        <tbody class="text-center">
          <tr v-for="item in bebida" :key="item.id">
            <td>{{ item.produto }}</td>
            <td>{{ item.descricao }}</td>
            <td>{{ item.preco }}</td>
            <td>{{ item.peso }}</td>
            <td>{{ item.entrada | formatDate }}</td>
            <td>
              <v-btn color="red" @click="excluirProduto(item.id)">X</v-btn>
            </td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </v-container>
</template>

<script>
import Axios from "axios";

export default {
  props: ["bebida"],
  methods: {
    excluirProduto(value) {
      Axios.delete("http://localhost:3000/bebida/" + value);
      this.$emit("delet", value);
    },
  },
};
</script>

<style>
</style>