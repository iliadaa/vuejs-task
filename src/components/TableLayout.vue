<template>
    <v-card class="card-form mt-2" width="100%">
        <v-table class="table-style">
            <thead>
                <tr>
                    <th v-for="header in headers" :key="header.value" class="text-center">{{ header.text }}</th>
                </tr>
            </thead>
            <tbody v-if="rows.length === 0">
                <tr>
                    <td :colspan="headers.length" class="text-center">No data available.</td>
                </tr>
            </tbody>
            <tbody v-else>
                <tr v-for="(row, index) in rows" :key="index">
                    <td v-for="header in headers" :key="header.value" class="text-center">
                        <template v-if="header.value === 'action'">
                            <v-btn v-for="(button, id) in buttonData" :key="id" @click="handleButtonClick(row)"
                                class="button-style ">
                                {{ button.text }}
                                <v-icon end icon="mdi-trash-can-outline"></v-icon> </v-btn>
                        </template>
                        <template v-else>
                            {{ row[header.value] }}
                        </template>
                    </td>
                </tr>
            </tbody>
        </v-table>
    </v-card>
</template>
  
<script>

export default {
    name: "TableLayout",
    props: {
        headers: {
            type: Array,
            required: true,
        },
        rows: {
            type: Array,
            required: true,
        },
        buttonData: {
            type: Array,
            default: () => [],
        },
    },
    methods: {
        handleButtonClick(row) {
            this.$emit("button-clicked", row);
        },
    },
};
</script>
  
<style>
.table-style {
    border-collapse: collapse;
    width: 100%;
}

.table-style th,
.table-style td {
    border: 1px solid #dddddd;
    padding: 8px;
}

.table-style th {
    background-color: #F3F8FF;
    font-weight: bold;
}

.button-style {
    color: #ffffff;
    width: 100%;
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

.button-style:hover {
    background-color: #0056b3;
}
</style>
  