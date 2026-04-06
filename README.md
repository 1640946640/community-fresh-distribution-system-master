<h1 align="center">社区生鲜配送系统</h1>

<p align="center">一个基于 Spring Boot 3 + Vue 3 的前后端分离社区生鲜配送项目，覆盖用户端下单与管理端运营两类场景。</p>

<p align="center">
  <a href="#项目简介">项目简介</a> ·
  <a href="#核心功能">核心功能</a> ·
  <a href="#技术栈">技术栈</a> ·
  <a href="#项目结构">项目结构</a> ·
  <a href="#快速启动">快速启动</a>
</p>

<h2 id="项目简介">项目简介</h2>

<p>本项目面向社区生鲜配送业务，采用前后端分离架构实现商品展示、购物车、订单处理、收货地址、社区交流、公告管理、轮播图管理与后台运营等功能。系统同时提供普通用户端和管理员端，两类角色共用一套后端服务与数据库。</p>

<ul>
  <li>用户端：登录注册、浏览商品、加入购物车、提交订单、管理地址、查看公告、参与社区交流</li>
  <li>管理端：商品管理、分类管理、订单管理、用户管理、公告管理、轮播图管理、配送地址管理</li>
  <li>服务端：JWT 鉴权、Redis 会话校验、MyBatis-Plus 数据访问、文件上传下载</li>
</ul>

<h2 id="核心功能">核心功能</h2>

<h3>用户端</h3>
<ul>
  <li>账号登录、注册、找回密码、个人资料维护</li>
  <li>生鲜商品分类浏览、关键字搜索与推荐展示</li>
  <li>购物车管理、订单创建、订单明细查看</li>
  <li>收货地址维护、社区交流、公告资讯查看</li>
</ul>

<h3>管理端</h3>
<ul>
  <li>首页数据统计与销量可视化</li>
  <li>生鲜商品与分类维护</li>
  <li>订单状态处理与配送地址维护</li>
  <li>用户、公告、社区交流内容、轮播图统一管理</li>
</ul>

<h2 id="技术栈">技术栈</h2>

<table>
  <thead>
    <tr>
      <th>层次</th>
      <th>技术</th>
      <th>说明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>后端</td>
      <td>Java 21、Spring Boot 3.3.4</td>
      <td>提供 REST 接口、参数校验、统一异常处理</td>
    </tr>
    <tr>
      <td>数据访问</td>
      <td>MyBatis-Plus、PageHelper、MySQL 8、Druid</td>
      <td>完成分页查询、乐观锁、逻辑删除等能力</td>
    </tr>
    <tr>
      <td>缓存鉴权</td>
      <td>Redis、JWT</td>
      <td>登录后生成 Token，并结合 Redis 做会话校验</td>
    </tr>
    <tr>
      <td>前端</td>
      <td>Vue 3、Vite 5、Vue Router 4、Pinia</td>
      <td>构建单页应用，区分用户端与管理端路由</td>
    </tr>
    <tr>
      <td>界面</td>
      <td>Element Plus、ECharts、md-editor-v3、Sass</td>
      <td>完成后台管理界面、图表展示和富文本编辑</td>
    </tr>
  </tbody>
</table>

<h2 id="项目结构">项目结构</h2>

<pre><code>Community-fresh-distribution-system-master
├─ README.md
├─ .gitignore
├─ pom.xml
├─ fresh_system.sql
├─ fresh-system-project（back-end-code）
│  ├─ pom.xml
│  ├─ src/main/java/com/orion
│  ├─ src/main/resources
│  └─ pictures
└─ fresh-system-project（front-end-code）
   ├─ package.json
   ├─ src
   └─ public
</code></pre>

<ul>
  <li><code>fresh-system-project（back-end-code）</code>：Spring Boot 后端工程，负责业务接口、鉴权、文件上传与数据库访问</li>
  <li><code>fresh-system-project（front-end-code）</code>：Vue 3 前端工程，包含用户端与管理端页面</li>
  <li><code>fresh_system.sql</code>：数据库初始化脚本，包含核心业务表结构</li>
  <li><code>pictures</code>：后端运行时上传目录，建议仅保留本地，不纳入代码仓库</li>
</ul>

<h2 id="业务流程">业务流程</h2>

<ol>
  <li>用户注册或登录后，前端将 Token 写入本地存储，并在请求头中携带 <code>Authorization</code></li>
  <li>后端拦截器校验 JWT 与 Redis 中的登录状态，通过后访问业务接口</li>
  <li>用户浏览商品、加入购物车、提交订单，系统写入订单与订单明细数据</li>
  <li>管理员在管理端处理商品、公告、轮播图、用户与订单信息</li>
  <li>商品图片、用户头像与轮播图文件通过后端接口上传，并保存到本地目录</li>
</ol>

<h2 id="环境要求">环境要求</h2>

<ul>
  <li>JDK 21</li>
  <li>Maven 3.9+</li>
  <li>Node.js 18+</li>
  <li>MySQL 8.x</li>
  <li>Redis 6.x 及以上，或兼容版本</li>
</ul>

<p>当前后端默认配置使用 <code>127.0.0.1:1252</code> 连接 MySQL，使用 <code>localhost:6379</code> 连接 Redis；启动前请根据本地环境修改后端配置文件。</p>

<h2 id="快速启动">快速启动</h2>

<h3>1. 初始化数据库</h3>
<ol>
  <li>创建数据库 <code>fresh_system</code></li>
  <li>执行根目录下的 <code>fresh_system.sql</code> 脚本导入表结构和演示数据</li>
</ol>

<h3>2. 配置后端</h3>
<p>打开后端配置文件 <code>fresh-system-project（back-end-code）/src/main/resources/application.yaml</code>，修改数据库、Redis、文件上传等本地配置。</p>

<h3>3. 启动 Redis</h3>
<p>可使用本机 Redis 服务，也可自行替换为其他可用实例。若本地没有 Redis，请先准备好对应运行环境。</p>

<h3>4. 启动后端</h3>
<pre><code>cd fresh-system-project（back-end-code）
mvn spring-boot:run
</code></pre>

<p>后端默认访问地址：<code>http://localhost:8080</code></p>

<h3>5. 启动前端</h3>
<pre><code>cd fresh-system-project（front-end-code）
npm install
npm run dev
</code></pre>

<p>前端开发服务启动后，按照 Vite 控制台输出地址访问即可。</p>

<h2 id="鉴权说明">鉴权说明</h2>

<ul>
  <li>登录成功后，后端签发 JWT，并将登录状态写入 Redis</li>
  <li>除登录、注册、找回密码和部分文件下载接口外，其余接口均受拦截器保护</li>
  <li>前端统一使用 Axios 请求封装，在请求头中追加 Token</li>
</ul>

<h2 id="数据库说明">数据库说明</h2>

<p>项目核心包含以下业务表：</p>

<p><code>address</code>、<code>cart</code>、<code>category</code>、<code>communication</code>、<code>fresh</code>、<code>notice</code>、<code>order</code>、<code>order_detail</code>、<code>slideshow</code>、<code>user</code>、<code>user_address</code></p>

<p>整体建模围绕“用户 - 地址 - 购物车 - 订单 - 商品”业务链路展开，同时补充公告、社区交流和轮播图等运营内容模块。</p>

<h2 id="文件上传说明">文件上传说明</h2>

<ul>
  <li>商品图、头像、轮播图文件由后端接口统一处理</li>
  <li>上传文件默认保存到后端工程本地目录，适合开发环境演示</li>
  <li>开源发布时建议忽略运行时图片目录，避免将本地测试资源直接提交到仓库</li>
</ul>

<h2 id="注意事项">注意事项</h2>

<ul>
  <li>前端请求默认直连 <code>http://localhost:8080</code>，当前未配置 Vite 代理</li>
  <li>如需部署到服务器，建议进一步拆分环境配置并重构文件存储方式</li>
  <li>仓库适合作为课程设计、毕业设计、实训项目或前后端分离练习案例</li>
</ul>

<h2 id="开源说明">开源说明</h2>

<p>本仓库适合以学习与交流为目的进行二次开发。发布到公开平台时，建议移除本地运行产物、临时文件、测试图片、演示视频与说明书文档，仅保留源码、配置示例与数据库脚本。</p>