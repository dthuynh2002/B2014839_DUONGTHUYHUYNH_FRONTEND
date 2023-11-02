<template>
  <div class="page">
    <h4>Tạo Liên hệ mới</h4>
    <contactForm :contact="newContact" @submit:contact="createContact" />
  </div>
</template>

<script>
import contactForm from "@/components/contactForm.vue";
import ContactService from "@/services/contact.service";

export default {
  components: {
    contactForm,
  },
  data() {
    return {
      newContact: {
        name: "",
        email: "",
        address: "",
        phone: "",
        favorite: false,
      },
    };
  },
  methods: {
    async createContact(contactData) {
      try {
        await ContactService.create(contactData);
        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.log(error);
        this.$router.push({
          name: "notfound",
          params: {
            pathMatch: this.$route.path.split("/").slice(1)
          },
          query: this.$route.query,
          hash: this.$route.hash,
        });
      }
    },
  },
};
</script>
