<script setup lang="ts">
import { ref } from "vue";

const password = ref("");
const copyPassword = () => {
  navigator.clipboard.writeText(password.value);
};

const m = Math;

const generateRandomPassword = () => {
  let randomPassword = "";

  const digits = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"],
    letters = [
      "a",
      "b",
      "c",
      "d",
      "e",
      "f",
      "g",
      "h",
      "i",
      "j",
      "k",
      "l",
      "m",
      "n",
      "o",
      "p",
      "q",
      "r",
      "s",
      "t",
      "u",
      "v",
      "w",
      "x",
      "y",
      "z",
    ],
    symbols = [
      " ",
      "!",
      '"',
      "#",
      "$",
      "%",
      "&",
      "'",
      "(",
      ")",
      "*",
      "+",
      ",",
      "-",
      ".",
      "/",
      ":",
      ";",
      "<",
      "=",
      ">",
      "?",
      "@",
      "\\",
      "^",
      "_",
      "\`",
      "{",
      "}",
      "|",
      "~",
    ];

  for (let i = 0; i < 32; i++) {
    // Random Digit variable
    let randomDigit = digits[m.abs(m.round(m.random() * digits.length - 1))];

    // Random Letter variable
    let randomLetter = letters[m.abs(m.round(m.random() * letters.length - 1))];

    // Capital Letter or not
    m.round(m.random()) > 0
      ? (randomLetter = randomLetter.toUpperCase())
      : (randomLetter = randomLetter.toLowerCase());

    // Random Symbol variable
    let randomSymbols =
      symbols[m.abs(m.round(m.random() * symbols.length - 1))];

    // Random Password Combination variable
    const random = [randomDigit, randomLetter, randomSymbols];

    // Random Password generator
    randomPassword += random[m.abs(m.round(m.random() * random.length - 1))];
  }
  password.value = randomPassword;
  console.log(randomPassword);
};
</script>

<template>
  <div class="container">
    <div class="display">
      <input type="text" class="password-input" v-model="password" />
      <button class="btn copy-btn">
        <img src="@/assets/images/copy.png" alt="" @click="copyPassword" />
      </button>
    </div>
    <button class="btn generator-btn" @click="generateRandomPassword">
      <img src="@/assets/images/generate.png" alt="" />
      <p>Generate password :D</p>
    </button>
  </div>
</template>

<style scoped>
.display {
  background-color: var(--white);
  width: 100%;
  display: flex;
}

.password-input {
  width: 85%;
  height: 2.5rem;
  background-color: var(--white);
  border-color: transparent;

  &:focus {
    outline: none;
  }
}

.btn {
  border-radius: 2px;
  border-color: transparent;
  cursor: pointer;
}

.copy-btn {
  display: flex;
  place-items: center;
  width: 15%;
  height: 2.5rem;
  background-color: var(--white);
}

.copy-btn img {
  width: clamp(25px, 100%, 30px);
  margin: 0 auto;
  filter: hue-rotate(30deg);
}

.generator-btn {
  display: flex;
  place-items: center;
  margin-top: 5px;
  width: 100%;
  height: 2.5rem;
  background-color: var(--aqua-blue);
}

.generator-btn p {
  width: 80%;
}

.generator-btn img {
  width: 10%;
  max-width: 24px;
  max-height: 35px;
  height: auto;
  margin: 0 auto;
}

@media (min-width: 448px) {
  .password-input {
    width: 80%;
  }

  .generator-btn p {
    width: 100%;
  }

  .generator-btn img {
    width: 10%;
  }

  .container {
    width: 80%;
    margin: auto;
  }
}

@media (min-width: 648px) {
  .container {
    width: 60%;
    margin: auto;
  }
}
</style>
