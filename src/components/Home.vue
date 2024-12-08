<template>
    <Layout>
        <template #header>
            <Header />
        </template>
        <template #resume>
            <Resume 
                :label="label"
                :total-amount="100000"
                :amount="amount">
                <template #graphic>
                    graphic
                </template>
                <template #action>
                    action
                </template>
            </Resume>
        </template>
        <template #movements>
            <Movements
                :movements="movements"
            />
        </template>
    </Layout>
</template>

<script>
import Layout from "@/components/Layout.vue";
import Header from "@/components/Header.vue";
import Resume from '@/components/Resume/Index.vue';
import Movements from '@/components/Movements/Index.vue';

export default {
    components: {
        Layout,
        Header,
        Resume,
        Movements
    },
    data() {
        return {
            amount: null,
            label: null,
            movements: [
                {
                    id: 0,
                    title: "Movimiento 1",
                    description: "Lorem ipsum dolor sit amet",
                    amount: 1000,
                }, {
                    id: 1,
                    title: "Movimiento 2",
                    description: "Lorem ipsum dolor sit amet",
                    amount: 1000,
                }, {
                    id: 2,
                    title: "Movimiento 3",
                    description: "Lorem ipsum dolor sit amet",
                    amount: 1000,
                }, {
                    id: 3,
                    title: "Movimiento 4",
                    description: "Lorem ipsum dolor sit amet",
                    amount: 1000,
                }, {
                    id: 4,
                    title: "Movimiento 5",
                    description: "Lorem ipsum dolor sit amet",
                    amount: 1000,
                }, {
                    id: 6,
                    title: "Movimiento 7",
                    description: "Lorem ipsum dolor sit amet",
                    amount: 1000,
                }, {
                    id: 7,
                    title: "Movimiento 8",
                    description: "Lorem ipsum dolor sit amet",
                    amount: 1000,
                }, {
                    id: 8,
                    title: "Movimiento 9",
                    description: "Lorem ipsum dolor sit amet",
                    amount: 1000,
                }
            ]
        }
    }
}
</script>