<template>
  <Page>
    <ActionBar flat="true" title="Đơn Hàng" />
    <FlexboxLayout flexDirection="row">
      <StackLayout orientation="vertical">
        <Label text="Đơn hàng - MU Shop" color="#FF0000" backgroundColor="lightgay"/>
        <GridLayout columns="80,100,60,70,50,80" rows="auto" verticalAlignment="top" backgroundColor="yellow">
          <Label text="Image" col="0" fontSize="14" color="#10C2B0" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/>
          <Label text="Name" col="1" fontSize="14" color="#10C2B0" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/>
          <Label text="Quantity" col="2" color="#10C2B0" fontSize="14" horizontalAlignment="center" verticalAlignment="bottom" margin="3"/>
          <Label text="One Item" col="3" color="#10C2B0" fontSize="14" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/>
          <Label text="Sum" col="4" color="#10C2B0" fontSize="14" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/>
          <Label text="Del" col="5" verticalAlignment="bottom" color="#10C2B0" />
        </GridLayout>
        <GridLayout :key="item.name" v-for="item in cart" columns="80,100,60,70,50,80" rows="auto,25" verticalAlignment="top" backgroundColor="white">
          <Image :src="item.imgsrc" class="imageSP" col="0" fontSize="14" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/>
          <Label :text="item.name" col="1" fontSize="14" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/>
          <Label :text="item.soluong" col="2" color="#10C2B0" fontSize="14" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/>
          <!-- <Label text="x" col="3" color="#10C2B0" fontSize="14" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/> -->
          <Label :text="item.price" col="3" color="#10C2B0" fontSize="14" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/>
          <Label :text="(item.price * item.soluong)" col="4" color="#10C2B0" fontSize="14" horizontalAlignment="left" verticalAlignment="bottom" margin="3"/>
          <Button text="X" @tap="Xoa(item)" col="5" color="white" background="red" height="30" width="40" verticalAlignment="bottom" horizontalAlignment="left" />
        </GridLayout>
        <GridLayout columns="50,*,auto,*,auto" rows="auto,25">
          <Label text=" Hóa Đơn : " row="0" col="0" colSpan="2" />
          <Label :text="itemcount" row="0" col="2" colSpan="2" />
          <Label :text="formatPrice(total)" row="0" col="4"/>
        </GridLayout>
        <Button text="Thêm người nhận" color="yellow" backgroundColor="red" width="150" borderRadius="15" height="50" @tap="showModal" />
        <GridLayout>
            <Button text="Đặt hàng" color="white" backgroundColor="aqua" fontSize="20" width="100" height="50" borderRadius="15" @tap="openHd()" />
        </GridLayout>
      </StackLayout>
    </FlexboxLayout>
  </Page>
</template>
<script>
import Receipt from "./Receipt.vue"
import NameModal from "./NameModal.vue"
export default {
  props: ["cart"],
  data() {
    return {
      people: []
    };
  },
  computed: {
    itemcount() {
      var tong = 0;
      for (var i = 0; i < this.cart.length; i++) {
        tong += this.cart[i].soluong
      }
      return tong;
    },
    total() {
      var tongtien = 0;
      for (var i = 0; i < this.cart.length; i++) {
        tongtien += this.cart[i].soluong * this.cart[i].price;
      }
      return tongtien;
    },
  },
  methods: {
    showModal() {
      this.$showModal(NameModal).then(data => this.addItemToProvinceList(data));
    },
    addItemToProvinceList(data){
      var mang = {
        "hoten": data[0],
        "diachi": data[1],
        "sodienthoai": data[2]
      };
      this.people.push(mang);
      this.$refs.listview.refresh()
    },
    formatPrice(value) {
      let val = (value / 1).toFixed(2).replace(".", ",");
      return "£" + val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    },
    Xoa(item){
        confirm({
        title: "Xóa",
        message: "Bạn có muốn xóa không ?",
        cancelButtonText: "Hủy bỏ",
        okButtonText: "Ok",
      }).then((result) => {
        if(result == true) {
          this.cart.splice(this.cart.indexOf(item),1);
        }
    });
    },
    openHd(){
        this.$navigateTo(Receipt,{
          props: {
            cart: this.cart,
            people: this.people
          }
        })
    }
  }
}
</script>

<style>
.imageSP {
  width: 150px;
  height: 150px;
}
</style>