<template>
    <div class="[ listing ] flex-column">

        <br><br>
        <br><br>
        <big>Polecani specjaliści</big>
        <br>

        <div class="[ list ]">
<!--            @todo Kliknięcie powinno pokazać ankietę z tekstem -->
<!--            'Wypełnij ankietę a zapytanie zostanie wysłane do specjalisty oraz innych zainteresowanych wykonawców'-->
            <div class="[ list__item company ] flex-row align-center" v-for="pin in pins">
                <div class="[ company__avatar ] flex-row align-center p2">
                    <img :src="pin.company_logo_url">
                </div>
                <div class="flex-column">
                    <div class="flex-row">
                        <div class="[ company__name ]">{{ pin.company_name }}</div>
                        <div class="flex-row">
                            <div class="[ company__tag ]">
                                {{ categories[(Math.ceil(Math.random() * 10) - 1)] }}
                            </div>
                        </div>
                    </div>
                    <div class="[ company__review ] flex-row align-center">
                        <!--                        @todo Recenzje przepisać -->
                        <div>
                            <img v-if="(Math.ceil(Math.random()*4)) <= 2.5" src='../assets/rating4.png' alt=""
                                 width="60px">
                            <img v-else src='../assets/rating5.png' alt="" width="60px">
                        </div>
                        <div class="[ company__comment ]">
                            {{ opinions[(Math.ceil(Math.random() * 4))] }}
                        </div>
                    </div>
                    <div class="[ company__location ]">{{ pin.street }}, {{ pin.city }}</div>
                </div>
            </div>
        </div>


        <!--        <button class="p1 m1" @click="$emit('openModal', pin.title)" v-for="pin in pins">{{ pin.title }}</button>-->
    </div>
</template>

<script>
import pins from '../../../eksperci2021/src/assets/pins.json';

export default {
    name: "Listing",
    data() {
        return {
            pins: pins,
            opinions: [
                'Profesjonalna firma poradzą jakich materiałów użyć żeby wszystko wyszło fajnie i zakres prac wykonany solidnie dokładnie i nie drogo i jeśli ktoś szuka dobrej firmy to polecam tą firmę z czystym sumieniem',
                'Bardzo solidna firma i rzetelna, wszystko zrobione na wysokim poziomie, polecam.',
                'Chłopaki bardzo dobrze wykonali swoją pracę, od samego początku można było im zaufać. Przede wszystkim bardzo uczciwi. Polecam w 100%.',
                'Gdy poszukujesz współpracy to profesjonaliści z Maja Dziurzyńska 5MBUD są dla Ciebie idealni. Skontaktuj się z nimi od razu, aby uzyskać szczegółowe informacje.',
                'Prace wykonane bardzo dobrze, dokładnie. Kontakt z wykonawcą bardzo dobry, jesteśmy zadowoleni ze współpracy. Dziękujemy.'
            ],
            categories: [
                'Remonty',
                'Ocieplenia',
                'Dachy',
                'Montaż wentylacji',
                'Budowa studni',
                'Okna dachowe',
                'Ocieplanie',
                'Rekuperatory',
                'Wentylacja',
                'Panele słoneczne',
            ],
            names: [
                'Janina K',
                'Andrzej S',
                'Mateusz G',
                'Martyna C',
                'Sławomir T',
                'Arkadiusz M',
                'Elżbieta W',
            ]
        }
    }
}
</script>

<style lang="less" scoped>

.list {
    height: 75vh;
    overflow: auto;

    &::-webkit-scrollbar {
        width: 10px;
        background-color: rgba(0, 0, 0, 0.03);
        border-radius: 5px;
    }

    &::-webkit-scrollbar-track {
        border-radius: 3px;
        background-color: transparent;
    }

    &::-webkit-scrollbar-thumb {
        border-radius: 5px;
        background-color: rgba(0, 0, 0, 0.1);
        //border:2px solid #eff1f5
    }

    &__item {
        margin-bottom: 20px;
        box-shadow: 0 5px 25px -10px rgba(0, 0, 0, 0.1);
        border: 1px solid rgba(0, 0, 0, 0.05);
        border-radius: 5px;
        transition: box-shadow 0.3s ease;


        &:hover {
            box-shadow: 0 5px 25px -10px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(0, 0, 0, 0.1);
            cursor: pointer;
        }
    }
}

.company {
    padding: 15px 0;
    margin-right: 10px;

    &__avatar {
        height: 50px;
        min-width: 50px;

        img {
            width: 50px;
        }
    }

    &__name {
        font-weight: 500;
    }

    &__tag {
        margin-left: 10px;
        font-size: 12px;
        padding: 3px 3px 2px;
        background: #efefef;
        color: #444;
    }

    &__review {
        margin-top: 8px;
    }

    &__comment {
        border-left: 2px solid blue;
        padding: 0 10px;
        margin-left: 10px;

        color: #555;
        font-size: 13px;

        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 1;
        overflow: hidden;
        max-width: calc(100% - 80px);
    }

    &__location {
        margin-top: 8px;
        font-size: 13px;
    }
}

//.listing {
//    height: 60vh;
//    overflow: auto;
//    overflow-x: hidden;
//    padding: 0 20px 10px;
//
//    &::-webkit-scrollbar {
//        width: 10px;
//        background-color: rgba(0, 0, 0, 0.03);
//    }
//
//    &::-webkit-scrollbar-track {
//        border-radius: 3px;
//        background-color: transparent;
//    }
//
//    &::-webkit-scrollbar-thumb {
//        border-radius: 5px;
//        background-color: rgba(0, 0, 0, 0.1);
//        //border:2px solid #eff1f5
//    }
//}
</style>