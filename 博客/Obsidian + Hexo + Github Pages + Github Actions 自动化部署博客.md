
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
	Local->>Hexo: 推送
	Hexo->>Obsidian: 触发
end
Hexo->>Obsidian: 拉取
Obsidian->>Obsidian:生成静态文件
Obsidian->>Github:推送
```
	click Obsidian "https://github.com/7zMonkey/Obsidian"
click Hexo "https://github.com/7zMonkey/obsidian2hexo-template"
click Github "https://github.com/7zMonkey/7zMonkey.github.io"
subgraph 触发方式1
Local--推送-->Obsidian
end
subgraph obsidian actions
Obsidian<--拉取-->Hexo
Obsidian==推送==>Github
end
subgraph 触发方式2
Local--推送-->Hexo
end
subgraph hexo actions
Hexo-.-触发-.->Obsidian
end