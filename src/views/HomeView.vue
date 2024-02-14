<template >
 <v-card flat>
  

    <v-divider></v-divider>
    <v-data-table v-model="selected" :items="items" show-select return-object>
      <template v-slot:[`header.stock`]>
        <div class="text-end">Stock</div>
      </template>

      <template v-slot:[`item.image`]="{ item }">
        <v-card class="my-2" elevation="2" rounded>
          <v-img
            :src="`${item.image}`"
            height="64"
            cover
          ></v-img>
        </v-card>
      </template>

      <template v-slot:[`item.rating`]="{ item }">
        <v-rating
          :model-value="item.rating.rate"
          color="orange-darken-2"
          density="compact"
          size="small"
          readonly
        ></v-rating>
      </template>
      <template v-slot:[`item.stock`]="{ item }">
        <div class="text-end">
          <v-chip :color="item.stock ? 'green' : 'red'" :text="item.stock ? 'In stock (' +item.stock+ ')' : 'Out of stock'"
            class="text-uppercase" label size="small"></v-chip>
        </div>
      </template>

    </v-data-table>
  </v-card>
  <v-col cols="auto">
        <v-btn size="large" @click="cart">Aggiungi Al Carrello</v-btn>
      </v-col>
</template>

<script>

export default {
  name: 'HomeView',
  data() {
    return {
      items: [],
      selected: []
    }
  },
  methods: {
    getProdotti() {
      if(localStorage.getItem("items")==null){
      fetch('https://fakestoreapi.com/products')
        .then((res) => res.json())
        .then((json) => {
          
          for(let i=0;i<json.length;i++){
          json[i].stock=Math.floor(Math.random() * 100);
          }
          this.items = json
          localStorage.setItem("items",JSON.stringify(this.items))
        })
      }
      else{
        this.items = JSON.parse(localStorage.getItem("items"))
      }
    },
    cart() {
      localStorage.setItem("selected",JSON.stringify(this.selected))
    }
  },
  mounted() {
    this.getProdotti();
    
  }
}
</script>
