<template>
  <div class="container">
      <h1 class="title">
        регистрация
      </h1>
      <span class="subtitle">
        Уже есть аккаунт?
        <a class="subtitle-link">Войти</a>
      </span>
      <form class="form" method="post" type="submit" @submit.prevent="submitForm">
        <ul>
          <li>
            <label for="name">имя</label>
            <input type="text" id="name" name="user-name" 
                   placeholder="Введите Ваше имя"
                   v-model.trim="form.name">
             <span v-if="!nameIsValid" class="error-message">
              введено некоректное значение
            </span>
          </li>
          <li>
            <label for="email">email</label>
            <input type="text" id="email" name="user-email" 
                   placeholder="Введите Ваше email"
                   v-model.trim="form.email">
             <span v-if="!emailIsValid" class="error-message">
              введено некоректное значение
            </span>
          </li>
          <li class="phone">
            <label for="phone">номер телефона</label>
            <input type="text" id="phone" name="user-phone" 
                placeholder="Введите номер телефона"
                v-model.trim="form.phoneNumber">
            <span v-if="!phoneIsValid" class="error-message">
              введено некоректное значение
            </span>
          </li>
          <li>
            <custom-selector/>
          </li>
        </ul>
        <div class="container-checkbox">
            <input type="checkbox" class="input-checkbox" id="checkbox">
            <label class="label-checkbox" for="checkbox">
              принимаю 
              <a class="link">условия</a> 
              использования
            </label>
        </div>
        <button :class="form.name!=='' && form.email!=='' && form.phoneNumber!=='' ? 'action-registr' : 'action-registr-disabled'" 
                :disabled="form.name!=='' && form.email!=='' && form.phoneNumber!=='' ? false : true">
          зарегистрироваться
        </button>
      </form>
  </div>
</template>

<script>
import CustomSelector from './CustomSelector.vue'
export default {
  components: { CustomSelector },
  name: 'sign-up',
  data() {
    return {
      form: {
        name: "",
        email: "",
        phoneNumber: "",
      },
      nameIsValid: true,
      emailIsValid: true,
      phoneIsValid: true,
    }
  },
  methods: {
    submitForm() {
      let checkField = (input, valid, typeField) => {
        let regexp 
        typeField === "name" ? regexp = /^[A-Za-z-А-Яa-я -]+$/g 
        : typeField === "email" ? regexp = /\S+@\S+\.\S+/g 
        : regexp = /^\+?[78][-\(]?\d{3}\)?-?\d{3}-?\d{2}-?\d{2}$/g
        let match = input.match(regexp)
        if (!match) return match
        return valid = match
      }
      const [nameField, emailField, phoneField] = [
        this.nameIsValid= checkField(this.form.name, this.nameIsValid, "name"), 
        this.emailIsValid= checkField(this.form.email, this.emailIsValid, "email"), 
        this.phoneIsValid = checkField(this.form.phoneNumber, this.phoneIsValid, "phone")
      ]
      nameField && emailField && phoneField ? alert("Form sent successfully") : this.isVFormValidated = true
      return [nameField, emailField, phoneField]
    }
  }
}
</script>

<style scoped lang="scss">
@import "../scss/_mixins.scss";

.container{
  margin: 1em auto;
  padding: 2.526em 1.875em;
  border-radius: 24px;
  background-color: #ffff;
  --link-color: rgba(8, 128, 174, 1);
  --error-color:rgba(255, 113, 113, 1);
  .title{
    padding-bottom: .251em;
      &::first-letter{
        text-transform: capitalize;
      }
      @media(min-width: 360px){ font-size: 1.5rem};
      @media(min-width: 630px){font-size: 2.125rem}
    }
  .subtitle{
     @include xs-size();
     @include sm-size();
    .subtitle-link{
      font-size: 1rem;
      font-weight: 400;
      padding-left: .375em;
      color: var(--link-color);
      line-height: 22px;
      @include xs-size();
      @include sm-size();
    }
  }
}
.form{
  margin-top: 3.537em;
  --label-color: #756F86;
  --shadow: 0 4px 8px 0 rgba(44, 39, 56, .04);
  ul li{
    display: flex;
    flex-direction: column;
    padding-bottom: 2.125em;
    label{
    padding-bottom: .4375em;
      &::first-letter{
        text-transform: capitalize;
      }
      @include xs-size();
      @include sm-size();
    }
  }
  ul li:last-child {
    padding-bottom: 1.954em;
  }
  #name, #email, #phone{
    width: 100%;
    height: 3.375em;
    padding: 0em 6.063em 0em 1em; 

    border: 1px solid #DBE2EA;
    border-radius: 6px;
    box-shadow: var(--shadow);
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;

    @include xs-size();
    @include sm-size();
      
    &::placeholder{
      color: rgba(124, 156, 191, 1);
      @include xs-size();
      @include sm-size();
    }
  }
  .error-message{
    font-size: .875rem;
    padding-top: .571em;
    color: var(--error-color);
    &::first-letter{
      text-transform: capitalize;
    }
  }
  /*Custom-Checkbox*/
  .container-checkbox{
    display: flex;
    position: relative;
    height: 28px;
    margin-bottom: 2.605em;
      .input-checkbox{
        position: absolute;
        -webkit-appearance: none;
        appearance: none;
      }
      .label-checkbox{
        align-self: center;
        font-weight: 500;
        line-height: 20.8px;
        color: #444;
        cursor: pointer;
        user-select:none;
        &::first-letter{ text-transform: capitalize};
        @include xs-size();
        @include sm-size();
        @media (min-width: 360px) { padding-left: 2em; }
         @media (min-width: 362px) { padding-left: 2.1em; }
         @media (min-width: 480px) { padding-left: 2.5em; }
          @media (min-width: 630px) { padding-left: 2.2em; }
        .link{
         color: var(--link-color)
        }
      }
      .label-checkbox::before{
        content: "";
        display: block;

        border: 2px solid #ccc;
        background-color: #fff;
        border-radius: 4px;
        box-shadow: var(--shadow);

        position: absolute;
        z-index: 1;

        transition: background .1s linear, border .1s linear;
         @media(min-width: 360px){
          width: 20px;
          height: 20px;
          top: .3em;
          left: .3em;
        }
        @media(min-width: 480px){
          width: 28px;
          height: 28px;
          top: 0;
          left: 0;  
        }
      }
      .label-checkbox::after {
        content: "";
        display: block;
        width: 15px;
        height: 11.3px;
        background: url("../../public/image/Check.svg") no-repeat;
        background-size: 15px 11.3px;
        opacity: 0;

        position: absolute;
        top: 8.5px;
        left: 6.5px;
        z-index: 2;

        transition: opacity .1s linear;
      }
      /* Hide/Show  Checkbox*/
      .input-checkbox:checked + .label-checkbox:before{
        border: 3px solid var(--link-color)
      }
       .input-checkbox:checked + .label-checkbox:after{
        opacity: 1;
      }
    }
    .action-registr, .action-registr-disabled{
      font-size: 1rem;
      width: 100%;
      height: 3.535em;

      border-radius: 6px;
      box-shadow: var(--shadow);

      font-weight: 500;
      line-height: 20.8px;
      color:rgba(235, 244, 248, 1);
      &::first-letter{ text-transform: capitalize};
      @include xs-size();
      @include sm-size();
    }
     .action-registr{
        background-color: var(--link-color);
        &:hover{
          box-shadow: 0 12px 24px 0 rgba(44, 39, 56, .16);
        }
        &:active{
        border: 3px solid rgba(44, 39, 56, 0.86);
        }
      }
    .action-registr-disabled{
      background-color: rgba(219, 226, 234, 1);
      color: rgba(44, 39, 56, .7);
    }
  }
</style>
