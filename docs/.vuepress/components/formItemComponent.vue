<script>
export default {
    props: ['ctrl', 'fn', 'formData'],
    render(h){
        let config = this.ctrl.config
        const self = this
        const renderMap = {
            0: h(this.renderType),
            1: h(this.renderType, {
                    style: config.style,
                    props: config.props,
                    attrs: config.attrs,
                    on: this.eventMap(config.on)
                }, config.text),
            2: h(this.renderType, {
                    style: config.style,
                    props: {
                        ...config.props,
                        value: self.formData[self.ctrl.vmname]
                    },
                    attrs: config.attrs,
                    on: {
                        ...this.eventMap(config.on),
                        input: (event) => {
                            self.formData[self.ctrl.vmname] = event
                            this.$forceUpdate()
                        }
                    }
                })
        }
        // return renderMap[3]
        console.log(this.ctrl)
        return renderMap[this.renderTypeCode]
    },
    data() {
        return {
            value: ''
        }
    },
    methods: {
        renderMap() {

        },
        eventMap(on, self) {
            //支持传String | Function两种方式
            let _on = {}
            Object.keys(on).forEach( key => {
                    if(typeof on[key] === 'function'){
                        _on[key] = on[key]
                    }else if (typeof on[key] === 'string'){
                        _on[key] = this.fn[on[key]]
                    }
                }
            )
            return _on
        },
        childRender(){
            let child = this.ctrl.config.child
        }
    },
    computed: {
        renderType(){
            return `el-${this.ctrl.type}`
        },
        childRenderType(){
            console.log(this.ctrl)
        },
        renderTypeCode(){
            //code 0 slot render
            //code 1 simple ex.button
            //code 2 mutiple ex.select
            const simple = [ 'button' ]
            const mutiple = [ 'input', 'select' ]
            if(simple.includes(this.ctrl.type)) return 1
            else if(mutiple.includes(this.ctrl.type)) return 2
            else return 0
        }
    }
}
</script>