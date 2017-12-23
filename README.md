## Pandas-files

Pandas-files是基于Pandas和HDFS格式文件的一个微存储分布式框架，可以在不同分区、不同结点下分布你的子文件，然后通过模块对应的索引结构将其关联。

目前支持所有基本数据类型，支持的数据结构有List、Dict、Tuple、Set、DataFrame、Array等。

（作者主要用于做金融数据的快速存储和查找。）

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

**Example 3.通过配置文件写入/读取**

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

**配置文件如下：**

```ini
;主文件配置名必填，为main
[main]

;temp_path ： 索引路径，必填
index_path = E:/MyGithub/pandas-files/pandasfiles/tmp

;temp_path ： 所有子文件统一的存储路径，若不填则需要确定每个子文件的路径
;temp_path = E:/MyGithub/stock-git/stockgit/store

;partition_name ：所有子文件的文件名,必填
partition_name = fgit

;log_file_path : log日志输出默认，可不填
log_file_path = E:/MyGithub/pandas-files/pandasfiles/log/fgit.log

;silent : Boolean，表示是否开始控制台输出log
silent = False


;子文件配置名可以随便填写
[zz1]
;index : 代表文件对应的唯一索引，(0,∞)
index = 0
;temp_path : index=0的子文件对应的存储路径
temp_path = E:/MyGithub/pandas-files/pandasfiles/tmp

[zz2]
index = 1
temp_path = E:/MyGithub/pandas-files/pandasfiles/tmp
```

### Change Logs

### 0.1.4 2017/12/14

- 创建第一个版本

### Others

Welcome to Star and Follow~