<template>
  <div id="special_sponsors">
    <h4>special sponsors</h4>
    <div class="special-sponsor-block" v-for="(patriot, index) in patriots" :key="index">
      <a :href="patriot.url" target="_blank">
        <div class="special-sponsor-image"><img :src="patriot.logo" :alt="patriot.name"></div>
      </a>
    </div>
    <div class="special-sponsor-footer">
      <a href="https://lando.dev/sponsor/" target="_blank">become a sponsor</a>
    </div>
  </div>
</template>


<script>
export default {
  props: {
    hideHeader: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      patriots: [],
    };
  },
  mounted() {
    this.$api().get('/v1/sponsors/patriot').then(response => {
      this.patriots = response.data || [];
    })
    .catch(error => {
      console.error(error);
    });
  },
};
</script>

<style lang="stylus">
#special_sponsors
  border 1px #ccc dashed
  padding 3em
  position absolute
  right 2em
  top 6em
  width 150px
  background white
  opacity .75
  text-align center
  font-size .8em
  .special-sponsor-block
    img
      width 150px

@media (max-width: 1300px)
  #special_sponsors
    display none
</style>
