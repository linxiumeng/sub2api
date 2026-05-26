# 私有开发说明

本项目基于 [Wei-Shaw/sub2api](https://github.com/Wei-Shaw/sub2api) 开源项目进行二次开发。

## 仓库结构

| Remote | 地址 | 说明 |
|--------|------|------|
| `origin` | https://github.com/linxiumeng/sub2api.git | 个人仓库 |
| `upstream` | https://github.com/Wei-Shaw/sub2api.git | 原始开源项目 |

## 分支策略

- `main` — 保持与上游同步，不直接在此开发
- `dev` — 个人开发主分支，所有改动在此进行
- `feature/xxx` — 具体功能分支（可选）

## 日常开发流程

```bash
# 确保在 dev 分支
git checkout dev

# 开发、提交
git add .
git commit -m "feat: 你的改动描述"
git push
```

## 同步上游更新

```bash
# 1. 拉取上游最新代码
git fetch upstream

# 2. 将上游合并到 main
git checkout main
git merge upstream/main
git push

# 3. 将 main 的更新 rebase 到 dev
git checkout dev
git rebase main

# 4. 推送（rebase 后需要强制推送）
git push --force-with-lease
```

## 将 dev 合并进 main（发布）

```bash
# 1. 同步上游（见上方流程）

# 2. 切到 main，合并 dev
git checkout main
git merge dev
git push

# 3. 切回 dev 继续开发
git checkout dev
```

## 冲突处理建议

- 尽量新增文件，避免修改原始文件
- 必须修改原始文件时，集中改动、减少改动范围
- 遇到 rebase 冲突：解决冲突后 `git add . && git rebase --continue`
- 放弃 rebase：`git rebase --abort`
