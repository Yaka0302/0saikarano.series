【Vercelへのアップロード方法】

1. このZIPを解凍します。
2. Vercelで「Add New」→「Project」を選びます。
3. 解凍したフォルダ内のファイルをアップロードします。
4. Framework Presetは「Other」のままで大丈夫です。
5. Build Command・Output Directoryは空欄で公開できます。

【フォルダ構成】

index.html
vercel.json
css/
  style.css
js/
  app.js
assets/
  bgm/
  sounds/

現在のBGMはindex.html内にBase64形式で埋め込まれているため、
音声ファイルを別途用意しなくても動作します。
assetsフォルダは、今後BGMや効果音を追加するときに使用できます。
