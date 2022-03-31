<template>
  <section>
    <base-card>
      <h2>{{ fullName }}</h2>
      <h3>${{ rate }}/hour</h3>
    </base-card>
  </section>
  <section>
    <base-card>
      <header>
        <h2>Interestd? Reach out now!</h2>
        <base-button link :to="contactLink">Contact</base-button>
      </header>
      <router-view></router-view>
    </base-card>
  </section>
  <section>
    <base-card>
      <base-badge
        v-for="area in areas"
        :key="area"
        :type="area"
        :title="area"
      ></base-badge>
    </base-card>
  </section>
</template>
<script>
export default {
  props: ["id"],
  data(){
    return {
      selectedCoach: null // lay tu tren url , config tai router (xem router.js)
    };
  },
  computed:{
    fullName(){
      return this.selectedCoach.firstName + " " + this.selectedCoach.lastName
    },
    rate(){
      return this.selectedCoach.hourlyRate;
    },
    areas(){
      return this.selectedCoach.areas
    },
    // contactLink(){
    //   return this.$router.component 
    // }
  },
  // mounted(){
  //   console.log(this.$router.hasRoute);
  // },
  created() {
    this.selectedCoach = this.$store.getters['coaches/coaches'].find(
      (coach) => coach.id === this.id
    )
  },  
};
</script>
