# Python

> Python是一个非常流行的编程语言，主要用于Web开发、数据分析、机器学习等领域。如果要掌握Python，他可能需要掌握以下几个方面的知识：
- [X] 1.  基础知识
- [X] 2.  数据结构
- [ ] 3.  模块和库
- [ ] 4.  编程 paradigms（编程范式）
- [ ] 5.  Web开发
- [ ] 6.  数据分析与可视化
- [ ] 7.  机器学习与深度学习
- [ ] 8.  测试与调试
- [ ] 9.  版本控制
- [ ] 10.  性能优化与调试  

## 1.  基础知识：
像**变量、数据类型、循环、条件判断、函数、类**等，这些都是Python的基本语法，必须得理解透彻，否则后续的代码开发会很吃力。

### 1.基础变量与语法

#### ① 变量与数据类型
```python
# 生物信息学常见数据类型应用
gene_name = "TP53"                  # 字符串：基因名称
is_oncogene = True                  # 布尔值：致癌基因标记
chromosome_location = 17            # 整数：染色体位置
protein_molecular_weight = 43.7     # 浮点：蛋白质分子量

```
#### ② 类型转换与检查
```python
# 测序质量值处理示例
quality_score = "36.8"              # 字符串形式的浮点数
converted_score = float(quality_score)  # 转换为浮点 → 36.8

# 类型检查在数据处理中的重要性
if type(converted_score) is float:
    print(f"质量值有效: {converted_score}")

```

### 2.流程控制

#### ① 条件判断 - if/elif/else
```python
# 基因表达量分类逻辑
expression_level = 8.2

if expression_level > 10:
    print("高表达")
elif 5 <= expression_level <= 10:
    print("中表达")  # 此条件将触发
else:
    print("低表达")


```
#### ②循环结构
for循环处理序列数据
```python
# 遍历DNA序列计算GC含量
dna_sequence = "ATGCGATAGCTAGCT"
gc_count = 0

for base in dna_sequence:
    if base in ['G', 'C']:
        gc_count += 1

gc_content = gc_count / len(dna_sequence) * 100
print(f"GC含量: {gc_content:.2f}%")  # 输出: GC含量: 46.67%

```
while循环处理未知长度数据
```python
# 模拟测序数据读取直到遇到终止符
raw_data = ["@READ1", "ATGCGTA", "+", "!!!!!!!", "@READ2", "CTAGCT", "...", "END"]
index = 0

while index < len(raw_data) and raw_data[index] != "END":
    if raw_data[index].startswith("@"):
        print(f"处理读段: {raw_data[index][1:]}")
    index += 1

```

### 3.函数基础

#### ①定义与调用
```python
# 计算序列GC含量的函数
def calculate_gc_content(sequence):
    """计算DNA序列的GC含量"""
    gc_count = sequence.count('G') + sequence.count('C')
    return gc_count / len(sequence) * 100 if sequence else 0

# 调用示例
dna = "ATGCTAGCTAGCTAG"
print(calculate_gc_content(dna))  # 输出: 46.67
```
 #### ②参数进阶用法
```python
# 带默认参数的序列格式化函数
def format_sequence(seq, line_length=60):
    """将长序列分割为多行显示"""
    return '\n'.join(seq[i:i+line_length] for i in range(0, len(seq), line_length))

# 使用默认值
print(format_sequence("ATGC"*50))

# 自定义行长
print(format_sequence("ATGC"*50, line_length=80))
```

## 2.  数据结构：
**列表、元组、栈、队列、字典、集合**等，这些都是Python中常用的容器，掌握它们的用法和性能差异很重要。 

### 1. 列表 (List) - 可变有序集合
```python
# 存储样本ID并操作
samples = ["SRR123", "SRR456", "SRR789"]

# 生物信息学常用操作
samples.append("SRR101")            # 添加新样本 → ["SRR123", "SRR456", "SRR789", "SRR101"]
del samples[1]                      # 删除问题样本 → ["SRR123", "SRR789", "SRR101"]
rna_samples = samples[0:2]          # 切片获取前两个样本 → ["SRR123", "SRR789"]

# 列表推导式快速处理数据
gc_contents = [45.6, 38.2, 49.1]
high_gc = [gc for gc in gc_contents if gc > 40]  # → [45.6, 49.1]

```

### 2. 元组 (Tuple) - 不可变有序集合
```python
# 存储基因坐标（不可变保证数据安全）
gene_location = ("chr7", 117175000, 117178000, "EGFR")

# 解包操作快速获取信息
chromosome, start, end, symbol = gene_location
print(f"{symbol}基因位于{chromosome}:{start}-{end}")
```
### 3. 字典 (Dict) - 键值映射
```python
# 存储基因功能注释
gene_functions = {
    "TP53": "肿瘤抑制蛋白",
    "BRCA1": "DNA修复酶",
    "MYC": "转录因子"
}

# 生物信息学典型应用
# 添加新注释
gene_functions["EGFR"] = "表皮生长因子受体"

# 安全获取值
function = gene_functions.get("APOE", "功能未知")  # 键不存在返回默认值

# 遍历基因-功能对
for gene, func in gene_functions.items():
    print(f"{gene}: {func}")
```

### 4. 集合 (Set) - 无序唯一元素
```python
# 筛选独特突变位点
all_mutations = ["chr1:1234A>T", "chr2:5678G>C", "chr1:1234A>T", "chr3:9012T>A"]
unique_mutations = set(all_mutations)  # 自动去重 → {"chr1:1234A>T", "chr2:5678G>C", "chr3:9012T>A"}

# 集合运算找共有突变
patient_A = {"chr1:1234A>T", "chr2:5678G>C"}
patient_B = {"chr1:1234A>T", "chr3:9012T>A"}
common_mutations = patient_A & patient_B  # 交集 → {"chr1:1234A>T"}

```
[实战练习](https://amanda-mona.github.io/BeautifulGirl.github.io/post/sheng-wu-xin-xi-xue-te-xun-（-shi-zhan-lian-xi-）.html)

## 3.  模块和库：
比如标准库里的**math、datetime、os、sys、re**等等，还有一些常用第三方库，比如**pandas、numpy、scikit-learn、requests**等，这些是Python生态系统的重要组成部分。  
## 4.  编程 paradigms（编程范式）：
比如**函数式编程（如map, filter, reduce）、递归、生成器**等，这些概念可以帮助编写更高效的代码。  
## 5.  Web开发：
比如使用**Django或Flask**这样的框架来构建Web应用，可能还需要了解**HTML、CSS、JavaScript**以及一些前端技术。  
## 6.  数据分析与可视化：
使用**Pandas**进行数据处理，**Matplotlib或Seaborn**进行图表绘制，这些都是数据分析常用的部分。  
## 7.  机器学习与深度学习：
使用**TensorFlow、PyTorch**等库进行模型训练，包括**分类、回归、聚类**等任务。  
## 8.  测试与调试：
了解如何编写测试用例，使用**Pytest或Coverage**，以及调试技能。  
## 9.  版本控制：
使用**Git**进行代码管理和协作开发，知道如何分支、合并、回滚等操作。  
## 10.  性能优化与调试：
如何让代码更高效，排除性能瓶颈。   

# R语言
>R主要是统计分析和数据可视化，与Python类似，但有一些不同的地方：
- [ ] 1.  统计基础 
- [ ] 2.  数据处理
- [ ] 3.  图形系统 
- [ ] 4.  机器学习 
- [ ] 5.  包管理
- [ ] 6.  数据科学工作流 
- [ ] 7.  ** shiny包**
- [ ] 8.  统计建模
- [ ] 9.  大数据处理
- [ ] 10.  版本控制

## 1.  统计基础：
统计学的基本概念，比如均值、方差、t检验、ANOVA等。  
## 2.  数据处理：
读取和写入数据，使用data.frame、矩阵等数据结构，与Python的Pandas相比，R的数据框结构更复杂。  
## 3.  图形系统：
ggplot2是最常用的可视化工具， trellis图也是其特色，Lattice等其他包也需要了解。 
## 4.  机器学习：
虽然R也有机器学习的包，比如 caret，但可能不如Python丰富，不过基础概念还是需要掌握的。  
## 5.  包管理：
知道如何从CRAN源获取包，如何安装、加载、卸载，以及依赖管理。  
## 6.  数据科学工作流：
数据清洗、整合、分析、可视化，整个流程都要了解。  
## 7.  ** shiny包**：
用来创建Web应用程序，不过现在可能用React或Rust等技术替代。 
 ## 8.  统计建模：
线性回归、逻辑回归、分类树、聚类等方法，以及模型评估和选择。  
## 9.  大数据处理：
如何处理大规模数据，可能需要使用数据存储和处理的高级方法。  
## 10.  版本控制：
同样使用Git，了解分支、merge等操作。   

# Linux
>Linux是一个强大的操作系统，也是很多人学习的平台： 

- [ ] 1.  基础操作  
- [ ] 2.  Shell脚本
- [ ] 3.  系统管理  
- [ ] 4.  网络操作  
- [ ] 5.  开发工具 
- [ ] 6.  系统编程
- [ ] 7.  日志与调试
- [ ] 8.  安全 
- [ ] 9.  存储与文件系统
- [ ] 10.  开发环境搭建

## 1.  基础操作：
文件系统、目录结构、命令行操作，比如cd、ls、mv、cp等，以及高级命令如mv-md5sum、grep、sed、awk等。  
## 2.  Shell脚本：
像Bash脚本，了解循环、条件判断、函数、变量扩展等。  
## 3.  系统管理：
安装软件包（比如apt-get）、配置文件（如etc/passwd、etc/shadow、etc config）、用户和组的管理。  
## 4.  网络操作：
HTTP协议、使用wget、curl、ftpd等工具，了解子网、IP配置、端口映射。  
## 5.  开发工具：
使用vim或nano编辑器，了解Makefile的使用，配置开发环境，比如安装头文件、编译选项。  
## 6.  系统编程：
了解进程、线程、信号处理，以及一些内核开发，比如内核模块。  
## 7.  日志与调试：
使用logrotate、syslog、dummit等工具，了解调试工具如gdb、valgrind。  
## 8.  安全：
基础的网络安全知识，如防火墙配置、密码管理、漏洞扫描。  
## 9.  存储与文件系统：
了解swap分区、swap空间管理、root权限的使用。  
## 10.  开发环境搭建：
安装系统、配置开发环境，比如自动装入软件包，设置环境变量。