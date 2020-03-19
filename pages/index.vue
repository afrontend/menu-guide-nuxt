<template>
  <div class="container">
    <v-row>
      <v-col cols="8" sm="6" md="3">
        <v-text-field
          v-model="menuName"
          label="Menu Name"
          @keypress="keypress"
        />
      </v-col>
      <v-col cols="4" sm="6" md="3">
        <v-btn @click="addMenu">이거요</v-btn>
      </v-col>
    </v-row>
    <div v-for="(i, index) in filteredMenuList" :key="index">
      <v-btn-toggle>
        <v-btn @click="increment(i.name)"> + </v-btn>
        <v-btn>{{ i.name }} ({{ i.count }}) </v-btn>
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
      menuName: '',
      filteredMenuList: this.getMenus(),
      menuList: this.getMenus()
    }
  },
  computed: {
    url() {
      const { origin, pathname } = window.location
      return origin + pathname + this.getUrlParameter()
    }
  },
  watch: {
    menuName() {
      this.filteredMenuList = this.menuList.filter(m =>
        m.name.includes(this.menuName)
      )
    }
  },
  methods: {
    keypress(e) {
      if (e.key === 'Enter') {
        this.addMenu()
      }
    },
    addMenu() {
      if (this.menuName) {
        this.menuList.push({
          name: this.menuName.trim(),
          count: 1
        })
        this.menuName = ''
        this.filteredMenuList = this.menuList
      }
    },
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
      this.menuList = this.menuList.filter(m => m.count !== -1)
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
}
</style>
