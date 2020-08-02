<template>
    <div>
        <ul class="star-container" @mouseleave="handleMouseLeave">
            <!--        亮星-->
            <li v-for="(n,index) of sonSum" :key="index+'a'" class="star-on" @mouseenter="handleMouseEnter(index)" @click="handleMouseClick(index)">
                {{ n }}
            </li>
            <!--        暗星-->
            <li v-for="(n,index) in 5-sonSum" :key="index" class="star-off" @mouseenter="handleMouseEnter(sonSum+index)" @click="handleMouseClick(sonSum+index)">
                {{ sonSum+n }}
            </li>
        </ul>
    </div>
</template>
<script>
    export default {

        props: {
            num: {
                type: Number,
                default: 0
            }
        },
        data() {
            return {
                sonSum: this.num
            }
        },
        methods: {
            handleMouseEnter(index) {
                this.sonSum = index + 1
            },
            handleMouseLeave() {
                this.sonSum = this.num
            },
            handleMouseClick(index) {
                this.$emit('update:num', index + 1)
            }
        }
    }
</script>
<style scoped>
    .star-container{
        display: flex;
        align-items: center;
        list-style: none;
    }
    .star-on,.star-off{
        display: flex;
        align-items: center;
    }
    .star-on::before{
        content: "";
        width: 16px;
        height: 16px;
        background-image: url("../../img/star-on.png");
    }
    .star-off::before{
        content: "";
        width: 16px;
        height: 16px;
        background-image: url("../../img/star-off.png");
    }
</style>
