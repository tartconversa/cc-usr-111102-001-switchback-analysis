# 跨时段促销实验的分配单元推断

本项目保存百货多业态经营研究的合成资料及输入读取工具。当前程序只解析文件并显示输入类型与记录数量，不进行统计分析、模型训练、优化求解或业务推荐。所有记录均为虚构，不能用于陈述真实商场经营结果。

## 输入约定

排班用 block_id、floor、slots 表示，slots 内含 slot_id、assigned、start_at；每块合法排班为 AABB/BBAA。订单 amount_fen 为分，units 为件数，slot_id 连接时段；status=missing 说明该单元缺测而非销售额为0。

fixtures 为资料目录，src/schedule_reader.py 为读取器，tests 为格式读取测试。输入在运行中保持不变；研究计算结果可写入独立的 .workspace-output 目录。

## 本地操作

Python 3.11 及以上版本，现有读取工具只依赖标准库，不需要下载第三方包。进入项目根目录：

    python -m src.schedule_reader fixtures/schedule.json

编译检查：

    python -m compileall -q src tests

格式读取测试：

    python -m unittest discover -s tests -v

## 固定运行环境

    docker build -t switchback-analysis:local .
    docker run --rm switchback-analysis:local

容器默认运行输入测试。镜像使用完整内容摘要固定，研究输入随项目一起复制。
