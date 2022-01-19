<template>
    <div ref="el">
        <nodeHeader  title="Script"/>
        <p>Number</p>
        
        <br>
        <el-input v-model="number" df-url placeholder="Type your number" size="small" >
            <template #prepend>Number is:</template>
        </el-input>
    </div>
</template>
<script>
import { defineComponent, onMounted, getCurrentInstance, readonly, ref, nextTick } from 'vue'
import nodeHeader from './nodeHeader.vue'

export default defineComponent({
    components: {
        nodeHeader
    },
    setup(){
        const el = ref(null);
        const nodeId = ref(0);
        let df = null
        const number = ref('');
        const method = ref('get');
        const dataNode = ref({});

        df = getCurrentInstance().appContext.config.globalProperties.$df.value;

        onMounted(async () => {
            await nextTick()
            nodeId.value = el.value.parentElement.parentElement.id.slice(5)
            dataNode.value = df.getNodeFromId(nodeId.value)
            
            number.value = dataNode.value.data.number;
            method.value = dataNode.value.data.method;
        });

        return {
            el, number, method
        }
    }

})



</script>