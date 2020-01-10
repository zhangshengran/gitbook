
##虚拟dom转换
```js
<body>
    <div id="virtual-dom" b='123'>
        <p>Virtual DOM</p>
        <ul id="list">
            <li class="item">Item 1</li>
            <li class="item">Item 2</li>
            <li class="item">Item 3</li>
        </ul>
        <div class="test">Hello World</div>
        333
    </div>
    <div id="app"></div>
</body>
<script>
    // 解析dom节点为虚拟dom
    let dom = document.querySelector('#virtual-dom')
    function Element(dom) {
        if (dom.nodeType == 3) {//如果是文本节点
            return dom.textContent
        } else {//正常dom节点
            let domObj = {};

            domObj.el = dom.nodeName.toLowerCase();//dom名称转小写
            domObj.attrs = {}
            let attrs = [];
            let attrKeysArr = Object.keys(dom.attributes);//拿属性id class之类的
            attrKeysArr.forEach((attrKey) => {
                domObj.attrs[dom.attributes[attrKey].name] = dom.attributes[attrKey].value;
            })

            let childDomArr = [];
            let childNodes = dom.childNodes;

            for (let i = 0; i < childNodes.length; i++) {

                childDomArr.push(Element(dom.childNodes[i]))

            }

            domObj.childNodes = childDomArr;

            return domObj

        }
    }
    console.log(Element(dom))
    let shaowDom = Element(dom)
    // 将虚拟dom转为dom
    function render(dom) {
        if (typeof dom === 'string') {//如果传进来的是文本节点，直接创建文本节点并返回
            return document.createTextNode(dom)
        } else {//传入的为dom节点，构建dom节点
            let el = document.createElement(dom.el);//拿到元素类型
            let attrs = dom.attrs;//元素属性
            let attrsKeyArr = Object.keys(attrs);
            attrsKeyArr.forEach((attrKey) => {
                el.setAttribute(attrKey, dom.attrs[attrKey])
            })
            if (dom.childNodes) {
                dom.childNodes.forEach((child) => {
                    el.appendChild(render(child));
                })
                return el;
            } else {
                return el;
            }
        }
    }

    document.querySelector('#app').appendChild(render(shaowDom))
</script>


```