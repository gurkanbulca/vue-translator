<template>
  <div class="well">
    <h3>Arama Geçmişi</h3>
    <ul class="list-group text-left">
      <li class="list-group-item" v-for="(item,index) in history" :key="index">
        <div>
          <strong>
            {{item.from}}
            <i class="fas fa-long-arrow-alt-right"></i>
            {{item.to}}
          </strong>
        </div>
        <div>
          <strong class="text-success">{{item.text}}</strong>
          <br />
          <span class="text-info">{{item.translatedText}}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["history"]
};
</script>

<style>
</style>