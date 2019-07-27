<template>
    <div :class="`ticket num-0${num}`" :data-id="num">
        <input type="button" v-for="item in 20" :key="item" :value="item" @click="onClickInner" class="ticket__item"/>
    </div>
</template>

<script>
export default {
    data(){
        return {

        }
    },
    props: {
        num: Number
    },
    methods:{
        onClickInner() {
            let el=event.target;
            let valueId=this.num;
            this.$emit('onClick', {el,valueId});
        },
    }
}
</script>

<style>

</style>
