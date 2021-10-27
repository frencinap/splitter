<template>
  <div>
    <h3 class="title">
      SPLI <br />
      TTER
    </h3>
    <div class="tips">
      <div class="tips__left">
        <section class="left__input">
          <p class="input__title">Cuenta</p>
          <input type="number" class="input__input" v-model.number="bill" />
        </section>
        <section class="left__buttons">
          <p class="buttons__title">Elija Propina %</p>
          <section class="buttons__display">
            <button class="display__button" @click="fivePercent">5%</button>
            <button class="display__button" @click="tenPercent">10%</button>
            <button class="display__button" @click="fifteenPercent">15%</button>
            <button class="display__button" @click="twentyfivePercent">
              25%
            </button>
            <button class="display__button" @click="fiftyPercent">50%</button>
            <input
              type="number"
              class="display__input"
              placeholder="Otra"
              v-model.number="custom"
            />
          </section>
        </section>
        <section class="left__people">
          <section class="people__info">
            <p class="people__title">Personas</p>
            <p v-show="cero" class="people__alert">No puede ser 0!</p>
          </section>
          <input type="number" class="people__input" v-model.number="people" />
        </section>
      </div>
      <div class="tips__right">
        <section class="right__top">
          <div>
            <section class="top__info">
              <p>Propina<br /><span class="info__subtitle">/ persona</span></p>
              <h2 v-if="integer">{{ perPerson.toFixed() }}</h2>
            </section>
            <section class="top__info">
              <p>Total<br /><span class="info__subtitle">/ persona</span></p>
              <h2>{{ total.toFixed() }}</h2>
            </section>
          </div>
        </section>
        <section class="right__reset">
          <button class="reset__button" @click="reset">RESET</button>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Tips",
  data() {
    return {
      bill: null,
      tip: null,
      custom: null,
      people: null,
    };
  },
  methods: {
    fivePercent() {
      this.tip = 0.05;
    },
    tenPercent() {
      this.tip = 0.1;
    },
    fifteenPercent() {
      this.tip = 0.15;
    },
    twentyfivePercent() {
      this.tip = 0.25;
    },
    fiftyPercent() {
      this.tip = 0.5;
    },
    customPercent() {
      this.tip = this.custom;
    },
    reset() {
      (this.bill = null),
        (this.tip = null),
        (this.custom = null),
        (this.people = null);
    },
  },
  computed: {
    total() {
      if (this.tip === null && this.custom != null) {
        return this.bill * (this.custom / 100);
      } else {
        return this.bill * this.tip;
      }
    },
    perPerson() {
      return this.total / this.people;
    },
    integer() {
      return Number.isFinite(this.perPerson);
    },
    cero() {
      if (this.people === 0) {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>

<style>
.title {
  color: hsl(184, 14%, 15%);
  letter-spacing: 0.4rem;
}
.tips {
  background-color: white;
  border-radius: 5px;
  display: flex;
  flex-flow: column;
  justify-items: center;
  padding: 1rem;
  width: 90%;
}
.tips__left {
  width: auto;
  text-align: left;
  padding: 0.1rem 2rem;
  display: flex;
  flex-flow: column;
}
.tips__left p {
  font-size: 0.8rem;
  font-weight: 700;
  color: hsl(183, 100%, 15%);
}
.input__input {
  width: 100%;
  margin: 0;
  background-image: url("../assets/images/icon-dollar.svg");
  background-position-x: 5%;
  background-repeat: no-repeat;
  background-position-y: center;
  background-size: 4%;
  text-align: right;
  border-radius: 3px;
  padding-right: 1rem;
  color: hsl(183, 100%, 15%);
  font-weight: 700;
  border: none;
  background-color: hsl(189, 41%, 97%);
}
.input__input:hover {
  border: 2px solid hsl(172, 67%, 45%);
  cursor: pointer;
}
.input__input:target {
  border: 2px solid hsl(172, 67%, 45%);
  cursor: pointer;
}
.display__button {
  background-color: hsl(183, 100%, 15%);
  color: white;
  border: none;
  border-radius: 2px;
  width: 3.5rem;
  height: 1.5rem;
  margin: 0.2rem;
  font-weight: 700;
  transition-duration: 0.2s;
}
.display__button:hover {
  color: hsl(183, 100%, 15%);
  background-color: hsl(172, 67%, 45%);
  cursor: pointer;
}
.display__input {
  width: 3.5rem;
  border: none;
  background-color: hsl(189, 41%, 97%);
  text-align: right;
  color: hsl(183, 100%, 15%);
}
.display__input::placeholder {
  text-align: center;
  color: hsl(183, 100%, 15%);
  font-weight: 700;
}
.people__input {
  width: 100%;
  margin: 0;
  background-image: url("../assets/images/icon-person.svg");
  background-position-x: 5%;
  background-repeat: no-repeat;
  background-position-y: center;
  background-size: 4%;
  text-align: right;
  border-radius: 3px;
  padding-right: 1rem;
  color: hsl(183, 100%, 15%);
  font-weight: 700;
  border: none;
  background-color: hsl(189, 41%, 97%);
}
.people__info {
  display: flex;
  flex-flow: row;
  justify-content: space-between;
}
.people__alert {
  color: orangered;
}
.people__input:hover {
  cursor: pointer;
  border: 2px solid hsl(172, 67%, 45%);
}
.tips__right {
  background-color: hsl(183, 100%, 15%);
  border-radius: 5px;
  width: auto;
  padding: 0.1rem 2rem;
  display: flex;
  flex-flow: column;
  justify-content: space-between;
  margin-top: 1rem;
}
.tips__right p {
  font-size: 0.8rem;
  font-weight: 700;
  color: white;
}
.top__info {
  display: flex;
  flex-flow: row;
  justify-content: space-between;
  text-align: left;
  height: 4rem;
}
.info__subtitle {
  color: hsl(184, 14%, 56%);
  font-size: 0.6rem;
}
.reset__button {
  width: 80%;
  height: 1.8rem;
  margin-bottom: 0.5rem;
  background-color: hsl(172, 67%, 45%);
  color: white;
  border: none;
  border-radius: 2px;
  font-weight: 500;
  letter-spacing: 0.5px;
}
.reset__button:hover {
  cursor: pointer;
}
h2 {
  color: hsl(172, 67%, 45%);
}

/* Eliminar las flechas del input type="number" */
/* Chrome: */
input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
/* Firefox: */
input[type="number"] {
  -moz-appearance: textfield;
}
input[type="number"]:hover,
input[type="number"]:focus {
  -moz-appearance: number-input;
}
/* Other */
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
/* Heredar font-family en componentes */
input,
button {
  font-family: inherit;
}
</style>
