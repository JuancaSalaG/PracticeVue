<template>
    <Layout>
        <template #header>
            <Header />
        </template>
        <template #resume>
            <Resume 
                :label="label"
                :total-amount="totalAmount"
                :amount="amount">
                <template #graphic>
                    <Graphic :amounts="amounts" @select="select"/>
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
            ]
        }
    },
    computed: {
        totalAmount() {
            return this.movements.reduce((acc, movement) => acc + movement.amount, 0);
        },
        amounts() {
            const lastDays = this.movements
                .filter(movement => {
                    const today = new Date();
                    const oldDate = today.setDate(today.getDate() - 30);

                    return movement.time > oldDate;
                })
                .map(movement => movement.amount);
            
            return lastDays.map((m, i) => {
                const lastMovements = lastDays.slice(0, i +1);
                return lastMovements.reduce((acc, m) => acc + m, 0);
            });
        }
    },
    mounted() {
        const movements = JSON.parse(localStorage.getItem("movements"));
        if (Array.isArray(movements)) {
            this.movements = movements.map(movement => ({
                ...movement,
                time: new Date(movement.time)
            }));
        }        
    },
    methods: {
        create(movement) {
            this.movements.push({
                id: this.movements.length,
                ...movement
            });
            this.save();
        },
        remove(id) {
            const index = this.movements.findIndex(movement => movement.id === id);
            this.movements.splice(index, 1);
            this.save();
        },
        save() {
            console.log(this.movements);            
            localStorage.setItem("movements", JSON.stringify(this.movements));
        },
        select(el) {
            console.log(el);
            this.amount = el;
        }
    }
}
</script>