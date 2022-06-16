# gruntでインデント削除タスクを追加する
## 前提
- gruntって何かは知っている
- gruntはすでに導入済み

## やり方
1. grunt.initConfigにreplaceタスクを追加する
2. 正規表現でreplaceする

```js
// 行頭の空白を置換する（gmフラグは必要）
from: /^\s+/gm,
to: ''
```

## 実例

```js
module.exports = function(grunt) { // (1): export
  // (2): task configuration
  grunt.file.defaultEncoding = 'utf-8';

  grunt.initConfig({
    // ...
    replace: {
      // ...
      mailmagazine_dir: 'static/template/mailMagazine',
      mail_magazine: {
        src: [
          '<%= mailmagazine_dir %>/uncompressed/*.ftl'
        ],
        dest: '<%= mailmagazine_dir %>',
        replacements: [{
          from: /^\s+/gm,
          to: ''
        }]
      }
    },
    // ...
    watch: {
      // ...
      ftl: {
        files: ['<%= mailmagazine_dir %>/uncompressed/*.ftl'],
        tasks: ['replace:mail_magazine']
      }
    }
  });
  // ...
  grunt.loadNpmTasks('grunt-text-replace');

  // (4): register default task(s)
  grunt.registerTask('default', ['watch']);
};
```