<template lang="pug">
.content-wrapper
  section
    .container
      h1.ui-title-2 Home
      input(
          type="text"
          placeholder="What we will watch?"
          v-model="taskTitle"
          @keyup.enter="newTask"
      )
      textarea(
          type="text"
          v-model="taskDescription"
          @keyup.enter="newTask"
      )
      .option-list
        input.what-watch--radio(
          type="radio"
          id="radioFilm"
          value="Film"
          v-model="whatWatch"
        )
        label(
          for="radioFilm"
        ) Film
        input.what-watch--radio(
          type="radio"
          id="radioSerial"
          value="Serial"
          v-model="whatWatch"
        )
        label(
          for="radioSerial"
        ) Serial

      .total-time

        // FILM TIME
        .total-time__film(
          v-if=" whatWatch === 'Film' "
        )
          // span Total Film Times
          span.time-title Hours
          input.time-input(
            type="number"
            v-model="filmHours"
          )
          span.time-title Minutes
          input.time-input(
            type="number"
            v-model="filmMinutes"
          )

          p {{ filmTime }}

        // SERIAL TIME
        .total-time__serial(
          v-if=" whatWatch === 'Serial' "
        )
          span.time-title How many season?
          input.time-input(
            type="number"
            v-model="serialSeason"
          )
          span.time-title How many series?
          input.time-input(
            type="number"
            v-model="serialSeries"
          )
          span.time-title How long is one series? (minutes)
          input.time-input(
            type="number"
            v-model="serialSeriesMinutes"
          )

          p {{ serialTime }}


          // span Total Serial Times  
      .tag-list
      .ui-tag__wrapper
        .ui-tag
          span.tag-title Dogs
          span.button-close  


</template>

<script>
export default {
  data () {
    return {
      taskTitle: '',
      taskDescription: '',
      whatWatch: 'Film',
      taskId: 3,

      // Total Time:
      // Film
      filmHours: 1,
      filmMinutes: 30,
      // Serial
      serialSeason: 1,
      serialSeries: 11,
      serialSeriesMinutes: 40
    }
  },
  methods: {
    newTask () {
      if (this.taskTitle === ''){
        return
      }
      const task = {
        id: this.taskId,
        title: this.taskTitle,
        description: this.taskDescription,
        whatWatch: this.whatWatch,
        completed: false,
        editing: false
      }
      console.log(task)

      //Reset
      this.taskId += 1
      this.taskTitle += ''
      this.taskDescription += ''
    },
    getHoursAndMinutes (minutes) {
      let hours = Math.trunc(minutes / 60)
      let min = minutes % 60
      return hours + ' Hours ' + min + ' Minutes '
    }
  },
  computed: {
    filmTime () {
      let min = (this.filmHours * 60) + (this.filmMinutes * 1)
      return this.getHoursAndMinutes(min)
    },
    serialTime () {
      let min = this.serialSeason * this.serialSeries * this.serialSeriesMinutes
      return this.getHoursAndMinutes(min)
    }
  }
}
</script>



<style lang="stylus" scoped>

.option-list
    display flex
    align-items center
    margin-bottom 20px
  .what-watch--radio
    margin-right 12px
  input 
    // margin-bottom 0  
  label 
    margin-right 20px
    margin-bottom 15px
    &:last-child   
      margin-right 0 

.tag-list
  margin-top 10px


// Total Time
.total-time
  margin-bottom 20px

.time-title
  display block
  margin-bottom 5px 

.time-input
  max-width 80px
  margin-right 10px

</style>



