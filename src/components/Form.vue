<template>
  <div class="site">
    <form class="form" @submit.prevent="submitForm()">
      <div class="form-row">
        <label for="first-name">First name</label>
        <input id="first-name" type="text" class="form-control" v-model.trim="$v.firstName.$model" :class="{ 'is-invalid' : $v.firstName.$error, 'is-valid' : !$v.firstName.$invalid }" />
        <div v-show="!$v.firstName.$invalid" class="valid-feedback">First name is valid!</div>
        <div class="invalid-feedback">
          <span v-show="!$v.firstName.required">First name is required</span>
          <span v-if="!$v.firstName.minLength">First name must have at least {{ $v.firstName.$params.minLength.min }} letters</span>
          <span v-if="!$v.firstName.maxLength">First name must have at most {{ $v.firstName.$params.maxLength.max }} letters</span>
        </div>
      </div>

      <div class="form-row">
        <label for="last-name">Last name</label>
        <input id="last-name" type="text" class="form-control" v-model.trim="$v.lastName.$model" :class="{ 'is-invalid' : $v.lastName.$error, 'is-valid' : !$v.lastName.$invalid }" />
        <div v-show="!$v.lastName.$invalid" class="valid-feedback">Last name is valid!</div>
        <div class="invalid-feedback">
          <span v-if="!$v.lastName.required">Last name is required</span>
          <span v-if="!$v.lastName.minLength">Last name must have at least {{ $v.lastName.$params.minLength.min }} letters</span>
          <span v-if="!$v.lastName.maxLength">Last name must have at most {{ $v.lastName.$params.maxLength.max }} letters</span>
        </div>
      </div>

      <div class="form-row">
        <label for="age">Age</label>
        <input id="age" type="number" class="form-control" v-model.number.lazy="$v.age.$model" :class="{ 'is-invalid' : $v.age.$error, 'is-valid' : !$v.age.$invalid }" />
        <div v-show="!$v.age.$invalid" class="valid-feedback">Age is valid!</div>
        <div class="invalid-feedback">
          <span v-if="!$v.age.between">Age must between {{ $v.age.$params.between.min }} and {{ $v.age.$params.between.max }}</span>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
  import { required, minLength, maxLength, between } from 'vuelidate/lib/validators'

  export default {
    name: 'Form',
    data() {
      return {
        firstName: '',
        lastName: '',
        age: 0,
        email: ''
      }
    },
    validations: {
      firstName: {
        required,
        maxLength: maxLength(20),
        minLength: minLength(3)
      },
      lastName: {
        required,
        maxLength: maxLength(20),
        minLength: minLength(3)
      },
      age: {
        required,
        between: between(15, 40)
      }
    }
  }
</script>

<style scoped lang="scss">
  .site {
    width: 100%;
    min-height: 100vh;
    background-color: #646464;
    color: #aaa;

    .form {
      padding: 80px 0;
      margin: 0 auto;
      width: 30%;
      height: auto;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;

      &-row {
        margin-top: 20px;
        width: 100%;
        display: flex;
        flex-direction: column;

        label {
          font-size: 20px;
          font-weight: 800;
          color: #fff;
          margin-bottom: 5px;
        }

        .form-control {
          height: 40px;
          font-size: 20px;
          outline: none;
          padding: 0 10px;
          color: #333;
          border-radius: 5px;
          border: none;
          font-family: Arial, Helvetica, sans-serif;

          &.is-invalid {
            outline: 1px solid red;
          }

          &.is-valid {
            outline: 1px solid green;
          }
        }

        .valid-feedback {
          color: limegreen;
          margin-top: 5px;
        }

        .invalid-feedback {
          margin-top: 5px;

          span {
            color: red;
          }
        }
      }
    }
  }
</style>
