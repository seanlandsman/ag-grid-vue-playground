<template lang="html">
    <div>
        <h1>Declarative Grid Example</h1>
        <ag-grid-vue
                class="ag-theme-balham"
                style="width: 700px; height: 400px;"
                :rowData="rowData"

                :sideBar="sideBar"
                :quickFilterText="quickFilterText"
                :icons="icons"

                suppressRowClickSelection
                rowSelection="multiple"
                enableColResize
                enableSorting
                enableFilter
                floatingFilter
                groupHeaders

                :defaultColDef="{
                    headerComponentFramework: 'SortableHeaderComponent',
                    headerComponentParams: {
                        menuIcon: 'fa-bars'
                    }
                }"

                dateComponentFramework="DateComponent">
            <ag-grid-column headerName="#" :width="30" checkboxSelection :sortable="false" suppressMenu :filter="false"
                            pinned="left"></ag-grid-column>
            <ag-grid-column headerName="Employee" headerGroupComponentFramework="HeaderGroupComponent">
                <ag-grid-column field="name" :width="150" enableRowGroup enablePivot pinned="left" editable></ag-grid-column>
                <ag-grid-column field="country" :width="150"
                                :cellRenderer="countryCellRenderer"
                                :filterParams="{
                                    cellRenderer: countryCellRenderer,
                                    cellHeight: 20
                                }"
                                enableRowGroup enablePivot pinned="left" editable></ag-grid-column>
                <ag-grid-column field="dob" :width="205" headerName="DOB" filter="agDateColumnFilter"
                                pinned="left" columnGroupShow="open"
                                :cellRenderer="dateCellRenderer"></ag-grid-column>
            </ag-grid-column>
            <ag-grid-column headerName="IT Skills">
                <ag-grid-column field="skills" :width="120" enableRowGroup enablePivot :sortable="false"
                                cellRendererFramework="SkillsCellRenderer" :menuTabs="['filterMenuTab']"
                                filterFramework="SkillFilter"></ag-grid-column>
                <ag-grid-column field="proficiency" :width="135" enableValue
                                cellRendererFramework="ProficiencyCellRenderer" :menuTabs="['filterMenuTab']"
                                :filter="ProficiencyFilter"></ag-grid-column>
            </ag-grid-column>
            <ag-grid-column headerName="Contact">
                <ag-grid-column field="mobile" :width="150" filter="agTextColumnFilter"></ag-grid-column>
                <ag-grid-column field="landline" :width="150" filter="agTextColumnFilter"></ag-grid-column>
                <ag-grid-column field="address" :width="500" filter="agTextColumnFilter"></ag-grid-column>
            </ag-grid-column>
        </ag-grid-vue>
    </div>
</template>
<script>
    import {AgGridVue} from "ag-grid-vue";

    import DateComponent from "./renderers/DateComponent"
    import HeaderGroupComponent from "./renderers/HeaderGroupComponent"
    import SortableHeaderComponent from "./renderers/SortableHeaderComponent"
    import SkillsCellRenderer from "./renderers/SkillsCellRenderer"
    import ProficiencyCellRenderer from "./renderers/ProficiencyCellRenderer"
    import RowDataFactory from "./utils/RowDataFactory";
    import RefData from "./utils/RefData";
    import {ProficiencyFilter} from "./filters/proficiencyFilter";
    import SkillFilter from "./renderers/SkillFilter";

    import 'ag-grid-enterprise';

    export default {
        name: 'DeclarativeGridExample',
        data() {
            return {
                quickFilterText: null,
                sideBar: false,
                rowData: new RowDataFactory().createRowData(),
                icons: {
                    columnRemoveFromGroup: '<i class="fa fa-remove"/>',
                    filter: '<i class="fa fa-filter"/>',
                    sortAscending: '<i class="fa fa-long-arrow-down"/>',
                    sortDescending: '<i class="fa fa-long-arrow-up"/>',
                    groupExpanded: '<i class="fa fa-minus-square-o"/>',
                    groupContracted: '<i class="fa fa-plus-square-o"/>'
                },
                ProficiencyFilter
            };
        },
        beforeMount() {
        },
        components: {
            AgGridVue,
            DateComponent,
            HeaderGroupComponent,
            SortableHeaderComponent,
            SkillsCellRenderer,
            ProficiencyCellRenderer,
            SkillFilter
        },
        methods: {
            dobFilter() {
                let dateFilterComponent = this.api.getFilterInstance('dob');
                dateFilterComponent.setModel({
                    type: 'equals',
                    dateFrom: '2000-01-01'
                });

                this.api.onFilterChanged();
            },

            countryCellRenderer(params) {
                if (params.value) {
                    return `<img border='0' width='15' height='10' style='margin-bottom: 2px' src='http://flags.fmcdn.net/data/flags/mini/${RefData.COUNTRY_CODES[params.value]}.png'> ${params.value}`;
                } else {
                    return null;
                }
            },

            dateCellRenderer(params) {
                return this.pad(params.value.getDate(), 2) + '/' +
                    this.pad(params.value.getMonth() + 1, 2) + '/' +
                    params.value.getFullYear();
            },
            pad(num, totalStringSize) {
                let asString = num + "";
                while (asString.length < totalStringSize) asString = "0" + asString;
                return asString;
            }
        }
    };
</script>
<style lang="css">
    @import "~ag-grid-community/dist/styles/ag-grid.css";
    @import "~ag-grid-community/dist/styles/ag-theme-balham.css";

    @import 'http://maxcdn.bootstrapcdn.com/font-awesome/4.2.0/css/font-awesome.min.css';
</style>