<template>
    <div>
        <declarative-grid-example></declarative-grid-example>
        <hr>
        <model-driven-grid-example></model-driven-grid-example>
        <hr>
        <auto-refresh-grid-example></auto-refresh-grid-example>
    </div>
</template>

<script>
    import DeclarativeGridExample from './components/DeclarativeGridExample';
    import ModelDrivenGridExample from './components/ModelDrivenGridExample';
    import AutoRefreshGridExample from './components/AutoRefreshGridExample';
    export default {
        name: 'App',
        components: {
            DeclarativeGridExample,
            ModelDrivenGridExample,
            AutoRefreshGridExample
        }
    }
</script>

