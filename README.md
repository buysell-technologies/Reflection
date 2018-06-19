# Reflection

Swift Package Manager製のライブラリ [Reflection](https://github.com/Zewo/Reflection) をCarthage化したものです

使い方
```
echo 'github "buysell-technologies/Reflection"' >> Cartfile
carthage update Reflection --platform iOS
# swiftファイル中で import Reflection できるようになる
```

## ビルド方法

あくまでもワークアラウンド的な方法なので、
もっと良いやり方があれば修正したいです。。。

- ReflectionをSwiftPackageManagerで取得してくる
```
$ ruby generate-dependencies-project.rb
```
.build以下に大元のReflectionのソースが入ってきます

- プロジェクト設定を変更
  - Reflectionのみをビルドするように他のビルドスキーマは消す（Dependencies-packageなど）
  - xcodeprojのSDKROOTが空になるようにする
    - これをしないと各種プラットフォーム向けのビルドが出来ない
    - 現状のリポジトリの設定を参考に修正します

- carthage用のビルド
```
$ carthage build --no-skip-current
```
これで出来たCarthageディレクトリ以下をzipで固めて`Reflection.framework.zip`としてパブリッシュします。
このとき、Reflection.framework関連以外のframeworkが含まれないようにします。
