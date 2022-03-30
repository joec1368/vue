<template>
    <button type="button"  @click = "this.$emit('setValue','all');" > show all tasks  </button>
    <button type="button"  @click = "this.$emit('setValue','done');" > show done tasks </button>
    <button type="button"  @click = "this.$emit('setValue','undone');" > show undone tasks </button>
    <h4></h4>
</template>


<script>

    export default{
        name:'buttonDecideElementToShow',
        components: {
        },
    props: ['value'],
    data() {
        return{
            setValue : this.value
        }
    },
    methods: {

    },
    computed: {
    }
        
}

</script>


<style>
</style>