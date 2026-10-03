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
2. Thêm đường dẫn thư mục skill (tính từ gốc repo) vào mảng `skills` của plugin tương ứng trong `.claude-plugin/marketplace.json`.
   Nếu là plugin mới: thêm một entry mới vào `plugins` với `source: "./"`, `strict: false` và danh sách `skills`.
3. Tăng `version` rồi commit, push.
