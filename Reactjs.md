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