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
           <v-btn size="large" @click="buy">Buy</v-btn>
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
        this.items = JSON.parse(localStorage.getItem("selected"))
       },
       buy() {
        localStorage.removeItem("selected")
       }
     },
     mounted() {
       this.getProdotti();
       
     }
   }
   </script>
   