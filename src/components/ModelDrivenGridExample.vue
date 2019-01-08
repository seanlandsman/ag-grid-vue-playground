<template lang="html">
    <div style="display: inline-block; width: 1100px">
        <h1>Model Driven Grid Example</h1>
        <h3>Note that the data bound table will not update as the row data is frozen.</h3>
        <div style="float: left; display: inline-grid">
            <span>Model Driven</span>
            <ag-grid-vue
                    ref="model"
                    class="ag-theme-balham"
                    style="width: 400px; height: 150px;"
                    :columnDefs="columnDefs"
                    v-model="modelRowData">
            </ag-grid-vue>
            <span>{{ modelRowData }}</span>
            <button @click="printRowData('modelRowData')">Print Row Data</button>
        </div>
        <div style="float: left; margin-left: 20px; display: inline-grid">
            <span>Data Bound</span>
            <ag-grid-vue
                    ref="normal"
                    class="ag-theme-balham"
                    style="width: 400px; height: 150px;float: left"
                    :columnDefs="columnDefs"
                    :rowData="rowData">
            </ag-grid-vue>
            <span>{{ rowData }}</span>
            <button @click="printRowData('rowData')">Print Row Data</button>
        </div>
    </div>
</template>
<script>
    import {AgGridVue} from "ag-grid-vue";

    export default {
        name: 'ModelDrivenGridExample',
        data() {
            return {
                columnDefs: null,
                rowData: null,
                modelRowData: null
            };
        },
        beforeMount() {
            this.columnDefs = [
                {headerName: 'Make', field: 'make', editable: true},
                {headerName: 'Model', field: 'model', editable: true},
            ];

            const tempRowData = [
                {make: 'Toyota', model: 'Celica'}
            ];

            // row data below is not reactive, so changes made by the grid will not automatically be reflected
            // in the template

            // both modelRowData and rowData will be updated by the grid (on edit for example), but the changes
            // wont be reflected in the ui in the case of rowData, but will be for modelRowData

            this.modelRowData = Object.freeze(
                this.copyRowData(tempRowData)
            );

            this.rowData = Object.freeze(
                this.copyRowData(tempRowData)
            );
        },
        methods: {
            printRowData(field) {
                this[field].forEach(datum => console.log(datum))
            },
            copyRowData(data) {
                return data.map(datum => {
                    return {
                        ...datum
                    }
                })
            }
        },
        components: {
            AgGridVue
        }
    };
</script>
<style lang="css">
    @import "~ag-grid-community/dist/styles/ag-grid.css";
    @import "~ag-grid-community/dist/styles/ag-theme-balham.css";
</style>