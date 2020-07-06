<template>
    <el-form label-width="80px">
        <template v-for="ctrl in formObject.form">
            <el-form-item :label="ctrl.label">
                <form-item-component :ctrl=ctrl :fn=fn :formData=formData></form-item-component>
            </el-form-item>
        </template>
    </el-form>
</template>
<script>
import formItemComponent from './formItemComponent'
export default {
    props: ['formJson', 'fn'],
    components: {
        'form-item-component': formItemComponent
    },
    created() {
        this.initFormData()
    },
    data(){
        return {
            formData:{

            }
        }
    },
    methods: {
        initFormData(){
            console.log('show')
            console.log(this.formObject)
            this.formObject.form.forEach(item => {
                if(item.vmname) this.formData[item.vmname] = null
            })
        },
        responseData(){
            //深拷贝返回
            let data = {...this.formData}
            this.$emit("getData", data)
        }
    },
    computed: {
        formObject() {
            if(this.formJson) return this.formJson
            else return {}
        }
    }
}
</script>