> typeRoots：告诉 tsc，声明文件的总的上下文
> types: 告诉 tsc，在 typeRoots 指定的总的上下文中，去加载指定的声明文件的`全局级别类型`

注意：只会加载全局级别的类型定义， 文件级别的不给予加载，但你可以自己根据路径手动引入

全局级别的类型和文件级别  的类型的区别：全局的，不需要 import 就能使用，文件级别的，需要手动 import 才能使用

根据`moduleResolution: node`的查找策略
只要找不到声明文件，tsc 会逐层去 node_modules/@types 去找， 不管你有没有在 typeRoots 里面定义

如果你在 types 里指定了一个在声明文件的总的上下文中没有的声明文件，tsconfig.json file 会报错，但不影响项目运行

即使某些声明文件在`exclude`中, 但它们在 typeRoots, types 中使用啦，那么也是不能被 exclude 掉，说明 typeRoots, types 的权重更高, 可以比对 foo 和 bar 在 `index.ts` 文件的表现

可以查看 tsconfig.json 文件，先指定声明文件总的上下文`typeRoots: ["types"]`, 然后指定只加载指定的声明文件的全局变量`types: ["foo", "yy"]`, 其中 foo 在总的上下文中， 但 yy 不在，yy 在`node_modules/@types`中, 但没有报错，说明，tsc 会逐层查找 node_modules/@types，最后找到了 yy

### Reference

- https://ts.xcatliu.com/basics/declaration-files.html
- https://stackoverflow.com/questions/40222162/typescript-2-custom-typings-for-untyped-npm-module
- https://stackoverflow.com/questions/42388217/having-error-module-name-resolves-to-an-untyped-module-at-when-writing-cu
