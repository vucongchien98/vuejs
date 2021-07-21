<template>
    <Page>
        <ActionBar title="Hóa Đơn Bán Hàng" />
        <FlexboxLayout flexDirection="row">
            <StackLayout orientation="vertical" marginTop="10">
                <!-- <Button row=0 text="Trở Về" @tap="$modal.close()" /> -->
                <Label text="Thông Tin Khách Hàng" color="red" fontSize="22" marginLeft="100" />
                <GridLayout columns="*,10,*" rows="auto,auto,auto" :key="i.hoten" v-for="i in people" >
                    <Label text="Họ tên :" row="0" col="0" colSpan="2" marginBottom="10" />
                    <Label :text="i.hoten " row="0" col="2" colSpan="2" marginBottom="10"/>
                    <Label text="Địa chỉ :" row="1" col="0" colSpan="2" marginBottom="10" />
                    <Label :text="i.diachi" row="1" col="2" colSpan="2" marginBottom="10"/>
                    <Label text="Số điện thoại :" row="2" col="0" colSpan="2" marginBottom="10" />
                    <Label :text="i.sodienthoai" row="2" col="2" colSpan="2" marginBottom="10"/>
                </GridLayout>
                <Label text="------------------------------------------------------" color="darkgray" />
                <Label text="Thông Tin Đơn Hàng" color="red" fontSize="22" marginLeft="100" />
                <GridLayout columns="150,*,*,*" rows="auto" verticalAlignment="top" backgroundColor="yellow">
                    <Label text="Tên hàng" col="0" fontSize="14" color="#10C2B0" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/>
                    <Label text="Số lượng" col="1" fontSize="14" color="#10C2B0" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/>
                    <Label text="Đơn giá" col="2" color="#10C2B0" fontSize="14" horizontalAlignment="center" verticalAlignment="bottom" margin="3"/>
                    <Label text="Thành tiền" col="3" color="#10C2B0" fontSize="14" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/>
                </GridLayout>
                <GridLayout :key="item.name" v-for="item in cart" columns="150,*,*,*" rows="auto,25" verticalAlignment="top" backgroundColor="white">                    
                    <Label :text="item.name" col="0" fontSize="14" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/>
                    <Label :text="item.soluong" col="1" color="#10C2B0" fontSize="14" horizontalAlignment="center" verticalAlignment="bottom" margin="3"/>
                    <Label :text="item.price" col="2" color="#10C2B0" fontSize="14" horizontalAlignment="center" verticalAlignment="bottom" margin="3"/>
                    <Label :text="(item.price * item.soluong)" col="4" color="#10C2B0" fontSize="14" horizontalAlignment="center" verticalAlignment="bottom" margin="3"/>                    
                </GridLayout>
                <Label text="------------------------------------------------------" color="darkgray" />
                <GridLayout columns="50,*,auto,*,auto" rows="auto,auto,auto">
                    <Label text="Hóa Đơn : " row="0" col="0" colSpan="2" />
                    <Label :text="itemcount" row="0" col="2" colSpan="2" />
                    <Label :text="formatPrice(total)" row="0" col="4"/>
                    <Label text="Phí vận chuyển" row="1" col="0" colSpan="2" />
                    <Label :text="formatPrice(3)" row="1" col="4"/>
                    <Label text="Tổng thanh toán : " row="2" col="0" color="red" colSpan="2" />
                    <Label text="" row="2" col="2" colSpan="2" />
                    <Label :text="formatPrice(total + 3)" row="2" color="red" col="4"/>
                </GridLayout>
                <GridLayout>
                    <Button text="Hoàn tất" color="white" backgroundColor="aqua" fontSize="20" borderRadius="15" width="100" height="50" @tap="complete()" />
                </GridLayout>
            </StackLayout>
        </FlexboxLayout>
    </Page>
</template>
<script>

export default {
    props:["cart","people"],
    data(){
        return {
        
        }
    },
    computed: {
    total() {
      var tongtien = 0;
      for (var i = 0; i < this.cart.length; i++) {
        tongtien += this.cart[i].soluong * this.cart[i].price;
      }
      return tongtien;
    },
    },
    methods: {
    formatPrice(value) {
      let val = (value / 1).toFixed(2).replace(".", ",");
      return "£" + val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    },
    complete(){
        confirm({
            title: "Xác nhận đơn hàng",
            message: "Chúng tôi sẽ liên lạc xác minh 1 lần nữa qua số điện thoại bạn cung cấp",
            okButtonText: "OK",
            cancelButtonText: "Cancel"
            }).then(result => {
            alert({
                title: "Thông báo",
                message: "Đơn đặt hàng thành công !",
                okButtonText: "OK"
                }).then(() => {
                console.log("Alert dialog closed");
            });
        });
    }
    }
}
</script>
<style scoped>

</style>