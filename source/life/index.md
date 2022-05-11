---
title: 热爱生活
date: 2022-05-06 16:38:29
---

<h4 class="title4">岁月永远年轻，我们慢慢老去，你会发现，童心未泯，是一件值得骄傲的事情 </h4>

<style type="text/css">
    .title4{
    text-align: center;
    color: #fafafa;
    letter-spacing: 0;
    font-size:32px;
    margin: 2em auto;
    background: #3f9;
    width: 34em;
    }
    
    
    .sidebar{
        display: none;
    }
    .content{
        margin-bottom: 360px;
    }
    .content-wrap{
       width: 100%;
       // box-sizing: content-box;
       padding: initial !important;
       //background:url('https://s1.ax1x.com/2020/05/11/YJxcgx.jpg');
    }
    
	.main-inner{
		width: 100%;
	}
	.sidebar-toggle{
	display: none !important;
	}
	.eye{
	display: none !important;
	}
	.aplayer-body{
	display: none;
	}
	.main {
        padding-bottom: 150px;
        margin-top: 30px !important;
        padding-top: 16em;
	}
	.main-inner{
		margin-top: unset;
	}
	.page-post-detail .post-meta{
		display: none;
	}
	body {
		background-image: unset;
		background-attachment: unset;
		background-size: 100%;
		/*background-position: top left;*/
	}
	
	}
	.menu .menu-item a{
		    font-weight: 300;
    		color: #e6eaed;
	}
	.footer-inner {
    	 padding-left: 0px;
    }
    
    img:hover {
        //opacity:0.8; /*透明度*/
        //filter:alpha(opacity=100); /* For IE8 and earlier */
    }
    
	.imgbox{
	    margin-top: 20px;
	    padding: 1px 10px;
        width: 100%;
        overflow: hidden;
        height: 250px;
	    border-right: 1px solid #bcbcbc;
	}
	.box{
		visibility: visible;
		overflow: auto; 
		zoom: 1;
	}
	.box li{
        float: left;
        width: 25%;
        position: relative;
        overflow: hidden;
        text-align: center;
        list-style: none;
        margin: 0;
        /*display: inline;*/
        padding: 0;
        height: 260px;
	}
	.box li span{
        display: block;
        padding: 4% 7% 10% 7%;
        min-height: 80px;
        //background: #fff;
        font-size: 16px;
        font-weight: 600;
        line-height: 26px;
        -webkit-box-sizing: border-box;
        box-sizing: border-box;
        color: #3f9;
	}

	img.imgItem{
		padding: unset;
		padding: unset;
		border: unset;
		position: relative;
		padding: 0px;
		height: 100%;
		width: 100%;
	}

    div#posts.posts-expand {
        border: unset;
        padding: unset;
        margin-bottom: 10px;
    }
    .posts-expand .post-body img{
        padding: 0px !important;
    }
    .box p{
        margin-top: -25px;
        display: block;
        background: #121212;
        color: #fff;
        font-size: 14px;
        -webkit-box-sizing: border-box;
        box-sizing: border-box;
        text-align: center;
    }
    
    .box span strong{
        background: rgba(0,0,0,0.4);
        padding: 20px;
    }
    
    .posts-expand .post-title {
        display: none;
    }
    
    .title{
        margin: 10px auto;
        display: inline-block;
        vertical-align: middle;
        //background: url(/images/beichen.jpg);
        font: 85px/250px 'ChaletComprimeMilanSixty';
        //background-position: left bottom !important;
        background-position: center center !important;
        color: #fff;
        background-size: 100% auto !important; 
        -webkit-background-size: cover; 
        -moz-background-size: cover;
        -o-background-size: cover;
        width: 100%;
        text-align: center;
        border: unset;
        height: 560px;
        cursor: unset !important;
        -webkit-box-sizing: border-box;
        box-sizing: border-box;
    }

    @media (max-width: 767px){
        .box li {
            width: 98%;
        }
        .title {
            height: 200px;
        }
        
        .box span {
            min-height: 80px;
            border-right: unset;
            font-size: 17px;
        }
        .box p{
            border-right: unset;
            font-size: 12px;
          
        }
        .posts-expand {
            margin: unset;
        }
    
    }

    @media (min-width: 1600px){
    
        .container .main-inner{
            width: 100%;
        }
    }

</style>

<div id="box" class="box"></div>

<script type="text/javascript">
   
   // 相册json  
   var json = 
    [
    	[
            {
                'title': '唯美背景',
                'url': 'http://ww1.sinaimg.cn/large/006brE51gy1gepyclhyj5j30v90kudk3.jpg'
            },
            {
                'title': ' ',
                'url': 'http://ww1.sinaimg.cn/large/006brE51gy1gepzx8g7dlj30dw08zwei.jpg'
            },
            {
                'title': ' ',
                'url': 'https://s1.ax1x.com/2020/05/11/YJxRKK.jpg'
            },
            {
                'title': ' ',
                'url': 'http://ww1.sinaimg.cn/large/006brE51gy1geq08gz2gnj30u80kuq66.jpg'
            }

    	],
    	
          
    ]
    
    var content = json2Array(json);
        
    var wid = 250;
    if ((window.innerWidth) > 1200) {
        wid = (window.innerWidth*3)/18;
    }
    var box = document.getElementById('box');
    
    var i=0;
    for (var i = 0; i < content.length; i++) {
    	var conBox = document.createElement("div");
    	conBox.id = 'conBox'+i;
    	box.appendChild(conBox);
    	var item = document.createElement("div");
    	var title = content[i][0].title;
    	var url = content[i][0].url;
    	item.innerHTML = "<button class = 'title' style = 'background: url(" + url + ");'><span style = 'display: inline;'><strong style = 'color:#f0f3f6;' >" + title + "</strong></span></button>";
    	conBox.appendChild(item);
    
    	for (var j = 1; j < content[i].length ; j++) {
    		var _title = content[i][j].title;
    		var _url = content[i][j].url;
    		var item = document.createElement("li");
    		item.innerHTML="<div class = 'imgbox' id = 'imgbox' style = 'height: " + wid + "px;'><img class = 'imgItem' src='" + _url + "' alt='" + _url + "'></div><span>" + _title +"</span>";
    		conBox.appendChild(item);
    	}
    }
    
    //json转二维数组
    function json2Array(arr) {
        for (var i=0; i<arr.length; i++) {
            var tmpArr = []
            for (var attr in arr[i]) {
                tmpArr.push(arr[i][attr])
            }
            arr[i] = tmpArr
        }
        return arr
    }

</script>
