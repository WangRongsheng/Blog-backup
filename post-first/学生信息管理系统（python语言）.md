---
title: 学生信息管理系统（python语言）
date: 2019-10-27 18:06:03
thumbnail: https://i.loli.net/2019/10/27/KlRfSsnaLrUP9bX.png
tags: 学生信息管理系统
categories: Python
---

本程序包含main.py和gro.py两个函数
可以使用**python main.py** 直接运行！

<!--more-->

主函数：main.py

```python
from gro import gro
import pickle as pk


def main():
    def printMenu():
        print("=" * 30)
        print("      学生管理系统")  # class maked
        print("1.添加学生信息")
        print("2.删除学生信息")
        print("3.修改学生信息")
        print("4.查询学生信息")
        print("5.显示所有学生信息")
        print("6.导出外部文件")
        #print("7.导入外部文件")
        print("7.导出外部文件并加密")
        #print("9.导入外部加密文件并解读")
        print("0.退出系统")
        print("=" * 30)

    CS1 = gro()
    while True:
        # 打印提示信息
        printMenu()
        key = input("请输入你要选择的操作：")
        if key == '0':
            exit()
        if key == '1':
            # 添加学生信息
            CS1.addstu_in()
        elif key == '2':
            CS1.del_itemin()
            # 删除学生信息
        elif key == '3':
            CS1.modifystu()
            # 修改学生信息
            # modifystu
        elif key == '4':
            CS1.sc_stu()
            # 查询学生信息
            # sc_stu
        elif key == '5':
            print("=" * 30)
            print("学生的信息如下：")
            print("序号  学号  姓名            成绩  ")
            i = 0
            for tempInfo in CS1.allstu:
                print("%d     %s     %s      %s"
                      % (i + 1, CS1.allstu[i].get('stuid'), CS1.allstu[i].get('stuname'),CS1.allstu[i].get('score')))
                i += 1
        elif key == '6':
            CS1.Output_txt()
            print("=" * 30)
            print("外部文件已导出...")
            # Output_txt
        elif key == '7':
            CS1.Input_txt()
            print("=" * 30)
            # Input_txt
            print("外部文件数据已导入...")
        elif key == '8':
            pass
            print("=" * 30)
            # Output_txt_s(stu_collection)
            print("外部加密文件已导出...")
        elif key == '9':
            pass
            print("=" * 30)
            # Input_txt_s(stu_collection)
            print("外部文件数据已解读...")


if __name__ == '__main__':
    main()
```

子函数：gro.py

```python
class stu:
    stuid = "001";
    stuname = "zhangsan";
    score = 80;

    def printstu(self):
        print(self.stuid)
        print(self.stuname)
        print(self.score)

    def savestudent(self):
        exmaple = {'stuid': 123, 'stuname': 'xxx', 'score': 100}
        temp = exmaple.fromkeys(['stuid', 'stuname', 'score'])
        temp['stuid'] = self.stuid
        temp['stuname'] = self.stuname
        temp['score'] = self.score
        return temp


class gro:
    allstu = []
    groname = 'CS1'

    def inputstu(self):
        newstu = stu()
        newstu.stuid = int(input("请输入学号:\n"))
        newstu.stuname = input("请输入学生姓名:\n")
        newstu.score = int(input("请输入成绩:\n"))
        newstu.savestudent()
        return newstu.savestudent()

    def addstu(self, stuobj):
        self.allstu.append(stuobj)

    def addstu_in(self):
        allnew = self.inputstu()
        self.addstu(allnew)

    def del_itemin(self):
        length = len(self.allstu)
        for s in range(length):
            if self.allstu[s]['stuid'] == int(input("输入删除学生的学号:\n")):
                self.allstu.pop(s)
            else:
                print("没有此学生相关信息!\n")
                break

    def modifystu(self):
        length = len(self.allstu)
        for s in range(length):
            if self.allstu[s].get('stuid') == int(input("输入修改的学生学号:\n")):
                self.allstu[s]['stuname'] = input("请输入预修改值(姓名):\n")
                self.allstu[s]['score'] = int(input("请输入预修改值(成绩):\n"))
                print("已修改!\n")
            else:
                print("没有此学生相关信息!")
                break

    def printallstu(self):  # 未使用
        for s in self.allstu:
            s.printstu()
            print("-" * 20)

    def sc_stu(self):
        length = len(self.allstu)
        for s in range(length):
            if self.allstu[s].get('stuid') == int(input("输入查询的学生学号:\n")):
                print(str(self.allstu[s].get('stuid')) +'  ' +str(self.allstu[s].get('stuname')) + '  ' +str(self.allstu[s].get('score')))
            else:
                print("没有此学生相关信息!")
                break

    def Output_txt(self):
        f = open("pydata.txt", "wt")
        length = len(self.allstu)
        for s in range(length):
            f.writelines(self.allstu[s] + "\n")

    def Input_txt(self):
        fw = open("pydata.txt", "rt")
        length = len(self.allstu)
        for line in fw:
            string = fw.readline()
            print(string)
            ts = string
            print(type(ts))
            for s in range(len(self.allstu)):
                if not (ts.get('stuid') == self.allstu[s].get('stuid')):
                    self.allstu.append(ts)
        print("读取成功!")
```
