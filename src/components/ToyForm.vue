<template>
   <div class="text-center">
    <v-dialog
      :value="showForm"
      width="500"
      persistent
    >
      <v-card>
        <v-card-title
          class="headline grey lighten-2"
          primary-title>
          {{ !!currentToy.id ? 'Actualizar juguete' : 'Nuevo juguete'}}
        </v-card-title>

        <v-container class="px-8 py-8">
            <v-text-field label="Codigo" type="text" :value="currentToy.data.code" @input="updateCode"/>
            <v-text-field label="Nombre" type="text" :value="currentToy.data.name" @input="updateName"/>
            <v-text-field label="Precio" prefix="$" :value="currentToy.data.price" @input="updatePrice"/>
            <v-text-field label="Stock" suffix="unidades" :value="currentToy.data.stock" @input="updateStock"/>
        </v-container>

        <v-divider></v-divider>

        <v-card-actions class="px-8 py-5">
          <v-btn
            color="primary"
            @click="cancelForm">
            cancelar
          </v-btn>
          <v-spacer></v-spacer>
          <v-btn
            color="success"
            @click="submitForm">{{ !!currentToy.id ? 'Actualizar' : 'Crear'}}
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'
export default {
    methods: {
        ...mapActions(['hideToyForm', 'updateCode', 'updateName', 'updatePrice', 'updateStock','postToy', 'updateToy', 'cancelForm']),

        submitForm(){
          if (this.currentToy.id) {
            this.updateToy(this.currentToy.id)
          }else{
            this.postToy()
          }
          this.hideToyForm()
        },
    },
    computed: {
        ...mapState(['showForm', 'currentToy'])
    },
}
</script>

<style>

</style>