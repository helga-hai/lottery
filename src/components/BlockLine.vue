<template>
    <div class="block" :id="id">
        <div class="block__line" @click="onPass" :blockId="blockId">
            <slot></slot>
        </div>
        <slot name="controls"></slot>
    </div>
</template>

<script>
export default {
    props:{
        blockId:Number,
        id:Number
    },
    methods:{
        onPass(){
            this.$emit('onClickLine',this.blockId)
        }
    }
}
</script>

<style>

</style>
