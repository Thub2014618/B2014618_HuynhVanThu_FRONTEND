<template>
    <div   v-if="contact" class="page">
        <h4>Thêm liên hệ</h4>
        <ContactForm
            :contact="contact"
            @submit:contact="addContact"
        />
        <p>{{ message }}</p> 
        <!-- xóa -->
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
                    this.message = "Liên hệ được thêm thành công.";
                    this.$router.push({ name: "contactbook", query: { message: this.message } });                
                } catch (error) {
                    console.log(error);
                }
            },
        },
        created() {
            this.message = "";
        },
    };
</script>