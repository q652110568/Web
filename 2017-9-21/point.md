## ǰ��
�þ�ûдcanvas�ˣ�׼����canvas����logo������ͻȻ���ֶ�DOM�ڵ�Ŀ�ȡ��߶ȵļ����е������ˣ����¸�ϰ�°ɡ�

---
## ����ģ��
�����ۿ��֮ǰ����˵��CSS�ĺ���ģ�ͣ�
ÿһ�����Ӷ����Է�Ϊ��content��padding��border��margin�ĸ����֡�
![box](http://img.blog.csdn.net/20170921195843863?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3dsOTc5NjIzMDc0/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
����ģ�ͷ�Ϊ���֣���׼����ģ�ͺ�IE����ģ��
**����**
 1.��׼����ģ����content�а���content
 2.IE����ģ����content�а���content��padding��border

---
## ����
ǰ�˿�߼����ܹ���Ϊ����Ļ�����ڡ��ĵ���DOM�ڵ㣩�ļ���

---
## ��Ļ
�������Ļ��ָ�ĵ�����ʾ����ÿ����Ļ�Ŀ�߶��ǹ̶�ֵ

```
let getScreenAttr = () => {
	return {
		width:screen.width,		
		height:screen.height,	//������Ļ�ĸ߶ȣ������������ĸ߶�
		availWidth:screen.availWidth,
		availHeight:screen.availHeight,	//������Ļ�ĸ߶ȣ��������������ĸ߶�
		availTop:screen.availTop,		//δ��ϵͳ����ռ�õ����Ϸ�������ֵ��ֻ������������
		availLeft:screen.availLeft,		//	δ��ϵͳ����ռ�õ�����������ֵ��ֻ������������
	}
}
```
������Ҫע���height��availHeight������height�ĸ߶Ȱ�����Ļ�¶˵��������ĸ߶ȣ�availHeight�������������ĸ߶ȡ�

---
## ����
����Ĵ���ָ���������ҳ�棬���ڵĴ�С���Ǵ���ʵ�����ŵĴ�С����λΪ����
```
let getWindowAttr = () => {
	return {
		innerWidth:window.innerWidth,		//���ڿ��������ܹ����ļ�����Ļ��������С֮�󣬿�ȸ߶ȶ��仯���Ŀ��
		innerHeight:window.innerHeight,		//���ڿ�������ĸ߶�
		outerWidth:window.outerWidth,		//�����������������
		outerHeight:window.outerHeight,		//�����������������
		screenTop:window.screenTop,			//�������ϽǾ��������Ļ���˵ľ���
		screenLeft:window.screenLeft,		//�������ϽǾ��������Ļ��˵ľ���
	}
}
```
���㴰�����ǳ��õ���innerHeight��innerWidth����outerHeight��outerWidth���������������Ƿ�����������͹�������

---
## �ĵ���DOM�ڵ㣩
������ĵ���body����ָ������HTMLҳ�棬��ȻҲ������ȥ����DOM�ڵ�Ŀ�ߡ�
```
let getDomAttr = ele => {
	if(!ele){
		ele = document.body;
	}
	let bound = ele.getBoundingClientRect();
	let str = `width: ${bound.width},height: ${bound.height},top: ${bound.top},bottom: ${bound.bottom},left: ${bound.left},right: ${bound.right},`;
	return {
		clientWidth:ele.clientWidth,		//body�������򣨼�body��ҳ�����ܿ��ļ����֣��Ŀ��(����box-content,padding)
		clientHeight:ele.clientHeight,	//body�������򣨼�body��ҳ�����ܿ��ļ����֣��ĸ߶�
		offsetWidth:ele.offsetWidth,		//ͬ��clientWidth�����ǰ����߿�Ŀ��(����padding,box-content,border)
		offsetHeight:ele.offsetHeight,	//ͬ��clientHeight�����ǰ����߿�Ŀ��
		clientTop:ele.clientTop,		//boder�Ŀ��
		clientLeft:ele.clientLeft,	//boder�Ŀ��
		getBoundingClientRect:str,	//���ӵĿ�ȡ��߶�(������margin)��top��left��right��botom(ע�⣺left��right����ʱ����Ԫ�ؿ�����������padding������border�������Ͻ�Ϊԭ����㣬top��bottom�����½�Ϊԭ�㣬����width:left+right;height:bottom-top;)
		getClientRect:ele.getClientRects(),
	}
}
```
### clientWidth��clientHeight
��Ҫע�����������API�ڼ���ʱ��ֻ����content��padding��ֵ��
### offsetWidth��offsetHeight
������API������**clientWidth��clientHeight**�������������Ǽ���ʱ�Ὣborder��ֵ�����ȥ
### clientTop��clientLeft
�������API�����������ӵ�border�Ŀ�ȵģ���Ȼ�������Ͽ����ǲ�������border���κι�ϵ
### getBoundingClientRect
���ò�˵��getBoundingClientRect�����᷵��һ��ClientRect����������������������
|����|����|
|----|----|
|width|���ص��Ǻ��ӵĿ�ȣ�����content��padding��border����Ҫע�����������margin��|
|heigh|���ص��Ǻ��ӵĸ߶ȣ�����content��padding��border����Ҫע�����������margin��|
|top|���ص��Ǻ������ϽǾ���������������Ĵ�ֱ�߶ȣ�**ע�⣺**��������Ͻ���border�����Ͻ�|
|bottom|���ص��Ǻ������½Ǿ���������������Ĵ�ֱ�߶ȣ�**ע�⣺**��������½���border�����½�|
|left|���ص��Ǻ������ϽǾ��������������ˮƽ���ȣ�**ע�⣺**��������Ͻ���border�����Ͻ�|
|right|���ص��Ǻ������ϽǾ�����������Ҳ��ˮƽ���ȣ�**ע�⣺**��������Ͻ���border�����Ͻ�|
### getClientRects
��getBoundingClientRect���ƣ����������ص���һ��ClientRectList����

---
# Ӧ��
## ����
���ȵ��������һ������������ĵ�֮��ļ����ϵ��������body����˵����
 > �ɹ����ĸ߶� = �ĵ��ĸ߶� - ���ڵĸ߶ȣ�������content�ĸ߶ȣ�
�����ǽ��ĵ��滻��DOMԪ��ʱ
 > �ɹ����ĸ߶� = DOM���ĵ��ĸ߶� - DOM�ĸ߶ȣ�������content�ĸ߶ȣ�

### �����߶ȵĻ�ȡ
```
let getScrollAttr = () => {
	return {
		scrollTop:document.body.scrollTop,			//��������Ĺ����������ĵ����˵ľ���
		scrollLeft:document.body.scrollLeft,		//��������Ĺ����������ĵ���˵ľ���
		scrollWidth:document.body.scrollWidth,		//�ĵ��Ŀ��,����box-content,padding
		scrollHeight:document.body.scrollHeight,	//�ĵ��ĸ߶�,����box-content,padding
	}
}
```

**���������ǣ�** document.body.clientHeight��document.body.scrollHeight���ǿ��Լ����ĵ��ĸ߶ȣ����Ƕ���ֻ����content��padding�����ǽ��������ϸ΢�Ĳ��ԭ��δ�鵽������ϣ�����ͬ������½���

---
## demo
���Ա�д��һ��demo
![����дͼƬ����](http://img.blog.csdn.net/20170921200150389?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3dsOTc5NjIzMDc0/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
### Դ�룺
```
<!DOCTYPE html>
<html>
<head>
	<title>document window screen DOM</title>
	<style type="text/css">
		html,body{
			padding: 0px;
			margin: 0px;
			height: 2000px;
		}
		
		#box{
			margin: 100px 400px;
			padding: 100px 0;
			border: 50px dashed #CCC;
			text-align:center;
			box-sizing: content-box;
		}
		
		table,td,th{
			border: 1px solid #CCC;
			border-collapse:collapse;
			text-align: center;
			padding: 5px;
		}
		
		.can{
			display: inline-block;
			margin: 0 20px;
		}
	</style>
</head>
<body>
	
	<div style="border: 1px solid blue;margin:10px;">
		<div id="box">
			<p style="width: 100px;height: 100px;background: blue;color: white;display: inline-block;line-height: 100px; ">box-content</p>
		</div>
	</div>
	<div id="rs"></div>
	<script type="text/javascript">
		//�������ɹ����߶�Ϊ���ĵ��ĸ߶ȣ�document.body.scrollHeight�� - ��Ļ�������ĸ߶ȣ�window.innerHeight��
		//���ԣ��������������ڵͶ˵������
		//document.body.scrollTop = document.body.scrollHeight - window.innerHeight
		//window.scrollTo(0,document.body.scrollHeight - window.innerHeight)

		let getWindowAttr = () => {
			return {
				innerWidth:window.innerWidth,		//���ڿ��������ܹ����ļ�����Ļ��������С֮�󣬿�ȸ߶ȶ��仯���Ŀ��
				innerHeight:window.innerHeight,		//���ڿ�������ĸ߶�
				outerWidth:window.outerWidth,		//�����������������
				outerHeight:window.outerHeight,		//�����������������
				screenTop:window.screenTop,			//�������ϽǾ��������Ļ���˵ľ���
				screenLeft:window.screenLeft,		//�������ϽǾ��������Ļ��˵ľ���
			}
		}

		let getDomAttr = ele => {
			if(!ele){
				ele = document.body;
			}
			let bound = ele.getBoundingClientRect();
			let str = `width: ${bound.width},height: ${bound.height},top: ${bound.top},bottom: ${bound.bottom},left: ${bound.left},right: ${bound.right},`;
			return {
				clientWidth:ele.clientWidth,		//body�������򣨼�body��ҳ�����ܿ��ļ����֣��Ŀ��(����box-content,padding)
				clientHeight:ele.clientHeight,	//body�������򣨼�body��ҳ�����ܿ��ļ����֣��ĸ߶�
				offsetWidth:ele.offsetWidth,		//ͬ��clientWidth�����ǰ����߿�Ŀ��(����padding,box-content,border)
				offsetHeight:ele.offsetHeight,	//ͬ��clientHeight�����ǰ����߿�Ŀ��
				clientTop:ele.clientTop,		//boder�Ŀ��
				clientLeft:ele.clientLeft,	//boder�Ŀ��
				getBoundingClientRect:str,	//���ӵĿ�ȡ��߶�(������margin)��top��left��right��botom(ע�⣺left��right����ʱ����Ԫ�ؿ�����������padding������border�������Ͻ�Ϊԭ����㣬top��bottom�����½�Ϊԭ�㣬����width:left+right;height:bottom-top;)
				getClientRect:ele.getClientRects(),
			}
		}

		let getScreenAttr = () => {
			return {
				width:screen.width,		
				height:screen.height,	//������Ļ�ĸ߶ȣ������������ĸ߶�
				availWidth:screen.availWidth,
				availHeight:screen.availHeight,	//������Ļ�ĸ߶ȣ��������������ĸ߶�
				availTop:screen.availTop,		//δ��ϵͳ����ռ�õ����Ϸ�������ֵ��ֻ������������
				availLeft:screen.availLeft,		//	δ��ϵͳ����ռ�õ�����������ֵ��ֻ������������
			}
		}

		//�����������ĸ߶� = �ĵ��ĸ߶� - ��������box���ĸ߶�
		let getScrollAttr = () => {
			return {
				scrollTop:document.body.scrollTop,			//��������Ĺ����������ĵ����˵ľ���
				scrollLeft:document.body.scrollLeft,		//��������Ĺ����������ĵ���˵ľ���
				scrollWidth:document.body.scrollWidth,		//�ĵ��Ŀ��,����box-content,padding
				scrollHeight:document.body.scrollHeight,	//�ĵ��ĸ߶�,����box-content,padding
			}
		}
		
		let createTable = (type,data) => {
			let header = ['Attribute','Value'];
			let fragment = document.createDocumentFragment();
			
			let box = document.createElement('div');
			box.className = 'can';
			let div = document.createElement('h3');
			let title = document.createTextNode(type);
			div.appendChild(title);
			box.appendChild(div)

			let table = document.createElement('table');
			let tr = document.createElement('tr');
			for(let val of header){
				
				let th = document.createElement('th');
				let nodeText = document.createTextNode(val);
				th.appendChild(nodeText);
				tr.appendChild(th);
				
			}
			table.appendChild(tr);

			for(let attr in data){
				let tr = document.createElement('tr');
				let td1 = document.createElement('td');
				let text1 = document.createTextNode(attr);
				td1.appendChild(text1);
				tr.appendChild(td1);

				let td2 = document.createElement('td');
				td2.style.width = '150px';
				let text2 = document.createTextNode(data[attr]);
				td2.appendChild(text2);
				tr.appendChild(td2);

				table.appendChild(tr);
			}
			box.appendChild(table);
			fragment.appendChild(box);
			document.getElementById('rs').appendChild(fragment);
		}
		
		let init = () => {
			createTable('window',getWindowAttr());
			createTable('document',getDomAttr());
			createTable('DOM-#box',getDomAttr(document.getElementById('box')));
			createTable('screen',getScreenAttr());
			createTable('scroll',getScrollAttr());
		}

		(()=>{
			let rs = document.getElementById('rs');
			let box = document.getElementById('box');
			rs.style.position = 'fixed';
			rs.style.left = '0px';
			rs.style.bottom = '20px';

			window.onload = init;
			window.onscroll = function(e){
				let docHeight = document.body.scrollHeight;
				let winHeight = window.innerHeight;
				let scrollTop = document.body.scrollTop;
				if(scrollTop >= docHeight - winHeight){
					document.body.scrollTop -= 1;
					return;
				}
				let eles = document.querySelectorAll('.can')
				for(let i = 0; i<eles.length;i++){
					let ele = eles[i];
					ele.parentNode.removeChild(ele);
				}
				init();

			};				
		})();
	</script>
</body>
</html>
```