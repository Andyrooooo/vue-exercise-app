<template>
    <!-- The site structure goes in here -->
    <form @submit.prevent="handleSubmit2" class="setExercise">

        <div class="title">
            <h2>{{ setTitle }}</h2>
            <span></span>
        </div>
        
        <div class="name">
            <label>Workout Name</label>
            <input type="text" placeholder="Exercise..." v-model="setExercise.setName">
        </div>

        <div class="sets">
            <label>Sets</label>
            <input type="number" v-model="setExercise.setSet">
        </div>

        <div class="reps">
            <label>Reps</label>
            <input type="number" v-model="setExercise.setReps">
        </div>

        <div class="weight">
            <label>Weight (lbs)</label>
            <input type="number" v-model="setExercise.setWeight">
        </div>

        <div class="date2">
            <label>Date</label>
            <input type="date" v-model="setExercise.setDate">
        </div>

        <button class="submit">Add</button>

    </form>
    
</template>
    
    
<script>
    // The site funtions go here
    export default {
        props: ['setTitle'],
        name: 'setExercise',
        data() {
            return {
                setExercise: {
                    setName: '',
                    setSet: '',
                    setReps: '',
                    setWeight: '',
                    setDate: '',
                }
            }
        },
        methods: {
        handleSubmit2() {
            this.$emit('add:previousSet', this.setExercise)
            console.log('it is being sent over')
            }
        }
      }
    
    
</script>
    
    
<style>
    /* component styling */
</style>