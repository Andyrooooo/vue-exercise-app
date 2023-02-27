<template >
<!---------------------- Exercise tracker with the buttons here -------------->

  <h1>My Exercise Tracker</h1>

  <div v-if="showTimedExercise">
    <timeExercise @add:previous="addExercise" :timedTitle="timedTitle" />
  </div>

  <div v-if="showSetExercise">
    <setExercise @add:previousSet="addSetExercise" :setTitle="setTitle"/>
  </div>

  <div class="showButtons">
    <button @click="toggleTimedExercise" class="show1">
      <span v-if="!showTimedExercise">Show Timed Exercise</span>
      <span v-if="showTimedExercise">Close Timed Exercise</span>
    </button>

    <button @click="toggleSetExercise" class="show2">
      <span v-if="!showSetExercise">Show Set Exercise</span>
      <span v-if="showSetExercise">Close Set Exercise</span>
    </button>
  </div>
<!---------------------- timed exercise history -------------------->
  <h1 class="history">History</h1>

<div v-for="(exercise, index) in exercises" :key="exercise.id" class="previous">

<!---------------- Timed exercise name ------------------->
    <div v-if="editing === index" class="previousName">
      <label>Workout</label>
      <input type="text" v-model="exercise.exerciseName"/>
    </div>

    <div v-else class="previousName">
        <label>Workout</label>
        <span>{{ exercise.exerciseName }}</span>
    </div>

<!---------------- Timed exercise distance ------------------->
    <div v-if="editing === index" class="previousDistance">
        <label>Distance</label>
        <input type="number" v-model="exercise.distance"/>
    </div>

    <div v-else class="previousDistance">
      <label>Distance</label>
      <span>{{ exercise.distance }}</span>
    </div>
        
<!---------------- Timed exercise duration ------------------->
  <div v-if="editing === index" class="previousDuration">
    <label>Duration</label>
    <input type="time" v-model="exercise.duration"/>
  </div>

    <div v-else class="previousDuration">
        <label>Duration</label>
        <span>{{ exercise.duration }}</span>
    </div>

<!---------------- Timed exercise date ------------------->
<div v-if="editing === index" class="previousDate">
  <label>Date</label>
  <input type="date" v-model="exercise.date"/>
</div>

    <div v-else class="previousDate">
        <label>Date</label>
        <span>{{ exercise.date }}</span>
    </div>

<!---------------- Timed exercise buttons ------------------->
    <div v-if="editing === index" class="editDelete">
      <button @click="saveExercise(exercise)" class="save">Save</button>
    </div>


    <div v-else class="editDelete">
      <div class="edit">
        <button @click="editTimeExercise(index)">Edit</button>
      </div>

      <div class="delete">
        <button @click="removeExercise(index)">Delete</button>
        </div>
    </div>
    
</div>

<!---------------------- set exercise history ------------------------>

  <div v-for="(setExercise, index) in setExercises" :key="setExercise.id" class="previous">

<!---------------- set exercise names ------------------->
    <div v-if="editingSet === index" class="previousName">
      <label>Workout</label>
      <input type="text" v-model="setExercise.setName"/>
    </div>

    <div v-else class="previousName">
        <label>Workout</label>
        <span>{{ setExercise.setName }}</span>
    </div>

    <!---------------- set exercise sets ------------------->
    <div v-if="editingSet === index" class="sets">
      <label>Set</label>
      <input type="number" v-model="setExercise.setSet"/>
    </div>
    
    <div v-else class="sets">
        <label>Set</label>
        <span>{{ setExercise.setSet }}</span>
    </div>

    <!---------------- set exercise reps ------------------->
    <div v-if="editingSet === index" class="reps">
      <label>Reps</label>
      <input type="number" v-model="setExercise.setReps"/>
    </div>

    <div v-else class="reps">
        <label>Reps</label>
        <span>{{ setExercise.setReps }}</span>
    </div>

    <!---------------- set exercise weight ------------------->
    <div v-if="editingSet === index" class="weight">
      <label>Weight(lbs)</label>
      <input type="number" v-model="setExercise.setWeight"/>
    </div>

    <div v-else class="weight">
        <label>Weight(lbs)</label>
        <span>{{ setExercise.setWeight }}</span>
    </div>

    <!---------------- set exercise date ------------------->
    <div v-if="editingSet === index" class="date2">
      <label>Date</label>
      <input type="date" v-model="setExercise.setDate">
    </div>

    <div v-else class="date2">
        <label>Date</label>
        <span>{{ setExercise.setDate }}</span>
    </div>

    <!---------------- set exercise buttons ------------------->
    <div v-if="editingSet === index" class="editDelete">
      <button @click="saveSetExercise(setExercise)" class="save">Save</button>
    </div>

    <div v-else class="editDelete">
      <div class="edit">
        <button @click="editSetExercise(index)">Edit</button>
      </div>

      <div class="delete">
      <button @click="removeSetExercise(index)">Delete</button>
      </div>
    </div>
    
    

  </div>
</template>

<!---------------------- methods are here ----------------------->
<script>
// The site funtions go here
import timeExercise from './components/timeExercise.vue'

import setExercise from './components/setExercise.vue'

export default {
    name: 'App',
    components: {
      timeExercise,
      setExercise
    },
    data() {
            return {
              timedTitle: 'Timed Exercise',
              setTitle: 'Set Exercise',
              showTimedExercise: false,
              showSetExercise: false,
              editing: null,
              editingSet: null,

                exercises: [
                    {
                    exerciseName: 'Jogging',
                    distance: 12,
                    duration: '4:00',
                    date: '12/12/2023',
                    id: 1
                    }
                ],
                setExercises: [
                  {
                  setName: 'Bench Press',
                  setSet: 3,
                  setReps: 14,
                  setWeight: 120,
                  setDate: '12/12/2023',
                  id: 1
                }
              ] 
            }
        },
        methods: {
/* ------------------------------ remove timed exercise ----------------------- */
            removeExercise(index) {
                this.exercises.splice(index, 1)
            },
/* ------------------------------ remove set exercise ----------------------- */
            removeSetExercise(index) {
              this.setExercises.splice(index, 1)
            },
/* ------------------------------ adds id and new exercise to timed exercise array objects ----------------------- */
            addExercise(exercise) {
              const lastId = this.exercises.length > 0 ? this.exercises[this.exercises.length -1].id : 0
              const id = lastId + 1

              const newExercise = {...exercise, id}

              this.exercises = [...this.exercises, newExercise]
            },
/* ------------------------------ adds id and new exercise to set exercise array objects ----------------------- */
            addSetExercise(setExercise) {
              const lastSetId = this.setExercises.length > 0 ? this.setExercises[this.setExercises.length - 1].id : 0
              const id = lastSetId + 1

              const newSetExercise = {...setExercise, id}

              this.setExercises = [...this.setExercises, newSetExercise]
            },

/* ------------------------------ toggles show timed exercise button ----------------------- */
            toggleTimedExercise() {
              this.showTimedExercise = !this.showTimedExercise
            },
/* ------------------------------ toggles show set exercise button ----------------------- */
            toggleSetExercise() {
              this.showSetExercise = !this.showSetExercise
            }, 
            
            editTimeExercise(index) {
              this.editing = index
            },

            saveExercise() {

              this.editing = null
            },

            editSetExercise(index) {
              this.editingSet = index
            },

            saveSetExercise() {

              this.editingSet = null
            }
        }
}
</script>


<style>
/* site styling */

</style>


