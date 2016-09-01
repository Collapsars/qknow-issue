## Canvas之全栈动画实现

****

先上图

![canvas.gif](http://7xw5qe.com1.z0.glb.clouddn.com/canvas.gif)

### 什么是Canvas

Canvas是在浏览器上绘图的一种机制。

传统的网页，总是使用GIF或者JPEG来显示图像，这种图形是需要事先画好，“静态”的图像；随着各种要求的发展，使用Flash或Java的“动态”图像也出现了。

而Canvas，则是不使用Flash和Java，而是用Javascript的一种绘图手段。

### 直接上代码

    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title></title>
        <link href="./css/colors.min.css" rel="stylesheet">
        <style media="screen">
          *{
            margin: 0;
            padding: 0;
          }
          .container{
            height: 700px;
            width: 540px;
          }
          #skill_canvas {
            width: 100%;
            background: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAa4AAAGuCAMAAAD/KxKoAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAytpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMDY3IDc5LjE1Nzc0NywgMjAxNS8wMy8zMC0yMzo0MDo0MiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wTU09Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9tbS8iIHhtbG5zOnN0UmVmPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvc1R5cGUvUmVzb3VyY2VSZWYjIiB4bWxuczp4bXA9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC8iIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6RURCRDc3RTk0QkQ2MTFFNTlFNTZDOEM3NDU4Q0M0RTQiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6RURCRDc3RTg0QkQ2MTFFNTlFNTZDOEM3NDU4Q0M0RTQiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgRmlyZXdvcmtzIENTNSAxMS4wLjAuNDg0IFdpbmRvd3MiPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDpEMTNDRTBDN0E2MDIxMUU0QURCMUNCMDRBNzA0RjEzMCIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDpEMTNDRTBDOEE2MDIxMUU0QURCMUNCMDRBNzA0RjEzMCIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PmEPxLgAAAL9UExURf39/vz9/fv8/fr7/Pn6/BIufPj4+/j5+/f4+vb3+vHz9/X2+fT1+fDy9/L0+Ozv9e3v9fP0+Ovu9O7w9uDk7uvt9OTn8OPm8O/x9uXo8d/j7urs8+nr8+bp8eHl793h7Ojr8uLm79zg6+fq8t7i7d7h7dvf69jd6dre6tfc6dnd6s3T487U5Nbb6MnP4dHX5srQ4tDV5czS49Xa6NHW5dPY58fO4MjP4dTZ58vR4s/U5NLY5sPK3sbN4MTL3sXM38LJ3RYxfsTL3zJKjR04glxwpba+1hk1gEZcmRk0gCI8hRcyfztSkxMvfSpDibrC2Z6qyiY/h8DH3EddmRs2gYSTu4aUvKy20WR2qaCry2h6rFRooI+cwamzzx45gx85g1lso2J0qK+507vD2YyZvxQwfRUwfq640oeVvb3F26u10XuLtqSvzX+OuCZAh0BWlWt9rYCPuXyLt3CBsLS91bK71G+Ar5Gewqexzo6bwJShxBo1gTFJjaiyz0pfm1ptpLG61JyoyXeHtHqKtoqYvqq00GV3qkhemhgzf25/r1hro0tgm6m00DNMjqGsy0BXljpRkrzE2rO81aWvzY+dwUJZl6OuzJ+rylJnnzRMjyM9hUNZl52pyWN1qZCdwjdPkXSEsoKQulNnoI2awElemoGQuWBzpyQ+hiU+hlZqoj1UlJikxiA6hE1inRw3gpKfwyxFinGCsF5xpoiWvbW91qawzi9HjD9VlSE7hIuZv1Vpobe/10RamHODsUxhnFdrojVNkGl7rE5jnZOgw0FYlnWGs5aixS1Gi11wprfA1ydBiGd5q2F0qIWUvFBlnoKRuniItShCiJqmx01inK230ilCiXaHs3KCscHI3W1+rk9knjlQkjNLjrC5036NuJumyFFmnzhQkWh5q19yp77G25WixH2Mt3mJtYmXvr/G3Gx+rlpupCtEijBIjLjB2Gp8rZynyC5Hi1tvpUVbmLnC2KKtzIOSu3WFspejxWZ4qjxTkz5VlJmlxjZOkP///zodC4kAAAD/dFJOU///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////AGb8ilkAACttSURBVHja7J0FmCM30rClZga7zczDzMu7YWZmZmbGSy6cXHJhvBwzMzMzM993dx/jT3p+zyYzbnvsGXtGarfdrnue3PbMboNeqVRVKpUA6mQBFI2AoGk0CiciEtKi2SAlWMWCDIIDWR8wUqk44kKZOI8kQ+IRw9EQdfYHd+h7U4ImIy4ezDF0spiUUTjuExEli0z5V3Dxo0D5P5DnGERrhkGDQDLqhwEr5EecoYpg9697uJx4XzEc01DYKuSAkIhprQwXSg7LSEplE5COJ3zUq2B7uAi9KlB8CRHksgUdcRKzgaGJ+Fghz6F4MqIgigY9XNjfU9ZzNJOxkgoSGFw3VYN5FcWiERNBuocL2zQVNoAcjUZoJBB4XSmXMZCeCsg9XBtHpQjI31cqTzYaQ/I5ZjAaQlxs0Qjp4Vr3uymZUgKJuuKA+c0ISIgO5xla43u4WhfOyIWREfRzDj4TKhqQUwUf3cPVkogiiJeiWjveDojxkEDHdKGHq0kJB/M+JLazvZhIKsMBpodrTX0UkFAsqFLtfg9aouhMxg97uFaTWCqluqZpwsGMAE2qh6v+hBXUkaq7SgMxkLKGc1QP10qJDIfc6KmKsaAANa6Hy+YMmxEdKZJLFzcgYKyBNOzhWp6xBkKiq4MJXDjI0wbTw4WEhAFkkUIuFwoJqVSM9jouNVsIo84QPpDhBNnDuKQ4pfk7ZOnilSGmRC3No7jkZDbWcUvwSigBPIgLclDpjCWm2gZjkF4wgadwASUVZVCnCh3IxtvVcO34XCAW4jTqYOEYqBuUJ3BR/oyMOjzdryxGyRI8gAvE++IAdYHAtEE77i8623LANKkwg7pF+FDI7GJcfCTlQ90kQshhi8lBXBD4LQl1mSiUFqC7EBdQMwKDulCUbErpOlww2J+jUVeKkIkhpqtwQU6MqKhrhYahBNU9uKSCj0JdLf5+Z2wOJ3AZAyEGdbnICdGJnSzkH8HTfhV5QaS81PG4QDDJIG8InejzdTguLp83kWdE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")
                        no-repeat 50%;
          }
        </style>
      </head>
      <body>
        <div class="container">
          <canvas id="skill_canvas" height="700" width="540">
          </canvas>
        </div>
      </body>
      <script charset="utf-8">
      (function(){
        var defalutValue = 1;
        var ele = $("#skill_canvas");
        var drawWidh = ele.width ;
        var drawHeigh = ele.height;
        var ctx = ele.getContext('2d');
        var data = {
          title: "WEB全栈",
          font: 20,
          radius: 65,
          border: 50,
          borderColor: "rgba(52, 152, 219, .1)",
          fillColor: "rgba(34, 167, 240, 1)",
          position: {
            x: drawWidh / 2,
            y: drawHeigh / 2
          },
          skills:[
            {
              radius: 120,
              child: [{
                title: "Node.js",
                font: 12,
                angle: 0,
                radius: 33,
                border: 22,
                borderColor: "rgba(235, 149, 50, .1)",
                fillColor: "rgba(249, 191, 59, .7)",
                position: {
                  x: 0,
                  y: 0
                }
              }, {
                title: "HTML5",
                font: 12,
                angle: 90,
                radius: 36,
                border: 22,
                borderColor: "rgba(111, 188, 228, .1)",
                fillColor: "rgba(111, 188, 228, .7)",
                position: {
                  x: 0,
                  y: 0
                }
              }, {
                title: "CSS3",
                font: 12,
                angle: 180,
                radius: 34,
                border: 22,
                borderColor: "rgba(1,255,112, .1)",
                fillColor: "rgba(1,255,112, .7)",
                position: {
                  x: 0,
                  y: 0
                }
              }, {
                title: "jQuery",
                font: 12,
                angle: 270,
                radius: 32,
                border: 22,
                borderColor: "rgba(189, 72, 238, .1)",
                fillColor: "rgba(189, 72, 238, .7)",
                position: {
                  x: 0,
                  y: 0
                }
              }]
            }, {
              radius: 215,
              child: [{
                title: "React.js",
                font: 12,
                angle: 0,
                radius: 38,
                border: 22,
                borderColor: "rgba(214, 69, 65, .1)",
                fillColor: "rgba(255,65,54, .7)",
                position: {
                  x: 0,
                  y: 0
                }
              }, {
                title: "Canvas",
                font: 12,
                angle: 72,
                radius: 35,
                border: 22,
                borderColor: "rgba(210, 215, 211, .1)",
                fillColor: "rgba(108, 122, 137, .7)",
                position: {
                  x: 0,
                  y: 0
                }
              }, {
                title: "Vue.js",
                font: 12,
                angle: 144,
                radius: 43,
                border: 22,
                borderColor: "rgba(133,20,75, .1)",
                fillColor: "rgba(133,20,75, .7)",
                position: {
                  x: 0,
                  y: 0
                }
              }, {
                title: "WebApp",
                font: 12,
                angle: 216,
                radius: 45,
                border: 22,
                borderColor: "rgba((4, 147, 114, .1)",
                fillColor: "rgba(38, 194, 129, .7)",
                position: {
                  x: 0,
                  y: 0
                }
              }, {
                title: "Angular.js",
                font: 12,
                radius: 40,
                angle: 288,
                border: 22,
                borderColor: "rgba(142, 68, 173, .1)",
                fillColor: "rgba(155, 89, 182, 1)",
                position: {
                  x: 0,
                  y: 0
                }
              }]
            }
          ]
        }


        //得到圆心
        //参考 http://www.cnblogs.com/xieon1986/archive/2013/01/28/2880367.html
        function getCentre(angle, radius) {
          return {
            x: drawWidh / 2 + radius * Math.cos(angle * Math.PI / 180),
            y: drawHeigh / 2 + radius * Math.sin(angle * Math.PI / 180)
          }
        }

       //设置每个圆的圆心
        function setItemPosition() {
          for (var i = 0; i < data.skills.length; i++)
            for (var j = 0; j < data.skills[i].child.length; j++) {
              var item = data.skills[i].child[j];
              item.angle += i % 2 ? (i / 3 + 1) * defalutValue : -(i / 3 + 1) * defalutValue;
              item.position = getCentre(item.angle, data.skills[i].radius);
            }
        }

        //画圆
        //参考 http://www.runoob.com/tags/ref-canvas.html
        function drawArc(p) {
          ctx.beginPath();
          ctx.arc(p.position.x, p.position.y, p.radius, 0, 2 * Math.PI);//
          ctx.strokeStyle = p.borderColor;
          ctx.lineWidth = p.border,
          ctx.stroke();
          ctx.fillStyle = p.fillColor;
          ctx.fill();
          ctx.font = p.font + "px Georgia";
          ctx.fillStyle = "#fff";
          ctx.textAlign = "center";
          ctx.fillText(p.title, p.position.x, p.position.y + p.font / 2);
          ctx.closePath();
        }

       //循环画所有圆
        function drawAllArc() {
          ctx.clearRect(0, 0, drawWidh, drawHeigh);// 清空canvas
          drawArc(data);//画中心圆
          for (var i = 0; i < data.skills.length; i++){
            for (var j = 0; j < data.skills[i].child.length; j++){
              drawArc(data.skills[i].child[j])
            }
          }
        }


        //递归动画
        function loop(){
          setItemPosition();
          drawAllArc();
          requestAnimationFrame(loop);
        }

        requestAnimationFrame(loop);

        //鼠标事件
        ele.addEventListener("mouseover", function() {
          defalutValue = .2;
        }), ele.addEventListener("mouseout", function() {
          defalutValue = 1;
        })

        //选择器
        function $(selector){
          return document.querySelector(selector);
        }
      })()
      </script>
    </html>


### 最后

Canvas在浏览器中可以做很多事情，希望大家可以多去尝试。

>参考
>[Canvas_API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API)
>[http://wiki.jikexueyuan.com/project/canvas-wiki/1.html](http://wiki.jikexueyuan.com/project/canvas-wiki/1.html)
>[HTML5 <canvas> 参考手册](http://www.runoob.com/tags/ref-canvas.html)
