# 哈尔滨回深圳机票调研执行计划

> **供代理型执行者使用：** 必需子技能：使用 `superpowers:subagent-driven-development`（推荐）或 `superpowers:executing-plans` 按任务逐项执行本计划。步骤使用复选框（`- [ ]`）语法跟踪。

**目标：** 执行已批准的调研规格，产出一份有来源支撑的 `2026-05-05` 从 `哈尔滨 / 长春 / 牡丹江` 前往 `深圳坪山站` 方向的航班报告，包含 Top 3 行程和购票时机建议。

**架构：** 采用 docs-first 工作流。先把 OTA 搜索结果归一化记录到 CSV，再用航司官方渠道校验入围行程，为非深圳直达方案补充到 `深圳坪山站` 的地面接驳信息，最后撰写区分已核实事实与趋势推断的最终报告。

**技术栈：** Markdown、CSV、Git、基于浏览器的 OTA 与航司搜索、Shell 校验工具（`rg`、`head`、`wc`、`awk`）

---

## 计划文件

- 创建：`data/flight-research/2026-05-05/candidates.csv`
- 创建：`data/flight-research/2026-05-05/evidence-log.md`
- 创建：`data/flight-research/2026-05-05/ground-transfer-notes.md`
- 创建：`data/flight-research/2026-05-05/trend-analysis.md`
- 创建：`data/flight-research/2026-05-05/shortlist.md`
- 创建：`docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md`

## 航线矩阵

所有搜索都必须限定在以下矩阵内：

- 出发地：`哈尔滨 (HRB)`、`长春 (CGQ)`、`牡丹江 (MDG)`
- 到达地：`深圳 (SZX)`、`香港 (HKG)`、`澳门 (MFM)`、`广州 (CAN)`、`珠海 (ZUH)`、`惠州 (HUZ)`
- 日期：`2026-05-05`
- 仅允许当日到达
- 允许直飞和中转行程
- 最短中转时间：`60` 分钟
- 目标到达锚点：`深圳坪山站`
- 票价口径：成人、含税、裸票
- 数据来源：航司官网、携程、飞猪、同程、去哪儿、航旅纵横

### 任务 1：搭建调研工作区

**文件：**
- 创建：`data/flight-research/2026-05-05/candidates.csv`
- 创建：`data/flight-research/2026-05-05/evidence-log.md`
- 创建：`data/flight-research/2026-05-05/ground-transfer-notes.md`
- 创建：`data/flight-research/2026-05-05/trend-analysis.md`
- 创建：`docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md`

- [ ] **步骤 1：创建调研目录**

运行：`mkdir -p data/flight-research/2026-05-05 docs/superpowers/research`
预期：命令成功退出且无输出

- [ ] **步骤 2：用精确表头初始化候选表**

```csv
captured_at,channel,origin_city,origin_airport,destination_city,destination_airport,airline,flight_numbers,depart_at,arrive_at,arrive_same_day,stops,stop_city,layover_minutes,listed_price_cny,price_basis,bookable,official_price_cny,official_checked_at,official_status,ground_mode_to_pingshan,ground_cost_cny,ground_minutes,total_minutes,risk_level,risk_notes,score,link_or_path
```

- [ ] **步骤 3：校验 CSV 表头正确**

运行：`head -n 1 data/flight-research/2026-05-05/candidates.csv`
预期：

```text
captured_at,channel,origin_city,origin_airport,destination_city,destination_airport,airline,flight_numbers,depart_at,arrive_at,arrive_same_day,stops,stop_city,layover_minutes,listed_price_cny,price_basis,bookable,official_price_cny,official_checked_at,official_status,ground_mode_to_pingshan,ground_cost_cny,ground_minutes,total_minutes,risk_level,risk_notes,score,link_or_path
```

- [ ] **步骤 4：初始化证据日志**

```md
# 证据日志

## 搜索参数

- 抓取日期：2026-04-07
- 出行日期：2026-05-05
- 出发地：哈尔滨 / 长春 / 牡丹江
- 到达地：深圳 / 香港 / 澳门 / 广州 / 珠海 / 惠州
- 最终比较锚点：深圳坪山站
- 票价口径：成人含税裸票
- 约束：当日出发且当日到达，中转 >= 60 分钟，且最好 <= 6 小时

## OTA 抓取

### 携程

### 飞猪

### 同程

### 去哪儿

### 航旅纵横

## 官方校验

## 价格冲突备注
```

- [ ] **步骤 5：初始化地面接驳备注**

```md
# 前往深圳坪山站的地面接驳备注

## 深圳

## 香港

## 澳门

## 广州

## 珠海

## 惠州
```

- [ ] **步骤 6：初始化趋势分析备注**

```md
# 价格趋势分析备注

## 已核实事实

## 邻近日期比较

## 7 天窗口

## 14 天窗口

## 21 天窗口

## 推断
```

- [ ] **步骤 7：初始化最终报告骨架**

```md
# 2026-05-05 哈尔滨方向回深圳机票深度调研

## 1. 任务参数确认

## 2. 候选方案总表

## 3. Top 3 性价比方案

## 4. 最低价方案

## 5. 最省时间方案

## 6. 高风险备选方案

## 7. 购买时机判断

## 8. 重点监控路线

## 9. 简短结论摘要
```

- [ ] **步骤 8：提交脚手架文件**

```bash
git add data/flight-research/2026-05-05/candidates.csv data/flight-research/2026-05-05/evidence-log.md data/flight-research/2026-05-05/ground-transfer-notes.md data/flight-research/2026-05-05/trend-analysis.md docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md
git commit -m "docs: 搭建机票调研工作区"
```

### 任务 2：抓取完整航线矩阵的 OTA 库存

**文件：**
- 修改：`data/flight-research/2026-05-05/candidates.csv`
- 修改：`data/flight-research/2026-05-05/evidence-log.md`

- [ ] **步骤 1：在证据日志中记录精确的航线矩阵**

在 `## OTA 抓取` 下添加以下清单：

```md
航线矩阵：
- HRB -> SZX / HKG / MFM / CAN / ZUH / HUZ
- CGQ -> SZX / HKG / MFM / CAN / ZUH / HUZ
- MDG -> SZX / HKG / MFM / CAN / ZUH / HUZ
```

- [ ] **步骤 2：搜索携程的全部 18 个出发地/到达地组合，并把每个可售且当日到达的行程追加到 CSV**

对每一行 CSV：
- `captured_at` 使用类似 `2026-04-07T10:35+08:00` 的本地 ISO 风格时间
- `channel` 填 `携程`
- `arrive_same_day` 填 `yes`
- `stops` 对直飞填 `0`，单次中转填 `1`
- 仅直飞行程允许 `stop_city` 和 `layover_minutes` 为空
- `price_basis` 必须精确填写为 `adult_tax_included_bare_fare`
- 只有来源页面展示实际购买路径时，`bookable` 才填 `yes`
- `link_or_path` 填 URL 或可复现的导航说明

- [ ] **步骤 3：以相同的 18 个组合搜索飞猪，并把每个可售且当日到达的行程追加到 CSV**

沿用步骤 2 的采集规则，并追加 `channel = 飞猪`。

- [ ] **步骤 4：以相同的 18 个组合搜索同程，并把每个可售且当日到达的行程追加到 CSV**

沿用步骤 2 的采集规则，并追加 `channel = 同程`。

- [ ] **步骤 5：以相同的 18 个组合搜索去哪儿，并把每个可售且当日到达的行程追加到 CSV**

沿用步骤 2 的采集规则，并追加 `channel = 去哪儿`。

- [ ] **步骤 6：以相同的 18 个组合搜索航旅纵横，并把每个可售且当日到达的行程追加到 CSV**

沿用步骤 2 的采集规则，并追加 `channel = 航旅纵横`。

- [ ] **步骤 7：为每个 OTA 渠道在证据日志中添加带时间戳的小节**

每个渠道小节都必须记录：
- 查询开始时间
- 查询结束时间
- 搜索日期
- 覆盖的航线矩阵
- 显著缺口，例如 “MDG -> HUZ 无结果”
- 价格异常（如有）

- [ ] **步骤 8：校验原始库存不为空**

运行：`wc -l data/flight-research/2026-05-05/candidates.csv`
预期：总行数大于 `1`

- [ ] **步骤 9：校验每个 OTA 渠道都有对应小节**

运行：`rg '^### ' data/flight-research/2026-05-05/evidence-log.md`
预期：

```text
### 携程
### 飞猪
### 同程
### 去哪儿
### 航旅纵横
```

- [ ] **步骤 10：提交 OTA 库存**

```bash
git add data/flight-research/2026-05-05/candidates.csv data/flight-research/2026-05-05/evidence-log.md
git commit -m "docs: 抓取 OTA 航班库存"
```

### 任务 3：在航司官方渠道校验不同的行程

**文件：**
- 修改：`data/flight-research/2026-05-05/candidates.csv`
- 修改：`data/flight-research/2026-05-05/evidence-log.md`

- [ ] **步骤 1：按 `airline + flight_numbers + depart_at + arrive_at` 对 OTA 库存去重，并生成不同航班组合的候选清单**

使用去重后的清单，避免对同一套航班组合在多个 OTA 上重复查询航司官网。

- [ ] **步骤 2：对每个不同的行程组合，搜索对应航司官网并记录官方结果**

对属于同一行程的每一行都更新以下 CSV 列：
- `official_price_cny`
- `official_checked_at`
- `official_status`

允许的 `official_status` 值：
- `matched`
- `not_found`
- `site_unavailable`
- `not_directly_bookable`

- [ ] **步骤 3：把每次官方校验结果记录到证据日志**

在 `## 官方校验` 下记录：
- 航司
- 航班号
- 校验时间
- 官方结果
- 若查到则记录官方价格
- 链接或导航路径

- [ ] **步骤 4：把价格冲突记录到专门章节**

对任何 OTA 价格与官方价格不一致的行程，在 `## 价格冲突备注` 下新增一条 bullet，包含：
- 行程标识
- 最低 OTA 价格
- 官方价格
- 如果能看出原因，则写明可能原因

- [ ] **步骤 5：校验每条抓取记录都有官方状态**

运行：`awk -F, 'NR>1 && $20=="" {print NR}' data/flight-research/2026-05-05/candidates.csv`
预期：无输出

- [ ] **步骤 6：提交官方校验结果**

```bash
git add data/flight-research/2026-05-05/candidates.csv data/flight-research/2026-05-05/evidence-log.md
git commit -m "docs: 校验航班官方渠道信息"
```

### 任务 4：补充前往深圳坪山站的地面接驳信息

**文件：**
- 修改：`data/flight-research/2026-05-05/candidates.csv`
- 修改：`data/flight-research/2026-05-05/ground-transfer-notes.md`

- [ ] **步骤 1：为每个非深圳落地点找出当日到达后前往深圳坪山站的最快可行路径**

覆盖以下城市分组：
- 香港
- 澳门
- 广州
- 珠海
- 惠州

每个分组都必须包含：
- 起始机场或到达区域
- 主要接驳方式
- 预估人民币费用
- 接驳总时长（分钟）
- 关键运营风险

- [ ] **步骤 2：把接驳备注记录到对应城市标题下**

每个城市章节都必须以一行建议收尾，例如：
- “作为评分默认接驳路径”
- “如果默认路径赶不上末班车，则采用此备选路径”

- [ ] **步骤 3：填充候选表中的地面接驳列**

为每一行更新：
- `ground_mode_to_pingshan`
- `ground_cost_cny`
- `ground_minutes`

对深圳直达落地：
- `ground_mode_to_pingshan` 可以填 `metro_or_taxi_from_szx`
- 但 `ground_cost_cny` 和 `ground_minutes` 仍必须填写最现实的当日估算值

- [ ] **步骤 4：为每个候选项计算 `total_minutes`**

`total_minutes` 必须包含：
- 飞行时长
- 中转时长
- 前往 `深圳坪山站` 的地面接驳时长

- [ ] **步骤 5：校验非深圳落地行没有缺失地面接驳数据**

运行：`awk -F, 'NR>1 && $5!="深圳" && ($21=="" || $22=="" || $23=="") {print NR}' data/flight-research/2026-05-05/candidates.csv`
预期：无输出

- [ ] **步骤 6：提交地面接驳数据**

```bash
git add data/flight-research/2026-05-05/candidates.csv data/flight-research/2026-05-05/ground-transfer-notes.md
git commit -m "docs: 补充地面接驳评分输入"
```

### 任务 5：应用硬筛选并产出候选清单

**文件：**
- 创建：`data/flight-research/2026-05-05/shortlist.md`
- 修改：`data/flight-research/2026-05-05/candidates.csv`

- [ ] **步骤 1：移除或标记任何违反已批准硬约束的记录**

淘汰任何违反以下条件的行：
- 不是当日到达
- 中转短于 `60` 分钟
- 中转时间明显超过偏好的 `6` 小时上限
- 出发地或到达地不在允许范围内
- 票价口径不是裸票
- 来源不在批准范围内

对于边界情况，用 `risk_notes` 解释，不要静默删除。

- [ ] **步骤 2：为每条剩余记录分配风险等级**

允许的 `risk_level` 值：
- `low`
- `medium`
- `high`

按规格中的规则处理：
- 直飞或同机场受保护且时间宽松的联程，标记为 low
- 同机场但更紧张，或接驳更折腾的行程，标记为 medium
- 自拼、跨境脆弱、或接近最短中转时间的路径，标记为 high

- [ ] **步骤 3：为剩余候选项评分**

使用已批准的权重模型：
- `40%` 票面价格
- `20%` 地面接驳成本
- `25%` 总时长
- `15%` 风险

把最终归一化结果写入 `score` 列。分数越低越好。

- [ ] **步骤 4：撰写候选清单摘要**

创建 `data/flight-research/2026-05-05/shortlist.md`，包含以下章节：

```md
# 候选清单

## 按评分排序的 Top 3

## 最低票价

## 最快到达深圳坪山站

## 高风险低价备选
```

- [ ] **步骤 5：校验所有保留记录都有评分**

运行：`awk -F, 'NR>1 && $27=="" {print NR}' data/flight-research/2026-05-05/candidates.csv`
预期：无输出

- [ ] **步骤 6：提交候选清单**

```bash
git add data/flight-research/2026-05-05/candidates.csv data/flight-research/2026-05-05/shortlist.md
git commit -m "docs: 机票候选排序并生成清单"
```

### 任务 6：分析价格趋势与购买窗口

**文件：**
- 修改：`data/flight-research/2026-05-05/trend-analysis.md`
- 修改：`data/flight-research/2026-05-05/evidence-log.md`

- [ ] **步骤 1：为评分靠前的路线抓取价格日历或相邻日期证据**

至少覆盖以下邻近日期：
- `2026-05-03`
- `2026-05-04`
- `2026-05-05`
- `2026-05-06`
- `2026-05-07`
- `2026-05-08`

- [ ] **步骤 2：把所有可直接观察到的事实记录到 `## 已核实事实` 下**

这里只能写抓取时来源页面明确可见的事实，例如：
- 某个相邻日期的价格
- 某个具体时间看到的官方票价
- 可见的低价日历模式

- [ ] **步骤 3：填写三个时间窗口章节**

在 `## 7 天窗口`、`## 14 天窗口` 和 `## 21 天窗口` 中分别写明：
- 有什么证据支持继续等待
- 有什么证据支持现在购买
- 什么情况会推翻当前判断

- [ ] **步骤 4：单独撰写推断章节**

在 `## 推断` 下写明：
- 可能的购买窗口
- 触发下单的价格阈值
- 最可能出现更优替代方案的路线

- [ ] **步骤 5：校验趋势分析文件同时包含事实与推断**

运行：`rg '^## ' data/flight-research/2026-05-05/trend-analysis.md`
预期：

```text
## 已核实事实
## 邻近日期比较
## 7 天窗口
## 14 天窗口
## 21 天窗口
## 推断
```

- [ ] **步骤 6：提交趋势分析**

```bash
git add data/flight-research/2026-05-05/trend-analysis.md data/flight-research/2026-05-05/evidence-log.md
git commit -m "docs: 分析价格趋势与购买窗口"
```

### 任务 7：撰写最终调研报告

**文件：**
- 修改：`docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md`
- 修改：`data/flight-research/2026-05-05/shortlist.md`

- [ ] **步骤 1：填写参数确认和候选方案摘要**

`## 1. 任务参数确认` 必须重述：
- 出行日期
- 允许的出发地
- 允许的到达地
- 当日到达规则
- 最短中转时间
- 票价口径
- 最终锚点为 `深圳坪山站`

`## 2. 候选方案总表` 必须总结保留下来的记录，而不是原始被淘汰的记录。

- [ ] **步骤 2：撰写 Top 3、最低价、最快方案和高风险备选章节**

每个被推荐的行程都必须回答：
- 为什么选它
- 适合什么人
- 主要风险
- 在什么价格以上它就不再值得推荐

- [ ] **步骤 3：撰写购买建议**

`## 7. 购买时机判断` 必须明确回答：
- 现在买还是继续等
- 最晚观察到哪一天
- 触发下单的价格
- 重点监控哪些路线

- [ ] **步骤 4：撰写最终摘要块**

`## 9. 简短结论摘要` 必须精确包含以下标签：

```md
- 综合最优：
- 最低价：
- 最省时间：
- 建议购买时间：
- 重点监控路线：
```

- [ ] **步骤 5：校验报告标题结构**

运行：`rg '^## ' docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md`
预期：

```text
## 1. 任务参数确认
## 2. 候选方案总表
## 3. Top 3 性价比方案
## 4. 最低价方案
## 5. 最省时间方案
## 6. 高风险备选方案
## 7. 购买时机判断
## 8. 重点监控路线
## 9. 简短结论摘要
```

- [ ] **步骤 6：提交最终报告**

```bash
git add docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md data/flight-research/2026-05-05/shortlist.md
git commit -m "docs: 添加哈尔滨回深圳机票调研报告"
```

### 任务 8：最终 QA 与发布

**文件：**
- 修改：`data/flight-research/2026-05-05/candidates.csv`
- 修改：`data/flight-research/2026-05-05/evidence-log.md`
- 修改：`data/flight-research/2026-05-05/ground-transfer-notes.md`
- 修改：`data/flight-research/2026-05-05/trend-analysis.md`
- 修改：`data/flight-research/2026-05-05/shortlist.md`
- 修改：`docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md`

- [ ] **步骤 1：对候选表运行完整性检查**

运行：`awk -F, 'NR>1 && ($15=="" || $17=="" || $20=="" || $22=="" || $23=="" || $24=="" || $25=="" || $27=="") {print NR}' data/flight-research/2026-05-05/candidates.csv`
预期：无输出

- [ ] **步骤 2：对所有交付物运行占位符扫描**

运行：`rg -n 'TBD|TODO|todo|待补|占位' data/flight-research/2026-05-05 docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md`
预期：无输出

- [ ] **步骤 3：只暂存可发布的调研文件，并检查已暂存文件列表**

运行：`git add data/flight-research/2026-05-05 docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md && git diff --cached --name-only`
预期：

```text
data/flight-research/2026-05-05/candidates.csv
data/flight-research/2026-05-05/evidence-log.md
data/flight-research/2026-05-05/ground-transfer-notes.md
data/flight-research/2026-05-05/shortlist.md
data/flight-research/2026-05-05/trend-analysis.md
docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md
```

- [ ] **步骤 4：创建发布提交**

```bash
git commit -m "docs: 发布哈尔滨回深圳机票调研"
```

- [ ] **步骤 5：推送分支**

```bash
git push origin HEAD
```

- [ ] **步骤 6：在报告交付说明中记录已推送的提交哈希**

先运行：

```bash
git rev-parse --short HEAD
```

预期：标准输出中出现一个短提交哈希

然后把实际哈希作为最后一行追加到报告中：

```md
> 已发布到 Git，提交：abc1234
```
