<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <ul>
      <li v-for="(ad, index) in ads" :key="index">
<!--        <h2> {{ad.title}} </h2>-->
        <a :href="`${ad.url}`" target="_blank">{{ad.title}}</a>
        <p> {{ ad.description }}</p>
        <img :src="`${ad.images[0]}`"/>
<!--        {{ad}}-->

      </li>
    </ul>


  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      ads: []
    }
  },
  methods : {
    setAdList(){

    }
  },
  async mounted(){
    await axios
        .get('https://kijiji-notifier-api.herokuapp.com/ads')
        .then(response => {
            this.ads = response.data.reverse();
        });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 10px 10px;
  padding-bottom: 80px;
}
a {
  color: #42b983;
}
</style>
