<script setup lang="ts">
import { ref } from "vue"

const companyName = ref("บริษัท (ชื่อบริษัท) จำกัด")
const objectives = ref([
  "เพื่อเสนอผลิตภัณฑ์ และ/หรือ บริการของบริษัทที่เหมาะกับความต้องการของท่าน",
])

function addObjective() {
  objectives.value.push("[โปรดระบุวัตถุประสงค์การประมวลผลข้อมูล]")
}

function removeObjective(index: number) {
  if (confirm("ต้องการลบหรือไม่?")) {
    objectives.value.splice(index, 1)
  }
}
</script>

<template>
  <main class="flex flex-col gap-4 p-16 text-xl">
    <section id="form">
      <input type="text" v-model="companyName" class="p-2 rounded border" />

      <ul class="flex flex-col gap-2">
        <li
          v-for="(objective, idx) in objectives"
          class="flex flex-row gap-2"
          :key="idx"
        >
          <input
            type="text"
            v-model="objectives[idx]"
            class="p-2 rounded border"
          />
          <button class="p-2 rounded-border" @click="removeObjective(idx)">
            ลบ
          </button>
        </li>
        <button class="p-2 rounded-border" @click="addObjective">+</button>
      </ul>
    </section>

    <h1 class="text-3xl font-bold text-center mt-16">
      หนังสือให้ความยินยอมในการเก็บรวบรวม/ใช้/เปิดเผยข้อมูลส่วนบุคคล
    </h1>

    <p>
      {{ companyName || "________" }} ("บริษัท")
      ให้ความสำคัญกับความเป็นส่วนตัวของท่าน
      บริษัทจึงขอความยินยอมจากท่านเพื่อการเก็บรวบรวม ใช้
      และ/หรือเปิดเผยข้อมูลส่วนบุคคลของท่านที่ให้ไว้แก้บริษัทหรือที่บริษัทได้รับมาจากแหล่งอื่น
      <!-- สำหรับวัตถุประสงค์ดังต่อไปนี้ -->
    </p>

    <p>
      ข้าพเจ้ายินยอมกับการให้ใช้ข้อมูลส่วนตัว สำหรับวัตถุประสงค์ต่างๆ
      ดังต่อไปนี้
    </p>

    <ol>
      <li v-for="(objective, idx) in objectives" :key="idx">
        {{ objective }}
      </li>
    </ol>

    <p>
      ข้าพเจ้ารับทราบว่าข้าพเจ้ามีสิทธิ์ถอนความยินยอมที่ให้ไว้ข้างต้นได้ทุกเมื่อ
    </p>

    <p>ลายมือชื่อ: <span class="ml-4 inline-block w-48 border-b"></span></p>
    <p>ชื่อ-นามสกุล: <span class="ml-4 inline-block w-48 border-b"></span></p>
    <p>วันที่: <span class="ml-4 inline-block w-24 border-b"></span></p>
  </main>
</template>
