<template>
    <button type="button"  @click = "this.$emit('setValue',0);" > show all tasks  </button>
    <button type="button"  @click = "this.$emit('setValue',1);" > show done tasks </button>
    <button type="button"  @click = "this.$emit('setValue',2);" > show undone tasks </button>
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