<template>
    <div class="flex-row w-100">
        <div class="[ board ]">
            <form class="[ main-form] flex-row">
                <input class="xxx" type="text" placeholder="Jakiej usługi szukasz?">
<!--                @todo ostylowac formularz -->
<!--                @todo focus na formularz powinien wyświetlić całe menu kategorii-->
                <input class="xxx xxx2" type="text" placeholder="Wrocław, Dolnośląskie">
            </form>
            <div class="[ tags ] flex-row">
                <div class="active">Remonty</div>
                <div>Ocieplenia</div>
                <div>Dachy</div>
                <div>Ocieplanie</div>
                <div>Panele słoneczne</div>
                <div>Tynkowanie</div>
            </div>
            <Listing />
        </div>
    <div v-show="showModal" style="padding: 20px; width: 300px">{{ data }}</div>
        <div class="[ map-wrapper ]">
            <Map/>
        </div>
    </div>
</template>

<script>
import Listing from "@/components/Listing";
import Map from "@/components/Map";
import Categories from "@/components/Categories";

export default {
    name: 'Home',
    data() {
        return {
            showModal: false,
            data: null
        }
    },
    components: { Categories, Map, Listing },
    methods: {
        openModal(data) {
            this.showModal = true;
            this.data = data
        }
    }
}
</script>

<style lang="less">
.board {
    width: 50%;
    padding: 20px 30px 20px 10px;
}

.map-wrapper {
    width: calc(50% - 20px);
    height: calc(100vh - 40px);
    margin: 20px 20px 20px 0;
}

.xxx {
    background: url('../assets/search.png') 10px center no-repeat, rgba(241, 243, 250, 1);
    background-size: 20px 20px;
    margin-bottom: 20px;
    width: 65%;
    padding: 10px 20px 8px 40px;
    border-radius: 8px;
    font-size: 15px;
    line-height: 1;

    color: #000;
    font-weight: 500;

    outline-color: #7b48ff;

    &::placeholder {
        font-weight: 400;
        color: #777;
    }
}

.xxx2 {
    width: 30%;
    min-width: 150px;
    margin-left: 10px;
    background: url('../assets/pininput64x64.png') 10px center no-repeat,
    url('../assets/down-filled-triangular-arrow.png') right 15px center no-repeat #fff;
    background-size: 20px 20px, 8px 8px;
    border: 1px solid rgba(241, 243, 250, 1);
    box-shadow: 0 2px 3px rgba(241, 243, 250, 1);

}

.tags {

    div {
        margin-right: 8px;
        font-size: 14px;
        padding: 5px 8px 4px;
        background: #8e99c7;
        color: #fefefe;
        border-radius: 5px;
        white-space: nowrap;

        &.active, &:hover {
            background: #7b48ff;
        }
    }
}
</style>
