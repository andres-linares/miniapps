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

    <div class="notification" ref="notification">
      {{ resultStatus === "good" ? "Great!" : "Almost!" }}
    </div>
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
      resultStatus: null,
      notificationTimeout: null
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
      if (this.userResult === '') return;

      if (this.notificationTimeout) clearTimeout(this.notificationTimeout);
      this.$refs.notification.classList.remove('good', 'bad', 'disappear');

      if (this.userResult === this.result) {
        this.level++;
        this.generateOperation();
        this.userResult = "";

        this.resultStatus = "good";
      } else {
        this.level = this.level - 2 <= 1 ? 1 : this.level - 2;
        this.generateOperation();
        this.userResult = "";

        this.resultStatus = "bad";
      }

      this.$refs.notification.classList.add(this.resultStatus);
      this.$refs.notification.classList.add("disappear");
      this.notificationTimeout = setTimeout(() => {
        this.$refs.notification.classList.remove("disappear");
      }, 1500);
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
  font-family: "Roboto Mono", monospace;
}

.operation .operation-content {
  display: flex;
  justify-content: space-between;
}

.notification {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  font-size: clamp(1.5rem, 2vw, 2.5rem);
  text-align: center;
  padding: 0.5em 0;
  transform: translateY(100%);
  opacity: 0;
}

.notification.disappear {
  transform: translateY(0);
  opacity: 1;
  animation: disappear 1.5s ease-in forwards;
}

@keyframes disappear {
  to {
    transform: translateY(100%);
    opacity: 0;
  }
}

.notification.good {
  background: var(--color-primary);
}

.notification.bad {
  background: #f64949;
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
