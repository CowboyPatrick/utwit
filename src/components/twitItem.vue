<template>
    <div class="twit-item" @click="favoriteTwit(twit.id)">
        <div class="user-profile_twit">
            <div class="twit-item_user"> 
                @{{ username }}
            </div>
            <div class="twit-item_content">
                {{ twit.content }}
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: "twitItem",
    props: {
        username: {
            type: String,
            required: true
        },
        twit: {
            type: Object,
            required: true
        }
    },
    methods: {
        favoriteTwit(id) {
            this.$emit('favorite', id)
        }
    }
};
</script>

<style lang="scss" scoped>
.twit-item {
    padding: 20px;
    background-color: white;
    border-radius: 4px;
    border: 1px solid #DFE3E8;
    box-sizing: border-box;
    cursor: pointer;
    transition: all .25s ease;

    &:hover {
    transform: scale(1.1, 1.1);
    }
    .twit-item_user {
    font-weight: bold;
    }
}

</style>