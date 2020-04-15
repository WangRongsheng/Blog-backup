# 简介

当我们想快速了解书籍、小说、电影剧本中的内容时，可以绘制 WordCloud 词云图，显示主要的关键词（高频词），可以非常直观地看到结果。

一般的云图可以利用在线的云图制作工具就可以满足，例如：[TAGUL](https://wordart.com/) 、[图悦](http://www.picdata.cn/picdata/) 、[Tagxedo](http://www.tagxedo.com/) 、[Tocloud](http://www.tocloud.com/) 等。

如果我们想要有一个好的云图展示，就需要进行 **分词** ，比较好的分词工具有：[Pullword](http://www.pullword.com/) 、[jieba](https://pypi.org/project/jieba/) 等。

# 词云制作

现在，我们就利用`python` 生成一个云图！

首先我们先安装我们所需要的`python`第三方库：

```html
numpy
jieba
matplotlib
wordcloud
```

```python
from wordcloud import WordCloud
import matplotlib.pyplot as plt
import jieba
from PIL import Image
import numpy as np

# 生成词云函数
def create_word_cloud(words):
     # 使用结巴分词
     text = " ".join(jieba.cut(words,cut_all=False, HMM=True))
     wc = WordCloud(
           # 字体样式
           font_path=r'C:\Windows\Fonts\simfang.ttf',
           max_words=100,
           width=2000,
           height=1200,
    )
     wordcloud = wc.generate(text)
     # 写词云图片
     wordcloud.to_file("wordcloud.jpg")
     # 显示词云文件
     plt.imshow(wordcloud)
     plt.axis("off")
     plt.show()
```

测试内容为：

```python
s= """
life lies in movement
sport is the source of all life
to keep on, day after day practice go down, and only activities to keep the enthusiasm of adequate training and improve motor skills
activity is the basis of life
people's sound, not only by foods, especially to rely on motion
the olympic motto is "higher, faster, stronger." 
the health of the body for motionless and destruction, for sports practice and keep for a long time
WangRongsheng
WangRongsheng
WangRongsheng
WangRongsheng
WangRongsheng
WangRongsheng
baiyunwei
baiyunwei
baiyunwei
baiyunwei
baiyunwei
1、希望睡前可以轻吻你，希望睡时可以抱着你，希望醒来可以看见你！一直都这样希望，直到永远。

2、你知道吗？我对你的思念像风一样跟随著你，无论你到哪就如同我再你身边一般，你感觉的到吗？

3、月光这么美，我睡不着；抖落心事，擦干心情；把梦，一件件晾在风竽上；远方的你让我好牵挂。

4、我的爱，每一个诗人都爱美，你的美更令诗人神飞心醉。但是美是变动的呀，我爱你永远无涯岸。

5、世界上最深沉的不是大海，而是你的心灵。我把自已整个都抛下，却不见泛起一丝涟漪！我好想你！

6、这样黑的夜里，我多想偎依在你的温暖的被窝里，享受那炽热的爱，美妙的感受沐浴在你的爱意中！

7、你是如此出众，从春到冬，天天在我思念中，我深深地体会到“失去了方知可贵”这句智理名言。

8、从见你的第一眼开始，我就发现终于找到我的另一半了。我要给你一生的幸福，我坚信一生不动摇！

9、在遇到梦中人之前，上天也许会安排我们先遇到的人；在我们终于遇见心仪的人时，便应当心存感激。

10、爱情是不按逻辑发展的，所以必须时时注意它的变化。爱情更不是永恒的，所以必须不断的追求。
"""
create_word_cloud(s)
```

# 运行展示

<img src="https://s1.ax1x.com/2020/04/06/Gs0SPJ.jpg" alt="Gs0SPJ.jpg" border="0" />

