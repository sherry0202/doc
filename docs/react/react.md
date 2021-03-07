---

id:react

title:react基本

---

## 在react中使用Typescript

创建一个ts项目

```markdown
yarn create react-app my-app --template typescript
```

## 解决react中无法配置webpack

创建项目完成以后，因为react默认不暴露配置文件, 所以无法自定义webpack配置。

这里我们使用 [craco](https://github.com/gsoft-inc/craco/)（一个对 create-react-app 进行自定义配置的社区解决方案）。

现在我们安装 craco 并修改 `package.json` 里的 `scripts` 属性。

```markdown
yarn add @craco/craco 
```

```markdown
/* package.json */
"scripts": {

- "start": "react-scripts start",
- "build": "react-scripts build",
- "test": "react-scripts test",

+ "start": "craco start",
+ "build": "craco build",
+ "test": "craco test", }
```

然后在项目根目录创建一个 `craco.config.js` 用于修改默认配置。

```js

/* craco.config.js */
module.exports = {
    // ...
};

```

## 处理css同名问题

这里为了处理react中css同名问题：

1. 使用webpack module(类似于vue中的scope)
1. 使用css in js (推荐使用比较火的库[styled-components](https://styled-components.com/))
1. 使用`BEM`命名规范(一般用于组件开发)

### css modules

先进行webpack配置css modules

```js
//先 yarn add craco-less 在craco.config.js中  
const CracoLessPlugin = require('craco-less');
module.exports = {
    plugins: [{
        plugin: CracoLessPlugin,
        options: {
            modifyLessRule: function (lessRule, _context) {
                lessRule.test = /\.(module)\.(less)$/;
                lessRule.exclude = /node_modules/;
                return lessRule;
            },
            cssLoaderOptions: {
                modules: {
                    localIdentName: '[hash:base64:5]',
                }
            },
            lessLoaderOptions: {
                lessOptions: {
                    javascriptEnabled: true,
                },
            }
        }
    }]
}
```

在`/src`下创建一个名为 `App.module.less` 的less文件

```less
/*App.module.less*/
.color {
  color: pink;
}
```

在App.tsx中使用这个文件

```tsx
import React, {FC} from 'react';
import style from './App.module.less'

const App: FC = () => <div className={style.color}>App</div>
```

当页面出现<span style={{color:'pink'}}>App</span>,说明配置成功!

### styled-components

安装`styled-components`

```markdown
yarn add styled-components @types/styled-components  
```
`@types/styled-components` 是typescript的声明文件。如果不是ts用户,可以不用安装。

```tsx
import styled from "styled-components";
import React, {FC} from 'react';
type Wrap = {
    color: string
}

const Wrapper = styled.div`
  color: ${(props: Wrap) => props.color};
`

const App: FC = () => <Wrapper color={'pink'}>App</Wrapper>
```
当页面出现<span style={{color:'pink'}}>App</span>,说明配置成功!









