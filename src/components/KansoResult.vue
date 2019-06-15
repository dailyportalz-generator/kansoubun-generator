<template>
  <div class="kanso-result">
    <table width="530" border="0" cellspacing="0" cellpadding="0">
      <tbody>
        <tr>
          <td width="27">
            <img src="@/assets/tb_01.gif" width="27" height="65" border="0">
          </td>
          <td width="354">
            <img src="@/assets/tb_02.gif" width="354" height="65" border="0">
          </td>
          <td width="149">
            <img src="@/assets/tb_03.gif" width="130" height="65" border="0">
          </td>
        </tr>
        <tr>
          <td class="left-bar" rowspan="2">
            <img src="@/assets/dummy.gif" width="26" height="10">
          </td>
          <td rowspan="2" class="kekkatxt bg-line" valign="top">
            <div class="kanso-result__message">
              <template v-for="(results, questionNumber) in resultsList">
                <p v-if="step > questionNumber+1" :key="questionNumber">
                  <template v-for="(result, resultIndex) in results">
                    <span
                      :key="result"
                      v-if="questions[`q${questionNumber+1}`] === resultIndex+1"
                    >{{result}}</span>
                  </template>
                </p>
              </template>
            </div>
          </td>
          <td>
            <img src="@/assets/tb_05.gif" width="128" height="105" border="0">
          </td>
        </tr>
        <tr>
          <td valign="bottom">
            <img src="@/assets/tb_06.gif" width="149" height="288" border="0">
          </td>
        </tr>
        <tr>
          <td valign="top">
            <img src="@/assets/tb_07.gif" width="27" height="53" border="0">
          </td>
          <td valign="top">
            <img src="@/assets/tb_08.gif" width="354" height="53" border="0">
          </td>
          <td>
            <img src="@/assets/tb_09.gif" width="149" height="76" border="0">
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import { stringify } from "querystring";

export default {
  props: {
    questions: Object,
    step: Number
  },
  computed: {
    resultsList() {
      return [
        ["走れメロス", "こころ", "注文の多い料理店", "猿の惑星"],
        [
          "この本はわかいうちに絶対に読んでおいたほうがいい、人生の教訓を含んでいると先輩に言われてこの本を手に取りました。",
          "先日、たまたまこの本が原作の映画をテレビで見て、原作を読んでみたいと思い、図書館で借りてきました。",
          "わたしの好きなロックバンド「イカ釣り漁船」のボーカルのチャッピーがこの本を薦めていたので読む気になりました。",
          "近所のTSUTAYA に行ったらなんか表紙がつるつるしてて触ると気持ちのいい本があったので買ってきました。それがこの本です。"
        ],
        [
          "あっという間に読み終えてしまい、感動して言葉がありませんでした。途中、なんども涙をぬぐいました。",
          "この物語の主人公の気持ちがわかる気がしてました。「うんうん」と心のなかでなんどもうなずきました。",
          "わたしが好きな「ごんぎつね」に比べるとちょっと長いかな、と思いましたがおもしろかったです。",
          "読んでいる途中でなんどもお母さんが「ごはんできたよ」とか「おつかい行ってきて」と言うので読み終えるのに時間がかかりました。"
        ],
        [
          "実はわたしにもこの物語に似た経験があるのです（詳しく書くことは紙面の都合で割愛しますが）。だからそう思ったのかもしれません。",
          "特に、物語前半で主人公が言うセリフが胸に刺さりました。なにげないなかにも優しさと勇気、そしてせつなさと。",
          "わたしの好きな物語に似ているからそう感じのたのだと思います。その物語は「ごんぎつね」です。",
          "よくわかんないんだけど、そう思った気がします。でも、どっちでもいいです。その日の晩ごはんはカレーでした。"
        ]
      ];
    }
  },
  methods: {
    handleClickRestart() {
      location.href = location.href.replace(location.search, "");
    }
  }
};
</script>

<style scoped>
img {
  user-select: none;
}

.kanso-result {
  width: 526px;
  margin: 0 auto;
}

.kanso-result_main {
  font-size: 0;
}

.kanso-result__message {
  padding: 16px;
  padding-top: 5px;
  font-size: 12px;
  flex: 1;
  min-height: 150px;
}

.kanso-result__message p:first-child {
  margin-top: 0;
}

.kanso-result_build {
  text-align: right;
}

.kanso-result_share {
  font-size: 12px;
}

.kanso-result_shareurl {
  width: 100%;
}

.kanso-result_share {
  display: flex;
  align-items: center;
}

input {
  margin: 4px 10px 4px 0;
  flex: 1;
}

.left-bar {
  background: url("../assets/tb_04.gif");
}

.bg-line {
  background: url("../assets/tb_bg.gif");
}

teble{
    border-spacing: 0;
}
</style>