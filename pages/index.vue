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
    <div v-for="i in 4" :key="i">
      <v-btn-toggle v-model="toggle_one">
        <v-btn>아아 x 10 </v-btn>
        <v-btn> X </v-btn>
      </v-btn-toggle>
    </div>
  </div>
</template>

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
