# welcome cdd

- このレポジトリは、npm へ publish するための環境です
- ここで作成したコンポーネントは、npm へ publish されます
- ユーザーは yarn add cdd-ui でインストールできます
- 使う側のレポジトリは、yarn add cdd-ui でインストールした後、import { MyComponent } from "cdd-ui" などで使用できます
- 最新のバージョンを使うには、package.json の version を変更してください
- また、npm publish をする前に、yarn build を実行してください
