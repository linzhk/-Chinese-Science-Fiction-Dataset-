
# -CSFD-
Chinese Science Fiction Dataset.一共有4千多篇科幻小说，资源来源于网络。数据仅供学习和交流使用，严禁用于商业或其他用途！如果侵权，将会在收到讯息的第一时间取消开源。
下载方式：
链接: https://pan.baidu.com/s/13oWdBpQ6ug4tZaXs72EuWA 提取码: s962 
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
