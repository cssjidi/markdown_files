<p>那么，组合框（combobox）、多选下拉框（multiselect）、列表框（listbox）和下拉菜单（dropdown）之间有何区别？尽管这些 UI 组件外观相似，但其用途各不相同。选择哪种组件通常取决于<strong>可选项数量</strong>及其是否默认可见。</p>
<p>我们来逐一了解它们的区别、<strong>各自用途</strong>，以及如何选择合适组件——避免误解和错误预期。</p>
<p><img src="https://files.smashing.media/articles/combobox-vs-multiselect-vs-listbox/1-combobox-vs-multiselect-vs-listbox.jpg" /></p>
并非所有列表模式都相同
<p>上述所有 UI 组件有一个共同点：均支持用户与列表交互。但其实现方式略有不同。</p>
<p>我们逐个来看：</p>
<ul>
<li><strong>下拉菜单（Dropdown）</strong> → 列表默认隐藏，仅在触发后显示。</li>
<li><strong>组合框（Combobox）</strong> → 支持输入过滤 + 单选。</li>
<li><strong>多选下拉框（Multiselect）</strong> → 支持输入过滤 + 多选。</li>
<li><strong>列表框（Listbox）</strong> → 所有列表项默认全部可见（支持滚动）。</li>
<li><strong>双列表框（Dual listbox）</strong> → 在两个列表框之间移动项目。</li>
</ul>
<p><img src="https://files.smashing.media/articles/combobox-vs-multiselect-vs-listbox/2-watson-design-system.jpg" /></p>
<p>换言之，<em>组合框（Combobox）</em>将文本输入框与下拉列表结合，使用户能够<strong>输入过滤</strong>并选择单个选项；而<em>多选下拉框（Multiselect）</em>则允许用户选择多个选项（通常以标签或芯片形式展示）。</p>
<p><em>列表框（Listbox）</em>默认<strong>完整显示所有列表项</strong>（常带滚动条），适用于用户需立即查看全部可选项的场景。<em>双列表框（Dual listbox）</em>（亦称<em>转移列表（transfer list）</em>）是列表框的一种变体，支持用户<strong>在两个列表框之间移动项目</strong>（左 ↔ 右），常用于批量选择。</p>
切勿隐藏常用选项
<p>如前所述，正确 UI 组件的选择取决于<strong>两个因素</strong>：列表选项数量，以及是否需要默认显示全部选项。所有列表还可支持树形结构、嵌套及分组选择。</p>
<p><img src="https://files.smashing.media/articles/combobox-vs-multiselect-vs-listbox/3-nongodb-design-system.jpg" /></p>
<p>我多年来一直遵循一个 UI 组件设计原则：<strong>切勿隐藏常用选项</strong>。若某选项被用户频繁使用，则将其隐藏毫无价值。</p>
<p>我们可将其设置为<strong>预选中</strong>，或（当仅有 2–3 个高频选项时）以<a href="https://smart-interface-design-patterns.com/articles/badges-chips-tags-pills/"><strong>标签或按钮</strong></a>形式直接展示，其余选项则在用户交互后展开。通常，始终展示热门选项是良好实践——即便可能略微增加界面复杂度。</p>
如何选择合适的组件？
<p>并非所有列表都需要复杂的选取方式。对于<strong>少于 5 项</strong>的列表，简单的单选按钮或复选框通常效果最佳。但若用户需从<strong>大量选项</strong>（例如 200+ 项）中选取（如国家选择），组合框或多选下拉框因其快速过滤能力而更具优势。</p>
<p><img src="https://files.smashing.media/articles/combobox-vs-multiselect-vs-listbox/4-matrix-options-multiselect-listboxes.jpg" /></p>
<p><strong>列表框（Listbox）</strong>适用于用户需同时访问<strong>大量选项</strong>的场景，尤其适合需从中选取多项的用例，也常用于高频使用的筛选器。</p>
<p><img src="https://files.smashing.media/articles/combobox-vs-multiselect-vs-listbox/5-dual-list-box.png" /></p>
<p><strong>双列表框（Dual listbox）</strong>常被忽视或忽略，但在处理复杂任务（如批量选择、角色分配、任务指派或职责划分）时极为有用。它是唯一一种允许用户在提交前，将完整已选列表与源列表并排对比的 UI 组件（亦称<em>“转移列表（Transfer list）”</em>）。</p>
<p>事实上，双列表框在速度、准确性和可访问性方面通常优于<a href="https://smart-interface-design-patterns.com/articles/drag-and-drop-ux/">拖放（drag-and-drop）</a>。</p>
可用性考量
<p>需特别注意：所有列表类型均需支持<strong>键盘导航</strong>（如 ↑/↓ 方向键），以确保可访问性。部分用户一旦开始输入，几乎总会依赖键盘选取选项。</p>
<p><img src="https://files.smashing.media/articles/combobox-vs-multiselect-vs-listbox/7-keyboard-navigation.png" /></p>
<p>此外：</p>
<ul>
<li>对于<strong>7 项以上</strong>的列表，建议添加“全选”和“清除全部”功能，以简化用户操作。</li>
<li>对于含组合框的长列表，应在点击/触摸时<strong>向用户完整展示所有选项</strong>，否则这些选项可能永远无法被发现。</li>
<li>最重要的是，<strong>切勿将非交互元素显示为按钮</strong>以免造成混淆，也不应将交互元素显示为静态标签。</li>
</ul>
总结：并非所有列表都是下拉菜单
<p>命名至关重要。<strong>垂直排列的选项列表</strong>通常被称为“下拉菜单（dropdown）”，但该术语往往过于笼统而缺乏实际意义。<em>“下拉菜单（Dropdown）”</em>暗示列表默认隐藏；<em>“多选下拉框（Multiselect）”</em>表示列表内支持多选（复选框）；<em>“组合框（Combobox）”</em>表示支持文本输入；而“列表框（Listbox）”仅指始终可见的可选项目列表。</p>
<p>目标并非机械地统一上述定义，而是<strong>对齐设计意图</strong>——在决策、设计、开发及使用这些 UI 组件时，使用一致的语言。</p>
<p>它<strong>必须适用于所有人</strong>——设计师、工程师和终端用户——只要静态标签不呈现为可交互按钮，且单选按钮不表现为复选框即可。</p>
欢迎了解《AI 界面设计模式》
<p>欢迎了解<a href="https://ai-design-patterns.com/"><strong>《AI 界面设计模式》</strong></a>——Vitaly 的全新<strong>视频课程</strong>，包含来自真实产品的实用案例，并即将举办<a href="https://smashingconf.com/online-workshops/workshops/ai-interfaces-vitaly-friedman/">现场 UX 培训</a>。<a href="https://www.youtube.com/watch?v=jhZ3el3n-u0">立即观看免费预览</a>。</p>
<p></p><a href="https://ai-design-patterns.com/"><img src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://files.smashing.media/articles/product-designer-career-paths/design-patterns-ai-interfaces.png" /></a>欢迎了解<a href="https://ai-design-patterns.com/">《AI 界面设计模式》</a>——Vitaly 关于界面设计与用户体验的视频课程。<p></p>
<div><div><ul><li><a href="#">
视频课程 + UX 培训</a></li><li><a href="#">仅视频课程</a></li></ul><div><h3>视频课程 + UX 培训</h3>$ 450.00 $ 799.00
<a href="https://smart-interface-design-patterns.thinkific.com/enroll/3476562?price_id=4401578">
获取视频课程 + UX 培训<div></div></a><p>30 节视频课（10 小时）+ <a href="https://smashingconf.com/online-workshops/workshops/ai-interfaces-vitaly-friedman/">现场 UX 培训</a>。<br />100 天无理由退款保障。</p></div><div><h3>仅视频课程</h3><div>$ 275.00$ 395.00</div>
<a href="https://smart-interface-design-patterns.thinkific.com/enroll/3476562?price_id=4397456">
获取视频课程<div></div></a><p>30 节视频课（10 小时）。每年更新。<br />亦可作为<a href="https://smart-interface-design-patterns.thinkific.com/enroll/3570306?price_id=4503439">UX 套装（含 3 门视频课程）</a>购买。</p></div></div></div>

实用资源
<ul>
<li><a href="https://smart-interface-design-patterns.com/articles/autocomplete-ux/">自动补全：UX 指南</a>，作者：Vitaly Friedman</li>
<li><a href="https://playbook.ebay.com/design-system/components/combobox">组合框（Combobox）</a>，eBay 👍</li>
<li><a href="https://eui.elastic.co/docs/components/forms/selection/combo-box/">组合框（Combobox）</a>，Elastic</li>
<li><a href="https://designsystem.elisa.fi/9b207b2c3/p/082dd3-combobox">组合框（Combobox）</a>，Elisa</li>
<li><a href="https://www.mongodb.design/component/combobox/live-example">组合框（Combobox）</a>，MongoDB 👍</li>
<li><a href="https://design.visa.com/components/combobox/">组合框（Combobox）</a>，Visa 👍</li>
<li><a href="https://watson.docplanner.design/latest/watson-web/components/combobox/usage-guidelines-L68K6G51">组合框（Combobox）</a>，Watson（Docplanner）</li>
<li><a href="https://doc.wikimedia.org/codex/latest/components/demos/combobox.html">组合框（Combobox）</a>，Wikimedia</li>
<li><a href="https://garden.zendesk.com/components/combobox">组合框（Combobox）</a>，Zendesk</li>
<li><a href="https://www.mongodb.design/component/combobox/design-docs">多选下拉框（MongoDB 组合框设计文档）</a>，MongoDB 👍</li>
<li><a href="https://doc.wikimedia.org/codex/latest/components/demos/multiselect-lookup.html">多选查找（Multiselect Lookup）</a>，Wikimedia</li>
<li><a href="https://vaadin.com/docs/latest/components/multi-select-combo-box">多选组合框（Multi-select Combo Box）</a>，Vaadin</li>
<li><a href="https://design.visa.com/components/multiselect/">多选下拉框（Multiselect）</a>，Visa</li>
<li><a href="https://ant.design/components/transfer">转移组件（Listbox 示例）</a>，Ant Design</li>
<li><a href="https://hopper.workleap.design/components/Listbox">列表框（Listbox）</a>，Hopper</li>
<li><a href="https://vaadin.com/docs/latest/components/list-box">列表框（List Box）</a>，Vaadin</li>
<li><a href="https://design.visa.com/components/listbox/">列表框（Listbox）</a>，Visa</li>
<li><a href="https://www.patternfly.org/components/dual-list-selector">双列表选择器（Dual List Selector）</a>，Red Hat（PatternFly）</li>
<li><a href="https://www.lightningdesignsystem.com/2e1ef8501/p/763763-dual-listbox">双列表框（Dual Listbox）</a>，Salesforce（Lightning 设计系统）</li>
<li><a href="https://v5.mantine.dev/core/transfer-list/">转移列表（Transfer List）</a>，Mantine</li>
<li><a href="https://dashlite.net/demo1/components/misc/dual-listbox.html">双列表框（Dual Listbox）</a>，Dashlite</li>
<li><a href="https://smart-interface-design-patterns.com/articles/badges-chips-tags-pills/">徽章 vs. 标签 vs. 芯片 vs. 标记</a>，作者：Vitaly Friedman</li>
<li><a href="https://www.nngroup.com/articles/listbox-dropdown/">列表框 vs. 下拉列表</a>，作者：Anna Kaley（NN/g）</li>
</ul>
