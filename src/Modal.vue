<template>
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <img :src="원룸들[누른거].image" style="width:100%">
      <h4>{{원룸들[누른거].title}}</h4>
      <p>{{원룸들[누른거].content}}</p>
      <input v-model.number="month">
      <!-- <input type="range" min="1" max="12"> -->
      <p>{{month}}개월 선택함 : {{원룸들[누른거].price * month}}원</p>
      <button @click="$emit('CloseModal', false)">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
    name: 'ModalComponent',
    data(){
        return {
            month : 1,
        }
    },
    watch : {
        month(a){
            if (a >= 13){
                alert("12이하의 숫자를 입력해주세요.")
                this.month = 1;
            } 
            
            if (typeof a == "string"){
                alert("숫자를 입력해주세요")
                this.month = 1;
            }
        }
    },
    props: {
        원룸들 : Array,
        누른거 : Number,
        모달창열렸니 : Boolean,
    },

    beforeUpdate() {
        if (this.month < 3){
            alert('3개월 이상만 가능합니다.');
            this.month = 3;
        }
    },

}
</script>

<style>

</style>