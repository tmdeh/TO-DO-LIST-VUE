<template>
    <div>
        <v-card 
            class="pa-3 mb-3"
            :class="{'done' : list.status === 'done'}"
            v-for="(list, index) in todoList"
            :key="index"
        >
            <p>{{list.memo}}</p>
            <v-btn fab flat small color="green" 
            v-if="list.status==='created'"
            @click="$emit('statusControl', index, 'done')">완료</v-btn>
            
            <v-btn fab flat small color="blue"
            v-else 
            @click="$emit('statusControl', index, 'created')">부활</v-btn>
            
            <v-btn fab flat small color="red"
            @click="$emit('listDelete', index)">제거</v-btn>

            <v-btn fab flat small color="yellow"
            v-if="list.status === 'created'"
            @click="listEdit(list.memo, index)">수정</v-btn>
        </v-card>
    </div>
</template>

<script>
import {eventBus} from '../main';

export default {
    props : ["todoList"],
    methods: {
        listEdit(memo, index) {
            eventBus.listEdit(memo, index)
        }
    }
}
</script>


// 여기만 style이 적용됨
<style scoped>
.done {
    background-color: rgba(0, 0, 0, 0.1);
}

.done p {
    text-decoration: line-through;
    color: rgba(0, 0, 0, 0.5);
}
</style>