<template>
  <div class="Container">
    <transition name="fade" appear>
      <div v-if="showModal" class="Modal">
      <div class="modal-box">
        <h3 class="modal-title">수정할 값을 입력해주세요!</h3>
        <input type="number" class="modal-input" v-model="modalValue" />

        <button class="apply" @click="changeTable">적용</button>
        <button class="close" @click="showModal = false">닫기</button>
      </div>
    </div>
    </transition>
    

    <transition name="fadeDrop" appear>
      <div v-if="showToast" class="Toast">
        <p class="msg">{{ toastMsg }}</p>
      </div>
    </transition>

    <div class="Header">
      <h1 class="title">Multiply Table</h1>

      <div class="input-section">
        <input class="input" type="number" v-model="number" />
        <button class="submit" @click="addTable">+ 추가</button>
      </div>
    </div>
    <div class="Body">
      <transition-group tag="div" name="plump" class="Body">
        <div class="card" v-for="(number, index) in array" v-bind:key="number">
          <div class="card-header flex">
            <h3 class="x-level">{{ number }}단</h3>

            <div class="buttons flex">
              <div class="btn modify" @click="openModal(index)">수정</div>
              <div class="btn delete" @click="deleteTable(index)">X</div>
            </div>
          </div>

          <div class="card-body">
            <div class="item" v-for="item in 9" v-bind:key="item">
              {{ number }} x {{ item }} = {{ number * item }}
            </div>
          </div>
        </div>
      </transition-group>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      number: null,
      array: [],

      showToast: false,
      toastMsg: "",

      showModal: false,
      modalValue: null,

      modalIndex: null,
    };
  },

  methods: {
    //구구단 추가
    addTable: function() {
      if (this.number == null || "") {
        this.showToast = true;
        this.toastMsg = "숫자를 입력해주세요";

        setTimeout(() => {
          this.showToast = false;
        }, 1500);

        return;
      }
      if (this.array.includes(this.number)) {
        this.showToast = true;
        this.toastMsg = "이미 해당하는 단이 존재합니다";

        setTimeout(() => {
          this.showToast = false;
        }, 1500);

        return;
      }
      this.array.push(this.number);
    },

    //구구단 삭제
    deleteTable: function(index) {
      console.log(index);
      this.array.splice(index, 1);
    },

    //구구단 수정
    changeTable: function() {
      if(this.modalValue == null)
        return;
      if(this.array.includes(this.modalValue))
        return;

      console.log("옿" + this.modalIndex);
      this.array.splice(this.modalIndex, 1, this.modalValue);

      this.closeModal = true;
    },

    //모달 열기
    openModal: function(index) {
      console.log("모달 열림");
      this.showModal = true;

      this.modalIndex = index;
      console.log(this.modalIndex)
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";

@font-face {
  font-family: "RixYeoljeongdo_Regular";
  src: url("https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2102-01@1.0/RixYeoljeongdo_Regular.woff")
    format("woff");
  font-weight: normal;
  font-style: normal;
}

body {
  overflow-x: hidden;
  overflow-y: scroll;
}

.Modal {
  position: fixed;

  top: 0;
  left: 0;

  width: 100vw;
  height: 100vh;

  background-color: rgba(0, 0, 0, 0.5);
  z-index: 9999;
}

.modal-box {
  width: 450px;
  height: 250px;

  margin: 0 auto;
  margin-top: 200px;

  border-radius: 15px;
  background-color: #fff;
  box-shadow: 5px 5px 10px 5px rgba(0, 0, 0, 0.1);
}

.apply {
  color: blue;
  position: absolute;

  width: 225px;
  height: 50px;

  margin-top: 45px;

  border: none;

  border-radius: 0 0 0 10px;

  cursor: pointer;
  background-color: rgb(237, 234, 255);

  transition: 0.2s ease-in-out;
}

.apply:hover {
  color: white;

  background-color: rgb(71, 88, 243);
  transform: scale(1.05);

  border-radius: 13px;
  z-index: 99;
}

.modify{
  width: 100px;
  height: 35px;

  line-height: 35px;
  border-radius: 30px;

  background-color: rgb(219, 218, 218);
}

.modify:hover{
  color: white;

  background-color: rgb(195, 224, 189);
  transform: scale(1.05);

  border-radius: 13px;
  z-index: 99;
}

/* for modal */
.close {
  color: rgb(255, 67, 67);
  position: absolute;

  width: 225px;
  height: 50px;

  margin-top: 45px;

  float: right;
  border: none;

  margin-left: 225px;

  border-radius: 0 0 10px 0;

  cursor: pointer;
  transition: 0.2s ease-in-out;
}

.close:hover {
  color: white;

  background-color: rgb(243, 71, 71);
  transform: scale(1.05);

  border-radius: 13px;
  z-index: 99;
}

.modal-title {
  display: inline-block;

  text-align: center;
  margin-top: 50px;
  margin-left: 115px;
}

.modal-input {
  display: block;
  margin: 0 auto;

  margin-top: 50px;

  width: 250px;
  height: 35px;

  border-radius: 30px;
  border: none;

  background-color: rgb(233, 233, 233);
}

.Toast {
  position: absolute;
  display: flex;

  top: 10px;
  right: 10px;

  width: 300px;
  height: 80px;

  border-radius: 15px;
  background-color: rgb(255, 78, 78);

  box-shadow: 5px 5px 10px 5px rgba(0, 0, 0, 0.1);
  transition: 0.3s ease-in-out;
}

/* fade effect */
.fade-enter-active,
.fade-leave-active{
  transition: 0.15s ease-in-out;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

/* fadeDrop effect */
.fadeDrop-enter-active {
  transition: 0.15s ease-in-out;
  transform: translateY(-200px);
}
.fadeDrop-leave-active {
  transition: 0.15s ease-in-out;
}

.fadeDrop-enter,
.fadeDrop-leave-to {
  opacity: 0;
}

/* plump effect */
.plump-enter-from {
  opacity: 0;
  transform: scale(1);
}

.plump-enter-to {
  opacity: 1;
  transform: scale(1.1);
}

.plump-enter-active {
  transition: all 0.4s ease-in-out;
}

.msg {
  color: white;

  margin-left: 35px;
  line-height: 80px;
}

.Container {
  width: 100vw;
  height: 100vh;
}

.flex {
  display: flex;
}

.Header {
  width: 100%;
  height: 200px;

  background-color: rgb(231, 231, 231);

  border-bottom: 1px solid #aaa;

  transition: 0.5s ease-in-out;
}

.Header:hover {
  background-color: rgb(255, 227, 227);
  box-shadow: 5px 5px 10px 5px rgba(0, 0, 0, 0.1);
}

.title {
  font-family: RixYeoljeongdo_Regular;
  text-align: center;

  padding-top: 10px;
}

.input {
  display: block;

  width: 300px;
  height: 35px;

  margin: 0 auto;
  margin-top: 35px;

  border: 0.1px solid grey;
  border-radius: 8px;
}

.input:focus {
  outline: none;
}

.submit {
  display: block;
  color: white;

  width: 300px;
  height: 30px;

  margin: 0 auto;
  margin-top: 10px;

  border: none;
  border-radius: 5px;

  font-family: RixYeoljeongdo_Regular;

  background-color: rgb(170, 168, 63);
  transition: 0.15s ease-in-out;
}

.submit:hover {
  background-color: rgb(57, 173, 82);
  transform: scale(1.05);

  cursor: pointer;
}

.card {
  width: 25%;
  height: 400px;

  margin-top: 50px;

  background-color: rgb(252, 252, 252);
  border: 0.5px solid rgb(228, 228, 228);

  border-radius: 10px;
  transition: 0.1s ease-in-out;
  
}

.x-level{
  line-height: 40px;
  margin-left: 20px;
}

.card:hover{
  cursor: pointer;

  box-shadow: 5px 5px 20px 5px rgba(0, 0, 0, 0.1);
  transform: scale(1.03);
}

.card-header {
  width: 100%;
  height: 40px;

  border-radius: 10px;

  justify-content: space-between;
  background-color: rgb(235, 235, 235);
}

.Body {
  width: 100vw;

  display: flex;
  flex-wrap: wrap;

  justify-content: space-around;
}

.item {
  font-size: 20px;

  width: 100%;
  margin-top: 15px;

  text-align: center;
  font-family: RixYeoljeongdo_Regular;
}

.btn {
 

  margin: 1px 2px;

  text-align: center;
  line-height: 35px;

  transition: 0.15s ease-in-out;
}

.delete:hover {
  cursor: pointer;
  transform: scale(1.2);

  width: 35px;
  height: 35px;

  background-color: rgb(172, 57, 57);
}

.delete {
  color: white;

  width: 35px;
  height: 35px; 

  background-color: rgb(248, 51, 51);

  border-radius: 300px;
}

input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

input:focus {
  outline: none;
}
</style>
