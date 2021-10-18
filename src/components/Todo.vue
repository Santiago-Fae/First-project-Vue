<template>
    <div class="tile flex-centered" :class="{checked: todo.checked}">
        <div class="tile-icon">
            <i class="icon" :class="todo.checked ? 'icon-check' : 'icon-time'"></i>
        </div>
        <ul class="tile-content">
            <li class="tile-subtitle">{{ todo.description }}</li>
        </ul>
        <div class="tile-action">
            <button @click="$emit('toggle', todo)" class="btn btn-link">
                <span v-if="todo.checked">Mark off</span> 
                <span v-else>Complete</span>
            </button>
            <button @click="$emit('remove', todo)" class="btn btn-link">
                <span class="text-error">Remove</span>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        todo: {type: Object, required: true}
    }
}
</script>

<style scoped>
.tile-subtitle {
  list-style: none;
  margin-top: 0px;
}
.checked {
    text-decoration: line-through;
    color: lightgray;
}
</style>