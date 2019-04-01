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
        .total-time__film(
          v-if=" whatWatch === 'Film' "
        )
          span Total Film Times
        .total-time__serial(
          v-if=" whatWatch === 'Serial' "
        )
          span Total Serial Times  
      .tag-list
      .ui-tag__wrapper
        .ui-tag
          span.tag-title Dogs
          span.button-close  


  section
    .container
      .task-list
        .task-item(
          v-for="task in tasks"
          :key="task.id"
          :class="{ completed: task.completed }"
        )
          .ui-card.ui-card--shadow
            .task-item__info
              .task-item__main-info
                span.ui-label.ui-label--light {{ task.whatWatch }}
                span Total Time:
              span.button-close
            .task-item__content
              .task-item__header
                .ui-checkbox-wrapper
                    input.ui-checkbox(
                      type='checkbox'
                      v-model="task.completed"
                    )
                span.ui-title-3 {{ task.title }}
              .task-item__body
                p.ui-text-regular {{ task.description }}
</template>

<script>
export default {
  data () {
    return {
      taskTitle: '',
      taskDescription: '',
      whatWatch: 'Film',
      taskId: 3,
      tasks: [
        {
          'id': 1,
          'title': 'GrowthBusters: Hooked on Growth',
          'description': 'It is a long established fact that a reader will be distracted by the readable content of a page when looking at its layout. The point of using Lorem Ipsum is that it has a more-or-less normal.',
          'whatWatch': 'Film',
          'completed': false,
          'editing': false
        },
        {
          'id': 2,
          'title': 'Game of the Trones',
          'description': 'Best serial',
          'whatWatch': 'Serial',
          'completed': false,
          'editing': false
        }
      ]
    }
  },
  methods: {
    newTask () {
      if (this.taskTitle === ''){
        return
      }
      this.tasks.push({
        id: this.taskId,
        title: this.taskTitle,
        description: this.taskDescription,
        whatWatch: this.whatWatch,
        completed: false,
        editing: false
      })

      //Reset
      this.taskId += 1
      this.taskTitle += ''
      this.taskDescription += ''

    }  
  }
}
</script>



<style lang="stylus" scoped>

.task-item
    margin-bottom 20px
    &:last-child
      margin-bottom 0

.ui-label
    margin-right 8px
    border-radius 3px
    // background-color blue

.task-item__info 
    display flex
    align-items center
    justify-content space-between
    margin-bottom  20px
.button-close
    width 20px
    height @width  

.task-item__header
    display flex 
    align-items center   
    margin-bottom 10px

.ui-checkbox-wrapper
    margin-right 10px

.ui-title-3 
    margin-bottom 10px

.option-list
    display flex
  .what-watch--radio
    margin-right 10px
  label 
    margin-right 20px
    &:last-child   
      margin-right 0 

.tag-list
  margin-top 20px

</style>



