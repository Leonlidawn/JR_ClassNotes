
react全家桶：https://www.youtube.com/watch?v=nNuBkCx1lXw&list=PLmOn9nNkQxJE7-X51lX9ixWkyQwIArDRv&index=35


在reactjs 里面用inline css,
要给在react component tag 的 style 参数 assign一个object

eg.
        
    import React, { Component } from 'react';

    class Menu extends Component {
        render() {
            var divStyle = {
                border: 'black solid',
                color: 'red',
                width: '50px',
                display: 'inline-block'
            };

            return (
                < div className="Menu" style={divStyle} >
                    <div>1 </div>
                    <div>2 </div>
                    <div>3 </div>
                </div>
            );
        }
    }

    export default Menu;



# Redux


# React-redux


# Redux-thunk

# React-router
组件：
```
<BrowserRouter>//
<HashRouter>//
<Route>//
<Ridirect>//
<Link>//
<NavLink>//
<Switch>//
```
对象：
```
history
match
```
函数
```
withRouter//
```

##### import { BrwoserRouter,HashRouter } from 'react-router-dom';
通常用在app.js这样的主要component 里面。或者直接在index.js，套在外层。

BrowserRouter: 
- typically for singlepage,same index.html is served for /react/route path or any other route on server side(server needd to be configured to handle dynamic urls,ie. to send the same index.html).
- On client side, window.location.pathname is parsed by React router.
- React router renders a component that it was configured to render for /react/route. application.
- uses HTML-5 history API.(例如用window.history的方法前进或后退，使用了state保存session history记录)
- not supported by IE9 or older browsers
-     baseurl/componentRoute/


HashRouter:
- uses URL hash, it puts no limitations on supported browsers or web server. 
- Server-side routing is independent from client-side routing.#之前的url都给server处理，#之后的client处理。
- On client side, window.location.hash is parsed by React router.（location.hash return the anchor part of a URL。 eg.#url ）
-     baseUrl/#/componentRoute


##### import { Route,Redirect，Switch} from 'react-router-dom';
通常用在父组件，决定渲染哪一个子component.

Route:
-     <Route exact path="/" component={reactComponent}/>
-     <Route path="/subPage" component={reactComponent}/>
- exact这个keyword会把path 匹配变成绝对匹配。
- component会接收到一些额外的props.

        {history: {
            length: 18, 
            action: "POP", 
            location: {…}, 
            createHref: ƒ, push: ƒ, …}
        location: {
            pathname: "/", 
            search: "", 
            hash: "", 
            state: undefined, 
            key: "axh80n"}
        match: {
            path: "/", 
            url: "/", 
            isExact: true, 
            params: {…}}
        staticContext: undefined
        }


Redirect:
- 在应用中 <Redirect> 可以设置重定向到其他 route 而不改变旧的 URL。
- 
    ```
    <Route component={App}>
    <Route path="about/:userId" component={UserProfile}/>
    {/* /profile/123 -> /about/123 */}
    <Redirect from="profile/:userId" to="about/:userId" />
    </Route>
    ```
Switch
- 在多个组件中作出单选渲染
- 渲染第一个被location匹配到的并且作为子元素的<Route>或者<Redirect>
- 例子
    ```
    <Switch>
        <Route exact path = "/" component={Home} >
        <Route path = "/signUp" component={SignUp} >
    </Switch> 
    // "/"匹配到第一个并渲染只第一个
    ```


##### import { Link, NavLink } from 'react-router-dom';
通常用在navbar这样具有很多链接的component 里面，决定path是怎么用的，与Route,Redirect 里面的path对应。

Link:
- 重新包装   \<a>,不会有发请求到server导致刷新
-       //<a href='/'>Home</a>
        <Link to='/'>Home</Link>

NavLink:
- 重新包装   <a></a>,不会有发请求到server导致刷新,同时还会在render出来的<a></a>里面加入listener，被点击之后link 的 class里会出现active。
-       //<a href='/'>Home</a>
        <NavLink to='/'>Home</NavLink>
- 对根据active class来改变style非常有用
 

##### import { withRouter } from 'react-router-dom';
通常用于需要使用history跳转的页面,withRouter()是一个higher ordered function. 把router的props加入到指定的component里面。

withRouter:
- export withRouter(component);






