# 题库练习系统 (Quiz Practice)

纯静态、零依赖的刷题网站。支持多学科切换，**考试、背题、逐章测试、错题本**四种模式。数据由 JSON 驱动，换题库只需替换 JSON 文件。

## 功能

| 模式 | 说明 |
|------|------|
| **考试** | 按章节占比抽题，题型数量和每题分值可自定义。限时可调。 |
| **背题** | 全部题目直接显示答案，可按章节/题型筛选。 |
| **测试** | 按章节逐题练习，进度自动保存（localStorage）。 |
| **错题本** | 做错的题自动收录，可筛选、复习、清空。 |

## 文件结构

```
quiz/
├── index.html              # 主页面（纯静态、零依赖）
├── subjects.json           # 学科列表配置
├── subjects/
│   └── 共同体概论.json      # 单一学科的题库数据
├── clean.py                # 题库清洗脚本（超星学习通 → JSON）
├── README.md
└── .gitignore
```

## 添加新学科

1. 准备题库 JSON 文件（格式见下方），放入 `subjects/` 目录
2. 在 `subjects.json` 中添加一行配置：

```json
{
  "id": "英语四级",
  "name": "大学英语四级题库",
  "shortName": "英语四级",
  "file": "subjects/英语四级.json",
  "questionCount": 1200,
  "chapters": 12
}
```

3. 刷新页面即可在顶部下拉框切换到新学科

题库名称会同时出现在页面标题和浏览器标签页。

## 题库 JSON 格式

```json
[
  {
    "chapter": "第一章",
    "sections": [
      {
        "type": "章节测验",
        "questions": [
          {
            "index": 1,
            "type": "单选题",
            "content": "题目正文",
            "options": [
              { "label": "A", "text": "选项A" },
              { "label": "B", "text": "选项B" }
            ],
            "answer": "B"
          }
        ]
      }
    ]
  }
]
```

支持的题型：`单选题`、`多选题`、`判断题`、`简答题`、`论述题`、`填空题`

## 部署到 GitHub Pages

1. Fork 此仓库（或直接使用）
2. 修改 `index.html` 中的 `REPO_ISSUES_URL` 为你的仓库 Issues 地址
3. 在仓库 Settings → Pages 中启用，Source 选 main 分支，目录选 `/ (root)`
4. 访问 `https://你的用户名.github.io/quiz/`

## 数据清洗

仓库内置了 `clean.py`，用于将超星学习通导出的题库清洗为标准 JSON 格式。包含一份**中华民族共同体概论**题库（1550题，16章）作为示例。

清洗其他题库时，修改 `clean.py` 顶部的 `INPUT` 路径，运行后即可输出 `题库.json`。

## 反馈

发现题目错误？点击页面底部的"提交反馈"链接，会在 GitHub Issues 中创建反馈，自动填入题目信息。
