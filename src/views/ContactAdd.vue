<template>
  <div class="page">
    <h4>Hiệu chỉnh Liên hệ</h4>
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
        this.message = "Thêm liên hệ thành công thành công.";
      } catch (error) {
        console.log(error);
      }
    },
    async deleteContact() {
      if (confirm("Bạn muốn xóa Liên hệ này?")) {
        try {
          await ContactService.delete(this.contact._id);
          this.$router.push({ name: "contactbook" });
        } catch (error) {
          console.log(error);
        }
      }
    },
  },
};
</script>