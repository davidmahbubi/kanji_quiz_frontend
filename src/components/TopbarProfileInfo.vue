<template>
    <div class="row">
        <div class="col-sm-6 col-6 col-sm-6 pr-3 text-right p-0">
            <h5 class="text-custom-primary topbar-user-name m-0">{{ getUserDetail.name || 'Loading User' }}</h5>
            <span>{{ getScoreCount }}xp</span>
        </div>
        <div class="col-sm-6 p-0 col-6 text-left">
            <div class="profile-img-wrapper rounded-circle">
                <img :src="`${getImageBaseUrl}/${getUserDetail.picture}`" alt="" class="profile-picture rounded-circle">
            </div>
        </div>
    </div>
</template>

<script>

import { BASE_URL } from '@/commons/config';

export default {
    computed: {
        getUserDetail() {
            return this.$store.getters['auth/getUserDetail'];
        },
        getScoreCount() {
            const quizResult = this.$store.getters['auth/getUserDetail'].quiz_result || [];
            if (quizResult.length > 0) {
                return quizResult.map(({ score }) => score).reduce((acc, curr) => acc + curr);
            } else {
                return 0;
            }
        },
        getImageBaseUrl() {
            return `${BASE_URL}/img/profiles`;
        }
    }
}

</script>

<style scoped>

.topbar-user-name {
    font-size: 17px;
}

.profile-picture {
    width: 64px;
    height: 64px;
    box-shadow: 0 0 10px rgba(146, 13, 255, 0.3);
}

.profile-img-wrapper {
    width: 64px;
    height: 64px;
    overflow: hidden;
}

</style>