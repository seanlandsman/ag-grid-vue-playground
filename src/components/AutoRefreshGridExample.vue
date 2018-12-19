<template>
    <div>
        <ag-grid-vue style="width: 600px; height: 150px;"
                     class="ag-theme-balham"
                     :columnDefs="columnDefs"
                     :rowData="rowData"
                     :components="components"
                     autoParamsRefresh
                     :firstDataRendered="this.onFirstDataRendered">
        </ag-grid-vue>
    </div>
</template>

<script>
    import {AgGridVue} from "ag-grid-vue";
    import AutoRefreshCellRenderer from "./renderers/AutoRefreshCellRenderer";

    const store = [
        {make: 'Toyota', model: 'Celica', price: 35000},
        {make: 'Ford', model: 'Mondeo', price: 32000},
        {make: 'Porsche', model: 'Boxter', price: 72000}
    ];

    export default {
        name: 'AutoRefreshGridExample',
        data() {
            return {
                columnDefs: [
                    {
                        field: 'make'
                    },
                    {
                        field: 'model'
                    },
                    {
                        headerName: "Auto Refresh Renderer",
                        field: 'price',
                        cellRendererFramework: 'AutoRefreshCellRenderer',
                        onCellDoubleClicked: (params) => {
                            const newStore = store.map(row => {
                                return {
                                    ...row,
                                    price: ~~(Math.random() * 100)
                                };
                            });

                            params.api.setRowData(newStore);

                            // will destroy and re-create component, so not useful
                            // in this example
                            // node.setDataValue(column.colId, value * 10);
                        }
                    },
                ],
                rowData: store,
                components: {
                    AutoRefreshCellRenderer
                }
            }
        },
        components: {
            AgGridVue,
            AutoRefreshCellRenderer
        },
        beforeMount() {
        },
        methods: {
            onFirstDataRendered(params) {
                params.api.sizeColumnsToFit();
            }
        }
    }
</script>

<style lang="css">
    @import '~ag-grid-community/dist/styles/ag-grid.css';
    @import '~ag-grid-community/dist/styles/ag-theme-balham.css';
</style>