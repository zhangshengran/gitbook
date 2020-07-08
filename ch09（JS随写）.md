
##发布订阅模型

总的设计模式为初始化一数据结构，数组或者对象都可以，然后监听addListener的时候将事件和回调Fn组成KV存进去。然后等触发事件emit的时候依据事件名从数组或者对象中取出Fn并执行。
```js

class EventEmeitter{
    constructor(){
        this.events = {};
    }

    addEventLister(eventName,Fn){
        this.events[eventName] = Fn;
    }
    emit(eventName,...args){
        this.events[eventName]? this.events[eventName](...args):false
    }

    removeEventLister(eventName){
     
        delete this.events[eventName]
    }
}
```

如果有多个监听者，每个事件列表对应一个数组往里面push Fn