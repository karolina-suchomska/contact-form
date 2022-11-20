<script>
export default {
  name: 'ContactForm',
  data () {
    return {
      form: {
        name: '',
        email: '',
        subject: '',
        message: ''
      },
      errors: {
        name: false,
        email: false,
        subject: false,
        message: false
      },
      errorsText: {
        name: '',
        email: ''
      },
      errorAllFormFields: false
    }
  },
  methods: {
    sendMessage () {
      this.validation();
    },
    clearValidation () {
      this.errorAllFormFields = false;

      Object.entries(this.form).forEach(
        ([key, value]) => {
          this.errors[key] = false;
        }
      );
    },
    async validation () {
      this.clearValidation();

      this.validationOfName();
      this.validationOfEmail();

      this.errors.message = this.form.message === '';
      
      Object.entries(this.errors).forEach(
        ([key, value]) => {
          if (value) {
            this.errorAllFormFields = true;
          }
        }
      );      
    },
    validationOfName () {
      if (this.form.name === '') {
        this.errors.name = true;
      } else if (this.form.name.length < 5) {
        this.errors.name = true;
        this.errorsText.name = 'Name must be at least 5 characters long';
      } else {
        this.errors.name = false;
        this.errorsText.name = '';
      }
    },
    validationOfEmail () {
      if (this.form.email === '') {
        this.errors.email = true;
      } else if (!/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(this.form.email)) {
        this.errors.email = true;
        this.errorsText.email = 'Please enter a valid email address';
      } else {
        this.errors.email = false;
        this.errorsText.email = '';
      }
    },
  }
};
</script>

<template>
    <div class="contact-form-container">
      <form>
        <div class="form-box">
          <p v-show="errorsText.name" class="error-message">{{ errorsText.name }}</p>
          <span
            class="character-counter"
            :class="{ 'max-character': form.name.length === 50 }"
          >
            {{ form.name.length }}/50
          </span>
          <label class="form-title-input">Name</label>
          <input 
            class="form-input" 
            :class="{ 'form-input-error': errors.name }"
            type="text" 
            maxlength="50"
            v-model="form.name"
            @keyup.enter="sendMessage"
            @change="validationOfName"
          >
        </div>
        <div class="form-box">
          <p v-show="errorsText.email" class="error-message email">{{ errorsText.email }}</p>
          <label class="form-title-input">E-mail</label>
          <input 
            class="form-input" 
            :class="{ 'form-input-error': errors.email }"
            type="text"
            v-model="form.email"
            @keyup.enter="sendMessage"
            @change="validationOfEmail"
          >
        </div>
        <div class="form-box">
          <span
            class="character-counter"
            :class="{ 'max-character': form.subject.length === 100 }"
          >
            {{ form.subject.length }}/100
          </span>
          <label class="form-title-input">Subject</label>
          <input 
            class="form-input" 
            type="text"
            maxlength="100"
            v-model="form.subject"
            @keyup.enter="sendMessage"
          >
        </div>
        <div class="form-box">
          <span
            class="character-counter"
            :class="{ 'max-character': form.message.length === 500 }"
          >
            {{ form.message.length }}/500
          </span>
          <label class="form-title-input">Message</label>
          <textarea 
            class="form-input" 
            :class="{ 'form-input-error': errors.message }"
            name="form-message" 
            id="formMessage" 
            cols="30" 
            rows="10"
            maxlength="500"
            v-model="form.message"
            @change="errors.message = form.message === ''"
           />
        </div>
        <div class="form-box button">
          <p v-show="errorAllFormFields" class="error-message">Complete the required fields</p>
          <button type="button" @click="sendMessage">Send</button>
        </div>
      </form>
    </div>
</template>