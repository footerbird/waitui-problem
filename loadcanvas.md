```
// 获取元素相对于视窗的偏移量
var rect = $(".container").get(0).getBoundingClientRect();
canvas.width = w;
canvas.height = h;
canvas.style.width = w + "px";
canvas.style.height = h + "px";
var context = canvas.getContext("2d");

context.translate(-rect.left,-rect.top);
html2canvas($('.container'), {
   canvas: canvas,
   onrendered: function(canvas) {
       var data = canvas.toDataURL("image/png"); //生成的格式
       $(".container").html('<img src= "'+data+'" />');
       var imgData = data.replace("image/png", "image/octet-stream");
       var link = document.createElement("a");
       link.href = imgData;
       link.download = new Date().getTime()+'.png';
       link.click();
   }
});
```
