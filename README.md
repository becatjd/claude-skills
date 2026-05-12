# claude-skills

个人 Claude Code skill 集合，通过 plugin marketplace 一键安装。

## 当前包含的 skill

| 名称 | 作用 |
|------|------|
| **fp-breakdown** | 根据系统功能描述拆分软件功能点（IFPUG 方法：ILF/EIF/EI/EO/EQ），输出标准表格并写入 `功能点清单.md`，用于投标、需求分析、工时估算场景 |

## 安装

在 Claude Code 中执行两条命令：

```
/plugin marketplace add becatjd/claude-skills
/plugin install fp-breakdown@claude-skills
```

第一条把本仓库注册为 marketplace，第二条从中安装 `fp-breakdown` plugin。

## 使用示例

安装后新开对话，给 Claude 一段系统功能描述：

> 帮我把这个学生选课系统拆成 40 个功能点：学生可注册登录、选课、退课、查成绩；教师可发布课程、录入成绩；管理员管理用户和课程

Claude 会自动调用 fp-breakdown，输出标准表格并在当前工作目录写入 `功能点清单.md`。

## 更新

仓库有新版本后：

```
/plugin marketplace update claude-skills
```

## 新增 skill 的步骤（仓库维护者）

1. 在 `skills/` 下新建文件夹，例如 `skills/your-skill/`
2. 放入 `SKILL.md`（含 frontmatter）
3. 编辑 `.claude-plugin/marketplace.json`，在 `plugins` 数组追加一项：
   ```json
   {
     "name": "your-skill",
     "description": "……",
     "source": "./",
     "strict": false,
     "skills": ["./skills/your-skill"]
   }
   ```
4. 提交并推到 GitHub
5. 用户执行 `/plugin marketplace update claude-skills` 即可看到新 plugin

## 本地调试（推 GitHub 之前）

```
/plugin marketplace add D:\Program\claude-skills
/plugin install fp-breakdown@claude-skills
```

marketplace 路径既支持 GitHub URL，也支持本地目录。

## 手动安装（无 plugin 命令时的兜底方案）

如果你的 Claude Code 环境没有 `/plugin` 命令（例如某些 IDE 扩展不支持），按以下步骤手动安装：

1. 把本仓库 `skills/fp-breakdown/` 整个文件夹复制到你的全局 skills 目录：
   - Windows：`C:\Users\<你的用户名>\.claude\skills\fp-breakdown\`
   - macOS / Linux：`~/.claude/skills/fp-breakdown/`
2. 重启 Claude Code，skill 即被自动识别
3. 验证：在新对话里说"拆 20 个功能点……"，Claude 应自动调用 fp-breakdown
