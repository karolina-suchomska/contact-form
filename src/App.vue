<script>
import ContactForm from './views/ContactForm.vue';

export default {
  name: 'App',
  components: {
    ContactForm
  },
};
</script>

<template>
  <div class="app_contact-form">
    <div class="contact-form">
      <div class="contact-form-title">
        <h2>Contact Form</h2>
      </div>
      <ContactForm />
    </div>
  </div>
</template>