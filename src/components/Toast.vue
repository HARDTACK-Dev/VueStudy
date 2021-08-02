<template>
    <div class="toast">
        {{errorMsg.alreadyExist}}
    </div>
</template>

<script>
export default {
  data() {
    return {
      errorMsg:  {
          alreadyExist : "해당 하는 단이 이미 존재합니다",
          blankInput : "숫자를 입력해주세요"
      }
    };
  },

  methods: {
   
  },
};
</script>

<style scoped>
.toast{
    position: absolute;
    display: flex;

    top: 10px;
    right: 10px;

    width: 300px;
    height: 80px;

    float: right;

    border-radius: 15px;
    background-color: rgb(255, 78, 78);
}
</style>