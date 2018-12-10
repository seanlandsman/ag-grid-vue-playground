<template>
    <div>
        <ag-grid-vue style="width: 500px; height: 200px;"
                     class="ag-theme-balham"
                     :columnDefs="columnDefs"
                     :rowData="rowData"
                     :components="components"
                     autoParamsRefresh
                     :deltaRowDataMode="deltaRowDataMode"
                     :getRowNodeId="getRowNodeId"
                     :firstDataRendered="this.onFirstDataRendered">
        </ag-grid-vue>
    </div>
</template>

<script>
    import {AgGridVue} from "ag-grid-vue";
    import AutoRefreshCellRenderer from "./components/AutoRefreshCellRenderer";

    import '../node_modules/ag-grid-community/dist/styles/ag-grid.css'
    import '../node_modules/ag-grid-community/dist/styles/ag-theme-balham.css'

    const store = [
        {make: 'Toyota', model: 'Celica', price: 35000},
        // {make: 'Ford', model: 'Mondeo', price: 32000},
        // {make: 'Porsche', model: 'Boxter', price: 72000}
    ];

    export default {
        name: 'App',
        data() {
            return {
                deltaRowDataMode: true,
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

                            console.log(store[0].price, newStore[0].price);
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
            },
            getRowNodeId(data) {
                return data.make;
            }
        }
    }
</script>

<style scoped>
</style>