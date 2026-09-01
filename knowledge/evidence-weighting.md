# 证据权重与冲突处理

## 权重模型

这是 `[FRAMEWORK]`，不是古籍分数。它把原典的“宫位、主星、会照、限运”信息转为可审计决策。

| 权重 | 证据 | 基础分 | 例子 |
|---|---|---:|---|
| L1 | 目标宫本宫、命/身宫、三方四正、对宫、主星、亮度、本命四化 | 3 | 夫妻宫贪狼平；命宫紫微天相 |
| L1-dynamic | 当前大限、流年/小限对目标结构的明确触发 | 3 | 大限落夫妻三方；流年化禄入目标 |
| L2 | 同宫组合、辅弼魁钺昌曲、禄存天马、四煞/空耗、会照 | 2 | 天钺同宫；铃星陷同度 |
| L3 | 单颗弱杂曜、泛化星性、未确认截图/OCR | 1 | 只见一颗天姚 |

## 结论门槛

1. 将支持证据和反向证据分开计分，不以总分抵销反证。
2. High：至少 3 个独立 L1/L1-dynamic 支持，且没有同等级反证。
3. Medium：2 个重要结构支持，或 3 个支持但有弱反证。
4. Low：主要依赖单星、L2/L3、模糊截图或争议流派。
5. 涉及婚姻、健康、投资等高风险主题时，整体置信度最多写 Medium，除非只是描述已观察事实而非预测。

## 独立性规则

同一星在同一宫的三种文案不算三个证据；“主星 + 宫位”“三方主星”“四化落点”“限运触发”才可视为相对独立。三方同一来源的重复描述要合并。

## 冲突协议

```text
collect support[] and counter[] with level, location, source, timeScope
if counter has same level as support:
  keep both; describe two-stage or conditional manifestation
  reduce confidence by one level
if source is [UNCERTAIN] or school is disputed:
  do not use it as sole support
explain what real-world observation could distinguish the readings
```

## 示例

“夫妻宫主星提供吸引力和互动需求（L1 支持），天钺提供贵人/体面资源（L2 支持），铃星同度带来突发争执风险（L2 反证），因此结论是‘有吸引力但稳定依赖边界与沟通’，Medium；不是‘一定多婚’。”
