<template lang="html">
    <div>
        <h1>Declarative Grid Example</h1>
        <ag-grid-vue
                class="ag-theme-balham"
                style="width: 500px; height: 150px;"
                :columnDefs="columnDefs"
                :rowData="rowData">
        </ag-grid-vue>
    </div>
</template>
<script>
    import {AgGridVue} from "ag-grid-vue";

    export default {
        name: 'DeclarativeGridExample',
        data() {
            return {
                columnDefs: null,
                rowData: null
            };
        },
        beforeMount() {
            this.columnDefs = [
                {headerName: 'Make', field: 'make'},
                {headerName: 'Model', field: 'model'},
                {headerName: 'Price', field: 'price'}
            ];

            this.rowData = [
                {make: 'Toyota', model: 'Celica', price: 35000},
                {make: 'Ford', model: 'Mondeo', price: 32000},
                {make: 'Porsche', model: 'Boxter', price: 72000}
            ];
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