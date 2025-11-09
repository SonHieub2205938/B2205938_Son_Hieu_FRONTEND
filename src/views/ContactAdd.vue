<template>
  <div class="page">
    <h4>Thêm Liên hệ</h4>
    <ContactForm :contact="{}" @submit:contact="addContact" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import ContactForm from '@/components/ContactForm.vue';
import ContactService from '@/services/contact.service';

export default {
  components: {
    ContactForm,
  },
  data() {
    return {
      message: '',
    };
  },
  methods: {
    async addContact(data) {
      try {
        await ContactService.create(data);
        this.message = 'Liên hệ được thêm thành công.';
        this.$router.push({ name: 'contactbook' });
      } catch (error) {
        console.log(error);
        if (error.response && error.response.data) {
          this.message = error.response.data.message;
        } else {
          this.message = 'Có lỗi xảy ra khi thêm liên hệ.';
        }
      }
    },
  },
};
</script>

<style scoped>
.page {
  max-width: 600px;
  margin: 20px auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}
h4 {
  text-align: center;
  color: #333;
}
</style>