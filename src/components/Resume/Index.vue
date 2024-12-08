<template>
    <main>
        <p>{{ labelVisual }}</p>
        <h1>{{ amountCurrency }}</h1>
        <div class="graphic">
            <slot name="graphic"></slot>
        </div>
        <div class="action">
            <slot name="action"></slot>
        </div>
    </main>
</template>

<script>
export default {
    props: {
        label: {
            type: String,
            required: true
        },
        totalAmount: {
            type: Number
        },
        amount: {
            type: Number,
            default: null
        }
    },
    computed: {
        labelVisual() {
            return this.label !== null? this.label : 'Ahorro total';
        },
        amountVisual() {
            return this.amount !== null? this.amount : this.totalAmount;
        },
        amountCurrency() {
            return new Intl.NumberFormat('es-ES', {
                style: 'currency',
                currency: 'EUR'
            }).format(this.amountVisual);
        }
    }
}
</script>

<style>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}

h1,
p {
  margin: 0;
  text-align: center;
}

h1 {
  margin-top: 14px;
  color: var(--brand-green);
}

.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
}
</style>