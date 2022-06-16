# dateコマンド
## dateコマンドについて

BSD系OS(Unix, Mac)とGNU系OS(Unix)でdateコマンドは異なる

例）

```bash
if date --version >/dev/null 2>&1 ; then
  echo Using GNUdate
else
  echo Not Using GNUdate
fi
```

※GNU版のdateコマンドのみdate --versionが成功する

```bash
if type gdate > /dev/null 2>&1; then
  Date = gdate
else
  Date = date
fi
```