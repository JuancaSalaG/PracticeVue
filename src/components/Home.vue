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
                    <Graphic :amounts="amounts" />
                </template>
                <template #action>
                    <Action @create="create"/>
                </template>
            </Resume>
        </template>
        <template #movements>
            <Movements
                :movements="movements"
                @remove="remove"
            />
        </template>
    </Layout>
</template>

<script>
import Layout from "@/components/Layout.vue";
import Header from "@/components/Header.vue";
import Resume from '@/components/Resume/Index.vue';
import Movements from '@/components/Movements/Index.vue';
import Action from "./Action.vue";
import Graphic from "./Resume/Graphic.vue";

export default {
    components: {
        Layout,
        Header,
        Resume,
        Movements,
        Action,
        Graphic
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
                    amount: 100,
                    time: new Date("2024-01-01"),
                }, {
                    id: 1,
                    title: "Movimiento 2",
                    description: "Lorem ipsum dolor sit amet",
                    amount: -320,
                    time: new Date("2024-06-01"),
                }, {
                    id: 2,
                    title: "Movimiento 3",
                    description: "Lorem ipsum dolor sit amet",
                    amount: 1000,
                    time: new Date("2024-06-15"),
                }, {
                    id: 3,
                    title: "Movimiento 4",
                    description: "Lorem ipsum dolor sit amet",
                    amount: 640,
                    time: new Date("2024-04-01"),
                }, {
                    id: 4,
                    title: "Movimiento 5",
                    description: "Lorem ipsum dolor sit amet",
                    amount: -750,
                    time: new Date("2024-10-12"),
                }, {
                    id: 6,
                    title: "Movimiento 7",
                    description: "Lorem ipsum dolor sit amet",
                    amount: -900,
                    time: new Date("2024-11-28"),
                }, {
                    id: 7,
                    title: "Movimiento 8",
                    description: "Lorem ipsum dolor sit amet",
                    amount: 500,
                    time: new Date("2024-03-19"),
                }, {
                    id: 8,
                    title: "Movimiento 9",
                    description: "Lorem ipsum dolor sit amet",
                    amount: -490,
                    time: new Date("2024-12-04"),
                },
                {
                    id: 9,
                    title: "Movimiento 10",
                    description: "Lorem ipsum dolor sit amet",
                    amount: 1000,
                    time: new Date("2024-12-01"),
                }
            ]
        }
    },
    computed: {
        amounts() {
            const lastDays = this.movements
                .filter(movement => {
                    const today = new Date();
                    const oldDate = today.setDate(today.getDate() - 30);

                    return movement.time > oldDate;
                })
                .map(movement => movement.amount);
            
            return lastDays.map((m, i) => {
                const lastMovements = lastDays.slice(0, i);
                return lastMovements.reduce((acc, m) => acc + m, 0);
            });
        }
    },
    methods: {
        create(movement) {
            this.movements.push({
                id: this.movements.length,
                ...movement
            });
        },
        remove(id) {
            const index = this.movements.findIndex(movement => movement.id === id);
            this.movements.splice(index, 1);
        }
    }
}
</script>