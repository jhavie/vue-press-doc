<template>
    <generator :formJson=json :fn={testFunc} @getData="showData"></generator>
</template>
<script>
import generator from './generator'
import formJson from '../mock.json'
export default {
    components:{
      generator
    },
    data(){
        return {
        }
    },
    methods: {
        showData(data){
            console.log(data)
        },
        testFunc() {
            console.log(111)
        },
        testFunc222(){
            console.log(222)
        }
    },
    computed: {
        json(){
            return formJson
        }
    }
}
</script>