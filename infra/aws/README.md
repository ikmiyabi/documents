# README
## インスタンスにログインする際に指定するユーザー名やキー名を省略する

```js
module.exports = {
  themeConfig: {
    // sidebar array
    // all pages will use the same sidebar
    sidebar: [
      // SidebarItem
      {
        text: 'Foo',
        link: '/foo/',
        children: [
          // SidebarItem
          {
            text: 'github',
            link: 'https://github.com',
            children: [],
          },
          // string - page file path
          '/foo/bar.md',
        ],
      },
      // string - page file path
      '/bar/README.md',
    ],
  },
}
```