## Pandas-files

pandas-files是基于Pandas和HDFS格式文件的一个微存储分布式框架，可以在不同分区、不同结点下分布你的子文件，然后通过模块对应的索引结构将其关联。

目前支持所有基本数据类型，支持的数据结构有List、Dict、Tuple、Set、DataFrame、Array等。

### Dependencies

- Python 2.x/3.x
- joblib>=0.11
- pandas>=0.18.1

### Installation

- 方式1：pip install pandas-files
- 方式2：python setup.py install
- 方式3：访问<https://pypi.python.org/pypi/pandas-files>下载安装

### Upgrade

```shell
pip install pandas-files --upgrade
```

### Quick Start

**Example 1.快速写入文件**

```python
import pandasfiles as pf
dis = pf.Distribution(chunk=2, mode='w',auto=True)
dis.start()
for i in range(5):
  name = 'st%s'%i
  dis.write(name,i)
dis.end()
```

**Example 2.读取文件**

```python
import pandasfiles as pf
dis = pf.Distribution(chunk=2, mode='r',auto=True)
# 无须start/end
dis.read('key')
```

Example 3.通过配置文件写入/读取

![](http://graysliver.oss-cn-shenzhen.aliyuncs.com/pandas-files.JPG)

```python
import pandasfiles as pf

#-----------------写入---------------
dis = pf.Distribution(conf_path='xxxx',chunk=1, mode='w',auto=False)
dis.start()
for i in range(5):
  name = 'st%s'%i
  dis.write(name,i)
dis.end()

#-----------------读取---------------
dis = pf.Distribution(conf_path='xxxx',chunk=1, mode='r',auto=False)
# 无须start/end
dis.read('key')
```

### Change Logs

### 0.1.4 2017/12/14

- 创建第一个版本

### Others

Welcome to Star and Follow~