<template>
  <div class="item px-3 py-1">
    <h1 class="title">{{data.title}}</h1>
    <p class="desc">{{data.desc}}</p>
    <div class="text-right mb-2">
        <button class="btn btn-outline-danger" @click="del">삭제</button>
        <button class="btn btn-outline-primary" @click="mod">수정</button>
    </div>
  </div>
</template>

<script>

export default {
  name: "child",
  props: ['data'],
  methods:{
      del(){
          this.$emit("del");
      },
      mod(){
          this.$emit("mod");
      }
  }
};
</script>

<style>
.item {
  margin-bottom: 10px;
  border: 1px solid #ddd;
  border-radius: 0.5rem;
  display: flex;
  flex-direction: column;
}

.item > .title {
  font-size: 30px;
  color: rgba(0, 0, 255, 0.8);
}

.item > .desc {
  margin-top: 10px;
  color: #777;
}
</style>