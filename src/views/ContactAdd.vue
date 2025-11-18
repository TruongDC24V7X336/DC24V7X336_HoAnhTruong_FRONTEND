<template>
  <div class="page">
    <h4>Thêm mới Liên hệ</h4>

    <ContactForm :contact="contact" @submit:contact="createContact" />

    <p v-if="message" class="mt-2">{{ message }}</p>
  </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
  components: {
    ContactForm,
  },

  data() {
    return {
      contact: {
        name: "",
        email: "",
        address: "",
        phone: "",
        favorite: false,
        maritalStatus: "",
        hobbies: [],
      },
      message: "",
    };
  },

  methods: {
    async createContact(data) {
      try {
        await ContactService.create(data);

        alert("Thêm liên hệ thành công.");
        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.log(error);
        const errMsg =
          error?.response?.data?.message ||
          error?.message ||
          "Đã có lỗi khi thêm liên hệ.";
        this.message = errMsg;
      }
    },
  },
};
</script>

<style scoped>
.page {
  max-width: 750px;
  text-align: left;
}
</style>
