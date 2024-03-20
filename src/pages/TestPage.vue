<template>
  <q-page class="flex flex-center">
    <q-list>
      <q-expansion-panel>
        <q-card>
          <q-card-section> {{ pepe }} </q-card-section>
        </q-card>
      </q-expansion-panel>
    </q-list>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      pepe: "texto de pepe",
    };
  },
};
</script>

<style>
</style>