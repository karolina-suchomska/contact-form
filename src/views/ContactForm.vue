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
        name: '',
        email: '',
        subject: '',
        message: ''
      },
      errorAllFormFields: false
    }
  },
  methods: {
    sendMessage () {
      this.validation();
    },
    validation () {
      const form = this.form;
      const errors = this.errors;

      this.errorAllFormFields = false;

      Object.entries(form).forEach(
        ([key, value]) => {
          this.errorAllFormFields = value === '';
        }
      );
  
    }
  }
};
</script>

<template>
    <div class="contact-form-container">
      <form @keyup.enter="sendMessage">
        <div class="form-box">
          <p v-show="errors.name">{{ errors.name }}</p>
          <label class="form-title-input">Name</label>
          <input 
            class="form-input" 
            type="text" 
            maxlength="50"
            v-model="form.name"
          >
        </div>
        <div class="form-box">
          <p v-show="errors.email">{{ errors.email }}</p>
          <label class="form-title-input">E-mail</label>
          <input 
            class="form-input" 
            type="text"
            v-model="form.email"
          >
        </div>
        <div class="form-box">
          <p v-show="errors.subject">{{ errors.subject }}</p>
          <label class="form-title-input">Subject</label>
          <input 
            class="form-input" 
            type="text"
            v-model="form.subject"
          >
        </div>
        <div class="form-box">
          <p v-show="errors.nessage">{{ errors.message }}</p>
          <label class="form-title-input">Message</label>
          <textarea 
            class="form-input" 
            name="form-message" 
            id="formMessage" 
            cols="30" 
            rows="10"
            v-model="form.message"
           />
        </div>
        <p v-show="errorAllFormFields">Complete all form fields</p>
        <button type="button" @click="sendMessage">Send</button>
      </form>
    </div>
</template>