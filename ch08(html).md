
##虚拟dom转换
```html
<body>
    <div id="virtual-dom" b='123'>
        <p>Virtual DOM</p>
        <ul id="list">
            <li class="item">Item 1</li>
            <li class="item">Item 2</li>
            <li class="item">Item 3</li>
        </ul>
        <div class="test">Hello World</div>
    </div>
    <div id="app"></div>
</body>
<script>
    // 解析dom节点为虚拟dom
    let dom = document.querySelector('#virtual-dom')
    function Element(dom) {
        let domObj = {};
        // console.log(dom.nodeName)
        domObj.el = dom.nodeName.toLowerCase();
        domObj.attrs = {}
        let attrs = [];
        let attrKeysArr = Object.keys(dom.attributes);

        if (!dom.children.length) {
            domObj.value = dom.innerText;
        }
        // debugger
        attrKeysArr.forEach((attrKey) => {
            domObj.attrs[dom.attributes[attrKey].name] = dom.attributes[attrKey].value;
        })
        let childDomArr = [];
        if (dom.children.length > 0) {
            for (let i = 0; i < dom.children.length; i++) {
                childDomArr.push(Element(dom.children[i]))
                // Element(dom.children[i])
            }
            domObj.childs = childDomArr;
            return domObj
        }
        else {
            return domObj
            // console.log(dom.nodeName)
        }

    }
    console.log(Element(dom))
    let shaowDom = Element(dom)
    // 将虚拟dom转为dom
    function render(dom) {
        let el = document.createElement(dom.el);//拿到元素类型
        el.innerText = dom.value;
        // debugger
        dom.value?el.innerText = dom.value:el.innerText = null;
        if( dom.value){
            console.log(123)
        }
        let attrs = dom.attrs;//元素属性
        // debugger
        let attrsKeyArr = Object.keys(attrs);
        attrsKeyArr.forEach((attrKey) => {
            el.setAttribute(attrKey, dom.attrs[attrKey])
        })
        if (dom.childs) {
            dom.childs.forEach((child) => {
                el.appendChild(render(child));
            })
            return el;
        } else {
            return el;
        }
    }

    document.querySelector('#app').appendChild(render(shaowDom))
</script>
```
