<template>
    <div>
        <immutable-props-grid-example></immutable-props-grid-example>
        <hr>
        <auto-refresh-grid-example></auto-refresh-grid-example>
    </div>
</template>

<script>
    import ImmutablePropsGridExample from './components/ImmutablePropsGridExample';
    import AutoRefreshGridExample from './components/AutoRefreshGridExample';
    export default {
        name: 'App',
        components: {
            ImmutablePropsGridExample,
            AutoRefreshGridExample
        }
    }
</script>

