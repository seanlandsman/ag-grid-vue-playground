<template>
    <div>
        <div v-if="params.enableMenu" ref="menuButton" class="customHeaderMenuButton" @click="onMenuClicked($event)"><i
                class="fa" :class="params.menuIcon"></i></div>
        <div class="customHeaderLabel">{{params.displayName}}</div>
        <div v-if="params.enableSorting" @click="onSortRequested('asc', $event)" :class="ascSort"
             class="customSortDownLabel"><i class="fa fa-long-arrow-down"></i></div>
        <div v-if="params.enableSorting" @click="onSortRequested('desc', $event)" :class="descSort"
             class="customSortUpLabel"><i class="fa fa-long-arrow-up"></i></div>
        <div v-if="params.enableSorting" @click="onSortRequested('', $event)" :class="noSort"
             class="customSortRemoveLabel"><i class="fa fa-times"></i></div>
    </div>
</template>

<script>
    export default {
        name: 'SortableHeaderComponent',
        data: function () {
            return {
                ascSort: null,
                descSort: null,
                noSort: null
            };
        },
        mounted() {
            this.params.column.addEventListener('sortChanged', this.onSortChanged);
            this.onSortChanged();
        },
        methods: {
            onMenuClicked() {
                this.params.showColumnMenu(this.$refs.menuButton);
            },

            onSortChanged() {
                this.ascSort = this.descSort = this.noSort = 'inactive';
                if (this.params.column.isSortAscending()) {
                    this.ascSort = 'active';
                } else if (this.params.column.isSortDescending()) {
                    this.descSort = 'active';
                } else {
                    this.noSort = 'active';
                }
            },

            onSortRequested(order, event) {
                this.params.setSort(order, event.shiftKey);
            }
        }
    }
</script>

<style scoped>
    .customHeaderMenuButton {
        margin-left: 4px;
        float: left;
    }

    .customHeaderLabel {
        margin-left: 5px;
        float: left;
    }

    .customSortDownLabel {
        float: left;
        margin-left: 10px;
    }

    .customSortUpLabel {
        float: left;
        margin-left: 3px;
    }

    .customSortRemoveLabel {
        float: left;
        font-size: 11px;
        margin-left: 3px;
    }
</style>