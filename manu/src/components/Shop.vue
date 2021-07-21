<template>
    <Page>
        <ActionBar>
            <StackLayout orientation="horizontal">
                <Image src="~/assets/images/cart.png" height="40" width="40" @tap="showCart"/>
            </StackLayout>
        </ActionBar>
         <ListView for="item in products">
            <v-template >
                <FlexboxLayout flexDirection="column" rows="auto,*,*,*" marginBottom="20">
                    <Button :text="item.name" class="ten" row="1" verticalAlignment="center" horizontalAlignment="center" color="#000" fontSize="20" />
                    <Image :src="item.imgsrc" class="thumb img-circle" row="0" color="#000" />
                    <Button :text="formatPrice(item.price)" row="2" verticalAlignment="center" color="#996600" width="30"/>                       
                    <Button class="btn" text="Add to cart" row="3" color="white" width="150" borderRadius="10" @tap="addCart(item)" backgroundColor="#ff3300" />
                </FlexboxLayout>
            </v-template>
          </ListView>
    </Page>
</template>
<script>
import Cart from "./Cart"
export default {
    data(){
        return {
            products: [
          {
            name: "Áo sân nhà",
            price: 50,
            soluong: 1,
            imgsrc: "~/assets/images/Ao-mu-san-nha-1-2.jpg",
          },
          {
            name: "Áo sân khách",
            price: 50,
            soluong: 1,
            imgsrc: "~/assets/images/ao-san-khach.jpg",
          },
          {
            name: "Giày đá bóng",
            price: 30,
            soluong: 1,
            imgsrc: "~/assets/images/giay-mu.png",
          },
          {
            name: "Mũ len MU",
            price: 15,
            soluong: 1,
            imgsrc: "~/assets/images/mulen.jpg",
          },
          {
            name: "Nón MU",
            price: 10,
            soluong: 1,
            imgsrc: "~/assets/images/non.jpg",
          }
        ],
        cart: []  
        }
    },
    methods: {
      showCart() {
        this.$navigateTo(Cart, {
            transition: {
                name: "slideLeft",
                duration: 300,
                curve: "easeIn"
            },
            props: {
                cart: this.cart,
            }
        });
      },
      addCart(item) {
      var temp = false;
      if (this.cart == null) {
        temp = false;
      } else {
        for (var i = 0; i < this.cart.length; i++) {
          if (this.cart[i].name == item.name) {
            temp = true;
          }
        }
      }
      if (temp == false) {
        item.soluong = 1;
        this.cart.push(item);
      } else {
        for (var i = 0; i < this.cart.length; i++) {
          if (item.name == this.cart[i].name && this.cart[i].quantity != 0) {
            this.cart[i].soluong++;
          }
        }
      }
    },
    formatPrice(value) {
      let val = (value / 1).toFixed(2).replace(".", ",");
      return "£" + val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    }
    }
}
</script>
<style scoped>

</style>