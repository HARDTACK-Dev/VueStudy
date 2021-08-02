<template>
  <div class="container">
    <transition name="fade" appear>
      <div v-if="showModal" class="modal">
      <div class="modal-box">
        <h3 class="modal-title">수정할 값을 입력해주세요!</h3>
        <input 
          type="number" 
          class="modal-input" 
          v-model="modalValue" 
          @keyup.enter="changeTable"
        />

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

    <div class="header">
      <h1 class="title">Multiply Table</h1>

      <div class="input-section">
        <input
          class="input" 
          type="number" 
          v-model="number" 
          @keyup.enter="addTable"
        />
        <button class="submit" @click="addTable">+ 추가</button>
      </div>
    </div>
    <div class="Body">
      <transition-group tag="div" name="plump" class="Body">
        <div class="card" v-for="(number, index) in array" v-bind:key="number" >
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
      this.array.splice(index, 1);
    },

    //구구단 수정
    changeTable: function() {
      if(this.modalValue == null)
        return;
      if(this.array.includes(this.modalValue))
        return;

      this.array.splice(this.modalIndex, 1, this.modalValue);

      this.closeModal = true;
    },

    //모달 열기
    openModal: function(index) {
      this.showModal = true;
      this.modalIndex = index;
    },
  },
};
</script>

<style scoped>
@import '../css/animation.css';
@import '../css/toast.css';
@import '../css/modal.css';

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

.container {
  width: 100vw;
  height: 100vh;
}

.flex {
  display: flex;
}

.header {
  width: 100%;
  height: 200px;

  background-color: rgb(231, 231, 231);

  border-bottom: 1px solid #aaa;

  transition: 0.5s ease-in-out;
}

.header:hover {
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
