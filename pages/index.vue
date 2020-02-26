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
    <div v-for="(i, index) in getMenus()" :key="index">
      <v-btn-toggle>
        <v-btn>{{ i.name }} x 10 </v-btn>
        <v-btn> X </v-btn>
      </v-btn-toggle>
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    window.console.log('apple')
  },
  methods: {
    getMenus() {
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
