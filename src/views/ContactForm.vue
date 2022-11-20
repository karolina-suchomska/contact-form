<script>
import InputText from '../components/InputText.vue';

export default {
  name: 'ContactForm',
  components: {
    InputText
  },
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
        message: false
      },
      errorAllFormFields: false
    }
  },
  methods: {
    sendMessage () {
      if (this.validation()) {
        return 0;
      }
     
      console.log(this.form);
    },
     /**
     * Resets all error states to default.
     */
    clearValidation () {
      this.errorAllFormFields = false;

      this.$refs.inputTextNameRef.clearError();
      this.$refs.inputTextEmailRef.clearError();
      this.$refs.inputTextMessageRef.clearError();
    },
    validation () {
      let isFormValid = true;

      this.clearValidation();

      this.validationOfName();
      this.validationOfEmail();
      this.validationOfMessage();
      
      Object.entries(this.errors).forEach(
        ([key, value]) => {
          if (value) {
            this.errorAllFormFields = true;
            isFormValid = true;
          } else {
            isFormValid = false
          }
        }
      );     
      
      return isFormValid;
    },
     /**
     * Checks all conditions for field id="name".
     */
    validationOfName () {
      this.errors.name = true;

      if (this.form.name.length < 5) {
        this.$refs.inputTextNameRef.setError(this.form.name === '' ? '' : 'Name must be at least 5 characters long');
      } else {
        this.errors.name = false;
        this.$refs.inputTextNameRef.clearError();
      }
    },
     /**
     * Checks all conditions for field id="email".
     */
    validationOfEmail () {
      this.errors.email = true;

      if (!/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(this.form.email)) {
        this.$refs.inputTextEmailRef.setError(this.form.email === '' ? '' : 'Please enter a valid email address');
      } else {
        this.errors.email = false;
        this.$refs.inputTextEmailRef.clearError();
      }
    },
     /**
     * Checks all conditions for field id="message".
     */
    validationOfMessage () {
      this.errors.message = true;

      if (this.form.message === '') {
        this.$refs.inputTextMessageRef.setError('');
      } else {
        this.errors.message = false;
        this.$refs.inputTextMessageRef.clearError();
      }
    }
  }
};
</script>

<template>
    <div class="contact-form-container">
      <form>
        <div class="form-box">
          <span
            class="character-counter"
            :class="{ 'max-character': form.name.length === 50 }"
          >
            {{ form.name.length }}/50
          </span>
          <label for="name" class="form-title-input">Name</label>
          <InputText 
            id="name"
            type="input"
            v-model="form.name"
            :max-length="50"
            ref="inputTextNameRef"
            @keyup.enter="sendMessage"
            @change="validationOfName"
          />
        </div>
        <div class="form-box">
          <label for="email" class="form-title-input">E-mail</label>
          <InputText 
            id="email"
            type="input"
            class="email"
            v-model="form.email"
            ref="inputTextEmailRef"
            @keyup.enter="sendMessage"
            @change="validationOfEmail"
          />
        </div>
        <div class="form-box">
          <span
            class="character-counter"
            :class="{ 'max-character': form.subject.length === 100 }"
          >
            {{ form.subject.length }}/100
          </span>
          <label for="subject" class="form-title-input">Subject (optional)</label>
          <InputText 
            id="subject"
            type="input"
            v-model="form.subject"
            :max-length="100"
            @keyup.enter="sendMessage"
          />
        </div>
        <div class="form-box">
          <span
            class="character-counter"
            :class="{ 'max-character': form.message.length === 500 }"
          >
            {{ form.message.length }}/500
          </span>
          <label for="message" class="form-title-input">Message</label>
          <InputText 
            id="message"
            name="message"
            type="textarea"
            :max-length="500"
            v-model="form.message"
            ref="inputTextMessageRef"
          />
        </div>
        <div class="form-box button">
          <p v-show="errorAllFormFields" class="error-message">Complete the required fields</p>
          <button type="button" @click="sendMessage">Send</button>
        </div>
      </form>
    </div>
</template>