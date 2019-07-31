<template>
  <div>
    <h1>컴포넌트 리스트입니다.</h1>
    <div class="list">
      <transition-group name="gondr" tag="div">
        <child :data="item" :key="item.id" v-for="(item, idx) in list" @del="del(idx)" @mod="mod(idx)"></child>
      </transition-group>
    </div>
    <div class="input-form">
      <input v-model="title" @keydown.enter="send" class="form-control" type="text" placeholder="제목을 입력하세요">
      <textarea v-model="content" @keydown.ctrl.enter="send" rows="5" class="form-control"
          placeholder="내용을입력하세요"></textarea>
      <button v-if="mode == 0" @click="send" class="btn btn-block btn-primary">입력</button>
      <button v-if="mode != 0" @click="send" class="btn btn-block btn-danger">수정</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      list: [
        { id: 1, title: "제목입니다1.", desc: "내용입니다1." },
        { id: 2, title: "제목입니다2.", desc: "내용입니다2." },
        { id: 3, title: "제목입니다3.", desc: "내용입니다3." },
        { id: 4, title: "제목입니다4.", desc: "내용입니다4." }
      ],
      id:5,
      title:'',
      content:'',
      mode:0,  //0번이 입력모드 1번이 수정모드
    };
  },
  methods: {
    del(idx) {
      this.list.splice(idx, 1);
    },
    send(){
      if(this.title.trim() == "" || this.content.trim() == ""){
        alert("값이 비어있습니다.");
        return;
      }

      if(this.mode == 0){
        this.list.push({
          id:this.id++, title:this.title, desc:this.content
        });
      }else{
        let item = this.list.find(x => x.id == this.mode);
        item.title = this.title;
        item.desc = this.content;
        this.mode = 0;
        this.title = "";
        this.content = "";
      }
    },
    mod(idx){
      let item = this.list[idx];
      this.title = item.title;
      this.content = item.desc;
      this.mode = this.list[idx].id;
    }
  }
};
</script>

<style>
.gondr-enter-active,
.gondr-leave-active {
  transition: all 1s;
}

.gondr-enter,
.gondr-leave-to {
  opacity: 0;
  transform: translateX(-100px);
}

.gondr-leave-active {
  position: absolute;
}

.gondr-move {
  transition: transform 1s;
}

.input-form {
            padding: 20px;
        }

.form-control {
    border: 1px solid #ddd;
    padding: 8px 12px;
    width: 100%;
    display: block;
    margin-bottom: 10px;
}

.long-btn {
    width: 100%;
    padding: 8px 12px;
    border: 1px solid rgba(0, 0, 255, 0.8);
    background-color: rgba(0, 0, 255, 0.7);
    color: #fff;
    border-radius: 0.25rem;
}
</style>
