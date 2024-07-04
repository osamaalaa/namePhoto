<template>
  <v-app>
    <v-main>
      <v-container class="fill-height">
        <v-row align="center" justify="center">
          <v-col cols="12" md="6" lg="4">
            <NamePhoto 
              name="Osama Alaaeldin" 
              :phone="'071522200730'" 
           
              :email="'osamaalaa133@gmail.com'" 
              gender="female"
              address="12 Almushrif, Abu Dhabi, UAE"
            />
          </v-col>
        </v-row>
      </v-container> 
    </v-main>
  </v-app>
</template>

<script>
import NamePhoto from '@/components/NamePhoto.vue';

export default {
  name: 'App',
  components: {
    NamePhoto
  }
};
</script>
