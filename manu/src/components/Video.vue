<template>
  <Page>
     <GridLayout columns="*" rows="80,*" orientation="vertical">
          <Button row=0 text="Trở Về" @tap="$modal.close()" />
          <!-- lẫy dữ liệu đỗ lên webView -->
          <WebView row=1 :src="item.webSrc"/>
      </GridLayout>
  </Page>
</template>
<script>
export default {
  props:['item'],
  data() {
    return {
    }
  },
}
</script>