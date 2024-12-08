<template>
    <Layout>
        <template #header>
            <Header />
        </template>
    </Layout>
</template>

<script>
import Layout from './Layout.vue'; "@/components/Layout.vue";
import Header from "@/components/Header.vue";

export default {
    components: {
        Layout,
        Header
    }
}
</script>