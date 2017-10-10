# mac.md  

## 不可視ファイルや不可視フォルダを表示する方法

```
defaults write com.apple.finder AppleShowAllFiles -boolean true
```


Finderを再起動します。

```
killall Finder
```

これで不可視ファイルや不可視フォルダが表示されます。

## 元に戻す

```
defaults delete com.apple.finder AppleShowAllFiles
killall Finder
```

---

