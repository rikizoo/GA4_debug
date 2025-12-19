## 目的
GA4、GTMの検証環境を構築する

## 環境構築
* https://qiita.com/at-sacai/items/cdb189996cbbacfc51e6
* https://rikizoo.github.io/GA4_debug/

## 実装
<details>
  <summary>イベントスコープでの参照元を取得する</summary>

  ### 目的
  * セッションスコープで見るべきではない場面でもセッションの参照元/メディアを使用してしまうことを防ぐため、イベントスコープの参照元を実装する
  
  ### 前提知識
  * GA4にデフォルトで設定されているのはセッションスコープでの参照元のみ</br>※Refererでイベントスコープの取得もできるがSPAサイトくらいでしか正確なデータが取れない</br>
    | ディメンション名 | 意味 |
    | ---- | ---- |
    | ユーザーの参照元/メディア | そのユーザーの最初のセッションの参照元/メディア |
    | セッションの参照元/メディア | セッションの最初の参照元/メディア |
    | 参照元/メディア | キーイベントが行われたセッションの最初の参照元/メディア |
  * utmパラメータ(URL末尾にクエリ文字列を追加)を使用して参照元を判別する
    * utm_medium, utm_sourceは必須、utm_content,utm_campaignもあった方がいい
    * [URL 生成ツール: カスタム URL でキャンペーン データを収集する](https://support.google.com/analytics/answer/10917952?hl=ja)

  ### GTM
  1. utmパラメータを取得するためのカスタム変数を作成する(ユーザ定義変数のカスタムJavascript)</br><img width="983" height="365" alt="image" src="https://github.com/user-attachments/assets/a8b28172-a81e-4752-8e65-1526cc9b308d" />
  2. 1で取得した値が各種イベントをトリガーとしたイベントパラメータとして送信されるように設定</br><img width="945" height="709" alt="image" src="https://github.com/user-attachments/assets/688342e4-fe4a-4d41-90c2-5a768aa8aec6" />
  3. プレビューutmパラメータを追加したURLを開き、想定通りの値が入っているか確認する</br><img width="655" height="477" alt="image" src="https://github.com/user-attachments/assets/78e141bd-12e7-4967-8a6e-8117dfbe22fa" /></br><img width="1193" height="618" alt="image" src="https://github.com/user-attachments/assets/d39bed7a-0c44-483b-9dc3-5003d2916f3b" />
  
  ### GA4
  1. GTMで送信したイベントパラメータをカスタムディメンションとして定義する
</details>
