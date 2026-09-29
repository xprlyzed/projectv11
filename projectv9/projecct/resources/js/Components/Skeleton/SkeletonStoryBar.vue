<script setup>
defineProps({
    count: { type: Number, default: 6 },
});
</script>

<template>
    <div class="story-bar" aria-hidden="true" data-testid="skeleton-story-bar">
        <div class="story-strip">
            <div v-for="n in count" :key="n" class="skel-story-item">
                <span class="skeleton skel-story-ring"></span>
                <span class="skeleton skel-story-name"></span>
            </div>
        </div>
    </div>
</template>

<style scoped>
.skel-story-item { display: flex; flex-direction: column; align-items: center; gap: 6px; flex-shrink: 0; width: 74px; }
.skel-story-ring { width: 66px; height: 66px; border-radius: 50%; display: block; }
.skel-story-name { width: 46px; height: 10px; border-radius: 5px; display: block; }
</style>
