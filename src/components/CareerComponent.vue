<template>
  <div class="row" style="width: 1200px">
    <div class="header col-3" style="font-size: 2rem; color: darkslateblue">
      {{ props.header }}
    </div>
    <div class="main col">
      <div class="row" v-for="(con, cIdx) in props.mainContents" :key="cIdx">
        <div
          class="caption q-mx-sm q-mb-sm q-px-sm"
          ref="captionRef"
          :style="{ minWidth: captionWidth + 'px' }"
          style="border-radius: 10px; border: 1px solid grey; color: grey"
        >
          {{ con.caption }}
        </div>
        <div class="content">
          {{ con.content }}
        </div>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { PropType, computed, nextTick, onMounted, ref } from 'vue';

export interface CareerMainContents {
  caption: string;
  content: string;
}

const props = defineProps({
  header: {
    type: String,
    required: true,
  },
  mainContents: {
    type: Array as PropType<CareerMainContents[]>,
    required: true,
  },
});

const captionRef = ref([]);
const captionWidth = ref(0);

function getCaptionWidth() {
  captionRef.value.forEach((item: any, index) => {
    const offsetWidth: number = item.offsetWidth;
    if (captionWidth.value < offsetWidth) {
      captionWidth.value = offsetWidth;
    }
  });
}

onMounted(() => {
  nextTick(() => {
    getCaptionWidth();
  });
});
</script>
