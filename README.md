# Claude Skills Marketplace

Marketplace chứa các plugin/skill cho Claude Code.

## Cấu trúc

```
.
├── .claude-plugin/
│   └── marketplace.json          # Danh mục plugin của marketplace
└── plugins/
    └── example-skills/
        ├── .claude-plugin/
        │   └── plugin.json       # Manifest của plugin
        └── skills/
            └── hello-world/
                └── SKILL.md      # Nội dung skill
```

## Cài đặt

Trong Claude Code:

```
/plugin marketplace add sontn224/claude-skills-marketplace
/plugin install example-skills@claude-skills-marketplace
```

## Thêm skill mới

1. Tạo `plugins/<plugin>/skills/<tên-skill>/SKILL.md` với frontmatter `name` và `description`.
2. Nếu là plugin mới: tạo `plugins/<plugin>/.claude-plugin/plugin.json` và thêm entry vào `plugins` trong `.claude-plugin/marketplace.json`.
3. Tăng `version` rồi commit, push.
