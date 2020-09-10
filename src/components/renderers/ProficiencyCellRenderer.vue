<template>
    <div class="div-percent-bar" :style="{width: `${params.value}%`, backgroundColor: backgroundColor }">
        <div class="div-percent-value">{{params.value}}%</div>
    </div>
</template>

<script>
    export default {
        name: 'ProficiencyCellRenderer',
        data() {
            return {
                backgroundColor: []
            }
        },
        beforeMount() {
            if (this.params.value < 20) {
                this.backgroundColor = 'red';
            } else if (this.params.value < 60) {
                this.backgroundColor = '#ff9900';
            } else {
                this.backgroundColor = '#00A000';
            }
        }
    }
</script>

<style scoped>
    .div-percent-bar {
        display: inline-block;
        height: 100%;
        position: relative;
    }

    .div-percent-value {
        position: absolute;
        padding-left: 4px;
        font-weight: bold;
        font-size: 13px;
    }
</style>
