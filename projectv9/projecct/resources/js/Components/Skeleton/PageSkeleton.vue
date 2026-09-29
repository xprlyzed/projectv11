<script setup>
import SkeletonCard from '@/Components/Skeleton/SkeletonCard.vue';
</script>

<template>
    <div class="page-skel" aria-hidden="true" data-testid="page-skeleton-root">
        <div class="page-skel-toolbar">
            <span class="skeleton page-skel-search"></span>
            <span class="skeleton page-skel-chip"></span>
            <span class="skeleton page-skel-chip"></span>
            <span class="skeleton page-skel-chip"></span>
        </div>
        <div class="page-skel-head">
            <span class="skeleton page-skel-title"></span>
        </div>
        <div class="row g-3">
            <div v-for="n in 8" :key="n" class="col-xl-3 col-lg-4 col-md-6">
                <SkeletonCard />
            </div>
        </div>
    </div>
</template>

<style scoped>
.page-skel { padding: 16px 0; }
.page-skel-toolbar { display: flex; align-items: center; gap: 12px; flex-wrap: wrap; margin-bottom: 22px; }
.page-skel-search { height: 42px; flex: 1; min-width: 220px; border-radius: 12px; display: block; }
.page-skel-chip { height: 34px; width: 96px; border-radius: 999px; display: block; }
.page-skel-head { margin-bottom: 16px; }
.page-skel-title { height: 20px; width: 200px; border-radius: 8px; display: block; }
</style>
