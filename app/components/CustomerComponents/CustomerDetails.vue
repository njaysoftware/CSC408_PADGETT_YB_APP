<template>
    <GridLayout rows="auto" columns="*, *" width="100%">
      <Label @onTap="onTap" :text="customer.name" row="0" col="0" textWrap="true" class="list-group-item-heading label-text" style="width: 60%"/>
      <Label @onTap="onTap" :text="customer.email" row="0" col="1" textWrap="true" class="list-group-item-heading label-text" style="width: 60%"/>
    </GridLayout>
</template>
<script>
import CustomerRentals from '@/components/CustomerComponents/CustomerRentals';
export default {
    data() {
        return{}
    },
    methods:{
        onTap(){
            this.$navigateTo(CustomerRentals, {
                props:{
                    id: this.customer.id
                }
            });
        }
    },
    props: ["customer"],
    mounted(){
        
    }
}
</script>
<style scoped>
.label-text{
    font-size: 14;
    color: black;
    text-align: center;
    margin: 20;
}

</style>
