<template>
  <div id="app">
    <Header></Header>
    <div class="columns">
      <GradeTable :grades="gradeData.grades" class="column box is-three-fifths"></GradeTable>
      <GradeInputForm
        class="column"
        @grade-submitted="addGrade"
      ></GradeInputForm>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import GradeTable from './components/GradeTable.vue'
import GradeInputForm from './components/GradeInputForm.vue'

export default {
  name: 'App',
  components: {
    Header,
    GradeTable,
    GradeInputForm
  },
  data () {
    return {
      gradeData: {
        nextId: 3,
        grades: [
          { id: 1, student: 'Ted Theodore Logan', course: 'History', grade: 100 },
          { id: 2, student: 'Tommy Bahama', course: 'Alphabet', grade: 20 }
        ]
      }
    }
  },
  mounted: function () {
    const storageGradeData = JSON.parse(localStorage.getItem('gradeData'))
    if (storageGradeData) {
      this.gradeData = storageGradeData
    }
  },
  methods: {
    addGrade (grade) {
      grade.id = this.gradeData.nextId
      this.gradeData.grades.push(grade)
      this.gradeData.nextId++
      this.syncStorage()
    },
    syncStorage () {
      localStorage.setItem('gradeData', JSON.stringify(this.gradeData))
    }
  }
}
</script>
