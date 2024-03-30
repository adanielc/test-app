<template>
  {{ answers }}
  <q-page class="flex flex-center">
    <q-list>
      <q-expansion-item
        expand-separator
        v-for="(question, key) in preguntas"
        :key="question.id"
        :label="question.pregunta"
      >
        <q-card>
          <q-card-section>
            <q-option-group
              :options="question.opciones"
              :true-value="question.opciones.value"
              v-model="answers[question.opciones.value]"
            />
          </q-card-section>
        </q-card>
      </q-expansion-item>
    </q-list>
  </q-page>
  <q-btn @click="submit">Aceptar</q-btn>
</template>

<script>
export default {
  data() {
    return {
      answers: [],
      preguntas: [
        {
          id: 1,
          pregunta: "Cuantos command points se pueden pagar por fase",
          respuesta: 1,
          opciones: [
            {
              value: 1,
              label: "Todos los que quieras",
            },
            {
              value: 2,
              label: "De un solo tipo",
            },
            {
              value: 3,
              label: "No se puede repetir",
            },
          ],
          tipo: "combate",
          tema: "",
        },
        {
          id: 2,
          pregunta: "Cuantas pulgadas para fuego defensivo ",
          respuesta: 2,
          opciones: [
            {
              value: 1,
              label: "3",
            },
            {
              value: 2,
              label: "6",
            },
            {
              value: 3,
              label: "12",
            },
          ],
          tipo: "disparo",
          tema: "",
        },
        {
          id: 3,
          pregunta: "A cuanto tiene que estar una carga",
          respuesta: 3,
          opciones: [
            {
              value: 1,
              label: "18",
            },
            {
              value: 2,
              label: "24",
            },
            {
              value: 3,
              label: "12",
            },
          ],
          tipo: "cargas",
          tema: "",
        },
      ],
    };
  },
  methods: {
    submit() {
      alert("Submit");
    },
  },
};
</script>

<style></style>
