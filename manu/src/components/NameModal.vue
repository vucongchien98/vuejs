<template>
    <Page>
        <StackLayout class="p-20">
            <Label text="Nhập thông tin người nhận" fontSize="20" fontWeight="bold" color="red" marginLeft="80" marginTop="10" MarginBottom="10" />
            <Label text="------------------------------------------------------" color="darkgray" />
            <Label  text="Họ tên" marginLeft="10" marginTop="10" MarginBottom="10" fontWeight="bold" />
            <TextField hint="Fullname" id="txtNameID" :text="hoten" marginLeft="10" marginTop="10" MarginBottom="10"/>
            <Label text="Địa chỉ" marginLeft="10" marginTop="10" MarginBottom="10" fontWeight="bold" />
            <TextField id="txtCityID"  hint="Address" :text="diachi" marginLeft="10" marginTop="10" MarginBottom="10"/>
            <Label text="Số điện thoại" marginLeft="10" marginTop="10" MarginBottom="10" fontWeight="bold" />
            <TextField id="txtPhoneID" hint="Phone number" :text="sodienthoai" marginLeft="10" marginTop="10" MarginBottom="10" />
            <Button backgroundColor="#ff3300" color="white" text="Xong" @tap="closeThisModal($event)" />
        </StackLayout>
    </Page>
</template>
<script>
export default {
    props:['hoten','diachi','sodienthoai'],
    data(){
        return {
        }
    },
    methods: {
        closeThisModal(event)
        { //cách 1
            var view = require("tns-core-modules/ui/core/view");
            var srcBtn = event.object; 
            var txtFieldProv = view.getViewById(srcBtn.parent,"txtNameID");
            var txtFieldCity = view.getViewById(srcBtn.parent,"txtCityID");
            var txtFieldPhone = view.getViewById(srcBtn.parent,"txtPhoneID");
            var data = [txtFieldProv.text,txtFieldCity.text,txtFieldPhone.text];
            

            this.$modal.close(data)
        }
    }
}
</script>
<style scoped>

</style>