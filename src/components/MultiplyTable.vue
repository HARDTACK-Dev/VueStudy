<template>
  <div class="Container">
    <div class="Header">
      <h1 class="title">Multiply Table</h1>

      <div class="input-section">
        <input class="input" type="number" v-model="number" />
        <button class="submit" @click="add">+ 추가</button>
      </div>
    </div>
    <div class="Body">
      <div class="card" v-for="(number, index) in array" v-bind:key="number">
        <div class="card-header flex">
          <h3 class="x-level">{{ number }}단</h3>

          <div class="buttons flex">
            <div class="btn modify" @click="modify(index)">수정</div>
            <div class="btn delete" @click="remove(index)">삭제</div>
          </div>
        </div>
        <div class="item" v-for="item in 9" v-bind:key="item">
          {{ number }} x {{ item }} = {{ number * item }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      number: null,
      array: [],
    };
  },

  methods: {
    add: function() {
      if (this.number == null){
        alert("숫자를 입력해주세요!");
        return;
      }
      if (this.array.includes(this.number))
        alert("이미 해당하는 단이 존재합니다!");
      else this.array.push(this.number);
        
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@font-face {
  font-family: "RixYeoljeongdo_Regular";
  src: url("https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2102-01@1.0/RixYeoljeongdo_Regular.woff")
    format("woff");
  font-weight: normal;
  font-style: normal;
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
  width: 300px;
  height: 500px;

  background-color: rgb(252, 252, 252);
  border: 0.5px solid rgb(228, 228, 228);
}

.card-header {
  width: 100%;
  height: 40px;

  justify-content: space-between;
  background-color: rgb(235, 235, 235);
}

.item{
  text-align: center;
  font-family: RixYeoljeongdo_Regular;
}

.btn {
  width: 50px;
  height: 35px;

  text-align: center;
  line-height: 30px;

  color: white;

  border: 1px solid rgb(206, 206, 206);
}

.modify {
  background-color: rgb(236, 244, 250);
}

.delete {
  background-color: rgb(248, 51, 51);
}
</style>
