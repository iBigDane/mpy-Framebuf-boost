# mpy-Framebuf-boost
FrameBuffer 增加多字体和中文支持 BMP文件操作
中文支持，需要加载对应的字库，使用font_load("文件名")，文件名需要注意大小写，释放字库使用font_free()
字库分为三类，gb2312开始的是6763汉字的全字库，内置unicode的查找表，在mpy中可以直接text方法进行中英文混合显示。
gbk开头的是大约2万汉字的字库，另外支持小字库，xzk.fon是一个例子，内置四种尺寸的小字库，小字库的范围包括：

str12="中文中文中文编码处理"
str16="拷贝文章内容到一个文件（通常人们都这么干）。直接读取文件内容。用方法能直接生成字符串。"
str24="用或结合迭代来自己构成字符串。"]
str32="知识点补充：读取文件中字符串，字符串用空格分隔"

为了保持text()的操作参数不变，字体设置使用单独的font_set(字形，旋转，放大，反白)
字形对于英文支持0xab，a：1-4对应四种字形，b：1-4对应12/16/24/32四种大小，对于中文，只识别b参数
旋转是描述文字显示的方向，0为向上，1-3依次顺时钟旋转90度
放大，1-4，针对当前字体，加倍显示，放大倍数1-4倍，最大字体32点阵，4被放大后可以获得128点阵的大小，适合显示项目的提示信息。
反白参数，0，正常显示，1反白显示

显示模式在RGB565的基础上增加了RGB565SW格式，差异是交换了颜色显示的高低字节，在我使用的ili9341显示器上，显示屏和fb里面的字节序相反。所以增加这个格式。

显示BMP功能
show_bmp("文件名",x0,y0,w,h)
文件名需要包括扩展名，x0和y0决定图像的左上角位置，w,h决定图片显示的宽和高，如果小于图片的宽高，则自动切换到图像的宽高
save_bmp("文件名",x0,y0,w,h)
目前在rgb565和rgb565sw模式下显示和存储bmp的格式是rgb888格式，因为大多数常用软件构建的都是rgb888的格式，这样更方便一些
在单色显示模式，只支持二值状态先的bmp显示和存储，但是因为时间关系，这一部分尚未测试

在上级存储库里面提供了一些示例程序
已经完成的有：

ili9341 2.2   320×240   真彩tft

st7789  1.14  135×240   真彩tft

ssd1306 0.96  128×64    单色oled             增加了录像

2021/2/26完成
st7735  0.96  80×160    真彩tft                                      增加了128×160的兼容处理

st7567  2.2   128x64    单色lcd              增加了录像

st7735  0.96  80x160    真彩tft16色显示      可以支持esp8266的板子     增加了128×160的兼容处理

后续计划增加

st7920  3.2   128x64    单色lcd

一款320480的tft显示器

st7789  1.3   240×240   真彩tft

st7789  1.3   240×240   真彩tft16色显示      可以支持esp8266的板子


