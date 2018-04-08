## react 入门到实战

#### 什么是react？
1. 一套用于构建用户界面的js框架
    - 跟jq非常像，主要的就是 对 DOM 进行 增删改查操作
2. 基于组件开发
    - 如果你用 react 去开发一个项目的话，
    - 整个项目当中，有可能，每一个东西都是一个组件
    - 比如说是 一个 button，一整个留言框。或者其他组件的功能，都可以使用组件的构建。
3. 基于虚拟DOM（速度非常快）
    * 当我们写完代码，或者操作逻辑，它会现在你的虚拟DOM中去实现，
    * 如果你的虚拟DOM跑成功了，会跟你真是的DOM 去匹配
    * 不同的地方，将会插入到你的真是DOM中来。
4. 隶属Facebook
    * 这是一个互联网巨头，它们出的框架，必属于经典了。



#### ReactDOM.render  的介绍。
1. 下载模板
```s
    $  start iexplore  http://www.thenewstep.com/ReactByHenry/ReactTemp
late.zip
```
2. src/demos/index.html 写入以下内容
```html
    <!-- 容器 -->
    <div id="container">

    </div>
    <script type="text/babel"> 
        // babel 可以将reactjs代码翻译成浏览器可以识别的代码

        /**
            ReactDOM.render 是React的最基本的方法，用于将模板转为HTML语言，
            并插入到DOM节点当中。
        */ 
        ReactDOM.render( 
            <h2>Welcome to React!</h2> ,
            document.getElementById("container")
        );
    </script>
```

#### 组件和属性
1. 第一个组件
```html
    <!-- 容器 -->
    <div id="container">

    </div>
    <!-- // babel 可以将reactjs代码翻译成浏览器可以识别的代码 -->
    <script type="text/babel"> 
        
        /**
            ReactDOM.render 是React的最基本的方法，用于将模板转为HTML语言，
            并插入到DOM节点当中。
        */ 
        // 创建一个组件
        var Bacon = React.createClass({
            render: function () {
                return (<h2>这是一个简单的组件</h2>)
            }
        })
        ReactDOM.render( 
            <Bacon />,
            document.getElementById("container")
        );
    </script>
```
2. 组件的复用，props属性
```html
<body>
    <!-- 容器 -->
    <div id="container">

    </div>
    d
    <!-- // babel 可以将reactjs代码翻译成浏览器可以识别的代码 -->
    <script type="text/babel"> 
        
        /**
            ReactDOM.render 是React的最基本的方法，用于将模板转为HTML语言，
            并插入到DOM节点当中。
        */ 
        // 创建一个组件
        // 组件类的名字的第一个字母必须大写,不然也会报错(Bacon)
        var Bacon = React.createClass({
            // 所有的组件类都必须拥有自己的组件类render，否则就会报错
            render: function () {
                return (
                    // 每个组件中只能有一个跟标签
                    // this指的是，当前组件，props是组件用来接收 ReactDOM 传过来的值。
                    <div>
                        <h2>{ this.props.title }</h2> 
                        <p> { this.props.genre }</p>
                    </div>
                );
            }
        });

        // 在调用的时候，如果想要调用多次组件，那么也需要给组件一个根标签
        ReactDOM.render( 
            <div>
                <Bacon  title="美丽人生" genre="romance" />
                <Bacon  title="美国队长" genre="action" />
                <Bacon  title="机械师2"  genre="action" />
            </div>,
            document.getElementById("container")
        );
    </script>
</body>
```
#### 事件的使用
###### 引入css样式
```html
    <link rel="stylesheet" href="../css/main.css">    <!-- 下面的所有 body 都得在 head 中引入这个 css 样式 -->
```

```html
<body>
    <!-- 容器 -->
    <div id="container">

    </div>
    <script type="text/babel"> 
        var Comment = React.createClass({
            edit:function(){
                alert('Editing Comment!')
            },
            remove:function(){
                alert("removeing comment!")
            },
            render: function () {
                return (
                    <div className="commentContainer">
                        <div>{ this.props.children }</div>
                        <button onClick={ this.edit } className="button-primary"> Edit </button>
                        <button onClick={ this.remove} className="button-danger"> Remove </button>
                    </div>
                );
            }
        });

        // 在调用的时候，如果想要调用多次组件，那么也需要给组件一个根标签
        ReactDOM.render( 
            <div className="board">
                <Comment>Hello Everybody</Comment>
                <Comment>Welcome to xieerduos</Comment>
                <Comment>快速掌握 react js </Comment>
            </div>,
            document.getElementById("container")
        );
    </script>
</body>
```

#### 状态state 

```html
<body>
    <!-- 容器 -->
    <div id="container">

    </div>
    <script type="text/babel"> 
        var CheckBox = React.createClass({
            // 初始化状态值
            getInitialState:function(){
                return {
                    checked: false
                }
            },
            
            handleChecked:function(){
                this.setState( { checked: !this.state.checked } )
            },
            render: function () {
                var msg;
                if( this.state.checked ) {
                    msg = "checked"
                }else{
                    msg = "unchecked"
                }

                return (
                <div>
                    <input onChange={ this.handleChecked } type="checkbox" defaultChecked={ this.state.checked } />
                    <h3>{ msg } </h3>
                    <p>{ this.props.title }</p>
                </div>
                )
            }
        });
        ReactDOM.render( 
            <CheckBox title="属性"/>,
            document.getElementById("container")
        );

        /**
            属性和状态两个的 区别是在于：
                属性一旦定义了，就没有办法改变它了。  this.props.title
                状态不一样，状态可以通过具体的业务逻辑去改变它。 

            状态和属性的最大区别就是，属性不能够改变，状态经常被改变的。
            另外一个是，属性是在组件当中 书写的，状态是在初始化的时候就有了，设定好的。

            数据，可以写在状态里面，这样，就可以对数据进行增删改查，
            这就是有变化的东西，这样就可以通过状态去书写对顶的数据了。

            属性，是不可以改变的，在组件之间去传递就是了。


            以上就是状态的应用。
        */ 
    </script>
</body>
```

#### 状态和组件并用
```html
<body>
    <!-- 容器 -->
    <div id="container">

    </div>
    <script type="text/babel"> 
        var Comment = React.createClass({
            getInitialState:function(){
                return ( { editing: false } );
            },
            edit:function(){
                this.setState( { editing: true });
            },
            remove:function(){
                alert("removeing comment!")
            },
            renderNormal: function(){
                return (
                    <div className="commentContainer">
                        <div>{ this.props.children }</div>
                        <button onClick={ this.edit } className="button-primary"> Edit </button>
                        <button onClick={ this.remove} className="button-danger"> Remove </button>
                    </div>
                );
            },

            save:function(){
                this.setState( {editing: false});
            },
            renderForm:function(){
                return(    
                    <div className="commentContainer">
                        <textarea defaultValue={ this.props.children}></textarea>
                        <button onClick={ this.save } className="button-success"> Save </button>
                    </div>
                    )
            },
            render: function () {
                if( this.state.editing){
                    return this.renderForm();
                } else{
                    return this.renderNormal();
                }
            }
        });

        // 在调用的时候，如果想要调用多次组件，那么也需要给组件一个根标签
        ReactDOM.render( 
            <div className="board">
                <Comment>Hello Everybody</Comment>
                <Comment>Welcome to xieerduos</Comment>
                <Comment>快速掌握 react js </Comment>
            </div>,
            document.getElementById("container")
        );
    </script>
</body>
```

#### 多组件嵌套
```html
<body>
    <!-- 容器 -->
    <div id="container">

    </div>
    <script type="text/babel"> 

        var Borad = React.createClass({
            getInitialState:function(){
                return ({
                    comments: ["hello everybody", "welcome to xieerduos of github ", "希望大家好好学习，reactjs!"]
                });
            },
            eachComment: function(item, index){
                return (
                    <Comment key={index} index={index}>{ item }</Comment>
                );
            }
            ,
            render: function(){
                return (
                    <div className="board">
                         {
                            this.state.comments.map(this.eachComment)
                        } 
                    </div>
                );
            }
        })

    
        var Comment = React.createClass({
            getInitialState:function(){
                return ( { editing: false } );
            },
            edit:function(){
                this.setState( { editing: true });
            },
            remove:function(){
                alert("removeing comment!")
            },
            renderNormal: function(){
                return (
                    <div className="commentContainer">
                        <div>{ this.props.children }</div>
                        <button onClick={ this.edit } className="button-primary"> Edit </button>
                        <button onClick={ this.remove} className="button-danger"> Remove </button>
                    </div>
                );
            },

            save:function(){
                var val = this.refs.newText.value;
                console.log("拿到的值是： ",val);
                this.setState( {editing: false});
            },
            renderForm:function(){
                return(    
                    <div className="commentContainer">
                        <textarea ref="newText" defaultValue={ this.props.children}></textarea>
                        <button onClick={ this.save } className="button-success"> Save </button>
                    </div>
                    )
            },
            render: function () {
                if( this.state.editing){
                    return this.renderForm();
                } else{
                    return this.renderNormal();
                }
            }
        });

        // 在调用的时候，如果想要调用多次组件，那么也需要给组件一个根标签
        ReactDOM.render( 
            <Borad />,
            document.getElementById("container")
        );
    </script>
</body>
```
#### 跨组件调用方法
```html
<body>
    <!-- 容器 -->
    <div id="container"> </div>
    <script type="text/babel"> 

        var Borad = React.createClass({
            getInitialState:function(){
                return ({
                    comments: []
                });
            },
            updateComment: function(newText, i){
                // console.log(newText,i );
                var arr = this.state.comments;
                arr[i] = newText;
                // 更新我们的状态
                this.setState( { comments: arr } );
            }
            ,
            removeComment:function(i){
                // console.log(i);
                var arr = this.state.comments;
                arr.splice(i,1); // arr.splice(从那个下标开始删除,删除多少个)
                // 更新状态
                this.setState({comments: arr});
            },

            eachComment: function(item, i){
                return (
                    <Comment deleteFromBoard={this.removeComment} updateCommentText={ this.updateComment } key={i} index={i}>{ item }</Comment>
                );
            }
            ,
            add: function(text) {
                var arr = this.state.comments;
                arr.push(text);
                this.setState({comments: arr});
            },
            render: function(){
                return (
                    <div>
                        <button onClick={ this.add.bind(null, "Default text") } className="button-info create">Add New</button>
                        <div className="board">
                            {
                                this.state.comments.map(this.eachComment)
                            } 
                        </div>
                    </div>
                );
            }
        })

    
        var Comment = React.createClass({
            getInitialState:function(){
                return ( { editing: false } );
            },
            edit:function(){
                this.setState( { editing: true });
            },
            remove:function(){
                // alert("removeing comment!")
                this.props.deleteFromBoard(this.props.index);
            },
            renderNormal: function(){
                return (
                    <div className="commentContainer">
                        <div>{ this.props.children }</div>
                        <button onClick={ this.edit } className="button-primary"> Edit </button>
                        <button onClick={ this.remove} className="button-danger"> Remove </button>
                    </div>
                );
            },

            save:function(){
                var val = this.refs.newText.value;
                // console.log("拿到的值是： ",val);
                this.props.updateCommentText(val, this.props.index )
                this.setState( {editing: false});
            },
            renderForm:function(){
                return(    
                    <div className="commentContainer">
                        <textarea ref="newText" defaultValue={ this.props.children}></textarea>
                        <button onClick={ this.save } className="button-success"> Save </button>
                    </div>
                    )
            },
            render: function () {
                if( this.state.editing){
                    return this.renderForm();
                } else{
                    return this.renderNormal();
                }
            }
        });

        // 在调用的时候，如果想要调用多次组件，那么也需要给组件一个根标签
        ReactDOM.render( 
            <Borad />,
            document.getElementById("container")
        );
    </script>
</body>
```