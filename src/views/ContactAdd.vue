<template>
  <div v-if="contact" class="page">
    <h4>Thêm Liên hệ</h4>
    <ContactForm :contact="contact" @submit:contact="addContact" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";
export default {
  components: {
    ContactForm,
  },
  props: {
    id: { type: String, required: true },
  },
  data() {
    return {
      contact: {},
      message: "",
    };
  },
  methods: {
    async addContact(data) {
      try {
        await ContactService.create(data);
        this.message = "Liên hệ được thêm vào danh bạ thành công.";
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
