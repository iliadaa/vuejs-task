<template>
    <v-dialog v-model="visible" fullscreen>
        <v-card>
            <div class="card-header">
                <v-spacer></v-spacer>
                <v-btn @click="closeModal" class="button-close-export">Close
                    <v-icon end icon="mdi mdi-close "></v-icon>
                </v-btn>
            </div>
            <pre class="json-body"> {{ jsonData }}</pre>
        </v-card>
    </v-dialog>
</template>
  
<script>
export default {
    props: {
        data: {
            type: Array,
            required: true,
        },
    },
    data() {
        return {
            visible: false,
        };
    },
    computed: {
        jsonData() {
            return JSON.stringify(this.data, null, 2);
        },
    },
    methods: {
        openModal() {
            this.visible = true;
        },
        closeModal() {
            this.visible = false;
        },
    },
};
</script>
  
<style>
.button-close-export {
    width: 100px;
    color: black;
}

.card-header {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    padding: 15px;
}

.json-body {
    border: 1px dashed gray;
    box-shadow: 0px 3px 0px -6px rgba(0, 0, 0, 0.2), 0px 2px 2px 0px rgba(0, 0, 0, 0.14), 0px 1px 5px 0px rgba(0, 0, 0, 0.12);
}
</style>
  