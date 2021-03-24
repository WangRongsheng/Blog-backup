## 1、复制yolov5工程到本地

https://github.com/ultralytics/yolov5

## 2、查看字体

默认调用`C:\Windows\Fonts` 下的字体，找个合适的，比如我这次使用`simhei.ttf` 。

## 3、`train.py文件`

```html
with open(opt.data) as f:
```
改为
```html
with open(opt.data, encoding='UTF-8') as f:
```

## 4、test.py文件

```html
with open(data) as f:
```
改为
```html
with open(data, encoding='UTF-8') as f:
```

## 5、utils/general.py文件

导包
```html
from PIL import Image, ImageDraw, ImageFont
```

## 6、utils/plot.py文件

修改`plot_one_box` 函数，`if label之后的代码`改为
```html
    if label:
        tf = max(tl - 1, 1)  # font thickness
        t_size = cv2.getTextSize(label, 0, fontScale=tl / 3, thickness=tf)[0]
        font_size = t_size[1]
        font = ImageFont.truetype('MSYH.TTC', font_size)
        t_size = font.getsize(label)
        c2 = c1[0] + t_size[0], c1[1] - t_size[1]
        cv2.rectangle(img, c1, c2, color, -1, cv2.LINE_AA)  # filled
        img_PIL = Image.fromarray(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
        draw = ImageDraw.Draw(img_PIL)
        draw.text((c1[0], c2[1] - 2), label, fill=(255, 255, 255), font=font)

        return cv2.cvtColor(np.array(img_PIL), cv2.COLOR_RGB2BGR)
```

## 7、utils/plot.py文件

`plot_images`函数中

```html
plot_one_box(box, mosaic, label=label, color=color, line_thickness=tl)
```

改为
```html
mosaic = plot_one_box(box, mosaic, label=label, color=color, line_thickness=tl)
```

## 8、detect.py文件

```html
plot_one_box(xyxy, im0, label=label, color=colors[int(cls)], line_thickness=3)
```
改为
```html
im0 = plot_one_box(xyxy, im0, label=label, color=colors[int(cls)], line_thickness=3)
```

## 9、中文标注数据

[中文LableIMG数据标注工具（提取码：wrsn ）](https://pan.baidu.com/s/13JQ8qIFIymRoL9J6VkumRA)


