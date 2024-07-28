<template>
  <div class="common-layout">
    <el-container>
      <!-- header -->
      <el-header>
        <h2 class="text-center">Rounding off to the nearest 10</h2>
        <el-divider />
      </el-header>
      <!-- header -->
      <!-- main -->
      <el-main>
        <!-- name & score -->
        <el-row>
          <el-col :span="12">
            <el-form-item label="Name" label-position="top" class="m-1">
              <el-input v-model="name" placeholder="Please enter your name"/>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="Score" label-position="top" class="m-1">
              <el-input v-model="score" disabled/>
            </el-form-item>
          </el-col>
        </el-row>
        <!-- name & score -->
        <!-- question -->
        <h5 class="text-center mt-3">Choose the correct answer</h5>
        <!-- question -->
        <el-row :gutter="15">
          <template v-for="(item, key) in arr" :key="key">
            <!-- responsive col for each screen size -->
            <el-col :xs="24" :sm="24" :md="12" :lg="6" :xl="6" class="text-center">
              <span class="d-block mt-5">
                <span class="fw-bold">{{ item.question }}</span> 
                rounded off to the nearest 10 is..
              </span>
              <!-- answer -->
              <el-radio-group v-model="answers[key]">
                <el-radio 
                  v-for="(answer, key) in item.answer" 
                  :key="key" 
                  :value="answer" 
                  style="margin-top: 5px;"
                  border 
                >
                  {{ answer }}
                </el-radio>
              </el-radio-group>
              <!-- answer -->
            </el-col>
          </template>
        </el-row>
        <el-divider />
        <!-- call to action -->
        <div class="text-center">
          <el-popconfirm
            confirm-button-text="Yes"
            cancel-button-text="No"
            :icon="InfoFilled"
            icon-color="#626AEF"
            title="Are you sure to reset?"
            @confirm="resetForm"
          >
            <template #reference>
              <el-button type="danger" :icon="DeleteFilled" :disabled="answers.length == 0">Reset</el-button>
            </template>
          </el-popconfirm>
          <el-button @click="submitForm" type="success" :icon="Promotion">Submit</el-button>
        </div>
        <!-- call to action -->
      </el-main>
      <!-- main -->
      <!-- footer -->
      <el-footer>
        <span class="fw-semibold fs-7">Copyright: www.mathinenglish.com</span>
      </el-footer>
      <!-- footer -->
    </el-container>
  </div>
</template>

<script>
import data from './data'
import { DeleteFilled, Promotion, InfoFilled } from '@element-plus/icons-vue'
import { ElMessageBox } from 'element-plus'

const arr = data

export default {
  name: 'MathWorksheet',
  methods: {
    resetForm() {
      this.answers = []
    },
    submitForm() {
      // check if the name is filled & all question answered
      if(this.name == "") {
        ElMessageBox.alert('Please enter your name', 'Info', {
          showClose: false,
          confirmButtonText: 'OK'
        })
      } else if(this.answers.length != 12) {
        ElMessageBox.alert('Please answer all the questions', 'Info', {
          showClose: false,
          confirmButtonText: 'OK'
        })
      }

      this.score = 0
      // calculate the score if all question is answered & user input their name
      if(this.name != "" && this.answers.length == 12) {
        for(const key in arr) {
          let correctAnswer = Math.round(arr[key].question / 10) * 10
          if(this.answers[key] == correctAnswer) {
            this.score++
          }
        }
        // inform user with the score
        ElMessageBox.alert('Congrats '+this.name+', you just scored '+this.score, 'Completed', {
          showClose: false,
          confirmButtonText: 'OK'
        })
      }
    }
  },
  data() {
    return {
      answers: [],
      name: "",
      score: 0
    }
  },
  setup() {
    return {
      arr,
      DeleteFilled,
      Promotion,
      InfoFilled
    }
  }
}
</script>