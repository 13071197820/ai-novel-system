# ai-novel-system
# 📚 AI 小说生成系统工作流指南
> 使用 VS Code + Cline 工具进行本地多模块 AI 小说创作

---

## 🧩 一、项目结构
```
ai-novel-system/
├── prompts/ # 所有 Prompt 模块模板
│ ├── 01_world_building.prompt.md
│ ├── 01b_power_system.prompt.md
│ ├── 02_lore_background.prompt.md
│ ├── 03_character_design.prompt.md
│ ├── 04_scene_creation.prompt.md
│ ├── 05_plot_structure.prompt.md
│ ├── 05b_conflict_refiner.prompt.md
│ ├── 05c_growth_curve.prompt.md
│ ├── 05d_plot_pacing.prompt.md
│ ├── 06_meme_injector.prompt.md
│ ├── 07_outline_generation.prompt.md
│ └── 08_chapter_writer.prompt.md
│
├── workflow.yaml # Cline 工作流定义文件（后续生成）
├── README_workflow.md # 当前说明文件
└── output/ # 输出内容目录
├── world.json
├── characters.json
├── outline.json
└── chapter_01.txt
```

---

## ⚙️ 二、运行前准备

2. **项目初始化**
   
🚀 三、推荐运行顺序（自动链式生成）
| 阶段    | 模块名称  | Prompt 文件                       | 输入                            | 输出文件                     |
| ----- | ----- | ------------------------------- | ----------------------------- | ------------------------ |
| 🪐 1  | 世界观生成 | 01_world_building.prompt.md     | genre, theme, tone, world_era | output/world.json        |
| ⚡ 2   | 力量体系  | 01b_power_system.prompt.md      | world_overview                | output/power.json        |
| 🏺 3  | 背景文化  | 02_lore_background.prompt.md    | world_overview, power_system  | output/lore.json         |
| 👤 4  | 人物构建  | 03_character_design.prompt.md   | world, lore, power            | output/characters.json   |
| 🏙️ 5 | 场景设定  | 04_scene_creation.prompt.md     | world, characters             | output/scenes.json       |
| ⚔️ 6  | 剧情结构  | 05_plot_structure.prompt.md     | world, characters, scenes     | output/plot.json         |
| 🔥 7  | 冲突净化  | 05b_conflict_refiner.prompt.md  | plot_structure                | output/conflicts.json    |
| 📈 8  | 成长曲线  | 05c_growth_curve.prompt.md      | refined_conflicts, characters | output/growth.json       |
| 🎵 9  | 节奏图谱  | 05d_plot_pacing.prompt.md       | growth_curve, emotional_tone  | output/pacing.json       |
| 💬 10 | 热梗注入  | 06_meme_injector.prompt.md      | pacing_map                    | output/meme_outline.json |
| 🧩 11 | 大纲生成  | 07_outline_generation.prompt.md | meme_outline                  | output/outline.json      |
| 📖 12 | 下一章生成 | 08_chapter_writer.prompt.md     | outline, characters, tone     | output/chapter_01.txt    |


🧠 四、 自动化执行方式
Cline 等agent支持 YAML 级工作流描述，可实现链式自动执行。

后续我们会生成 workflow.yaml，其逻辑如下图所示：

(world) → (power) → (lore) → (characters)
     ↓             ↓
   (scenes) → (plot) → (conflicts) → (growth)
                                   ↓
                             (pacing)
                                   ↓
                             (meme)
                                   ↓
                             (outline)
                                   ↓
                             (chapter)

每个节点会自动：

读取上一个节点的 .json 输出

将结果注入到下一个 .prompt.md

最终导出 .txt 或 .json 文件


🧩 五、文件命名规范

| 文件类型         | 扩展名         | 内容说明             |
| ------------ | ----------- | ---------------- |
| `.prompt.md` | Prompt 模板文件 | 包含 LLM 提示语与占位符变量 |
| `.json`      | 中间数据        | 模块输出结果           |
| `.txt`       | 小说文本        | 章节或故事输出          |
| `.yaml`      | 工作流定义       | 自动执行顺序与依赖定义      |


🎯 六、创作扩展建议
| 模块方向  | 可扩展思路                    |
| ----- | ------------------------ |
| 世界观扩展 | 增加分支世界、平行维度设定            |
| 力量体系  | 允许融合科技修真或灵魂系统            |
| 热梗注入  | 建立年度热词库 JSON 文件，按时间更新    |
| 节奏控制  | 可联动音乐 BPM 或镜头剪辑节奏（适合影视化） |
| 角色系统  | 引入 GPT Memory 记录角色长期性格演变 |



后续扩展（高级玩法）
| 模块   | 扩展内容       | 说明             |
| ---- | ---------- | -------------- |
| 章节生成 | 多视角 POV 版本 | 支持反派或配角视角      |
| 场景模块 | 自动生成概念图    | 调用图像生成 API     |
| 冲突模块 | 引入心理学曲线    | 让冲突更具真实情感触发逻辑  |
| 热梗模块 | 建立网络语料数据库  | 周期更新、自动嵌入当前流行语 |
| 成长曲线 | 绑定 XP 模型   | 模拟游戏化成长系统      |


执行完成后：

输出文件自动保存到 /output

章节文本可直接预览或继续编辑扩展



