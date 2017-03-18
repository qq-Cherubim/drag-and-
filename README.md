# drag-and-九宫格
拖拽吸附和九宫格


<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin: 0;
				padding: 0;
			}
			body{
				height:1000px;
			}
			#box{
				position:absolute;
				width: 100px;
				height: 100px;
				background: brown;
				overflow: auto;
			}
			#others{
				position: absolute;
				top:300px;
				left:500px;
				width:200px;
				height: 200px;
				background: yellow;
			}
		</style>
	</head>
	<body>
		aa
		<div id="box">
			
		</div>
		<div id="others">
			
		</div>
	</body>
	<script type="text/javascript">
		var box = document.getElementById('box');
		
		//鼠标初始位置
		var startP = {left:0,top:0};
		//元素初始位置
		var elementP = {left:0,top:0};
		box.onmousedown = function(ev){
			var ev = ev || event;
			//ev.preventDefault();	dom2的绑定方式，也可用在这
			
			//获取鼠标位置
			startP.left = ev.clientX;
			startP.top = ev.clientY;
			
			//获取元素位置
			elementP.left = box.offsetLeft;
			elementP.top = box.offsetTop;
			
			//全局捕获  处理ie8
			if(box.setCapture){
				box.setCapture();
			}
			
			
			document.onmousemove = function(ev){
				var ev = ev || event;
				
				//鼠标现在的位置
				var nowP = {};
				nowP.left = ev.clientX;
				nowP.top = ev.clientY;
				
				//鼠标的距离差
				var disX = 0;
				var disY = 0;
				disX = nowP.left - startP.left;
				disY = nowP.top - startP.top;
				
				//范围的限定
				var left = elementP.left + disX;
				var top = elementP.top + disY;
				
				if(left < 100){
					left = 0;
				}else if(left > document.documentElement.clientWidth-box.offsetWidth-100){
					left = document.documentElement.clientWidth-box.offsetWidth;
				};
				
				if(top < 100){
					top = 0;
				}else if(top > document.documentElement.clientHeight - box.offsetHeight-100){
					top = document.documentElement.clientHeight - box.offsetHeight;
				};
				
				
				
				box.style.left = left + 'px';
				box.style.top = top + 'px';
				
				var t1 = box.getBoundingClientRect().top;
				var l1 = box.getBoundingClientRect().left;
				var r1 = box.getBoundingClientRect().right;
				var b1 = box.getBoundingClientRect().bottom;
				
				var T1 = others.getBoundingClientRect().top;
				var L1 = others.getBoundingClientRect().left;
				var R1 = others.getBoundingClientRect().right;
				var B1 = others.getBoundingClientRect().bottom;
				
				if(t1>B1 || l1>R1 || r1<L1 ||b1<T1 ){
					others.style.background = 'yellow';
					others.innerText = 'yellow';
				}else{
					others.style.background = 'pink';
					others.innerText = 'pink';
				}
				
			}
			
			document.onmouseup = function(){
				document.onmousemove = document.onmouseup = null;
				if(box.releaseCapture){
					box.releaseCapture()
				}
				
			}
		
			//dom0
			return false;  //dom0的绑定方式
		}
		
		
		
		
	</script>
</html>

