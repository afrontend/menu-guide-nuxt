<template>
  <div>
    <div>
      <v-row>
        <v-col cols="8" sm="6" md="3">
          <v-text-field label="Menu Name" />
        </v-col>
        <v-col cols="4" sm="6" md="3">
          <v-btn>이거요</v-btn>
        </v-col>
      </v-row>
    </div>
    <div v-for="(i, index) in menuList" :key="index">
      <v-btn-toggle>
        <v-btn @click="increment(i.name)"> + </v-btn>
        <v-btn>{{ i.name }} x {{ i.count }} </v-btn>
        <v-btn @click="decrement(i.name)"> - </v-btn>
      </v-btn-toggle>
    </div>
    <a :href="url">{{ url }}</a>
  </div>
</template>

<script>
export default {
  data() {
    return {
      menuList: this.getMenus()
    }
  },
  computed: {
    url() {
      const { origin, pathname } = window.location
      return origin + pathname + this.getUrlParameter()
    }
  },
  methods: {
    getUrlParameter() {
      return '?menus=' + this.menuList.map(m => m.name).join(',')
    },
    increment(menuName) {
      this.menuList = this.menuList.map(m => {
        if (m.name === menuName) {
          m.count = m.count + 1
        }
        return m
      })
    },
    decrement(menuName) {
      this.menuList = this.menuList.map(m => {
        if (m.name === menuName) {
          m.count = m.count - 1
        }
        return m
      })
    },
    getMenus() {
      const { query } = this.$route
      if (query && query.menus) {
        const menuList = query.menus.split(',')
        return menuList.map(menu => ({
          name: decodeURIComponent(menu),
          count: 0
        }))
      }
      return [
        { name: '아아', count: 0 },
        { name: '아라', count: 0 },
        { name: '따아', count: 0 },
        { name: '따라', count: 0 }
      ]
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
