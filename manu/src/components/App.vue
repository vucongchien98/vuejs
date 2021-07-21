<template>
    <Page>
      <!-- Action bar  -->
        <ActionBar>
          <StackLayout orientation="horizontal" width="100%" height="100%" backgroundColor="#000">
            <Label text="MANCHESTER UNITED" verticalAlignment="center" />
            <Image src="~/assets/images/logo.png" height="40" width="40" verticalAlignment="right" />
          </StackLayout>
        </ActionBar>
        <!-- phần tab view  -->
        <TabView :selectedIndex="selectedIndex" iosIconRenderingMode="alwaysOriginal" fontSize="20" >
          <!-- trang 1 -->
          <TabViewItem title="Home" class="tab-view">
          <!-- banner -->
        <GridLayout orientation="vertical" columns="*" rows="*,auto" width="100%" height="100%">
          <StackLayout col="0" row="0">
          <StackLayout paddingLeft="20" paddingRight="20" paddingTop="20" paddingBottom="5" marginTop="5"
              backgroundImage="~/assets/images/banner.jpg" borderRadius="5" height="180" width="90%"
              class="album-image">
          </StackLayout>
          </StackLayout>
          <!-- Tin tức  -->
          <ScrollView orientation="vertical" marginTop="200">
            <StackLayout>
              <!-- thiết kế chữ tin chuyển nhượng -->
              <GridLayout columns="auto,*,auto" rows="auto">
                <Label text=" Tin chuyển nhượng " col="0" row="0" fontWeight="bold" marginLeft="10" fontSize="20"
                color="yellow" backgroundColor="red" marginBottom="10" borderColor="yellow" borderRadius="10" />
              </GridLayout>
              <!-- đỗ dữ liệu vào -->
              <ScrollView orientation="horizontal" OverflowX="hidden">
                <StackLayout orientation="horizontal">
                  <StackLayout v-for="i in News" :key="i.title" marginLeft="10">
                    <!-- để hình ảnh -->
                    <GridLayout class="album-image" height="110" width="125" :backgroundImage="i.imgsrc" borderRadius="5" @tap="showMore(i)">
                    </GridLayout>
                    <!-- thiết kế tên-->
                    <Label :text="i.title" fontSize="14" color="#000000"/>
                  </StackLayout>
                </StackLayout>
              </ScrollView>
            <!-- shop -->
            <GridLayout columns="auto,*,auto" rows="auto" marginTop="15">
                <Label text="Shop" col="0" row="0" fontWeight="bold" marginLeft="10" fontSize="20"
                color="yellow" backgroundColor="red" marginBottom="10" borderColor="yellow" borderRadius="10"  />
                <Label text="Xem thêm" col="2" row="0" fontSize="14" marginRight="20" color="blue" @tap="openShop()" />
              </GridLayout>
              <!-- đỗ dữ liệu vào -->
              <ScrollView orientation="horizontal" Overflow-x="hidden">
                <StackLayout orientation="horizontal">
                  <StackLayout v-for="pr in products" :key="pr.name" marginLeft="10">
                    <!-- thiết kế tên -->
                    <Label :text="pr.name" fontSize="14" color="#000000" marginLeft="15"/>
                    <!-- để hình ảnh -->
                    <GridLayout class="album-image" height="110" width="125" :backgroundImage="pr.imgsrc" borderRadius="5">
                    </GridLayout>
                  </StackLayout>
                </StackLayout>
              </ScrollView>
            <!-- bàn thắng đẹp -->
            <StackLayout marginTop="15">
              <GridLayout columns="auto,*,auto" rows="auto">
                <Label text="Các trận đấu hay mùa giải 2020-2021" col="0" row="0" fontWeight="bold" marginLeft="10" fontSize="20"
                color="yellow" backgroundColor="red" marginBottom="10" borderColor="yellow" borderRadius="10" />
              </GridLayout>
              <ListView for="obj in videos">
              <v-template>
                <FlexboxLayout flexDirection="row">
                  <StackLayout orientation="vertical">
                    <GridLayout columns="auto,*,auto" rows="auto,25"
                    verticalAlignment="top" backgroundColor="white" >
                      <Image :src="obj.imgsrc" col="0" horizontalAlignment="left"
                      verticalAlignment="bottom" margin="3" class="img"/>
                      <Label :text="obj.title" col="1" fontSize="14" horizontalAlignment="left"
                      verticalAlignment="center" class="name"/>
                      <Button text="Xem Video" col="2" color="#10C2B0" fontSize="14"
                      horizontalAlignment="center" marginLeft="10" width="100"
                       height="40" backgroundColor="red" textAlign="center" @tap="openWeb(obj)" borderRadius="10"/>
                    </GridLayout>
                  </StackLayout>
                </FlexboxLayout>
              </v-template>
        </ListView>
            </StackLayout>
            </StackLayout>
          </ScrollView>
          </GridLayout>
          </TabViewItem>
          <!-- trang 2 -->
        <TabViewItem title="Team" class="tab-view">
           <ListView for="obj in footballers">
              <v-template>
                <FlexboxLayout flexDirection="row">
                  <StackLayout orientation="vertical">
                    <Label :text=obj.header class="name-title"/>
                    <GridLayout :key="item.name" v-for="item in obj.items" columns="auto,*,auto" rows="auto,25"
                    verticalAlignment="top" backgroundColor="white" >
                      <Image :src="item.imgsrc" col="0" horizontalAlignment="left"
                      verticalAlignment="bottom" margin="3" class="img" />
                      <Label :text="item.name" col="1" fontSize="14" horizontalAlignment="left"
                      verticalAlignment="center" class="name" @tap="showInfor(item)" />
                      <Label :text="item.position" col="2" color="blue" fontSize="14"
                      horizontalAlignment="center" verticalAlignment="center" margin="3"/>
                    </GridLayout>
                  </StackLayout>
                </FlexboxLayout>
              </v-template>
        </ListView>
        </TabViewItem>        
      </TabView>
    </Page>
</template>
<script >
import Team from "./Team"
import Video from "./Video"
import newMore from "./newMore"
import Shop from "./Shop"
  export default {
  watch: {
  },
    data() {
      return {
        News : [
          {
            title : "Jadon Sancho",
            imgsrc: "~/assets/images/sancho.jpg",
            content: "Sau nhiều tháng đàm phán, truyền thông Anh đồng loạt đưa tin MU đã đạt thỏa thuận với Dortmund về việc chiêu mộ Jadon Sancho với giá 73 triệu bảng.<br/>"
          },
          {
            title : "Juan Mata",
            imgsrc: "~/assets/images/juan.jpg",
            content: "Mata chính thức kí hợp đồng với MU thêm 1 năm nữa.!!"
          },
          {
            title : "Raphael Varane",
            imgsrc: "~/assets/images/varane.jpg",
            content: "Theo tin từ Manchester Evening Evening News, MU đã chính thức gửi lời đề nghị trị giá 50 triệu bảng đến Real Madrid để chiêu mộ Raphael Varane, người hiện đang thi đấu ấn tượng cùng đội tuyển Pháp ở EURO 2021. Tuy nhiên, con số này vẫn thấp hơn yêu cầu của Real Madrid đến…. 30 triệu bảng. Phía MU, tất nhiên, không đồng ý với đòi hỏi của đội bóng hoàng gia Tây Ban Nha, do Varane chỉ còn hợp đồng đến hè sang năm."
          },
          {
            title : "Tom Heaton",
            imgsrc: "~/assets/images/tom.jpg",
            content: "CHÍNH THỨC: WELCOME [BACK] TO OLD TRAFFORD .<br> Chào mừng sự trở lại của Tom Heaton, một sản phẩm của lò đào tạo Carrington và sẽ bổ sung nhân sự ở vị trí thủ môn cho MU sau khi Joel Pereira hết HĐ và ra đi. "
          }
        ],
        videos: [
            {
              title: "Manchester City",
              imgsrc: "~/assets/images/manc2.jpg",
              webSrc: "https://www.youtube.com/watch?v=ghs3S48bNcE"
            },
            {
              title: "Tottenham",
              imgsrc: "~/assets/images/tot.jpg",
              webSrc: "https://www.youtube.com/watch?v=8MuEN4-xiss"
            },
            {
              title: "As Roma",
              imgsrc: "~/assets/images/asroma.jpg",
              webSrc: "https://www.youtube.com/watch?v=F0Cv2WZWCa0"
            }
        ],
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
        footballers: [
          {
            header: "GOALKEEPERS",
            items: [
              {
                imgsrc: "~/assets/images/gea.png",
                name: "David DeGea",
                birthday: "7/11/1990",
                position: "GK",
                national: "Spain"
              },
              {
                imgsrc: "~/assets/images/dean.png",
                name: "Dean Henderson",
                birthday: "12/03/1997",
                position: "GK",
                national: "England"
              }
            ]
          },
          {
            header: "DEFENDERS",
            items: [
              {
                imgsrc: "~/assets/images/l2.png",
                name: "Victor Lindelof",
                birthday: "17/07/1994",
                position: "CB",
                national: "Sweden"
              },
              {
                imgsrc: "~/assets/images/m5.png",
                name: "Harry Maguire",
                birthday: "05/03/1993",
                position: "CB",
                national: "England"
              },
              {
                imgsrc: "~/assets/images/shaw3.png",
                name: "Luke Shaw",
                birthday: "12/07/1995",
                position: "LB",
                national: "England"
              },
              {
                imgsrc: "~/assets/images/wanbi.png",
                name: "Aaron Wan-Bissaka",
                birthday: "26/11/1997",
                position: "RB",
                national: "Congo"
              }
            ]
          },

          {
            header: "MIDFIELDERS",
            items: [
              {
                imgsrc: "~/assets/images/p6.png",
                name: "Pau Pogba",
                birthday: "15/03/1993",
                position: "AC",
                national: "France"
              },
              {
                imgsrc: "~/assets/images/fredd.png",
                name: "Fred",
                birthday: "05/03/1993",
                position: "CDM",
                national: "Brazil"
              },
              {
                imgsrc: "~/assets/images/mctomi.png",
                name: "Scott McTominay",
                birthday: "08/12/1996",
                position: "CDM",
                national: "Scotland"
              },
              {
                imgsrc: "~/assets/images/bruno18.png",
                name: "Bruno Fernandes",
                birthday: "08/09/1994",
                position: "DM",
                national: "Portugal"
              }
            ]
          },

          {
            header: "FORWARDS",
            items: [
              {
                imgsrc: "~/assets/images/m9.png",
                name: "Anthony Martial",
                birthday: "05/12/1995",
                position: "ST",
                national: "France"
              },
              {
                imgsrc: "~/assets/images/r4.png",
                name: "Marcus Rashford",
                birthday: "31/10/1997",
                position: "AL",
                national: "England"
              },
              {
                imgsrc: "~/assets/images/g11.png",
                name: "Mason Greenwood",
                birthday: "01/10/2001",
                position: "AR",
                national: "England"
              },
              {
                imgsrc: "~/assets/images/c7.png",
                name: "Edison Cavani",
                birthday: "14/02/1987",
                position: "ST",
                national: "Uruguay"
              }
            ]
          },
        ]
      }
    },
    methods :{
      showInfor(item){
        this.$navigateTo(Team,{
          animated: true,
          transition: {
              name: "slideLeft",
              duration: 250, 
              curve: "easeIn", 
          },
          props: {
            item: item
          }
        })
      },
      openWeb(obj){
        this.$showModal(Video,{
          props: {
            item: obj
          }
        })
      },
      showMore(i){
        this.$navigateTo(newMore, {
          props: {
            item: i
          }
        })
      },
      openShop(){
        this.$navigateTo(Shop)
      }
    }
  }
</script>

<style scoped>
    ActionBar {
        color: yellow;
    }
    #logo {
      margin-top: 20;
    }
    .img {
      border-radius: 20;
      width: 100;
      height: 100;
    }
    .name {
      font-size: 20;
      color: red;
      font-weight: bold;
    }
    .name-title {
      height: 30;
      color:#FF0000;
      background-color: #33FFCC;
    }
    .album-image{
      background-repeat: no-repeat;
      background-size: cover;
      background-position: center;
    }
    .tab-view {
      font-size: 18;
      font-weight: bold;
    }
    /* #btn-show {
      margin-bottom: 30;
      width: 100%;
      height: 30;
      background: red;
      border-radius: 20;
      color: yellow;
      font-size: 20;
      font-weight: bold;
    } */
</style>
