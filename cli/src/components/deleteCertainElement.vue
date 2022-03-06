<template>
    <button type="button" @click="this.$emit('deleteCertainNode',newtime);">delete</button>
</template>

<script>

export default{
    name : 'buttonDeleteCertainElement',
    props: ['time'],
    data() {
        return {
            newtime: this.time
        }
    },
    methods: {
    }
}
</script>


<style>
</style>