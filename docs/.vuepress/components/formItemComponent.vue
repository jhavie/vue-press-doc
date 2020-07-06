<script>
export default {
    props: ['ctrl', 'fn', 'formData'],
    render(h){
        const self = this
        const ctrl = self.ctrl
        return this.renderMapFn(h, self, ctrl)
        // let config = this.ctrl.config
        // const self = this
        // return renderMap[this.renderTypeCode]
    },
    data() {
        return {
            childCtrl: ''
        }
    },
    methods: {
        renderMapFn(h, self, ctrl){
            const that = this
            console.log(ctrl)
            const renderMap = {
                0: h(self.renderType(ctrl)),
                1: h(self.renderType(ctrl), {
                        style: ctrl.config.style,
                        props: ctrl.config.props,
                        attrs: ctrl.config.attrs,
                        on: self.eventMap(ctrl.config.on)
                    }, ctrl.config.text),
                2: h(self.renderType(ctrl), {
                        style: ctrl.config.style,
                        props: {
                            ...ctrl.config.props,
                            value: self.formData[ctrl.vmname]
                        },
                        attrs: ctrl.config.attrs,
                        on: {
                            ...self.eventMap(ctrl.config.on),
                            input: (event) => {
                                self.formData[ctrl.vmname] = event
                                self.$forceUpdate()
                            }
                        }
                    }, ctrl.config.hasOwnProperty('child') ? [this.renderMapFn(h, that, ctrl.config.child[0])] : [])
            }
            return renderMap[this.renderTypeCode]
        },
        eventMap(on) {
            if(!on) return {}
            //支持传String | Function两种方式
            const _on = {}
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
        renderType(ctrl){
            return `el-${ctrl.type}`
        },
        childRender(){
            let child = this.ctrl.config.child
        }
    },
    computed: {
        childRenderType(){
            console.log(this.ctrl)
        },
        renderTypeCode(){
            //code 0 slot render
            //code 1 simple ex.button
            //code 2 mutiple ex.select
            const simple = [ 'button' ]
            const mutiple = [ 'input', 'select', 'option']
            if(simple.includes(this.ctrl.type)) return 1
            else if(mutiple.includes(this.ctrl.type)) return 2
            else return 0
        }
    }
}
</script>