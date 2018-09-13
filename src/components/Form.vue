<template>
  <div>
    <div class="progress">
      <div class="progress--circle" :class="{active: step === 1 || step === 2 || step === 3}"></div>
      <div class="progress--circle" :class="{active: step === 2 || step === 3}"></div>
      <div class="progress--circle" :class="{active: step === 3}"></div>
    </div>
    <form class="form">
      <div class="form--first-step" :class="{active: step === 1}">
        <div class="form-field">
          <input type="text"
                 placeholder="Name"
                 v-model="nameValue"
                 v-on:keyup="handleInputChange('name')">
          <p class="error"
             :class="{'not-valid': nameValid !== null && !nameValid}">
            Name must have more than 3 symbols
          </p>
        </div>
        <div class="form-field">
          <input type="email"
                 placeholder="Email"
                 v-model="emailValue"
                 v-on:keyup="handleInputChange('email')">
          <p class="error"
             :class="{'not-valid': emailValid !== null && !emailValid}">
            Enter valid email
          </p>
        </div>
        <div class="form-field">
          <input type="tel"
                 placeholder="Phone"
                 v-model="phoneValue"
                 v-on:keyup="handleInputChange('phone')">
          <p class="error"
             :class="{'not-valid': phoneValid !== null && !phoneValid}">
            Phone must have more than 5 numerals
          </p>
        </div>
      </div>

      <div class="form--second-step"
           :class="{active: step === 2}">
        <div class="form-field">
          <input type="number"
                 min="1"
                 placeholder="Years of experience"
                 v-model="experienceValue"
                 v-on:keyup="handleInputChange('experience')">
          <p class="error"
             :class="{'not-valid': experienceValid !== null && !experienceValid}">
            Experience must be at least 1 year
          </p>
        </div>
        <div class="form-field">
          <input type="text"
                 placeholder="Previous employer"
                 v-model="employerValue"
                 v-on:keyup="handleInputChange('employer')">
          <p class="error"
             :class="{'not-valid': employerValid !== null && !employerValid}">
            Employer must have more than 1 symbol
          </p>
        </div>
        <div class="form-field">
          <input type="text"
                 placeholder="Link to LinkedIn"
                 v-model="linkValue"
                 v-on:keyup="handleInputChange('link')">
          <p class="error"
             :class="{'not-valid': linkValid !== null && !linkValid}">
            Enter correct URL
          </p>
        </div>
      </div>

      <div class="form--third-step"
           :class="{active: step === 3}">
        <h2>Your application is complete</h2>
        <p>Name:
          <span>{{nameValue}}</span>
        </p>
        <p>Email:
          <span><a :href="`mailto:${emailValue}`">{{emailValue}}</a></span>
        </p>
        <p>Phone:
          <span>{{phoneValue}}</span>
        </p>
        <p>Experience:
          <span>{{experienceValue}} years</span>
        </p>
        <p>Last employer:
          <span>{{employerValue}}</span>
        </p>
        <p>LinkedIn:
          <span><a :href="linkValue" target="_blank">{{linkValue}}</a></span>
        </p>
      </div>

      <button class="main-btn"
              :style="step === 3 ? {display: 'none'} : ''"
              @click="e => handleChangeStep(e, step)">
        {{step === 1 ? 'Next' : 'Complete application'}}
      </button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'Form',
    data() {
      return {
        step: 1,
        nameValue: '',
        emailValue: '',
        phoneValue: '',
        experienceValue: '',
        employerValue: '',
        linkValue: '',
        nameValid: null,
        emailValid: null,
        phoneValid: null,
        experienceValid: null,
        employerValid: null,
        linkValid: null
      };
    },
    methods: {
      handleChangeStep(e, step) {
        e.preventDefault();
        if (step === 1) {
          if (this.nameValid === null) {
            this.nameValid = false;
          }
          if (this.emailValid === null) {
            this.emailValid = false;
          }
          if (this.phoneValid === null) {
            this.phoneValid = false;
          }
          if (this.nameValid === true &&
            this.emailValid === true &&
            this.phoneValid === true) {
            this.step = this.step + 1;
          }
        } else if (step === 2) {
          if (this.experienceValid === null) {
            this.experienceValid = false;
          }
          if (this.employerValid === null) {
            this.employerValid = false;
          }
          if (this.linkValid === null) {
            this.linkValid = false;
          }
          if (this.experienceValid === true &&
            this.employerValid === true &&
            this.linkValid === true) {
            this.step = this.step + 1;
          }
        }
      },
      handleInputChange(input) {
        const emailValidation = /^\w+@[a-zA-Z_]+?\.[a-zA-Z]{2,3}$/,
          phoneValidation = /^\d+$/,
          linkValidation = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/;

        if (input === 'name') {
          if (this.nameValue.length >= 3) {
            return this.nameValid = true;
          } else {
            return this.nameValid = false;
          }
        }
        if (input === 'email') {
          if (this.emailValue.match(emailValidation)) {
            return this.emailValid = true;
          } else {
            return this.emailValid = false;
          }
        }
        if (input === 'phone') {
          if (this.phoneValue.match(phoneValidation) && this.phoneValue.length >= 5) {
            return this.phoneValid = true;
          } else {
            return this.phoneValid = false;
          }
        }
        if (input === 'experience') {
          if (this.experienceValue >= 1) {
            return this.experienceValid = true;
          } else {
            return this.experienceValid = false;
          }
        }
        if (input === 'employer') {
          if (this.employerValue.length >= 1) {
            return this.employerValid = true;
          } else {
            return this.employerValid = false;
          }
        }
        if (input === 'link') {
          if (this.linkValue.match(linkValidation)) {
            return this.linkValid = true;
          } else {
            return this.linkValid = false;
          }
        }
      },
    }
  };
</script>

<style lang="sass">
  .form
    text-align: center
    &--first-step,
    &--second-step,
    &--third-step
      display: none
      &.active
        display: block
      .form-field
        position: relative
        .error
          color: red
          position: absolute
          bottom: -10px
          left: 0
          display: none
          font-size: 12px
          &.not-valid
            display: block
      input
        width: 100%
        height: 40px
        margin-bottom: 20px
        border: none
        border-bottom: 2px solid #42bef5
      p
        span
          font-size: 20px
          word-break: break-word
          a
            color: #42bef5
            text-decoration: none
      h2
        color: #42bef5
        border-bottom: 2px solid #42bef5
        padding-bottom: 10px

  .progress
    display: flex
    justify-content: space-around
    margin-bottom: 20px
    &--circle
      width: 50px
      height: 50px
      border-radius: 50%
      border: 2px solid #42bef5
      position: relative
      &:first-child,
      &:nth-child(2)
        &:after
          position: absolute
          content: ''
          background: #42bef5
          height: 2px
          width: 82px
          left: calc(100% + 1px)
          top: calc(25px - 1px)
      &.active
        background: #3250aa
        border: 2px solid #3250aa
</style>
