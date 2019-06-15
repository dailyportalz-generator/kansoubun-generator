<template>
  <div id="app">
    <template>
      <span v-if="step < 5">
        <b>step{{step}}</b>
      </span>

      <SelectQuestion
        key="question1"
        v-if="step === 1"
        v-model="questions.q1"
        @next="handleNext"
        :message="messageList[0]"
        :choices="choicesList[0]"
      />

      <SelectQuestion
        key="question2"
        v-if="step === 2"
        v-model="questions.q2"
        @next="handleNext"
        :message="messageList[1]"
        :choices="choicesList[1]"
      />

      <SelectQuestion
        key="question3"
        v-if="step === 3"
        v-model="questions.q3"
        @next="handleNext"
        :message="messageList[2]"
        :choices="choicesList[2]"
      />

      <SelectQuestion
        key="question4"
        v-if="step === 4"
        v-model="questions.q4"
        @next="handleNext"
        :message="messageList[3]"
        :choices="choicesList[3]"
      />
    </template>

    <KansoResult :step="step" :questions="questions"/>
  </div>
</template>

<script>
import SelectQuestion from "./components/SelectQuestion.vue";
import KansoResult from "./components/KansoResult.vue";
import { parse } from "querystring";

export default {
  name: "app",
  data() {
    return {
      step: 1,
      questions: {
        q1: 1,
        q2: 1,
        q3: 1,
        q4: 1
      }
    };
  },
  components: {
    SelectQuestion,
    KansoResult
  },
  mounted() {
    const params = parse(location.search.replace("?", ""));
    const isValid = ["q1", "q2", "q3", "q4"].every(val => {
      if (!params[val]) {
        return false;
      }
      if (parseInt(params[val]) < 1) {
        return false;
      }
      return true;
    });
    if (isValid) {
      const questions = {
        q1: parseInt(params.q1),
        q2: parseInt(params.q2),
        q3: parseInt(params.q3),
        q4: parseInt(params.q4)
      };
      this.questions = questions;
      this.step = 5;
    }
  },
  methods: {
    handleNext() {
      this.step++;
    }
  },
  computed: {
    messageList() {
      return [
        "まず、課題作品をきめよう",
        "なぜこの本を選んだか",
        "読み終えてのとりあえずの感想",
        "何でそう思ったんだろう"
      ];
    },
    choicesList() {
      return [
        ["走れメロス", "こころ", "注文の多い料理店", "猿の惑星"],
        [
          "うそくさいほどまじめに",
          "今の若者のように",
          "アイドルっぽく",
          "バカっぽく"
        ],
        [
          "優等生的に",
          "わかった気がして",
          "読んでないのでごまかして",
          "やっぱりバカっぽく"
        ],
        [
          "すごいこと告白してみる",
          "ありがちに",
          "知ってる話にずらしてしまう",
          "ひらきなおって"
        ]
      ];
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 640px;
  font-size: 12px;
  padding: 0 50px;
}

img {
  vertical-align: bottom;
}
</style>
