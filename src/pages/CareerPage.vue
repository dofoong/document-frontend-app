<template>
  <div>
    <div>Career</div>
    <div class="flex flex-center">
      <career-component
        v-for="(carr, caIdx) in Careers"
        :key="caIdx"
        :header="carr.haeder"
        :main-contents="carr.mainContents"
      />
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue';
import CareerComponent, {
  CareerMainContents,
} from 'src/components/CareerComponent.vue';

export interface careerListModel {
  haeder: string;
  mainContents: CareerMainContents[];
}

const Careers = ref([
  {
    haeder: 'PROFILE',
    mainContents: [
      {
        caption: 'CAPTION test4',
        content: 'CONTENT test1',
      },
      {
        caption: 'CAPTION test4545454',
        content: 'CONTENT test2',
      },
    ],
  },
] as careerListModel[]);
</script>
