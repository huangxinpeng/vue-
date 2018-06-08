<template>
	<div class="wrapper">
		<div class="model" v-show="model" @click="model = false">
			<div class="model-show">
				<img :src="modelSrc" alt="">
			</div>
		</div>
		<div class="content">
			<div class="show-info">
				<h2>example2 自动生成截图框 固定比例 w : h => 4 : 3</h2>
				<div v-if="show" class="test">
					<vueCropper
						ref="cropper2"
						:img="example2.img"
						:outputSize="example2.size"
						:outputType="example2.outputType"
						:info="example2.info"
						:canScale="example2.canScale"
						:autoCrop="example2.autoCrop"
						:autoCropWidth="example2.autoCropWidth"
						:autoCropHeight="example2.autoCropHeight"
						:fixed="example2.fixed"
						:fixedNumber="example2.fixedNumber"
					></vueCropper>
					<button @click="finish2('base64')" class="btncq ">返回</button>
					<button @click="finish2('base64')" class="btncq btncqout">确定</button>
				</div>
				<!-- <div v-for="(img,index) in modelSrc" :key="index">
					<img :src="img" alt="">
				</div> -->
				<div  v-for="(i,index) in modelSrc" :key="index">
					<img  :src="i" alt="">
				</div>
				<label  class="btn" for="upload2">上传</label>
				<input type="file" id="upload2" style="position:absolute; clip:rect(0 0 0 0);" accept="image/png, image/jpeg, image/gif, image/jpg" @change="uploadImg($event, 2)">
				<button @click="finish2('base64')" class="btn">确定裁切</button>
			</div>
		</div>
	</div>
</template>

<script>
import vueCropper from './vue-cropper'
import codes from './code'

export default {
  data: function () {
    return {
			show:false,//显示裁切框
			model: false,
			modelSrc: [],
			modelshow:false,
		 	crap: false,
			previews: {},
			option: {
				img: '',
				size: 1,
				full: false,
				outputType: 'png',
				canMove: true,
				fixedBox: false,
				original: false,
				canMoveBox: true
			},
			example2: {
				// img: 'http://ofyaji162.bkt.clouddn.com/bg1.jpg',
				img: '',
				info: true,
				size: 1,
				outputType: 'jpeg',
				canScale: true,
				autoCrop: true,
				// 只有自动截图开启 宽度高度才生效
				autoCropWidth: 300,
				autoCropHeight: 250,
				fixed: true,
				fixedNumber: [4, 3]
			},
			downImg: '#'
    }
  },
	methods: {
		finish2 (type) {
			this.$refs.cropper2.getCropData((data) => {
				// this.model = true
				this.model = false
				this.modelSrc.push(data)
				// this.modelSrc = data
				this.show = false
				console.log(this.modelSrc)//图片路径
			})
		},
		uploadImg (e, num) {
			//上传图片
			// this.option.img
			var file = e.target.files[0]
			if (!/\.(gif|jpg|jpeg|png|bmp|GIF|JPG|PNG)$/.test(e.target.value)) {
				 alert('图片类型必须是.gif,jpeg,jpg,png,bmp中的一种')
				 return false
			 }
			var reader = new FileReader()
			reader.onload = (e) => {
				let data
				if (typeof e.target.result === 'object') {
					// 把Array Buffer转化为blob 如果是base64不需要
					data = window.URL.createObjectURL(new Blob([e.target.result]))
				} else {
					data = e.target.result
				}
				if (num === 1) {
					this.option.img = data
				} else if (num === 2) {
					this.example2.img = data
				}
			}
			// 转化为base64
			// reader.readAsDataURL(file)
			// 转化为blob
			reader.readAsArrayBuffer(file)
			this.show = true
			console.log(reader)
			console.log(file)
			console.log(this.example2.img)
		}
	},
	components: {
		vueCropper,
		codes
	},

}
</script>

<style>
  * {
	  margin: 0;
		padding: 0;
	}

	.content {
		margin: auto;
		max-width: 1200px;
		margin-bottom: 100px;
	}
	.btncq{
		width:65px;
		height:32px;
		background:rgba(74,74,74,1);
		color: #fff;
		font-size: 14px;
		border-radius:4px;
		line-height: 32px;
		text-align: center;
		border:none;
	}
	.btncqout{
		background:linear-gradient(127.4deg,rgba(255,79,90,1),rgba(255,118,86,1));
	}
	.btn {
		display: inline-block;
		line-height: 1;
		white-space: nowrap;
		cursor: pointer;
		background: #fff;
		border: 1px solid #c0ccda;
		color: #1f2d3d;
		text-align: center;
		box-sizing: border-box;
		outline: none;
		margin:20px 10px 0px 0px;
		padding: 9px 15px;
		font-size: 14px;
		border-radius: 4px;
		color: #fff;
		background-color: #50bfff;
		border-color: #50bfff;
		transition: all .2s ease;
		text-decoration: none;
		user-select: none;
	}
	.test {
		width: 100%;
	  height: 500px;
	}

	.model {
		position: fixed;
		z-index: 10;
		width: 100vw;
		height: 100vh;
		overflow: auto;
		top: 0;
		left: 0;
		background: rgba(0, 0, 0, 0.8);
	}

	.model-show {
		display: flex;
		justify-content: center;
		align-items: center;
		width: 100vw;
		height: 100vh;
	}

	.model img {
		display: block;
		margin: auto;
		max-width: 80%;
		user-select: none;
		background-position: 0px 0px, 10px 10px;
		background-size: 20px 20px;
   		background-image: linear-gradient(45deg, #eee 25%, transparent 25%, transparent 75%, #eee 75%, #eee 100%),linear-gradient(45deg, #eee 25%, white 25%, white 75%, #eee 75%, #eee 100%);
	}

	.c-item {
		display: block;
		padding: 10px 0;
		user-select: none;
	}

	@keyframes slide {
    0%  {
      background-position: 0 0;
    }
    100% {
      background-position: -100% 0;
    }
  }

</style>
