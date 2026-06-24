# 解耦策略参考

## 策略A：死代码删除

### 适用场景
违规依赖的代码（include、变量、函数、调用代码块）在项目中**没有任何外部调用方**，属于历史遗留的死代码。

### 识别方法
```
1. 用 Grep 全项目搜索违规函数名/变量名
2. 确认只在目标模块自身文件中出现
3. 确认无外部 include 文件使用相关类型
```

### 操作步骤
1. 删除 `.c` 中的 `#include "违规头文件.h"`
2. 删除相关的 `static` 全局变量
3. 删除相关的函数实现
4. 删除函数内的条件调用代码块
5. 删除 `.h` 中的函数声明

### 典型案例
```
违规点：logger.c → oled_display.h

死代码清单：
- #include "oled_display.h"          ← 违规依赖
- static bool g_oled_enabled = false  ← 始终为false，从未改变
- void logger_enable_oled(bool)       ← 无人调用
- oled_display_log(tag, log_buf)      ← 条件永不成立

结论：4处全部可直接删除，零功能损失。
```

### 优点
- 零风险，纯减法
- 不需要修改任何外部调用方
- 代码行数净减少

---

## 策略B：系统API替换

### 适用场景
违规依赖是自定义封装（如 `logger.h` 提供的 `LOGI/LOGE/LOGW/LOGD` 宏），但存在功能等价的**系统框架API**（如 `esp_log.h` 提供的 `ESP_LOGI/ESP_LOGE/ESP_LOGW/ESP_LOGD`）。

### 前提条件
- 替换前后功能完全等价
- 系统API在所有目标平台可用
- 不改变日志输出格式和行为

### 操作步骤
1. 将 `#include "自定义头文件.h"` 替换为 `#include "系统头文件.h"`
2. 批量替换宏调用：
   - `LOGI(` → `ESP_LOGI(`
   - `LOGW(` → `ESP_LOGW(`
   - `LOGE(` → `ESP_LOGE(`
   - `LOGD(` → `ESP_LOGD(`
3. 注意排除包含 `ESP_LOG` 前缀的已有调用（如 `ESP_LOGI(TAG, ...)` 已经是系统API）

### 典型案例
```
违规点：flash_cache.c → logger.h

替换前：                                替换后：
#include "logger.h"                     #include "esp_log.h"
LOGI(TAG, "init")                       ESP_LOGI(TAG, "init")
LOGW(TAG, "warning")                    ESP_LOGW(TAG, "warning")
LOGE(TAG, "error")                      ESP_LOGE(TAG, "error")

结论：纯文本替换，零功能变化。日志TAG宏和格式字符串保持不变。
```

### 批量替换技巧
- PowerShell正则替换（谨慎使用，可能损坏文件）：
  ```powershell
  (Get-Content file.c) -replace '\bLOGI\(', 'ESP_LOGI(' | Set-Content file.c
  ```
- 推荐方式：使用 SearchReplace 逐批替换，每批后验证
- 如果文件被损坏，`git checkout` 恢复后用 SearchReplace 逐条处理

### 优点
- 功能零损失
- 使用框架原语，可移植性更好
- 减少自定义中间层

---

## 策略C：业务逻辑归还

### 适用场景
目标模块中包含**业务层类型**（如 `plant_type_t` 枚举、`hx_data_t` 结构体）或**业务层序列化逻辑**（如好感度数据的 NVS 存取函数）。这些不属于基础设施层职责，应该回归到使用它们的业务模块中。

### 核心原则
1. **基础设施模块只提供通用存储原语**
   - ✅ 保存字符串：`nvs_set_str(handle, key, value)`
   - ✅ 保存 blob：`nvs_set_blob(handle, key, data, size)`
   - ❌ 保存 `hx_data_t` 结构体：`nvs_save_hx_data(hx_data_t *data)`

2. **不迁移代码，不新建中间层**
   - 不要写一个新的 `nvs_save_hx_data()` 放到 `data_collector.c`
   - 让调用方直接用 NVS 原语（`nvs_open` → `nvs_set_blob` → `nvs_commit` → `nvs_close`）

3. **业务类型留在业务模块**
   - `plant_type_t` 留在 `plant_config.h`
   - `hx_data_t` 留在 `hx_algo.h`
   - 基础设施模块不需要知道这些类型

### 操作步骤
1. 删除 `.h` 中的业务类型 include（如 `#include "plant_config.h"`、`#include "hx_algo.h"`）
2. 删除 `.h` 中的业务函数声明
3. 删除 `.c` 中的业务函数实现（通常是大段代码，约100-500行）
4. **不修改调用方** — 在执行报告中标注调用方待修改清单

### 典型案例
```
违规点：nvs_storage.h → plant_config.h + hx_algo.h

删除内容：
头文件：
  - #include "plant_config.h"
  - #include "hx_algo.h"
  - void nvs_save_plant_type(plant_type_t type);      // 死代码
  - void nvs_load_plant_type(plant_type_t *type);     // 死代码
  - void nvs_save_hx_data(hx_data_t *hx_data);       // 违规依赖
  - void nvs_load_hx_data(hx_data_t *hx_data);       // 违规依赖
  - void nvs_clear_hx_data(void);                      // 违规依赖

实现文件：
  - 删除 nvs_save_plant_type() 实现（~30行）
  - 删除 nvs_load_plant_type() 实现（~31行）
  - 删除 nvs_save_hx_data() 实现（~119行）
  - 删除 nvs_load_hx_data() 实现（~167行）
  - 删除 nvs_clear_hx_data() 实现（~110行）
  - 删除 KEY_PLANT_TYPE 宏定义

总计：净删除约 460 行代码，零新增。

调用方后续自行处理：
  data_collector.c 的 5 处调用 → 改用 nvs_open + nvs_set_blob/nvs_get_blob
  main.c 的 1 处调用 → 改用 nvs_open + nvs_erase_key
```

### 优点
- 基础设施模块职责清晰，不携带业务概念
- 纯减法，代码总量净减少
- plant_config.h / hx_algo.h 完全不受影响

---

## 修改后验证清单

每个违规点修复后，验证：

```
□ Grep 确认违规 include 已消失
□ Grep 确认违规函数声明已删除（.h 文件）
□ Grep 确认违规函数实现已删除（.c 文件）
□ Grep 确认所有 LOGx 宏无残留（策略B场景）
□ 文件 include 列表仅含系统/标准库文件
□ 文件行数变化合理
```