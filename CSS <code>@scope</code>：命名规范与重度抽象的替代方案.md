<p>学习基础 CSS 原理时，人们通常被教导要编写模块化、可复用且语义清晰的样式，以确保可维护性。但当开发者投入真实项目开发时，往往感觉在不造成样式泄漏至非预期区域的前提下添加 UI 功能几乎不可能。</p>
<p>这一问题常演变为一种自我实现的循环：理论上仅作用于某个元素或类的样式，却开始出现在本不该出现的位置。这迫使开发者创建更具体的选择器来覆盖泄漏的样式，而这些新选择器又意外覆盖了全局样式，如此往复。</p>
<p>严格的类名规范（例如 <a href="https://getbem.com/introduction/">BEM</a>）是解决该问题的一种理论方案。<strong>BEM（块、元素、修饰符）方法论</strong>是一种<a href="https://www.smashingmagazine.com/2012/04/a-new-front-end-methodology-bem/">系统化的 CSS 类命名方式</a>，旨在保障 CSS 文件内的可复用性与结构。此类命名规范可<a href="https://www.smashingmagazine.com/2018/06/bem-for-beginners/">通过利用领域语言描述元素及其状态来降低认知负担</a>；若正确实施，<a href="https://www.smashingmagazine.com/2025/06/css-cascade-layers-bem-utility-classes-specificity-control/">还可使大型应用的样式更易于维护</a>。</p>
<p>然而在现实中，情况并非总如理论所示。优先级可能变化，随之而来的是实现的一致性下降。HTML 结构的微小调整可能要求大量修订 CSS 类名。对于高度交互的前端应用，遵循 BEM 模式的类名可能变得冗长且难以管理（例如：<code>app-user-overview__status--is-authenticating</code>），而未能完全遵守命名规则则会破坏整个系统的结构性，从而抵消其优势。</p>
<p>鉴于上述挑战，开发者转向各类框架也就不足为奇，其中 Tailwind 是<a href="https://2024.stateofcss.com/en-US/tools/">最受欢迎的 CSS 框架</a>。与其在样式间看似无法取胜的特异性战争中苦苦挣扎，不如放弃<a href="https://css-tricks.com/the-c-in-css-the-cascade/">CSS 层叠机制</a>，转而使用能保证样式完全隔离的工具。</p>
开发者更依赖工具类
<p>我们如何得知部分开发者热衷于避免层叠样式？答案在于“现代”前端工具链的兴起——例如<a href="https://www.smashingmagazine.com/2016/04/finally-css-javascript-meet-cssx/">CSS-in-JS 框架</a>——它们正是为此目的而设计。对特定组件紧密作用的隔离样式，仿佛令人耳目一新。它消除了命名需求——<a href="https://24ways.org/2014/naming-things/">这仍是前端开发中最令人厌恶且耗时的任务之一</a>——并允许开发者无需深入理解或充分利用 CSS 继承优势即可高效产出。</p>
<p>但放弃 CSS 层叠机制也带来自身问题。例如，在 JavaScript 中组合样式需要复杂的构建配置，并常常导致样式与组件标记或 HTML 混杂在一起。我们不再精心设计命名规范，而是交由构建工具自动生成选择器和标识符（例如：<code>.jsx-3130221066</code>），这迫使开发者额外掌握一门伪语言。（更何况，理解组件中所有 <code>useEffect</code> 的行为本身已带来巨大认知负荷！）</p>
<p>将类命名工作进一步抽象至工具层面，意味着基本调试往往受限于专为开发编译的应用版本，而非利用浏览器原生支持实时调试的功能（例如开发者工具）。</p>
<p>这几乎等同于我们需要开发专门用于调试“用于抽象 Web 原生能力的工具”的工具——全为逃避编写标准 CSS 所谓的“痛苦”。</p>
<p>幸运的是，现代 CSS 特性不仅使标准 CSS 编写更加灵活，还赋予我们更强的能力去管理层叠机制，使其真正为我们所用。<a href="https://www.smashingmagazine.com/2022/01/introduction-css-cascade-layers/">CSS 层叠层（Cascade Layers）</a>便是一个绝佳示例，但另一项特性却出人意料地长期缺乏关注——尽管随着其最近达成<strong>Baseline 兼容性</strong>，这一状况正在改变。</p>
CSS <code>@scope</code> 规则
<p>我认为<strong>CSS <code>@scope</code> 规则</strong>有望治愈前述因样式泄漏引发的焦虑，且无需为抽象化和额外构建工具而牺牲 Web 原生优势。</p>
<blockquote>“<code>@scope</code> CSS 规则使你能在特定 DOM 子树中选择元素，精准定位目标元素，无须编写难以覆盖的过度具体选择器，也无需将选择器与 DOM 结构过度耦合。”<br /><br />— <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/@scope">MDN</a></blockquote>

<p>换言之，我们可在特定场景下使用隔离样式，<strong>同时不牺牲继承性、层叠性，甚至不违背前端开发长期以来坚持的关注点分离原则</strong>。</p>
<p>此外，它拥有<a href="https://caniuse.com/css-cascade-scope">出色的浏览器兼容性</a>。事实上，<a href="https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/146">Firefox 146</a> 已于 12 月加入对 <code>@scope</code> 的支持，使其首次成为<a href="https://developer.mozilla.org/en-US/docs/Glossary/Baseline/Compatibility">Baseline 兼容特性</a>。以下是对采用 BEM 模式按钮与 <code>@scope</code> 规则的简单对比：</p>
<pre><code>&lt;!-- BEM --&gt; 
&lt;button class="button button--primary"&gt;
  &lt;span class="button__text"&gt;点击我&lt;/span&gt;
  &lt;span class="button__icon"&gt;→&lt;/span&gt;
&lt;/button&gt;

&lt;style&gt;
  .button .button__text { /* 按钮文字样式 */ }
  .button .button__icon { /* 按钮图标样式 */ }
  .button--primary { /* 主按钮样式 */ }
&lt;/style&gt;
</code></pre>

<pre><code>&lt;!-- @scope --&gt; 
&lt;button class="primary-button"&gt;
  &lt;span&gt;点击我&lt;/span&gt;
  &lt;span&gt;→&lt;/span&gt;
&lt;/button&gt;

&lt;style&gt;
  @scope (.primary-button) {
    span:first-child { /* 按钮文字样式 */ }
    span:last-child { /* 按钮图标样式 */ }
  }
&lt;/style&gt;
</code></pre>

<p><code>@scope</code> 规则实现了<strong>更高精度与更低复杂度的统一</strong>。开发者不再需要借助类名建立边界，从而得以基于原生 HTML 元素编写选择器，彻底消除对规定性 CSS 类名模式的需求。仅通过移除类名管理这一环节，<code>@scope</code> 即可缓解大型项目中与 CSS 相关的恐惧感。</p>
基础用法
<p>入门只需在 CSS 中添加 <code>@scope</code> 规则，并指定一个根选择器作为样式的限定范围：</p>
<pre><code>@scope (&lt;selector&gt;) {
  /* 限定于 &lt;selector&gt; 的样式 */
}
</code></pre>

<p>例如，若需将样式限定于 <code>&lt;nav&gt;</code> 元素，则可能如下所示：</p>
<div>
<pre><code>@scope (nav) {
  a { /* 导航内链接样式 */ }

  a:active { /* 激活链接样式 */ }

  a:active::before { /* 激活链接配合伪元素的额外样式 */ }

  @media (max-width: 768px) {
    a { /* 响应式调整 */ }
  }
}
</code></pre>
</div>

<p>单就这一点而言，该特性并无革命性突破。然而，<code>@scope</code> 还支持传入第二个参数，定义<strong>下界</strong>，从而明确界定作用域的起止位置。</p>
<div>
<pre><code>/* 任何位于 &lt;ul&gt; 内的 &lt;a&gt; 元素均不会应用这些样式 */
@scope (nav) to (ul) {
  a {
    font-size: 14px;
  }
}
</code></pre>
</div>

<p>这种实践称为<strong>环形作用域（donut scoping）</strong>，<a href="https://css-tricks.com/solved-by-css-donuts-scopes/">存在多种实现方式</a>，包括一系列高度具体且紧耦合于 DOM 结构的选择器、<code>:not</code> 伪选择器，或为 <code>&lt;nav&gt;</code> 内的 <code>&lt;a&gt;</code> 元素指定特定类名以处理差异化 CSS。</p>
<p>无论采用其他何种方式，<code>@scope</code> 方法都更为简洁。更重要的是，它规避了因类名变更、误用或 HTML 结构修改而导致样式失效的风险。如今 <code>@scope</code> 已达成 Baseline 兼容性，我们无需再依赖变通方案！</p>
<p>我们还可通过多个结束边界进一步拓展此理念，形成“样式数字八”：</p>
<div>
<pre><code>/* 任何位于 &lt;aside&gt; 或 &lt;nav&gt; 内的 &lt;a&gt; 或 &lt;p&gt; 元素均不会应用这些样式 */
@scope (main) to (aside, nav) {
  a {
    font-size: 14px;
  }
  p {
    line-height: 16px;
    color: darkgrey;
  }
}
</code></pre>
</div>

<p>将其与未使用 <code>@scope</code> 规则的版本对比：后者需将样式“重置”为默认值：</p>
<div>
<pre><code>main a {
  font-size: 14px;
}

main p {
  line-height: 16px;
  color: darkgrey;
}

main aside a,
main nav a {
  font-size: inherit; /* 或其他默认值 */
}

main aside p,
main nav p {
  line-height: inherit; /* 或其他默认值 */
  color: inherit; /* 或指定颜色 */
}
</code></pre>
</div>

<p>请查看以下示例。您是否注意到在精准选取嵌套选择器的同时排除其他元素竟如此简单？</p>
<p>参见 CodePen 上的 <a href="https://codepen.io/smashingmag/pen/wBWXggN">@scope 示例 [forked]</a>，作者：<a href="https://codepen.io/blakeeric">Blake Lundquist</a>。</p>
<p>考虑一种场景：需为<a href="https://www.smashingmagazine.com/2025/07/web-components-working-with-shadow-dom/">Web 组件</a>内插槽内容应用独特样式。当内容插入 Web 组件时，该内容虽属于 Shadow DOM，但仍会继承父文档样式。开发者可能希望根据内容插入的 Web 组件不同，应用不同样式：</p>
<pre><code>&lt;!-- 相同的 &lt;user-card&gt; 内容，不同上下文 --&gt;
&lt;product-showcase&gt;
  &lt;user-card slot="reviewer"&gt;
    &lt;img src="avatar.jpg" slot="avatar"&gt;
    &lt;span slot="name"&gt;Jane Doe&lt;/span&gt;
  &lt;/user-card&gt;
&lt;/product-showcase&gt;

&lt;team-roster&gt;
  &lt;user-card slot="member"&gt;
    &lt;img src="avatar.jpg" slot="avatar"&gt;
    &lt;span slot="name"&gt;Jane Doe&lt;/span&gt;
  &lt;/user-card&gt;
&lt;/team-roster&gt;
</code></pre>

<p>在此例中，开发者可能仅希望当 <code>&lt;user-card&gt;</code> 渲染于 <code>&lt;team-roster&gt;</code> 内部时才应用特定样式：</p>
<pre><code>@scope (team-roster) {
  user-card {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
  }

  user-card img {
    border-radius: 50%;
    width: 40px;
    height: 40px;
  }
}
</code></pre>

更多优势
<p><code>@scope</code> 还可通过其他方式消除对类管理的需求，避免诉诸工具类或 JavaScript 生成的类名。例如，<code>@scope</code> 开启了轻松<strong>针对任意选择器后代元素</strong>的可能性，而不仅限于类名：</p>
<div>
<pre><code>/* 仅包含直接子元素为 button 的 div 元素被纳入根作用域 */
@scope (div:has(&gt; button)) {
  p {
    font-size: 14px;
  }
}
</code></pre>
</div>

<p>并且它们<strong>支持嵌套</strong>，即在作用域内创建新的作用域：</p>
<pre><code>@scope (main) {
  p {
    font-size: 16px;
    color: black;
  }
  @scope (section) {
    p {
      font-size: 14px;
      color: blue;
    }
    @scope (.highlight) {
      p {
        background-color: yellow;
        font-weight: bold;
      }
    }
  }
}
</code></pre>

<p>此外，根作用域可在 <code>@scope</code> 规则内便捷引用：</p>
<div>
<pre><code>/* 应用于 main 的直接子元素 section 内的元素，但在这些 section 的直接子元素 aside 处停止生效 */
@scope (main &gt; section) to (:scope &gt; aside) {
  p {
    background-color: lightblue;
    color: blue;
  }
  /* 应用于根作用域的直接后续兄弟元素 ul */
  :scope + ul {
    list-style: none;
  }
}
</code></pre>
</div>

<p><code>@scope</code> 规则还为 CSS 特异性解析引入了全新的<strong>邻近性（proximity）</strong>维度。在传统 CSS 中，当两个选择器匹配同一元素时，特异性更高的选择器胜出。而使用 <code>@scope</code> 后，当两个选择器特异性相等时，其作用域根节点离匹配元素更近者胜出。这消除了为覆盖父级样式而手动提升元素特异性的需求，因为内部组件样式天然优于外部元素样式。</p>
<div>
<pre><code>&lt;style&gt;
  @scope (.container) {
    .title { color: green; } 
  }
  &lt;!-- &lt;h2&gt; 离 .container 更近，因此 "color: green" 生效。 --&gt;
  @scope (.sidebar) {
    .title { color: red; }
  }
&lt;/style&gt;

&lt;div class="sidebar"&gt;
  &lt;div class="container"&gt;
    &lt;h2 class="title"&gt;你好&lt;/h2&gt;
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>
</div>

结论
<p>以工具类为先的 CSS 框架（如 Tailwind）在原型设计和小型项目中效果显著。然而，在涉及多名开发者的大型项目中，其优势迅速减弱。</p>
<p>过去几年，前端开发日趋复杂化，CSS 也不例外。虽然 <code>@scope</code> 规则并非万能解药，但它可减少对复杂工具链的依赖。当替代或协同战略性类名命名使用时，<code>@scope</code> 能让编写可维护 CSS 变得更轻松、更有趣。</p>
<h3>延伸阅读</h3>
<ul>
<li><a href="https://developer.mozilla.org/en-US/docs/Web/CSS/@scope">CSS <code>@scope</code></a>（MDN）</li>
<li>“<a href="https://css-tricks.com/almanac/rules/s/scope/">CSS <code>@scope</code></a>”，Juan Diego Rodríguez（CSS-Tricks）</li>
<li><a href="https://www.firefox.com/en-US/firefox/146.0/releasenotes/">Firefox 146 发布说明</a>（Firefox）</li>
<li><a href="https://caniuse.com/css-cascade-scope">浏览器兼容性</a>（CanIUse）</li>
<li><a href="https://2024.stateofcss.com/en-US/tools/">主流 CSS 框架</a>（State of CSS 2024）</li>
<li>“<a href="https://css-tricks.com/the-c-in-css-the-cascade/">CSS 中的“C”：层叠（Cascade）</a>”，Thomas Yip（CSS-Tricks）</li>
<li><a href="https://getbem.com/introduction/">BEM 入门</a>（Get BEM）</li>
</ul>
