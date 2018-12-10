<template>
    <div >
        <div>{{ params.value }}</div>
    </div>
</template>

<script>
    export default {
        name: 'AutoRefreshCellRenderer',
        methods: {
            /* autoParamsRefresh is equivalent to the following:
            refresh(params) {
                this.params = params;
                return false;
            } */
        },
        beforeDestroy() {
            console.log("beforeDestroy");
        }
    }
</script>
