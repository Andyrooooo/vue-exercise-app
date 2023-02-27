<template>
    <!-- The site structure goes in here -->
    
      <form @submit.prevent="handleSubmit" class="timeExercise">

        <div  class="title">
            <h2>{{ timedTitle }}</h2>
        </div>
       
        <div class="name">
            <label>Workout Name</label>
            <input type="text" placeholder="Exercise..."  v-model="exercise.exerciseName">
        </div>
    
        <div class="distance">
            <label>Distance (Miles)</label>
            <input type="number" v-model="exercise.distance">
        </div>

        <div class="duration">
            <label>Duration</label>
            <input type="time" v-model="exercise.duration">
        </div>
        
        <div class="date">
            <label>Date</label>
            <input type="date" v-model="exercise.date">
        </div>
        
        <button class="submit">Add</button>
    </form>
    

</template>
    
    
    <script>
    // The site funtions go here
    export default {
        props: ['timedTitle'],
        name: 'timeExercise',
        data() {
            return {
                exercise: {
                    exerciseName: '',
                    distance: '',
                    duration: '',
                    date: ''
                }
            }
        },
        methods: {
            handleSubmit() {
            this.$emit('add:previous', this.exercise)
            console.log(this.exercise)
            }
        }
      }
    
    
    </script>
    
    
    <style >
    /* site styling */
    </style>