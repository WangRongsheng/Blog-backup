## 自定义ProgressBar

```python
import sys
import time

def progressbar(it, prefix="", size=60, file=sys.stdout):
    count = len(it)
    def show(j):
        x = int(size*j/count)
        file.write("%s[%s%s] %i/%i\r" % (prefix, "#"*x, "."*(size-x), j, count))
        file.flush()        
    show(0)
    for i, item in enumerate(it):
        yield item
        show(i+1)
    file.write("\n")
    file.flush()

    
for i in progressbar(range(15), "Computing: ", 40):
    progressbar(50)
    time.sleep(0.1)
```

自己定义的好处就是可以将进度条定义成我们想要的形式比如上面就是使用`#`与`·`来输出，为什么不用`print`？因为`sys.stdout`就是`print`的一种默认输出格式，而`sys.stdout.write()`可以不换行打印，`sys.stdout.flush()`可以立即刷新输出的内容。当然也可以封装成类来更好的使用 ，但效果是类似的。

```python
from __future__ import print_function
import sys
import re


class ProgressBar(object):
    DEFAULT = 'Progress: %(bar)s %(percent)3d%%'
    FULL = '%(bar)s %(current)d/%(total)d (%(percent)3d%%) %(remaining)d to go'

    def __init__(self, total, width=40, fmt=DEFAULT, symbol='=',
                 output=sys.stderr):
        assert len(symbol) == 1

        self.total = total
        self.width = width
        self.symbol = symbol
        self.output = output
        self.fmt = re.sub(r'(?P<name>%\(.+?\))d',
            r'\g<name>%dd' % len(str(total)), fmt)

        self.current = 0

    def __call__(self):
        percent = self.current / float(self.total)
        size = int(self.width * percent)
        remaining = self.total - self.current
        bar = '[' + self.symbol * size + ' ' * (self.width - size) + ']'

        args = {
            'total': self.total,
            'bar': bar,
            'current': self.current,
            'percent': percent * 100,
            'remaining': remaining
        }
        print('\r' + self.fmt % args, file=self.output, end='')

    def done(self):
        self.current = self.total
        self()
        print('', file=self.output)
        
from time import sleep

progress = ProgressBar(80, fmt=ProgressBar.FULL)

for x in range(progress.total):
    progress.current += 1
    progress()
    sleep(0.1)
progress.done()
```

## tqdm

```python
from tqdm import trange
import time
for i in trange(10): 
    time.sleep(1)
```

## rich

```python
from rich.progress import track
import  time

for step in track(range(30)):
    print('早起Python')
    time.sleep(0.5)
```