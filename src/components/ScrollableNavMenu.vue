<template>
  <div
    class="relative px-10 py-6 rounded-lg w-[1100px] bg-green-200 shadow-[rgba(100,_100,_111,_0.2)_0px_7px_29px_0px] overflow-hidden"
  >
    <div
      @click="left"
      ref="leftIconRef"
      class="icon-left absolute top-0 left-0 h-full w-[150px] hidden items-center pl-4 bg-gradient-to-r from-green-200 to-transparent"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 20 20"
        fill="currentColor"
        class="size-12 text-green-600 leading-[3rem] text-center rounded-full text-[1.3rem] cursor-pointer transition-all border border-transparent hover:bg-green-100"
      >
        <path
          fill-rule="evenodd"
          d="M11.78 5.22a.75.75 0 0 1 0 1.06L8.06 10l3.72 3.72a.75.75 0 1 1-1.06 1.06l-4.25-4.25a.75.75 0 0 1 0-1.06l4.25-4.25a.75.75 0 0 1 1.06 0Z"
          clip-rule="evenodd"
        />
      </svg>
    </div>
    <ul
      ref="menuRef"
      class="flex gap-5 overflow-x-hidden scroll-smooth"
      @mousedown="isDragging = true"
      @mousemove="drag"
      @mouseup="stopDrag"
    >
      <li
        v-for="menuItem in list"
        :key="menuItem"
        @click="() => setItem(menuItem)"
        :class="[
          menuItem === item
            ? 'border-green-700 text-green-50 bg-green-700'
            : '',
        ]"
        class="select-none border border-green-500 rounded-lg px-2 py-1 cursor-pointer text-green-900"
      >
        {{ menuItem }}
      </li>
    </ul>
    <div
      @click="right"
      ref="rightIconRef"
      class="icon-right absolute top-0 right-0 h-full w-[150px] flex items-center pr-4 justify-end bg-gradient-to-l from-green-200 to-transparent"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 20 20"
        fill="currentColor"
        class="size-12 text-green-600 leading-[3rem] text-center rounded-full text-[1.3rem] cursor-pointer transition-all border border-transparent hover:bg-green-100"
      >
        <path
          fill-rule="evenodd"
          d="M8.22 5.22a.75.75 0 0 1 1.06 0l4.25 4.25a.75.75 0 0 1 0 1.06l-4.25 4.25a.75.75 0 0 1-1.06-1.06L11.94 10 8.22 6.28a.75.75 0 0 1 0-1.06Z"
          clip-rule="evenodd"
        />
      </svg>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, toRefs } from "vue";
const props = defineProps<{
  list: string[];
  item: string;
  scrollDistance: number;
}>();
const { list, item, scrollDistance } = toRefs(props);
const emit = defineEmits<{ (e: "update:item", payload: string): void }>();
const isDragging = ref<boolean>(false);
const menuRef = ref();
const leftIconRef = ref();
const rightIconRef = ref();

const drag = (el: any) => {
  if (!isDragging.value) return;
  menuRef.value.classList.remove("scroll-smooth");
  el.target.classList.add("scroll-auto");
  el.target.scrollLeft -= el.movementX;
  setTimeout(() => toggleIcons(), 40);
};
const stopDrag = (el: any) => {
  isDragging.value = false;
  menuRef.value.classList.add("scroll-smooth");

  el.target.classList.remove("scroll-auto");
};

const left = () => {
  menuRef.value.scrollLeft -= scrollDistance.value;
  setTimeout(() => toggleIcons(), 40);
};

const right = () => {
  menuRef.value.scrollLeft += scrollDistance.value;
  setTimeout(() => toggleIcons(), 40);
};

const toggleIcons = () => {
  let scroll = menuRef.value.scrollLeft;
  let maxScroll = menuRef.value.scrollWidth - menuRef.value.clientWidth;
  if (scroll > 0) {
    leftIconRef.value.style.display = "flex";
  } else {
    leftIconRef.value.style.display = "none";
  }

  if (maxScroll > scroll) {
    rightIconRef.value.style.display = "flex";
  } else {
    rightIconRef.value.style.display = "none";
  }
};

const setItem = (item: string) => {
  emit("update:item", item);
};
</script>
