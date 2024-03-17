<template>
    <div v-if="!contact" class="page">
        <h4>Thêm mới danh bạ</h4>
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
        id: { type: String, default: null },
    },
    data() {
        return {
            contact: null,
            message: "",
        };
    },
    methods: {
        async addContact(data) {
            try {
                await ContactService.create(data);
                alert('Thêm mới danh bạ thành công.');
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.log(error);
            }
        }
    },
    created() {
        this.contact = false;
    },
};
</script>