<template>
    <div>
 <div id="demo">
   
    <li v-for="(item, index) in itemlist" v-bind:key="item">
      <label
        > <input
          type="checkbox"
          :value="index"
          name="condiment"
          v-model="selected"
          :disabled="
            selected.length >= max && selected.indexOf(index) == -1
          "
        />
        {{ item }}</label
      >
    </li>
    <div>{{ selected.join(", ") }}</div>
  </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      selected: [],
      itemlist: ["Mayo", "Ketchup", "Mustard", "Honey"],
      max: 1,
    };
  },
};
</script>

<style lang="scss" scoped>
label {
  display: block;
}
</style>
