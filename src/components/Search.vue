<template>
  <div class="search-engine">
    <input
      type="text"
      name="search"
      placeholder="Enter City Name"
      v-model="localSearch"
    />
    <button @click="handleClick">Search</button>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
const props = defineProps({
  search: {
    type: String,
    required: true,
  },
});

//获取传值的值
const localSearch = ref(props.search);

const emit = defineEmits(["updateSearch"]);

watch(
  () => props.search,
  (newVal) => {
    if (newVal !== props.search) localSearch.value = newVal;
  }
);

const handleClick = () => {
  emit("updateSearch", localSearch.value);
  console.log(localSearch.value);
};
</script>

<style lang="scss" scoped>
.search-engine {
  border: none;
  border-radius: 8px;
  width: 100%;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  margin-bottom: 30px;
  margin-top: 10px;
}

.search-engine input {
  width: 20%;
  height: 45px;
  border: none;
  box-shadow: 5px 5px #000;
  border-radius: 8px;
  padding: 2px 15px;
  font-size: 16px;
  outline: none;
  background-color: #fff;
  color: #555;
  transition: width 0.5s ease;
}

.search-engine input:focus {
  width: 70%;
}

.search-engine button {
  box-shadow: 5px 5px #fff;
  border: none;
  border-radius: 8px;
  background-color: #000;
  color: #fff;
  font-size: 20px;
  outline: none;
  cursor: pointer;
  padding: 13px 15px;
  transition: all 0.5s ease;
}

.search-engine button:hover {
  background-color: #fff;
  color: #000;
  box-shadow: 10px 10px #000;
  transform: translateY(5px);
}
</style>
