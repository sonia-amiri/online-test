<template>
  <div>
    <el-row :gutter="5">
      <el-col :span="2">
        <div class="grid-content bg-purple">مدیریت  پرسش</div>
      </el-col>
      <el-col :span="1">
        <el-button @click="query" type="primary" icon="el-icon-search" circle></el-button>
      </el-col>
    </el-row>
    <el-table :data="questionList">
      <!-- <el-table-column label="id" prop="id" width="60" /> -->
      <el-table-column label="شماره" prop="index" width="60" />
      <el-table-column label="سوال" resizable prop="question" show-overflow-tooltip />
    </el-table>

  </div>
</template>

<script>
// import PaginateTable from './PaginateTable'
// import queryQuestion from '@/api/question/queryQuestion'
// import createQuestion from '@/api/question/createQuestion'
// import deleteQuestion from '@/api/question/deleteQuestion'
// import getQuestionById from '@/api/question/getQuestionById'

// import SubjectSelector from './SubjectSelector'
// import QuestionTypeSelector from './QuestionTypeSelector'
import { errorTip, successTip } from '@/utils/tips'
import store from '../store'

export default {
  name: 'QuestionManage',
  // components: { PaginateTable, SubjectSelector, QuestionTypeSelector },
  created () {
    this.query()
  },
  data () {
    return {
      state: store.state,
      questionList: [],
      pagination: {},
      form: {
        myCreate: false,
        keyword: '',
        subjectId: null,
        typeId: null
      },
      // typeFormatter: createQuestion.typeFormatter,
      // forTypeName: createQuestion.forTypeName,
      detailOpened: false,
      addDialogOpen: false,
      detail: {
        id: 0,
        subjectId: 0,
        subjectName: '',
        typeId: 1,
        creatorId: 0,
        creatorName: 'xxx',
        description: {
          options: [
            {
              id: 0,
              name: 'string'
            }
          ],
          title: 'string'
        },
        answer: {
          optionId: 0,
          optionIds: [
            0
          ],
          text: '',
          trueOrFalse: true
        }
      },
      newQuestion: {
        subjectId: 0,
        question: {
          typeId: 1,
          description: {
            options: [],
            title: ''
          },
          answer: {
            optionId: 0,
            optionIds: [],
            text: '',
            trueOrFalse: true
          }
        }
      }
    }
  },
  methods: {
    query () {
      this.changePage(1)
    },
    changePage (pageNum) {
      this.$axios.get(process.env.VUE_APP_BACKEND_URL + '/exam/questions/' + this.$route.params.id)
        .then(data => {
          this.questionList = data
          successTip('با موفقیت بارگذاری شد')
        })
        .catch(errorTip)
    },
    openDetail (row, column, event) {
      console.log('با موفقیت ایجاد شد! ' + row.id)
      // getQuestionById.request(row.id)
      //     .then(resp => {
      //       this.detail = resp
      //       this.detailOpened = true
      //     })
      //     .catch(errorTip)
      // },
      // createQuestion () {
      // const newQuestion = this.newQuestion
      // createQuestion.request(newQuestion)
      // .then(value => {
      //   successTip('با موفقیت ایجاد شد')
      //   this.addDialogOpen = false
      //   this.query()
      // })
      // .catch(errorTip)
      // }

    // handleDelete (id) {
      // console.log(id)
      // deleteQuestion.request(id)
      //   .then(value => {
      //     successTip('با موفقیت حذف شد')
      //     this.query()
      //   })
      //   .catch(errorTip)
    // }
    // toOption (id) {
    //   return String.fromCharCode(id + 65)
    }
  }
}
</script>

<style scoped>

</style>
