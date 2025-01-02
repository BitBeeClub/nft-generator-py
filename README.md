# nft-generator-py

## 1 原始项目
- [nft-generator-py](https://github.com/Jon-Becker/nft-generator-py)
- [原始readme](https://github.com/BitBeeClub/nft-generator-py/blob/main/README.md.bak)

## 2 ChangeLog
1. 当图层图片大小不一致时，使用第一个图层图片的尺寸
2. 增加图层顺序

## 3 Getting Started
Clone the repository and install the requirements.
```
git clone https://github.com/BitBeeClub/nft-generator-py
cd nft-generator-py
python3 -m pip install -r requirements.txt
```

## 4 使用说明

### 4.1 将所有图层文件夹，放到一个目录中(example: trait-layers)，并进行编号，最底层的图层编号最小

例如：从底到顶三个图层
- 01-background
- 02-foreground
- 03-text

### 4.2 生成配置文件
```
python main.py build_config --trait-dir <所有图层所在文件夹> [--output <配置文件输出路径，默认是generated.json>]
```

Example

```
python main.py build_config --trait-dir trait-layers
```

## 4.3 修改配置文件

### 4.3.1 metadata

如果需要metadata，需要修改第2步生成配置文件的以下字段
- baseURI
- name
- description

### 4.3.2 图层中元素的权重

如果需要配置图层中各元素的权重，修改第2步生成配置文件中`layers`下需要配置权重的图层，权重字段为`weights`，需要保证每个图层下所有元素的和为100

### 4.4 生成图片

```
python main.py generate -n <图片数量，不能超过各个图层中所有元素数量的乘积> -c <第2步生成的配置文件路径> --start-at <start token id> -s <十进制随机数字> [--output <输出路径，默认为output>] --no-pad
# --no-pad: 不在metadata中对tokenId进行补零
```

Example

```
python main.py generate -n 5 -c generated.json  --start-at 1 -s 88 --output output --no-pad
```
