<template>
  <div class="common-layout">
    <el-container>
      <el-header>
        <h2>Rounding off to the nearest 10</h2>
      </el-header>
      <el-main>
        <el-row>
          <el-col :span="12">
            <el-form-item label="Name" label-position="top" class="m-1">
              <el-input/>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="Score" label-position="top" class="m-1">
              <el-input/>
            </el-form-item>
          </el-col>
        </el-row>
        <span class="fw-normal text-center d-block">Circle the correct answer</span>
        <div v-for="(item, key) in arr" :key="key" class="mb-4">
          <span class="d-block"><span class="fw-bold">{{ item.question }}</span> rounded off to the nearest 10 is..</span>
          <el-radio-group v-model="answers[key]">
            <el-radio v-for="(answer, key) in item.answer" :key="key" :value="answer" border style="margin-top: 5px;">{{ answer }}</el-radio>
          </el-radio-group>
        </div>
      </el-main>
      <el-footer>
        <span class="fw-semibold fs-7">Copyright: www.mathinenglish.com</span>
      </el-footer>
    </el-container>
  </div>
</template>

<script>
import data from './data'

const arr = data

export default {
  name: 'MathWorksheet',
  data() {
    return {
      answers: []
    }
  },
  setup() {
    return {
      arr
    }
  }
}
</script>