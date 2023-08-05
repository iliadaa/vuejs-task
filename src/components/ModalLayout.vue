<template>
    <v-dialog v-model="dialogVisible" max-width="400px" class="modal-layout" :persistent="true">
        <v-card>
            <v-card-title class="text-center modal-title">{{ title }}</v-card-title>
            <v-card-actions class="justify-space-around">
                <v-btn class="button-modal" @click="confirm">OK</v-btn>
                <v-btn class="button-modal" @click="cancel">Cancel</v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>
  
<script>
export default {
    props: {
        showModal: {
            type: Boolean,
            required: true,
        },
        title: {
            type: String,
            required: true,
        },

    },
    computed: {
        dialogVisible: {
            get() {
                return this.showModal;
            },
            set(value) {
                this.$emit("update:showModal", value);
            },
        },
    },
    methods: {
        confirm() {
            this.$emit("confirm");
        },
        cancel() {
            this.$emit("cancel");
        },
    },
};
</script>
<style>
.button-modal {
    color: #ffffff;
    width: 25%;
    padding: 6px 12px;
    border: none;
    cursor: pointer;
    border-radius: 10px;
    background-color: #0e55cb;
    color: #fff;
    font-size: 15px;
    font-style: normal;
    font-weight: 500;
    text-transform: capitalize;
}

.modal-layout>.v-overlay__content>.v-card {
    height: 150px;
    justify-content: space-around;
    border-radius: 10px;
}

.modal-title {
    color: #43546f;
    font-weight: 600;
}
</style>
  