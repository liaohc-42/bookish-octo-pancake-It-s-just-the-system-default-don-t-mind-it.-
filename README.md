# bookish-octo-pancake-It-s-just-the-system-default-don-t-mind-it.-
# ClipCat

本地优先的命令行剪贴板历史工具：自动记录、智能分类（代码/网址/密码/验证码等）、全文搜索。

## 为什么不用 AI 做分类
- 隐私：剪贴板含敏感信息，本地规则引擎确保数据不出本机
- 性能：正则+启发式毫秒级响应，无模型加载开销
- 可解释：每条分类逻辑透明，便于调试

## 功能
- 自动监听剪贴板变化（1s 轮询，跨平台）
- 7 类自动分类 + MD5 去重
- 命令行检索：`list` / `search` / `stats`
- 纯 Python + pyperclip，零重依赖

## 快速开始
\`\`\`bash
pip install pyperclip
python clipcat.py monitor
python clipcat.py search "http"
\`\`\`

## 设计细节
- 去重：内容 MD5 作 ID，重复复制只更新时间戳与访问计数
- 分类优先级：URL > Email > Phone > Code > Password > Note
- 启动即快照：monitor 启动瞬间先记录当前剪贴板内容

## 已知局限
- 仅支持文本，不处理图片/富文本
- 明文存储，生产环境需加敏感字段加密
- 1s 轮询间隔内连续复制可能丢中间帧
