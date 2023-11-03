# Testing tokenization in multilingual context


This is also inspired by [tokenmonster](https://github.com/alasdairforsythe/tokenmonster).

## tokenizer 速度测试
| 模型 | Arabic (203673) |  | English (403630) |  | Chinese (121106) |  |
| --- | --- | --- | --- | --- | --- | --- |
|  | token | time(s) | token | time(s) | token | time(s) |
| Bloom (250k) | 50825 | 0.2077 | 89558 | 0.3469 | 77893 | 0.2185 |
| Llama (32k) | 183904 | 0.4261 | 106614 | 0.6880 | 169253 | 0.3682 |
| Baichuan2 (125k) | 172505 | 0.4330 | 99267 | 0.7666 | 80966 | 0.3087 |
| mt5 | 73172 | 4.2103 | 104994 | 9.0237 | 90329 | 0.4704 |

假设一个词表的大小，1k,2k,4k,8k, .. 训bpe，在给定的validation下算压缩率（暂时没找到合适的validation，以train dataset代替），饱和 (提升的比例随着词表大小不显著), 数据集wikipedia
最后一个token的frequency
###### 中文词表
| num |  compression ratio | last word frequency |
| --- | --- | --- |
| 8000 | 0.7813 | 48 |
| 16000 | 0.5964 | 2 |
| 24000 | 0.5485 | 2 |
| 32000 | 0.5212 | 1 |

根据训练预料需要7000+token能够达到99.95%的覆盖率，故从8k开始。

###### 阿拉伯语词表
| num |  compression ratio | last word frequency |
| --- | --- | --- |
| 1000 | 0.4172 | 553 |
| 2000 | 0.3603 | 553 |
| 4000 | 0.3130 | 10 |
| 8000 | 0.2752 | 10 |
| 16000 | 0.2466 | 7 |
| 24000 | 0.2338 | 6 |
| 32000 | 0.2262 | 1 |


## reference
```
@misc{X-tokenization-2023,
  title={X-tokenization, towards a universal across languages.},
  author={Jianqing Zhu and Benyou Wang},
  year = {2023},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/FreedomIntelligence/X-tokenization}},
}
```
