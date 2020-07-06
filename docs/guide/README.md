# 需求
 根据配置JSON动态生成表单组件


## 使用场景
- 后端JSON
- 前端JS 支持callback slot render

## 开发前Spec
1. 可扩展性
- 开闭原则
- 代理模式
- 策略模式
- 工厂模式
---
2. 易维护性
- 单一职责
- 纯函数
- 代码注释
---
3. 灵活多配置
- 支持json配置
- 支持slot自定义模板
- getStyle
- getClass
---
4. 高性能
- 大量数据
- 递归性能
- 嵌套问题
- 1000个form表单的性能问题
- json diff
- while循环性能好


## 配置

- 无嵌套

类型 | 必须Label | 可否嵌套子组件 | 可否配置
-|-|-|-|
Button | false | false | true |
Select | false | false | true |
Switch | false | false | true |
Input | true | false | true |
DatePicker | false | false | true |
Divider
- 组件多层嵌套


## 测试

# 按钮

使用方法1

<!-- <el-button>test</el-button> -->
<!-- <btn></btn> -->
<!-- <generator></generator> -->
<test></test>

## JSON样例

```
{
    "layout": "horizontal",
    "type": "default | modal",
    "col": 3,
    "row": 4,
    "width": "100px",
    "height": "300px",
    "form": [
        {
            "label": "按钮",
            "type": "button",
            "vmname": "btn1",
            "config": {
                "text": "btn1-name",
                "on": {
                    "click": "testFunc"
                },
                "style": {
                    "color": "white"
                },
                "props": {
                    "type": "primary"
                }
            }
        },
        {
            "label": "输入框",
            "type": "input",
            "vmname": "input1",
            "config": {
                "on": {
                    "click": "testFunc"
                },
                "style": {
                    "color": "white"
                },
                "props": {
                    "show-word-limit": true
                },
                "attrs": {
                    "placeholder": "请输入."
                }
            }
        }
    ]
}
```