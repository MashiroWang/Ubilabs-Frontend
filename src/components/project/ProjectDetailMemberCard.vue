<template>
<div class="project-member-wrapper">
  <author-info :author="member" :key="member._id"></author-info>
  <div :id="'chart-'+this.member._id.substring(0, 8)"></div>
</div>
</template>

<script>
import AuthorInfo from '@/components/forum/AuthorInfo'
import CalendarHeatMap from 'calendar-heatmap-mini'
import { mapGetters } from 'vuex'
export default {
  name: 'projectDetailMemberCard',
  props: ['isLeader', 'member'],
  components: {
    AuthorInfo
  },
  computed: {
    ...mapGetters({
      project: 'project/project'
    }),
    notes: function () {
      return this.project.notes.filter(note => note.author._id === this.member._id)
    }
  },
  methods: {
    updateChart: function () {
      if (this.project) {
        const table = {}
        const array = []
        this.notes.forEach(note => {
          const countDate = new Date(note.createdAt)
          const date = `${countDate.getFullYear()}-${countDate.getMonth() + 1}-${countDate.getDate()}`
          if (!table[date]) {
            const insideObj = {
              date: new Date(date),
              count: 1
            }
            table[date] = insideObj
          } else {
            table[date].count ++
          }
        })
        for (let key in table) {
          array.push(table[key])
        }
        console.log(array)
        const chart = CalendarHeatMap()
                .data(array || [])
                .selector(`#chart-${this.member._id.substring(0, 8)}`)
                .colorRange(['#EBEDF0', '#1D602A'])
                .tooltipEnabled(true)
                .legendEnabled(false)
        chart()
      }
    }
  },
  mounted () {
    this.updateChart()
  },
  updated () {
    this.updateChart()
  }
}
</script>

<style lang="scss" scoped>
@import '~calendar-heatmap-mini/src/calendar-heatmap-mini.css';
.project-member-wrapper {
  margin-bottom: 10px;
}
</style>

