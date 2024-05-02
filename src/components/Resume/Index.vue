<script>
const currencyFormat = new Intl.NumberFormat('fr-FR', {
    currency: "EUR",
    style: "currency",
})
export default {
    props: {
        label: {
            type: String,
        },
        dateLabel: {
            type: String,            
        },
        totalAmount: {
            type: Number,
        },
        amount: {
            type: Number,
            default: null,
        }
    },
    computed: {
        visualAmount() {
            return this.amount !== null ? this.amount : this.totalAmount;
        },
        visualLabel() {
            if (this.amount !== null) {
                return this.dateLabel
            } else {
                return this.label
            }
        },
        visualAmountCurrency() {
            return currencyFormat.format(this.visualAmount)         
        }       
    }    
}
</script>
<template>
    <main>
        <p>{{ visualLabel }}</p>
        <h1>{{ visualAmountCurrency }}</h1>
        <div class="graphic">
            <slot name="graphic"></slot>
        </div>
        <div class="action">
            <slot name="action"></slot>
        </div>
    </main>
</template>

<style scoped>
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
  /* VERY IMPORTANT don't use padding left or right in .graphic ===> Problem with calculation in Graph */
  padding: 48px 0px; 
  padding-top: 40px;
  padding-bottom: 24px;
  box-sizing: border-box;
}
</style>