<script setup>
import Grid from '../Grid.vue';
    import { gymHealthFacts } from '../../utils';

    const props = defineProps({
        handleSelectWorkout: {
            type: Function,
            required: true
        }
    })
    
    //generate random number between 0 and length of gymHealthFacts array
    const randomNumber = Math.floor(Math.random() * gymHealthFacts.length);
    const todayFact = gymHealthFacts[randomNumber];
    

</script>

<template>
    <section id="dashboard">
        <div class="card tip-container">
            <h2>Welcome Gym rat</h2>
            <p class="tip"><strong>Daily Tip</strong><br /> {{ todayFact }}</p>
        </div>
        <div>
            <button>Start Workout &rarr;</button>
        </div>
        <Grid v-bind="props" />
    </section>
</template>

<style scoped>
    .tip-container, 
    .tip-container div,
    #dashboard {
        display: flex;
    }
    .tip-container,
    #dashboard {
        flex-direction: column;
    }
    #dashboard {
        gap: 2rem;
    }
    .tip-container {
        gap: 0.25rem;
    }

    @media (min-width: 640px) {
        .tip-container {
            gap: 1rem;
        }
    }
</style>
