<template>
  <q-page>
    <q-list>
      <q-expansion-item
        expand-separator
        v-for="question in preguntas"
        :key="question.id"
        :label="question.pregunta"
      >
        <q-card>
          <q-card-section>
            <q-option-group
              :options="question.opciones"
              :true-value="question.opciones.value"
              :model-value="modelValue"
              v-model="answersModel[question.id]"
              @update:model-value="
                (newStore) => {
                  updateOptions(
                    newStore,
                    question.id,
                    question.respuesta,
                    question.tipo,
                    question.pregunta
                  );
                }
              "
            />
          </q-card-section>
        </q-card>
      </q-expansion-item>
    </q-list>
  </q-page>
  <q-btn @click="submit">Aceptar</q-btn>
</template>

<script>
import json from "../../public/questions1.json";

export default {
  data() {
    return {
      answers: [],
      answersModel: [],
      modelValue: "",
      vmo: "",
      qu: json,
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
      validacion: [
        {
          pregunta: 1,
          respuesta: 1,
        },
        {
          pregunta: 2,
          respuesta: 2,
        },
        {
          pregunta: 3,
          respuesta: 3,
        },
      ],
    };
  },
  methods: {
    submit() {
      let validResponses = this.answers.filter((ans) => ans.isCorrect == true);
      console.log("validResponses: " + validResponses.length);
      let invalidResponses = this.answers.filter(
        (ans) => ans.isCorrect == false
      );
      let inv = invalidResponses.map((q) => {
        q.tipo, q.pregunta;
      });
      console.log("nuevo mapa: " + inv);
      console.log("invalidResponses: " + JSON.stringify(invalidResponses));
      console.log("invalidResponses length: " + invalidResponses.length);
      let subjects = Map.groupBy(invalidResponses, (grupo) => {
        return grupo.tipo;
      });
      let sub = Array.from(subjects);
      console.log("sub: " + sub);
      console.log("sub json: " + JSON.stringify(sub));
      let total = this.preguntas.length;
      let grade = (validResponses.length / total) * 100;
      console.log("total: " + total);
      console.log("grade: " + grade);
      console.log("subjects: " + subjects);
      alert(grade);
    },
    updateOptions(value, key, response, tipo, pregunta) {
      console.log("value: " + value);
      console.log("key: " + key);
      console.log("modelValue: " + this.modelValue);
      let answer = {
        quesion: key,
        option: value,
        pregunta: pregunta,
        isCorrect: response == value ? true : false,
        tipo: tipo,
      };
      if (this.answers != null && this.answers != undefined) {
        console.log("answers not null");
        let result = this.answers.find((obj) => {
          console.log("obj: " + JSON.stringify(obj));
          console.log("obj question: " + obj.quesion);
          return obj.quesion === key;
        });
        console.log("result: " + JSON.stringify(result));
        if (result != undefined) {
          console.log("result not null");
          this.answers.pop(result);
        }
      }
      this.answers.push(answer);
      console.log("answers: " + JSON.stringify(this.answers));
    },
  },
};
</script>

<style></style>
