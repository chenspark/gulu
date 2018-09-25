<template>
    <div class="row"
         :class="rowClass"
         :style="{marginLeft: -gutter/2 + 'px', marginRight: -gutter/2 + 'px'}">
        <slot></slot>
    </div>
</template>
<script>

    export default {
        name: "GuluRow",
        props: {
            gutter: [Number, String]
        },
        mounted() {
            // 把父级的gutter传到子级
            this.$children.forEach(vm => {
                vm.gutter = this.gutter;
            });
        },
        computed: {
            rowClass() {
                let {align} = this;
                return [align && `align-${align}`];
            }
        }
    };
</script>

<style lang="scss" scoped>
    .row {
        display: flex;
        flex-wrap: wrap;
        &.align-left {
            justify-content: flex-start;
        }
        &.align-right {
            justify-content: flex-end;
        }
        &.align-center {
            justify-content: center;
        }
    }
</style>
