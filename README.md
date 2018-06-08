使用方法: （注意index.js  改为loaclhost或者ip在浏览器输入）  


参考资料： https://github.com/xyxiao001/vue-cropper


1: cnpm install 下载所有依赖

2：cnpm install vue-cropper   在项目里面直接使用 import VueCropper from vue-cropper

名称	功能	默认值	可选值
img	裁剪图片的地址	空	url 地址 || base64 || blob
outputSize	裁剪生成图片的质量	1	0.1 - 1
outputType	裁剪生成图片的格式	jpg (jpg 需要传入jpeg)	jpeg || png || webp
info	裁剪框的大小信息	true	true || false
canScale	图片是否允许滚轮缩放	true	true || false
autoCrop	是否默认生成截图框	false	true || false
autoCropWidth	默认生成截图框宽度	容器的80%	0~max
autoCropHeight	默认生成截图框高度	容器的80%	0~max
fixed	是否开启截图框宽高固定比例	true	true | false
fixedNumber	截图框的宽高比例	[1 : 1]	[宽度 : 高度]
full	是否输出原图比例的截图	false	true | false
fixedBox	固定截图框大小 不允许改变	false	true | false
canMove	上传图片是否可以移动	true	true | false
canMoveBox	截图框能否拖动	true	true | false
original	上传图片按照原始比例渲染	false	true | false


内置方法 通过this.$refs.cropper 调用
this.$refs.cropper.startCrop() 开始截图
this.$refs.cropper.stopCrop() 停止截图
this.$refs.cropper.clearCrop() 清除截图
this.$refs.cropper.changeScale() 修改图片大小 正数为变大 负数变小
获取截图信息
this.$refs.cropper.cropW 截图框宽度

this.$refs.cropper.cropH 截图框高度

// 获取截图的base64 数据
this.$refs.cropper.getCropData((data) => {
  // do something
  console.log(data)  
})

// 获取截图的blob数据
this.$refs.cropper.getCropBlob((data) => {
  // do something
  console.log(data)  
})