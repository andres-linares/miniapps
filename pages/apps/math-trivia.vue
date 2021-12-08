<template>
  <div class="operation">
    <div class="number number-1">{{ number1 }}</div>

    <div class="operation-content">
      <div class="operator">
        {{ operatorSymbol }}
      </div>
      <div class="number number-2">{{ number2 }}</div>
    </div>

    <form @submit.prevent="checkResult">
      <input
        class="result"
        type="number"
        v-model.number="userResult"
        style="text-align: end"
        @blur="checkResult"
      />
    </form>
  </div>
</template>

<script>
export default {
  name: "MathTrivia",
  data() {
    return {
      number1: null,
      number2: null,
      operator: null,
      result: null,
      userResult: "",
      level: 1,
    };
  },
  computed: {
    operatorSymbol() {
      if (this.operator === "+") return "+";
      if (this.operator === "-") return "-";
      if (this.operator === "*") return "×";
      if (this.operator === "/") return "÷";
    },
  },
  created() {
    this.$store.commit("setTitle", this.$metaInfo.title);
    this.generateOperation();
  },
  methods: {
    checkResult() {
      if (this.userResult === this.result) {
        this.level++;
        this.generateOperation();
        this.userResult = "";
      }
    },
    generateOperator() {
      const operators = {
        0: "+",
        1: "-",
        2: "*",
        3: "/",
      };

      const random = Math.round(Math.random() * 3);
      return operators[random];
    },
    randomNumberUpTo(max) {
      const random = Math.round(Math.random() * (max - 1) + 1);

      return random;
    },
    generateOperation() {
      this.operator = this.generateOperator();

      if (this.operator === "+") {
        this.number1 = this.randomNumberUpTo(this.level * 5);
        this.number2 = this.randomNumberUpTo(this.level * 5);

        this.result = this.number1 + this.number2;
      } else if (this.operator === "-") {
        const number1 = this.randomNumberUpTo(this.level * 5);
        const number2 = this.randomNumberUpTo(this.level * 5);

        [this.number1, this.number2] =
          number1 >= number2 ? [number1, number2] : [number2, number1];

        this.result = this.number1 - this.number2;
      } else if (this.operator === "*") {
        this.number1 = this.randomNumberUpTo(this.level) + 1;
        this.number2 = this.randomNumberUpTo(this.level) + 1;

        this.result = this.number1 * this.number2;
      } else if (this.operator === "/") {
        this.result = this.randomNumberUpTo(this.level * 1.5);

        this.number2 = this.randomNumberUpTo(this.level * 2);
        this.number1 = this.result * this.number2;
      }
    },
  },
  head() {
    return {
      title: "Math Trivia",
    };
  },
};
</script>

<style scoped>
.operation {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  margin: 0 auto;
  font-size: clamp(3rem, 6vw, 5rem);
  max-width: 4em;
  height: 100%;
  justify-content: center;
  font-family: 'Roboto Mono', monospace;
}

.operation .operation-content {
  display: flex;
  justify-content: space-between;
}

form,
input {
  width: 100%;
  box-sizing: border-box;
}

input {
  border: none;
  border-top: 0.5vh solid #aaa;
  background: #fafafa;
  margin-bottom: 10vh;
}
</style>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@400&display=swap");
</style>
