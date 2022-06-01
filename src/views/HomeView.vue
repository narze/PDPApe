<script setup lang="ts">
import { nextTick, ref } from "vue"

const companyName = ref("บริษัท (ชื่อบริษัท) จำกัด")
const objectives = ref([
  "เพื่อเสนอผลิตภัณฑ์ และ/หรือ บริการของบริษัทที่เหมาะกับความต้องการของท่าน",
])

const objectiveRefs = ref([])
function addObjective() {
  objectives.value.push("[โปรดระบุวัตถุประสงค์การประมวลผลข้อมูล]")

  nextTick(() => {
    const lastItem = objectiveRefs.value.slice(-1)[0] as HTMLInputElement

    lastItem.focus()
    lastItem.select()
  })
}

function removeObjective(index: number) {
  if (confirm("ต้องการลบหรือไม่?")) {
    objectives.value.splice(index, 1)
  }
}

function print() {
  window.print()
}
</script>

<template>
  <main class="container mx-auto flex flex-col gap-4">
    <section
      id="form"
      class="print:hidden flex flex-col items-center justify-center"
    >
      <h1 class="font-medium">PDPApe 🙈</h1>
      <p class="mt-0">พิมพ์หนังสือให้ความยินยอมข้อมูลส่วนบุคคลอย่างง่ายๆ</p>

      <div class="flex flex-col gap-2 mt-8 w-full md:w-128">
        <div class="flex flex-row gap-2 items-center">
          ชื่อบริษัท:
          <input
            type="text"
            v-model="companyName"
            autofocus="true"
            onfocus="this.select()"
            class="p-2 grow rounded border"
          />
        </div>
        <div
          v-for="(_objective, idx) in objectives"
          class="flex flex-row gap-2 objectives items-center"
          :key="idx"
        >
          วัตถุประสงค์ที่ {{ idx + 1 }}:
          <input
            type="text"
            v-model="objectives[idx]"
            class="p-2 grow rounded border"
            ref="objectiveRefs"
          />
          <button
            v-if="objectives.length > 1"
            class="p-2 rounded-border"
            @click="removeObjective(idx)"
          >
            ลบ ❌
          </button>
        </div>
        <button class="p-2 rounded-border" @click="addObjective">
          เพิ่มวัตถุประสงค์ ➕
        </button>
        <button class="p-2 rounded-border" @click="print">พิมพ์ 🖨</button>
      </div>
    </section>

    <h2 class="print:hidden text-center mt-8 mb-0">ตัวอย่างแบบฟอร์ม</h2>

    <section
      id="print"
      class="flex flex-col gap-4 p-12 border border-rounded-xl print:border-none mt-8 print:mt-0"
    >
      <h1 class="text-xl font-bold text-center mt-12">
        หนังสือให้ความยินยอมในการเก็บรวบรวม/ใช้/เปิดเผยข้อมูลส่วนบุคคล
      </h1>

      <p>
        {{ companyName }} ("บริษัท") ให้ความสำคัญกับความเป็นส่วนตัวของท่าน
        บริษัทจึงขอความยินยอมจากท่านเพื่อการเก็บรวบรวม ใช้
        และ/หรือเปิดเผยข้อมูลส่วนบุคคลของท่านที่ให้ไว้แก้บริษัทหรือที่บริษัทได้รับมาจากแหล่งอื่น
      </p>

      <p>
        ข้าพเจ้ายินยอมกับการให้ใช้ข้อมูลส่วนตัว สำหรับวัตถุประสงค์ดังต่อไปนี้
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
    </section>

    <section id="links" class="flex gap-4 print:hidden justify-center">
      <a href="https://github.com/narze/PDPApe" target="_blank">GitHub</a>
    </section>
  </main>
</template>

<style>
html {
  font-family: "Kanit", sans-serif;
}
</style>
