<template>
  <div>
<!--    <h2>IT'S THE FUCKING WAY TO START THE FIRE</h2>-->
    <component :is="life" />
    <!--    <button @click="sonChange" />-->
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

import birth from './birth/index'
import death from './death/index'
export default {
  name: 'Index',
  components: {
    birth, death
  },
  data() {
    return {
      life: 'birth',
      clickCheck: false
    }
  },
  computed: {
    ...mapGetters([
      'roles'
    ])
  },
  mounted() {
    if (this.roles.includes('admin')) {
      this.life = 'birth'
    } else {
      this.life = 'death'
    }
    // console.log(this.roles)
  },
  methods: {
    // sonChange() {
    //   this.roles = !this.roles
    //   this.roles = 'a'
    //   if (!this.clickCheck) {
    //     this.roles = 'birth'
    //   }
    // }
  }
}
</script>

<style scoped>

</style>
