### Mobx
#### Mobx是? 
> `JavaScript`状态管理库，用来管理状态之间的依赖关系
> `MobX`提供了优化应用状态与`React`组件同步的机制

#### 安装
  `npm install --save mobx mobx-react`

#### 核心概念
  1. state(状态): 状态是驱动应用的数据
  2. observable && @obervable
    * 其值可以是JS基本数据类型、引用类型、普通对象、类实例、数组和映射
    * 其修饰的`state`会暴露出来供观察者使用
    ```javascript
    const map = observable.map({ key: "value"});
    map.set("key", "new value");

    const list = observable([1, 2, 4]);
    list[2] = 3;

    const person = observable({ firstName: "Clive Staples", lastName: "Lewis" });
    person.firstName = "C.S.";
    
    const temperature = observable(20);
    temperature.set(25);
    ```
  3. observer(观察者)：被`observer`修饰的组件，将会根据组件内使用到的被`observable`修饰的`state`的变化而自动重新渲染
    ```javascript
    let FirstTry = observer(({appState}) => {
    return (
      <div className="first-try">
        <h5>Time passed: {appState.timer}</h5>
        <button onClick={appState.resetTimer}>reset timer</button>
      </div>
    )
  })
    ```
  4. action(动作): 只有在`actions`中，才可以修改`Mobx`中`state`的值
    > 注意：当你使用装饰器模式时，`@action`中的`this`没有绑定在当前这个实例上，要用过`@action.bound`来绑定 使得`this`绑定在实例对象上
    ```javascript
    setInterval(
      action(() => {
        appState.timer += 1
      }, 1000)
    )

    @action.bound setName () {
      this.myName = 'HUnter'
    }
    ```
  5. computed(计算值): 根据现有的状态或其它计算值衍生出的值
    > getter 获取计算得到新的`state`并返回
    > setter 不能用来直接改变计算属性的值，可以用来逆向衍生
    ```javascript
    var upperCaseName = computed(() =>
      name.get().toUpperCase()
    );
    ```
  6. autorun: 处理从反应式代码桥接到命令式代码，例如打印日志、持久化或者更新UI的代码
    > 如果有一个函数应该自动运行，但不会产生一个新的值，请使用`autorun`。 其余情况都应该使用`computed`
  7. reactions: 和计算值很像，但它不是产生一个新的值，而是会产生一些副作用，比如打印到控制台、网络请求、递增地更新`React`组件树以修补DOM等
  