<template>
    <input v-model="premessage">
    <button type = "button" @click = "fixElementName();"> fixElementName </button>
</template>

<script>
export default{
    name : 'buttonFixElementName',
    props: ['target', 'time'],
    data() {
        return {
            message: this.target,
            premessage: "none",
            newtime: this.time
        }
    },
    methods: {
        fixElementName() {
            var update = [];
            this.message = this.premessage;
            update.push({
                "time": this.newtime,
                "newmessage": this.premessage,
                "oldmessage": this.message,
            });
            console.log("send");
            this.$emit('fixElementName', update);
            
        }
    }
}
</script>


<style>
.done {
  color: red;
}
</style>