<template>
    <div>
        <v-textarea
        solo
        v-model="memo"
        label="Todo List를 입력하세요" />
        <v-btn @click="listAdd" v-if="mode==='add'">TODO LIST ADD</v-btn>
        <v-btn @click="listEdit" v-else>TODO LIST EDIT</v-btn>
    </div>
</template>

<script>
import {eventBus} from '../main';

export default {
    data() {
        return{
            memo: null,
            index: null,
            mode: 'add'
        }
    },
    created() {
        eventBus.$on('listEdit', (memo, index) => {
            this.mode = 'edit'
            this.memo = memo;
            this.index = index;
        });
    },
    methods: {
        listAdd() {
            if(this.memo === null) {
                alert("할일을 입력해주세요");
            } else {
                this.$emit('listAdd', this.memo); 
                this.memo = null
            }
        },
        listEdit() {
            if(this.memo === null) {
                alert("할일을 입력해주세요");
            } else {
                this.$emit('listEdit', this.memo, this.index); 
                this.memo = null
                this.mode = 'add'
            }
        }
    }
}
</script>