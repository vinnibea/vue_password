
<template>
  <div class='wrapper'> 
    <input class='input' v-model="text" type="password" placeholder="Type your password" />
    <div
      :class="{
        'password': true,
        'password-short': isPasswordShort,
        'password-weak': isPasswordWeak,
        'password-medium': isPasswordMedium,
        'password-strong': isPasswordStrong,
      }"
    >
      {{ text }}
    </div>
  
    <div
      :class="{
        'password': true,
        'password-short': isPasswordShort,
        'password-medium': isPasswordMedium,
        'password-strong': isPasswordStrong,
      }"
    ></div>
  
    <div
      :class="{
        'password': true,
        'password-short': isPasswordShort,
        'password-strong': isPasswordStrong,
      }"
    ></div>
  </div>
  </template>  

<script>
export default {
  name: 'App',

  data() {
    return {
      text: "",
    };
  },

  computed: {
    isPasswordShort() {
      return this.text.length < 8 && this.text.length > 0;
    },

    isPasswordWeak() {
      let reg = /^\d+$/gi;
      let regLetters = /^[a-zA-Z]+$/gi;
      let regSymbols = /^[?*=.@#$%!^":,/;<'>+\-_]+$/gi;
      const weakPasswordRegx = [reg, regLetters, regSymbols];

      return weakPasswordRegx.some((reg) => this.text.match(reg));
    },

    isPasswordMedium() {
      const letterAndNumber = /^(?=.*?[a-z])(?=.*?[0-9]).{8,}$/;
      const letterAndSymbol = /^(?=.*?[a-z])(?=.*?[#?!@$%^&*-]).{8,}$/;
      const symbolAndNumber = /^(?=.*?[0-9])(?=.*?[#?!@$%^&*-]).{8,}$/;

      return [letterAndNumber, symbolAndNumber, letterAndSymbol].some(
        (regExp) => regExp.test(this.text.toLowerCase())
      );
    },

    isPasswordStrong() {
      const strongRegExp = /^(?=.*?[a-z])(?=.*?[0-9])(?=.*?[#?!@$%^&*-]).{8,}$/;
      return strongRegExp.test(this.text.toLowerCase());
    },
  },
};
</script>


<style>
.wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 0 400px;
  min-width: 300px;
}
.password {
  padding: 5px;
  margin-top: 20px;
  height: 50px;
  border-radius: 5px;
  background-color: grey;
  box-shadow: 2px 2px 2px grey;
}

.password-short {
  background-color: rgb(165, 70, 70);
}
.password-weak {
  background-color: rgb(165, 70, 70);
}
.password-medium {
  background-color: yellow;
}
.password-strong {
  background-color: green;
}

.input {
  border: none;
  outline: none;
  background-color: beige;
  padding: 5px;
  border-radius: 3px;
}
</style>
