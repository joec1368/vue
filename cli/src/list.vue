<template>
    <h3>tasks:{{undoneTasks}} tasks Done:{{doneTasks}} </h3>
    <h4></h4>
    <button type="button" @click="deleteAllNodes" > tasks byebye </button>
    <button type="button" @click="deleteDoneNode"> done tasks byebye </button>
    <h4></h4>
    <buttonDecideElementToShow :value="this.value" @setValue = "setValue"></buttonDecideElementToShow>
    
    <button type="button" @click="create">add</button>
    <input v-model="message"> {{message}}

    <div v-for="element in decideWhatToShow" :key="element.time">
        <buttonToggleElementState  :time="element.time" :aaaa="element.isActive" :target="element.message" @toggleElementState="toggleElementState" :key="element.time"></buttonToggleElementState>
        <buttonDeleteCertainElement :time="element.time" @deleteCertainNode="deleteCertainNode" :key="element.time"></buttonDeleteCertainElement>>
        <buttonFixElementName :time="element.time" :target="element.message" @fixElementName="fixElementName" :key="element.time"></buttonFixElementName>
    </div>

</template>


<script>
    import buttonToggleElementState from './components/toggleElementState.vue'
    import buttonFixElementName from './components/fixElementName.vue'
    import buttonDeleteCertainElement from './components/deleteCertainElement.vue'
    import buttonDecideElementToShow from './components/decideElementToShow'

    export default{
        name:'listToDoList',
        components: {
            buttonToggleElementState,
            buttonDeleteCertainElement,
            buttonFixElementName,
            buttonDecideElementToShow
        },
    data() {
        return{
            message : "temp",
            value: 0,
            undoneTasks: 0,
            doneTasks: 0, 
            list: []
        }
    },
    methods: {
        setValue(newvalue){
            this.value = newvalue;
        },
        forceToUpdate(){
              for (var y = 0; y < this.list.length; y++) {
                this.list[y].time += 1;
            }
            this.countElementNumber();
        },
        countElementNumber() {
            this.undoneTasks = 0;
            this.doneTasks = 0;
            if (this.list.length == 0);
            else {
                var i = 0;
                for (; i < this.list.length; i++) {
                    if (this.list[i].isActive == false) this.undoneTasks++;
                    else this.doneTasks++;

                    }
                }
            },
        toggleElementState(message) {
            console.log("receive state");
            var i = 0;
            for (; i < this.list.length; i++) {
                if (this.list[i].time == message) break;
            }
            var temp_active = !this.list[i].isActive;
            console.log(temp_active);
            let arr = this.list.slice();
            arr[i].isActive = temp_active;
            this.list = arr;
            this.forceToUpdate();    
            this.countElementNumber();
        },
        deleteAllNodes() {
            this.list.splice(0, this.list.length);
            this.countElementNumber();

        },
        deleteCertainNode(message) {
            console.log(message);
            var i = 0;
            for(; i <this.list.length ; i++){
                if(message == this.list[i].time) break;
            }
            this.list.splice(i, 1);
            this.countElementNumber();
            console.log(this.list);
        },
        deleteDoneNode() {
            if (this.list.length == 0); 
            else {
                var i = 0;
                for (; i < this.list.length; i++) {
                    if (this.list[i].isActive) this.list.splice(i--, 1);

                }
            }
            this.countElementNumber();
        },
        create() {
            var time = Date.now();
            this.list.push({
                "message": this.message,
                "time": time,
                "isActive": false
            })
            this.countElementNumber();
        },
        fixElementName(update) {
            console.log("get");
            var i = 0;
            for (; i < this.list.length; i++) {
                if (this.list[i].time == update[0].time) break;
            }
            this.list[i].message = update[0].newmessage;
            this.forceToUpdate();           
        }
    },
    computed: {
        decideWhatToShow () {
            if (this.value == 0) return this.list;
            else if (this.value == 1) return this.list.filter(i => i.isActive === true);
            else if (this.value == 2) return this.list.filter(i => i.isActive === false);
            else return this.list; 
        },
    }
        
}

</script>


<style>
</style>