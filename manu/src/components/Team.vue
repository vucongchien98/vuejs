<template>
    <Page>
        <ActionBar title="THÔNG TIN CẦU THỦ">   
        </ActionBar>
        <FlexboxLayout flexDirection="row">
            <StackLayout orientation="vertical">
                <Image :src="item.imgsrc" width="100%" height="300" stretch="aspectFill"/>
                <Label :text="'Tên cầu thủ: '+ item.name" fontSize="20" fontWeight="bold" marginTop="10" marginLeft="100"  />
                <Label :text="'Ngày sinh: ' +item.birthday" margin="10"/>
                <Label :text="'Vị trí: ' +item.position" marginLeft="10"/>
                <Label :text="'Quốc tịch: ' +item.national" margin="10"/>
            </StackLayout>
        </FlexboxLayout>
    </Page>
</template>
<script>
export default {
    props:["item"],
    data(){
        return {
        }
    }
}
</script>
<style scoped>

</style>