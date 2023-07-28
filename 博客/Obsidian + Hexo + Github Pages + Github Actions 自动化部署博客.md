---
title: Obsidian + Hexo + Github Pages + Github Actions 自动化部署博客
tags: 
	- 博客
categories:
date: 2023-07-29 12:43:27
hidden: false
---
```mermaid
sequenceDiagram
participant Local as Local
participant Obsidian as Obsidian
participant Hexo as Hexo Template
participant Github as Github Pages
opt 推送 Obsidian 触发
	Local->>Obsidian:推送
	Obsidian->>Obsidian: 触发
end
opt 推送 Hexo template 触发
	Note over Local: 这是一个提示信息
	Local->>Hexo: 推送
	Note over Hexo: Hexo Actions
	activate Hexo
	Hexo->>Obsidian: 触发
	deactivate Hexo
end
activate Obsidian
Note over Obsidian: Obsidian Actions
Hexo->>Obsidian: 拉取
Obsidian->>Obsidian:生成静态文件
Obsidian->>Github:推送
deactivate Obsidian
```
