# Sort-SRT

一个用于将 FastWhisper 输出的 JSON 文件转换为 SRT 字幕文件的工具。

## 功能特点

- 将 FastWhisper 的 JSON 输出转换为标准 SRT 字幕格式
  - 时长准则：每个字幕块理想持续时间为1-4秒
  - 字符数量：每行不超过40-45个字符（中文约15-20个字）。本项目选择16
  - 行数限制：每个字幕块最多显示两行
  - 句子完整性：尽量保持语法和语义的完整性。用中文分词器实现

## 安装

确保已安装 Rust 开发环境，然后克隆项目：

```bash
git clone https://github.com/yourusername/sort-srt.git
cd sort-srt
```

## 使用方法

1. 编译项目：

```bash
cargo build --release
```

2. 运行程序：

```bash
./target/release/sort-srt input.json
```

或者直接使用 cargo run：

```bash
cargo run -- input.json
```

程序会生成同名的 .srt 文件，例如：`input.json` -> `input.srt`

## 输入文件格式

输入文件应为 FastWhisper 输出的 JSON 格式，包含以下字段：
- text: 完整文本
- segments: 语音片段数组
  - id: 片段ID
  - start: 开始时间
  - end: 结束时间
  - text: 片段文本
  - words: 单词数组
    - start: 单词开始时间
    - end: 单词结束时间
    - word: 单词文本

## 输出格式

生成的 SRT 文件格式如下：

```
1
00:00:00,000 --> 00:00:05,860
第一行字幕

2
00:00:06,040 --> 00:00:10,660
第二行字幕

...
```

## 开发环境

- Rust 1.70.0 或更高版本
- Cargo 包管理器

## 依赖项

- clap: 命令行参数解析
- serde: JSON 序列化/反序列化
- serde_json: JSON 处理
