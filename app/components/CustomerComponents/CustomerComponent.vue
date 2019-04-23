<template>
    <StackLayout>
        <GridLayout rows="auto" columns="*, *" width="100%">
            <Label text="Name:" row="0" col="0" textWrap="true" class="list-group-item-heading label-text" style="width: 60%"/>
            <Label text="Email:" row="0" col="1" textWrap="true" class="list-group-item-heading label-text " style="width: 60%"/>
        </GridLayout>
        <ListView for="customer in customers" style="height:1250px">
            <v-template>
                <FlexboxLayout flexDirection="row" class="list-group-item">
                    <customer-details :customer="customer"></customer-details>
                </FlexboxLayout>
            </v-template>
        </ListView>
    </StackLayout>
</template>
<script>
import CustomerDetails from '@/components/CustomerComponents/CustomerDetails.vue';
export default {
    data() {
        return{}
    },
    methods: {
    },
    props: ["customers"],
    components: {
        CustomerDetails
    }    
}
</script>
<style scoped>
.label-text{
    font-size: 20;
    color: black;
    text-align: center;
    margin-top: 10;    
}
</style>
