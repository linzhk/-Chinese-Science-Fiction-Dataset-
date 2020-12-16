
# -CSFD-
Chinese Science Fiction Dataset.一共有4千多篇科幻小说，资源来源于网络。数据仅供学习和交流使用，严禁用于商业或其他用途！如果侵权，将会在收到讯息的第一时间取消开源。
下载方式：
链接: https://pan.baidu.com/s/13oWdBpQ6ug4tZaXs72EuWA 提取码: s962 

# TO DO LIST
- 基于该数据训练文本生成模型（Language Model）
- 丰富更多的条件和监督信号，以训练条件语言模型，实现类似于人机协作等智能写作场景。
- 该方向更多进展，研究请参考deepcamp2020队伍“AI科幻世界”相关报道：  
          - [创造，在人工智能的挑战下（艺海观澜）](http://paper.people.com.cn/rmrb/html/2020-11/13/nw.D110000renmrb_20201113_1-20.htm)  
          - [11位科幻作家参与，首次AI人机共创写作实验启动](https://mp.weixin.qq.com/s?__biz=MjM5NTE5NzUwMA==&mid=2650982185&idx=1&sn=bc53dbe3af5d132b557a22ad4331d170&chksm=bd0a407a8a7dc96c786224ea0526abb239d44031c18dfb63b1281c1b3d7ef51b524d48524ad2&mpshare=1&scene=1&srcid=1027xOuD6raE1aHNcR0Lwpxc&sharer_sharetime=1608110912368&sharer_shareid=8305d06dc198527cf6890e94a751cac7&key=60ce052490790c2c8eabdfc3c892fae791baf5aaba9fd120b2c0234111012a07d4732c8ee980837c342081055865cdca03d56e7d1cc66d3aa5d6f7ebadb6441765c229adc49ba8b8971a947a94a5679252ca7b5801d9fa9da82de256632bccc57aafe926beff82811c120a2a5a1999b01505efa05a6e07f9ef6f13d4297ba0fc&ascene=1&uin=MTQwNzMxNzcyOQ%3D%3D&devicetype=Windows+10+x64&version=6300002f&lang=zh_CN&exportkey=A4dqjkSgvRaATvwKfUt8tFc%3D&pass_ticket=AUVOTl1MMqBR4u3DPoUZ26CUA7mFJEibf6rmaLCzhVHQuPO4qhcauoo2Ua3diL%2FN&wx_header=0)  
          - 腾讯AI Lab 开源的[中文预训练文本生成模型](https://github.com/lipiji/Guyu)  
          - 我个人的[知乎专栏](https://www.zhihu.com/column/c_1145745033553563648)

# 数据介绍
## 文件命名

data_版本号_小说序号_量级.json

- 版本号:第二版
- 小说序号:序号范围为1~4623
- 量级：一共有4个量级描述文本长度，分别为小于5千字(5K)、5k到1w(1W)，1w到10w(10W)，10w以上(10W+)。

- 备注：如果预处理失败，文件格式为data_2_1725_WRONG.json。本次损失了3篇小说语料。

## 数据格式

### 第一层
每篇小说被整理为一下形式：  
data = {  
          'novel_per_dict':novel_per_dict,  
          'novel_loc_dict':novel_loc_dict,  
          'novel_org_dict':novel_org_dict,  
          'novel_zhuan_dict':novel_zhuan_dict,  
          'novel_context':novel_context  
      }  

- novel_per_dict : 这篇小说出现过的人名，例如：  
  {  
    '张三':'PER1',  
    '林镇坤':'PER2',  
    '镇坤':'PER2',  
    '李四':'PER4'  
  }  
  小说当中的人名会被上面的标识符全部代替。序号只能保证1号对1人，不能反映出人名数量等信息。
- novel_loc_dict :地名。处理逻辑同上。标识符为'LOC'
- novel_org_dict :机构名。标识符为'ORG'
- novel_zhuan_dict:专业名词. 标识符为'ZHUAN'
- novel_context : 具体的文本内容，介绍如下：

### 第二层
- 已经做过脏数据清洗
- novel_context （小说）: list 元素为一个文本段落（以换行符分割）
- novel_context[0] （段落）: list 元素为一个句子（一个段落可能有多句或一句，对话默认是一个句子）
- novel_context[0][0] （句子）: dict 格式如下：  
{  
  'context':句子,  
  'type':句子类型,// 对话 : 0  
                 // 场景 : 1  
                 // 人物 : 2  
  'length':长度  
}
