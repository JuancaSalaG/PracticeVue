<template>
    <header>
        <img
            @click="reload"
            src="@/assets/cashflow-icon.svg" 
            alt="logo"
        >
        <h1>
            <span>Cash</span>Flow
        </h1>
    </header>
</template>

<script>
export default {
    methods: {
        reload() {
            window.location.reload();
        }
    }
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 100vw;
}
img,
span {
  width: 48px;
}
h1 {
  font-size: 1.4rem;
  color: var(--brand-blue);
}
h1 span {
  color: var(--brand-green);
}
</style>