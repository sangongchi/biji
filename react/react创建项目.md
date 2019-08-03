## react创建项目

### 1. 创建项目的两种方式

- > ==npm install -g create-react-app==
    >
    > ==create-react-app my-app(项目名)==
    >
    > ==cd my-app==
    >
    > ==npm start | npm run start==

- > ==npx create-react-app my-app==    此处的npx 不是拼写错误，他是npm 5.2+ 附带的package运行工具
    >
    >  ==cd my-app==
    >
    > ==npm start==

- > 通过引入的方式进行使用rect
    >
    > <script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
    > <script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
    > <!-- 生产环境中不建议使用 -->
    >
    > <script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>