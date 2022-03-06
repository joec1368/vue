<template>
    <button type = "button" @click = "this.$emit('toggleElementState',newtime);"  >Ok</button>
    <span v-if="Active" class = "done">{{message}}</span>
    <span v-else >{{message}}</span>
</template>

<script>

export default{
    name : 'buttonToggleElementState',
    props: ['target', 'aaaa', 'time'],
    data() {
        return {
            Active: this.aaaa,
            message: this.target,
            premessage: "none",
            newtime: this.time
        }
    },
    methods: {
    }
}
</script>


<style>
.done {
  color: red;
}
</style>