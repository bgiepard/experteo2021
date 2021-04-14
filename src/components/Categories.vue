<template>
    <div class="[ categories ]">
        <ul class="flex-row flex-wrap list">
            <li v-for="category in categories" class="item">
                <div>
                    <div>
                        {{ category.title }}
                    </div>
<!--                    <ul>-->
<!--                        <li v-for="item in category.content">-->
<!--                            {{ item.name }}-->
<!--                        </li>-->
<!--                    </ul>-->
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
import categories from '../../../eksperci2021/src/assets/categories.json';

export default {
    name: "Categories",
    data() {
        return {
            categories
        }
    }
}
</script>

<style scoped>
.categories {
    background: rgba(250, 247, 244, 1);
}

.list {
    padding: 10px 30px;
}

.item {
    font-size: 14px;
    font-weight: 400;
    color: #444;
    padding:  5px 0;

    width: calc(100% / 8);


}
</style>