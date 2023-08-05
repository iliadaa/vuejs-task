<template>
    <v-container>
        <FormLayout @form-submitted="onFormSubmitted" />
        <v-container class="d-flex flex-column align-end">
            <v-btn @click="openExportModal" class="">Export
                <v-icon end icon="mdi mdi-export"></v-icon>
            </v-btn>
            <ExportModal :data="formDataTable" ref="exportModal"></ExportModal>
            <TableLayout :rows="formDataTable" :headers="tableHeaders" :button-data="buttonData"
                @button-clicked="handleDelete" />
        </v-container>
        <ModalLayout :show-modal="showModal" title="Are you sure?" @confirm="deleteRow" @cancel="cancelDelete"
            @update:show-modal="showModal = $event" />
    </v-container>
</template>

<script>
import FormLayout from "../components/FormLayout.vue";
import TableLayout from "../components/TableLayout.vue";
import ModalLayout from "../components/ModalLayout.vue";
import ExportModal from "../components/ExportModal.vue";

export default {
    name: "HomeLayout",
    components: {
        FormLayout,
        TableLayout,
        ModalLayout,
        ExportModal,
    },
    data() {
        return {
            formDataTable: [
                {
                    id: "1",
                    name: "John",
                    surname: "Doe",
                    email: "john.doe@example.com",
                    age: 30,
                    favoriteColor: "Blue",
                    contactPreference: "Email",
                },
                {
                    id: "2",
                    name: "Jane",
                    surname: "Smith",
                    email: "jane.smith@example.com",
                    age: 25,
                    favoriteColor: "Green",
                    contactPreference: "Phone",
                },
            ],
            tableHeaders: [
                { text: "Name", value: "name" },
                { text: "Surname", value: "surname" },
                { text: "Email", value: "email" },
                { text: "Age", value: "age" },
                { text: "Favorite Color", value: "favoriteColor" },
                { text: "Contact Preference", value: "contactPreference" },
                { text: "Action", value: "action" },
            ],
            buttonData: [{ text: "Delete", action: "delete" }],
            showModal: false,
            rowToDelete: null,
        };
    },
    methods: {
        onFormSubmitted(formData) {
            const id = Date.now();
            const newRow = {
                id,
                name: formData.name,
                surname: formData.surname,
                email: formData.email,
                age: formData.age,
                favoriteColor: formData.favoriteColor,
                contactPreference: formData.contactPreference.join(", "),
            };
            this.formDataTable.push(newRow);

        },

        handleDelete(row) {
            this.rowToDelete = row.id;
            this.showModal = true;
        },

        deleteRow() {
            const index = this.formDataTable.findIndex(
                (item) => item.id === this.rowToDelete
            );
            this.formDataTable.splice(index, 1);
            this.showModal = false;
        },

        cancelDelete() {
            this.showModal = false;
            this.rowToDelete = null;
        },

        openExportModal() {
            this.$refs.exportModal.openModal();
        },
    },
};
</script>


