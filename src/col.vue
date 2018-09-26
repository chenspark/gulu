<template>
    <div class="col"
         :class="colClass"
         :style="colStyle">
        <div style="border: 1px solid green;">
            <slot></slot>
        </div>
    </div>
</template>
<script>
    // 对接到的值进行遍历过滤
    const validator = (value) => {
        let keys = Object.keys(value);
        let valid = true;
        keys.forEach(key => {
            if (!['span', 'offset'].includes(key)) {
                valid = false;
            }
        });
        return valid;
    };
    export default {
        name: "GuluCol",
        props: {
            span: [Number, String],
            offset: [Number, String],
            align: {
                type: String,
                validator(val) {
                    return ['left', 'right', 'center'].includes(val);
                }
            },
            phone: {
                type: Object,
                validator
            },
            ipad: {
                type: Object,
                validator
            },
            narrowPc: {
                type: Object,
                validator
            },
            pc: {
                type: Object,
                validator
            },
            widePc: {
                type: Object,
                validator
            }
        },
        data() {
            return {
                gutter: 0
            }
        },
        methods: {
            creatClasses(obj, str =''){
                if(!obj) return [];
                let array = [];
                if(obj.span){
                    array.push(`col-${str}${obj.span}`);
                }
                if(obj.offset){
                    array.push(`offset-${str}${obj.offset}`)
                }
                return array;
            }
        },
        computed: {
            // 给div增加样式的方法
            colClass() {
                let {span, offset, ipad, narrowPc, pc, widePc} = this;
                let x = this.creatClasses;
                return [
                    ...x({span, offset}),
                    ...x(ipad, 'ipad-'),
                    ...x(narrowPc, 'narrow-pc-'),
                    ...x(pc, 'pc-'),
                    ...x(widePc, 'wide-pc-')
                ]
            },
            colStyle() {
                return {
                    paddingLeft: this.gutter / 2 + 'px',
                    paddingRight: this.gutter / 2 + 'px'
                }
            }
        }
    };
</script>

<style scoped lang="scss">
    .col {
        width: 50%;
        $class-prefix: col-;
        @for $n from 1 through 24 {
            &.#{$class-prefix}#{$n} {
                width: ($n / 24) * 100%;
            }
        }
        $class-prefix: offset-;
        @for $n from 1 through 24 {
            &.#{$class-prefix}#{$n} {
                margin-left: ($n / 24) * 100%;
            }
        }

        @media (min-width: 577px) {
            $class-prefix: col-ipad-;
            @for $n from 1 through 24 {
                &.#{$class-prefix}#{$n} {
                    width: ($n / 24) * 100%;
                }
            }
            $class-prefix: offset-ipad-;
            @for $n from 1 through 24 {
                &.#{$class-prefix}#{$n} {
                    margin-left: ($n / 24) * 100%;
                }
            }
        }

        @media (min-width: 769px) {
            $class-prefix: col-narrow-pc-;
            @for $n from 1 through 24 {
                &.#{$class-prefix}#{$n} {
                    width: ($n / 24) * 100%;
                }
            }
            $class-prefix: offset-narrow-pc-;
            @for $n from 1 through 24 {
                &.#{$class-prefix}#{$n} {
                    margin-left: ($n / 24) * 100%;
                }
            }
        }

        @media (min-width: 993px) {
            $class-prefix: col-pc-;
            @for $n from 1 through 24 {
                &.#{$class-prefix}#{$n} {
                    width: ($n / 24) * 100%;
                }
            }
            $class-prefix: offset-pc-;
            @for $n from 1 through 24 {
                &.#{$class-prefix}#{$n} {
                    margin-left: ($n / 24) * 100%;
                }
            }
        }

        @media (min-width: 1201px) {
            $class-prefix: col-wide-pc-;
            @for $n from 1 through 24 {
                &.#{$class-prefix}#{$n} {
                    width: ($n / 24) * 100%;
                }
            }
            $class-prefix: offset-wide-pc-;
            @for $n from 1 through 24 {
                &.#{$class-prefix}#{$n} {
                    margin-left: ($n / 24) * 100%;
                }
            }
        }

    }
</style>
