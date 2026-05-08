# Software Tools 复习整理（来自 `softwaretool.docx`）

## 使用说明

- 这份笔记按考试高频主题重排，方便快速查找。
- 页码默认指向 `index777.pdf` 的 PDF 页码（如 `p.9`）。
- 涉及真题时，会标注 `tb2-example-answers.pdf` 的对应考点。

---

## Week 01 - HTTP 与协议基础

### 1) 请求消息 vs 响应消息（`p.4`）
- **请求（Request）**：客户端发给服务器，包含方法、路径、请求头等。
- **响应（Response）**：服务器返回，包含状态码、响应头、响应体。
- **考试常见点**：看清“是否有响应体”、状态码含义、头字段用途。

### 2) Q1 简答思路 + 答案（`tb2 Q1`）
**思路（3步）**
1. 先看请求方法：`HEAD`。
2. `HEAD` 规则：只返回头，不返回消息体。
3. 即使有 `Content-Length`，也只是“对应 GET 时的长度”。

**答案**
- 需要处理的 message body 字节数是 **0**（选 **A**）。

### 3) Q2 简答思路 + 答案（`tb2 Q2`）
**思路（2步）**
1. URI 里默认不区分大小写的是 `scheme` 和 `host`。
2. `path` 不应默认当作不区分大小写。

**答案**
- case-insensitive 的是 **scheme + host**（选 **C**）。

### 4) Q3 简答思路 + 答案（`tb2 Q3`）
**思路（2步）**
1. 先看状态码首位：`204` 属于 `2xx`。
2. `2xx` 表示请求成功完成。

**答案**
- 可以合理推出“请求已成功完成”（选 **A**）。

### 5) `fetch` Promise 的状态（`p.9`）
- `fetch(url)` 的 Promise 目标是“拿到一个 Response 对象”。
- 只要收到了 HTTP 响应（即使是 `404`/`500`），Promise 仍是 **fulfilled**。
- 只有网络层失败（DNS、连不上、协议错误等）才是 **rejected**。

---

## Week 02 - HTML

### 1) HTML Elements 基础（`p.20`）
- 重点是识别合法元素与语义用途（结构含义，而不是外观）。
- 题目常见陷阱：看起来像属性名/值的词并不是元素名。

### 2) Q4 简答思路 + 答案（`tb2 Q4`）
**思路（2步）**
1. 先判断是不是“标签名”（element tag）：`select` / `thead` / `input` 都是标签。
2. 再看剩下选项是否更像属性：`value` 是属性名，不是 HTML5 元素。

**答案**
- 不是 HTML5 element 的是 **D. `value`**。

**必备知识点**
- HTML **元素**是标签（如 `<input>`、`<select>`、`<thead>`）。
- HTML **属性**是写在标签里的键值（如 `value="abc"`、`id="x"`、`class="y"`）。
- 做题时优先区分“标签名”与“属性名”，能快速排除干扰项。

### 3) Q5 简答思路 + 答案（`tb2 Q5`）
**思路（3步）**
1. 先判断题目在问“语义作用”还是“视觉样式”。
2. `h1` 的核心价值是语义：标记页面顶级标题，便于程序理解文档结构。
3. 字体大小粗细属于 CSS 控制，不是必须靠 `h1` 默认样式。

**答案**
- 正确选项是 **C**：`h1` 让程序知道这段文本是 top-level heading。

**对应 `index777` 知识点（可迁移）**
- `p.17-21`（HTML 周）：HTML 强调语义结构，标签应表达内容角色而非仅表达外观。
- 标题层级用于构建文档结构（heading hierarchy），便于搜索引擎和辅助技术解析页面。
- “语义”和“样式”要分离：结构用 HTML，表现用 CSS。

**必备知识点**
- `h1` 是顶级标题语义标签，不是“字体变大工具”。
- 页面不要求“必须有一个 `h1` 才合法”；没有 `h1` 不会因此触发 quirks mode。
- 选标签先问“这段内容在文档中的角色是什么”，再考虑样式。

### 4) Q6 简答思路 + 答案（`tb2 Q6`）
**思路（2步）**
1. 绝对 URL 的关键词是“完整定位”，即包含协议和主机名（域名）。
2. 其余选项要么混淆概念（永久链接），要么与 URL 无关。

**答案**
- 正确选项是 **A**：absolute URL 指向位置时使用协议和域名。

**对应 `index777` 知识点（可迁移）**
- `p.5-6`：HTTP 请求行与 `Host` 头共同指向完整目标资源。
- `p.6`：`request-target`（path + query）与主机组合后，才是完整资源定位。
- URI/URL 复习时要区分“完整地址”与“相对路径”。

**必备知识点**
- 绝对 URL 典型形式：`scheme://host/path?query`（如 `https://example.com/docs/a.html`）。
- 相对 URL 依赖当前页面上下文（如 `./about.html`, `/images/logo.png`）。
- absolute 不是“永久不变”的意思，也不等于“站点根目录”。

---

## Week 03 - CSS 选择器与盒模型

### 1) 选择器核心（`p.32`）
- `#jumble`：匹配 `id="jumble"`
- `.jumble`：匹配 `class="jumble"`
- 空格：后代选择器（任意层级）
- `>`：子选择器（仅直接子元素）

### 2) Q7 简答思路 + 答案（`tb2 Q7`）
**题目要点**
- 目标是：选中“`id="jumble"` 的 `span` 内部（后代）的 `div`”。

**思路（2步）**
1. `id='jumble'` 必须用 `#jumble`，不是 `.jumble`。
2. 题目写的是 descendant（后代），要用空格，不是 `>`。

**答案**
- 正确选项是 **D. `span#jumble div`**。

**更多应用例子（可直接套用）**
- `span#jumble div`  
  简短说明：选中 `span id="jumble"` 里面所有层级的 `div`（后代）。

- `span#jumble > div`  
  简短说明：只选中直接子元素 `div`，孙元素不选。

- `#jumble div.note`  
  简短说明：在 `id="jumble"` 区域内，只选 class 为 `note` 的 `div`。

- `#jumble p strong`  
  简短说明：选中 `#jumble` 内所有 `p` 里的 `strong`（多层后代链）。

- `#jumble + div`  
  简短说明：选中紧挨在 `id="jumble"` 元素后面的第一个同级 `div`（不是内部后代）。

- `#jumble ~ div`  
  简短说明：选中 `id="jumble"` 后面所有同级 `div`（允许中间隔其他元素）。

### 3) 组合器速记（`p.33`）
- 后代选择器：`A B`
- 子选择器：`A > B`
- 相邻兄弟：`A + B`（紧挨着）
- 通用兄弟：`A ~ B`（后续同级）

### 4) 典型题：`form+button, .stray`
- 逗号 `,` 表示“选择器列表”，两边独立生效。
- `form+button` 表示“紧跟在 `form` 后面的 `button`”，不是 form 内部的 button。
- `.stray` 匹配所有 class 为 stray 的元素。

### 5) Box Model / Margin（`p.40`）
- inline 与 block 的行为差异是常考点。
- `margin collapse` 关注“垂直相邻外边距合并”。

### 6) Media Query 做题流程（`p.40`）
1. 先判定媒体类型：`screen` 还是 `print`
2. 过滤不匹配的 media 条件（宽度、设备等）
3. 再看选择器优先级与继承
4. 最后判断最终样式（常见是颜色）

---

## Week 04 - CSS 布局进阶

### 1) Grid Layout（`p.50`）
- 自动放置（auto-placement）沿文档书写方向推进（通常左到右、上到下）。
- 常见错误：误以为新项总放同一格，或忽略 writing mode。

---

## Week 05 - JavaScript 基础

### 1) 字符串拼接陷阱（`p.56`）
- 字符串与数字用 `+` 时，会发生字符串拼接。
- 例如：`14 + "5"` 结果是 `"145"`，不是 `19`。

---

## Week 07 - 异步 JavaScript

### 1) `Promise.all([...]).then(handler)`（`p.67`）
- 只有当所有 Promise 都 fulfilled，才会调用 `then`（且只调用一次）。
- 任意一个 rejected，整体立即 rejected，`then` 不执行，走 `catch`。

---

## Week 08 - Web Scraping 与输入校验

### 1) `wget` 下载覆盖行为（`p.71`）
- 默认：同名文件可能生成 `.1`, `.2`...
- `-nc`（no-clobber）：已有同名文件则拒绝下载，不覆盖、不生成 `.1`
- `-N`（timestamping）：按时间戳判断是否重下

### 2) 校验放在哪里最安全
- **结论**：必须做 **server-side validation**（服务端校验）。
- 前端校验（HTML/JS）主要用于提升体验，不能作为安全防线。

---

## Week 09 - 密码学 / 证书 / 邮件安全

### 1) 证书链字段阅读
- `s` (subject)：证书属于谁
- `i` (issuer)：谁签发
- `NotAfter`：过期时间

### 2) 为什么“签名 + 加密”邮件
- 加密：保证内容机密性（他人不能读）
- 签名：验证发送者身份，并保证内容未被篡改

---

## Week 10 - RFC 与网络工具

### 1) RFC 与 IETF（`p.90`）
- RFC：互联网标准相关文档体系
- IETF：标准制定的重要组织

---

## Week 11 - Testing（`p.101`）

### 1) 测试复习重点
- 明确测试目标：找 bug、覆盖边界、验证性质
- 区分常见方法：示例测试、随机输入、性质测试等

---

## 考前速记（超短版）

- `fetch` 收到 404 仍是 fulfilled；网络失败才 rejected。  
- `Promise.all`：全 fulfilled 才 then；有一个 rejected 就走 catch。  
- CSS 选择器先看符号：空格（后代）、`>`（子代）、`+`（相邻兄弟）、`~`（通用兄弟）。  
- 安全校验必须在服务端。  
- 状态码先看首位：2 成功、3 重定向、4 客户端错、5 服务端错。  

---

## 必备知识笔记（不依赖原题）

### HTTP / 网络基础
- HTTP 是应用层协议，典型请求-响应模型，且是 stateless（无状态）。
- 常见协议栈顺序：`HTTP -> TLS -> TCP -> IP`。
- OSI 对应：HTTP 在应用层，TCP 在传输层，IP 在网络层。
- HTTP 报文基本结构：`start-line + headers + 空行 + body`（body 可为空）。
- `HEAD` 返回头部元数据，不返回消息体。
- `GET` 通常只读；`POST` 常用于提交数据；`PUT/DELETE` 通常讨论幂等性。

### URI / Request Target
- URI 常拆为：`scheme://host/path?query`。
- 默认大小写规则：`scheme`、`host` 不敏感；`path` 不应默认不敏感。
- request-line 形式：`METHOD request-target HTTP/version`。
- `request-target` 核心是 `path (+ query)`，用于定位资源与筛选参数。

### 状态码与响应语义
- 先看首位判大类：`1xx/2xx/3xx/4xx/5xx`。
- `2xx` 是成功类，`204` 也是成功（只是无内容）。
- `4xx` 偏客户端问题（如请求格式、资源不存在）。
- `5xx` 偏服务端故障。
- 状态码 + 头部字段一起读，语义更完整（如重定向常配 `Location`）。

### Headers 常用判断
- `Host`：目标主机。
- `User-Agent`：客户端环境线索（但不能过度推断）。
- `Accept` / `Accept-Language` / `Accept-Encoding`：客户端可接受格式、语言、压缩。
- `Content-Type`：消息体类型；`Content-Length`：消息体字节数。
- `Connection: keep-alive`：倾向复用连接，不等于“多客户端并发”。

### HTML / CSS
- HTML 复习重点是“语义”而非视觉表现（如 `h1` 的语义作用）。
- 选择器高频：`#id`、`.class`、后代空格、子代 `>`、相邻兄弟 `+`、通用兄弟 `~`。
- inline / block 行为差异与 box model 是基础必考。
- `margin collapse` 主要发生在垂直相邻块级元素。
- media query 先判媒体类型（screen/print），再判条件，再看层叠与继承。
- Grid auto-placement 默认按书写方向放置（通常左到右、上到下）。

### JavaScript / 异步
- `+` 在字符串参与时可能触发拼接，先确认类型再算结果。
- `let` 不能在同一作用域重复声明。
- `fetch`：收到 HTTP 响应（即使 404/500）通常 fulfilled；网络失败才 rejected。
- `Promise.all`：全部 fulfilled 才进入 `then`；任一 rejected 则整体 rejected。

### Scraping / 安全 / 测试
- `wget -nc`：已有同名文件不覆盖且不重下；`-N` 按时间戳比较。
- 客户端校验主要提升体验，安全性必须由服务端校验兜底。
- 证书链看三项：`subject`、`issuer`、`NotAfter`。
- 邮件“加密+签名”分别对应机密性与身份/完整性验证。
- Testing 重点：边界条件、随机输入、性质测试（property-based）思维。
