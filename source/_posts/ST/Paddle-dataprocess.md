---
title: PaddleSpeech ST 数据预处理问题
date: 2022-05-01 21:32:05
tags: PaddleSpeech
categories: ST
---

数据预处理：构建字典已经成功，train的时候提示fbank特征提取处理有点问题，数据格式报错

原因：经大佬指点，发现是数据的格式有问题，fbank处理的为单通道，采样率为16000HZ的声音

内心os:原来直接第一步数据处理就错了hhhhhh

解决方式：编写shell利用sox批量处理音频至16000单通道

```bash
#!/bin/bash
for x in ./*.wav
do 
  b=${x##*/}
  sox $b -c1 -r 16000 new_$b #-c1为单通道 -r 16000为采样率变为16000 
  rm -rf $b
  mv new_$b $b
done
```

成功后重新运行data.sh，重新进行数据预处理就很顺利了

现在的问题是：每次识别的都一样😂肯定还有问题，继续解决ing
