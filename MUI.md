# 2024年のMUI導入フローと概要

## はじめに

このドキュメントは、2024年1月時点でのMUIの導入フローと概要をまとめたものです。

ターゲットは、MUIを初めて使用する方、導入から改めて学び直したい方です。職務は、フロントエンドエンジニア、デザイナー、UIの具体的な実装を行う方です。

エンジニアはデザイン観点での理解を深めることで、デザイナーはエンジニア観点での理解を深めることで、より良いコミュニケーションができるようになることを目的としています。

## MUI概要

MUI（旧称 Material-UI）は、React用のUIライブラリで、Googleのマテリアルデザインをベースにしたコンポーネントを提供しています。

ReactでWebアプリケーションを開発する際に、UIコンポーネントを簡単に作成することができます。

### バージョンまわりの注意点

2024年1月時点で現在の最新バージョンは5です。

取得されるMUIの情報は旧称Material-UI=バージョン4であることも多いので、注意が必要です。

特に検索する際は、以下の点に注意してください。

- `makeStyles`や`withStyles`などの古い情報が出てくることがありますが、これらはMUI5では非推奨となっています。
- 検索した情報の中に`makeStyles`などが出てきた場合は明らかに古い情報なので、MUI5の公式ドキュメントを参照し、検索範囲を直近1年以内に絞ったりMUI5であること明示するなどフィルタリングすると良いでしょう。

### Googleマテリアルデザインとは

Googleが提唱するデザインの指針です。Googleが提供する多くのサービスやアプリケーションで採用されています。

- 主な特徴は、フラットデザインで、シャドウやグラデーションなどの影や立体感を排除し、シンプルで直感的なデザインを実現しています。
  - 厳密にはフラットデザインではなく、フラットデザインをベースにしたデザインです。
- マテリアルデザインは、ユーザーインターフェースのデザインに関する指針を提供するだけでなく、アニメーションやトランジションなどの動きに関する指針も提供しています。
- 採用されたサービスの代表例は、Gmail、Googleドライブ、Googleマップ、YouTubeなどです。

- マテリアルデザインは 2024年1月時点で[Material Design 2](https://m2.material.io/)と[Material Design 3](https://material.io/design/)があり、MUIはMaterial Design 2をベースにしています。
  - 2と３の違いは、主にアニメーションやトランジションなどの動きに関する指針が変更されています。
  - 今後のアップデートではどのようになるかはまだわかりませんが、順当にいけば、MUIは Material Design 3に対応することも考えられます。

関連書籍：

- [0 から学ぶマテリアルデザイン 2: Google マテリアルデザインガイドライン日本語解説 Kindle 版](https://shrtm.nu/pXB)
- [基礎から学ぶマテリアルデザイン 3: Google が提唱する UI デザインの 最新バージョン 「マテリアル 3」の基礎を日本語解説 Kindle 版](https://shrtm.nu/pXC)
- [フラットデザインの基本ルール Webクリエイティブ&アプリの新しい考え方](https://shrtm.nu/pXE)

---

### アウトライン

- MUIのインストールとプロジェクトのセットアップ
- 必要なコンポーネントのインポートとユーザーインターフェースの構築
- MUIテーマのカスタマイズ
- MUIテーマの構成
- テーマオブジェクトの作成とMuiThemeProviderへの適用
- コンポーネントでのテーマ利用
- テーマで定義したスタイルのアクセスと適用

## MUIの基本導入設定

基本的な導入設定は以下の手順で行います

**MUI パッケージのインストール

まず、プロジェクトにMUIをインストールします。npmまたはyarnを使用して、必要なパッケージをプロジェクトに追加します。コマンドは以下の通りです。

```bash
npm install @mui/material @emotion/react @emotion/styled
```

または

```bash
yarn add @mui/material @emotion/react @emotion/styled
```

**Roboto フォントの追加**: MUIはデフォルトでRobotoフォントを使用します。このフォントをプロジェクトに追加するには、以下のリンクをHTML ファイルの`<head>`部分に挿入します。

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap" />
```

ただし、個人的にはRobotoでなく、Noto Sans JPとInterを使用することをおすすめします。

- Noto Sans JP: <https://fonts.google.com/specimen/Noto+Sans+JP>
  - Noto Sans JPは、日本語のフォントを含むフォントで、癖が少なく、Windows/Macでのタイポグラフィの差異を解消することができます。デザインのバランス、統一性を保つためにも、Noto Sans JPを使用することをおすすめします。
- Inter: <https://fonts.google.com/specimen/Inter>
  - Interは、英語のフォントで、Noto Sans JPと同様に癖が少なく、Noto Sans JPとの融合された時のデザインのバランス、統一性を保つためにも、Interを使用することをおすすめします。
  - また、Next.jsのデフォルトフォントでもあるため、Next.jsを使用する場合は、特にインストールする必要はありません。

**SVG アイコンの使用**: SVG アイコンを使用する場合は、`@mui/icons-material`パッケージをインストールします。

```bash
npm install @mui/icons-material
```

または

```bash
yarn add @mui/icons-material
```

**MUI コンポーネントの使用**: 基本設定が完了したら、MUI のコンポーネントをインポートして使用できます。例えば、ボタンコンポーネントは以下のように使用します。

```jsx
import Button from "@mui/material/Button"

function App() {
  return <Button variant="contained">Hello World</Button>
}
```

これらの手順で MUIの基本的な導入が完了します。
公式ドキュメント（<https://mui.com/material-ui/getting-started/installation/> ）では、さらに詳しい情報とガイドが提供されています。

---

## ２つのユースケース： Themeの拡張とカスタムコンポーネント

1. theme の拡張
   例えばこのButtonコンポーネントの基本VariantをContainedやOutlinedに規定、つまりVariant未定であればDefault値が設置されるような設定を、テーマファイル`theme.ts`に対して設置する。
   - 設置しないと未指定時=Defaultボタンのスタイルが（あまりメインでは使わない）Textになったりする
2. コンポーネントの拡張
   <ButtonPrimary ...some>などのButtonコンポーネントを拡張したオリジンなスタイルを設置したカスタムボタンコンポーネントを作成してみる
   - なぜカスタムボタンコンポーネントを作成するのか？
     - 例えば、頻繁に使用するボタンのスタイルを定義しておくことで、そのスタイルを適用したボタンコンポーネントを作成しておくことで、コードの重複を防ぐことができます。

### 1. テーマの拡張

`theme.ts` または `theme.tsx` ファイルで、`Button` コンポーネントのデフォルトの `variant` を設定することができます。以下に例を示します。

```tsx
// theme.ts or theme.tsx
import { createTheme } from "@mui/material/styles"

const theme = createTheme({
  components: {
    MuiButton: {
      defaultProps: {
        // デフォルトのvariantを 'contained' または 'outlined' に設定
        variant: "contained", // または 'outlined'
      },
    },
  },
})

export default theme
```

### 2. カスタムコンポーネントの拡張

`Button` コンポーネントを拡張して、独自のスタイルを適用したカスタムコンポーネントを作成することができます。以下にサンプルコードを示します。

```tsx
// ButtonPrimary.tsx
import React from "react"
import Button from "@mui/material/Button"
import { styled } from "@mui/material/styles"

const CustomButton = styled(Button)({
  // カスタムスタイル
  background: "linear-gradient(45deg, #FE6B8B 30%, #FF8E53 90%)",
  border: 0,
  borderRadius: 3,
  boxShadow: "0 3px 5px 2px rgba(255, 105, 135, .3)",
  color: "white",
  height: 48,
  padding: "0 30px",
})

const ButtonPrimary = (props) => {
  return <CustomButton {...props}>{props.children}</CustomButton>
}

export default ButtonPrimary
```

### 3. その他の UI コンポーネントの拡張

他の UI コンポーネントを拡張する方法として、以下の例を挙げます。

- **カスタムテーマの色**: `createTheme` 関数を使って、色やフォントなどのテーマ設定をカスタマイズできます。
- **グローバルスタイルの適用**: `createTheme` で `components` キーを使用して、複数のコンポーネントに共通するスタイルを定義できます。
- **スタイルドコンポーネントの使用**: `styled` 関数を使用して、既存の MUI コンポーネントに新しいスタイルを適用するカスタムコンポーネントを作成できます。

これらの手法を使用することで、MUI のコンポーネントを自由にカスタマイズし、アプリケーションの UI を独自のものにすることができます。

---

## Theme のアーキテクチャ

この theme ファイルはどのようにプロダクトに反映されるのか

以下の環境のユースケース別に実装してみましょう

1. React + ts
2. React on Vite
3. Next.js version=13
4. Next.js version=14

### DarkThemeへの対応

加えて、上記のCustomButtonButtonに色の指定がありますが、light/darkのテーマ切り替えに対応させてみましょう

ちなみにダークテーマとダークモードは厳密には違います。ダークテーマは一意の色の指定、ダークモードはOSの設定に準拠した色の指定です。

1. ダークモードはCSSのprefers-color-schemeを使用して実装します。色の判定はOSの設定に準拠します。
2. 一方で、ダークテーマは開発側やユーザーが任意に切り替えられるように実装します。色の判定はユーザーの設定に準拠します。

パターンとしては以下のようなものがあります。

1. インラインで light/dark を三項演算子などで分岐で書くケース (1. OS 設定準拠 / 2. ユーザーが任意に選択)
2. lightTheme.ts darkTheme.ts など２つのファイルで構成するケース （toggle + localStorage）
3. 応用的に darkThemeHighContrast.ts など３つ目を加えたケース（Select Menu+ localStorage）

MUI のテーマをプロジェクトに反映させるには、`ThemeProvider` コンポーネントを使用して、アプリケーションのルートレベルでテーマをラップします。以下のユースケース別の設定を示します。

### 1. React + TypeScript

```tsx
// theme.ts
import { createTheme } from "@mui/material/styles"

const theme = createTheme({
  // テーマ設定...
})

export default theme

// App.tsx
import React from "react"
import { ThemeProvider } from "@mui/material/styles"
import theme from "./theme"

function App() {
  return <ThemeProvider theme={theme}>{/* コンポーネント */}</ThemeProvider>
}

export default App
```

### 2. React on Vite

Vite プロジェクトでも、上記の React + TypeScript の設定と同様に`ThemeProvider`を使用します。

### 3. Next.js version=13

Next.js 13 では、`_app.tsx` ファイルで`ThemeProvider`を使用します。

```tsx
// _app.tsx
import { ThemeProvider } from "@mui/material/styles"
import theme from "../path/to/your/theme"

function MyApp({ Component, pageProps }) {
  return (
    <ThemeProvider theme={theme}>
      <Component {...pageProps} />
    </ThemeProvider>
  )
}

export default MyApp
```

### 4. Next.js version=14

Next.js 14 でも、`_app.tsx`で同様に`ThemeProvider`を使用します。Next.js のバージョンがアップデートされても、この基本的な流れは変わりません。

---

## Colorの指定

### インラインで light/dark を三項演算子で分岐するケース

```tsx
// CustomButton.tsx
import React from "react"
import Button from "@mui/material/Button"
import { styled, useTheme } from "@mui/material/styles"

const CustomButton = styled(Button)(({ theme }) => ({
  background:
    theme.palette.mode === "dark"
      ? "linear-gradient(45deg, #333 30%, #666 90%)"
      : "linear-gradient(45deg, #FE6B8B 30%, #FF8E53 90%)",
  // その他のスタイル...
}))

const ButtonPrimary = (props) => {
  const theme = useTheme()
  return (
    <CustomButton theme={theme} {...props}>
      {props.children}
    </CustomButton>
  )
}

export default ButtonPrimary
```

### lightTheme.ts と darkTheme.ts を使用するケース

```tsx
// lightTheme.ts
import { createTheme } from "@mui/material/styles"

export const lightTheme = createTheme({
  palette: {
    mode: "light",
    // その他の色設定...
    primary: {
      main: #some for light
    },
  },
})

// darkTheme.ts
import { createTheme } from "@mui/material/styles"

export const darkTheme = createTheme({
  palette: {
    mode: "dark",
    // その他の色設定...
    primary: {
      main: #some for dark
    },
  },
})

// App.tsx
import React, { useState } from "react"
import { ThemeProvider } from "@mui/material/styles"
import { lightTheme, darkTheme } from "./path/to/themes"

function App() {
  const [mode, setMode] = useState("light")
  const theme = mode === "dark" ? darkTheme : lightTheme

  return <ThemeProvider theme={theme}>{/* コンポーネント */}</ThemeProvider>
}

export default App
```

### darkThemeHighContrast.ts を加えたケース

```tsx
// darkThemeHighContrast.ts
import { createTheme } from "@mui/material/styles"

export const darkThemeHighContrast = createTheme({
  palette: {
    mode: "dark",
    // 高コントラスト設定...
    primary: {
      main: #some for highContrast
    },
  },
})

// App.tsx
import React, { useState } from "react"
import { ThemeProvider } from "@mui/material/styles"
import { lightTheme, darkTheme, darkThemeHighContrast } from "./path/to/themes"

function App() {
  const [mode, setMode] = useState("light")
  let theme

  switch (mode) {
    case "dark":
      theme = darkTheme
      break
    case "highContrast":
      theme = darkThemeHighContrast
      break
    default:
      theme = lightTheme
  }

  return <ThemeProvider theme={theme}>{/* コンポーネント */}</ThemeProvider>
}

export default App
```

---

## テーマの切り替えロジック

では、このthemeをlocalStorageで保存しながら切り替えが可能なコンポーネントの作成方法を見ていきましょう。

凡例として

- Common 背景色
- Common Text 色
- Button Designのlight/dark

を設定します。

MUI テーマを`localStorage`で保存しながら切り替える機能を持つコンポーネントを作成するには、以下のステップに従います。

1. **テーマの状態を管理する**: React の`useState`と`useEffect`を使用して、現在のテーマモードを管理します。
2. **`localStorage`にテーマを保存**: ユーザーがテーマを切り替えるたびに、その選択を`localStorage`に保存します。
3. **テーマ切り替え機能の実装**: テーマを切り替えるためのボタンやスイッチを提供し、クリックイベントでテーマを切り替えます。
4. **具体的なデザインの指定**: 共通の背景色、テキスト色、ボタンのデザインをテーマごとに定義します。

以下に実装例を示します。

### テーマの定義

まずは`lightTheme.ts`と`darkTheme.ts`を定義します。これらのファイルでは、共通の背景色、テキスト色、ボタンのデザインを設定します。

```tsx
// lightTheme.ts
import { createTheme } from "@mui/material/styles"

export const lightTheme = createTheme({
  palette: {
    mode: "light",
    background: {
      default: "#ffffff",
    },
    text: {
      primary: "#000000",
    },
  },
  // その他の設定...
})

// darkTheme.ts
import { createTheme } from "@mui/material/styles"

export const darkTheme = createTheme({
  palette: {
    mode: "dark",
    background: {
      default: "#121212",
    },
    text: {
      primary: "#ffffff",
    },
  },
  // その他の設定...
})
```

### テーマ切り替えコンポーネント

次に、テーマを切り替えるコンポーネントを作成します。このコンポーネントは、初期状態を`localStorage`から読み込み、ユーザーの操作によってテーマを切り替える機能を持ちます。

```tsx
// ThemeSwitcher.tsx
import React, { useState, useEffect } from "react"
import { ThemeProvider } from "@mui/material/styles"
import { lightTheme, darkTheme } from "./path/to/themes"
import Switch from "@mui/material/Switch"

const ThemeSwitcher = ({ children }) => {
  const [themeMode, setThemeMode] = useState(localStorage.getItem("themeMode") || "light")

  useEffect(() => {
    localStorage.setItem("themeMode", themeMode)
  }, [themeMode])

  const handleThemeChange = () => {
    setThemeMode(themeMode === "light" ? "dark" : "light")
  }

  const theme = themeMode === "light" ? lightTheme : darkTheme

  return (
    <ThemeProvider theme={theme}>
      <Switch checked={themeMode === "dark"} onChange={handleThemeChange} />
      {children}
    </ThemeProvider>
  )
}

export default ThemeSwitcher
```

### アプリケーションでの使用

最後に、アプリケーションのルートコンポーネントで`ThemeSwitcher`を使用します。

```tsx
// App.tsx
import React from "react"
import ThemeSwitcher from "./ThemeSwitcher"
import YourComponent from "./YourComponent"

function App() {
  return (
    <ThemeSwitcher>
      <YourComponent />
      {/* その他のコンポーネント */}
    </ThemeSwitcher>
  )
}

export default App
```

### 凡例

- **共通背景色**: lightTheme では白(#ffffff)、darkTheme では暗い灰色(#121212)。
- **共通テキスト色**: lightTheme では黒(#000000)、darkTheme では白(#ffffff)。
- **ボタンデザイン**: テーマに応じて、異なる色やスタイルを適用します。例えば、lightTheme では明るい色、darkTheme では暗い色を使用するなど。

この方法により、アプリケーションにテーマ切り替え機能を簡単に組み込むことができます。また、`localStorage`を使用することで、ユーザーのテーマ選択を記憶し、アプリケーションの再訪時に同じテーマを適用することが可能です。

---

#### 疑問

では、Button Conponentのlight/darkのSwitch連動のデザインは、コンポーネントファイルでなくtheme.tsファイルで実装すれば運用的にも良いのでしょうか

#### 回答

Button コンポーネントの light/dark テーマに応じたスタイルは、`theme.ts`ファイルで定義することが望ましいです。これにより、テーマに基づくスタイルの一貫性が保たれ、コンポーネントファイルをシンプルに保つことができます。

以下に具体的なコード例を示します。

### `theme.ts`での Button スタイルの定義

`theme.ts` ファイルでは、light テーマと dark テーマで異なる Button スタイルを定義します。

```tsx
// theme.ts
import { createTheme } from "@mui/material/styles"

const commonButtonStyles = {
  // すべてのテーマで共通のButtonスタイル
}

export const lightTheme = createTheme({
  palette: {
    mode: "light",
    // その他のlightテーマ設定...
  },
  components: {
    MuiButton: {
      styleOverrides: {
        root: {
          ...commonButtonStyles,
          // lightテーマ特有のスタイル
          backgroundColor: "#e0e0e0",
          color: "#000",
          "&:hover": {
            backgroundColor: "#d5d5d5",
          },
        },
      },
    },
  },
})

export const darkTheme = createTheme({
  palette: {
    mode: "dark",
    // その他のdarkテーマ設定...
  },
  components: {
    MuiButton: {
      styleOverrides: {
        root: {
          ...commonButtonStyles,
          // darkテーマ特有のスタイル
          backgroundColor: "#424242",
          color: "#fff",
          "&:hover": {
            backgroundColor: "#383838",
          },
        },
      },
    },
  },
})
```

### テーマプロバイダーでの使用

アプリケーションのルートコンポーネントで、作成したテーマを`ThemeProvider`に適用します。

```tsx
// App.tsx または 他のルートコンポーネント
import React from "react"
import { ThemeProvider } from "@mui/material/styles"
import { lightTheme, darkTheme } from "./theme"
import Button from "@mui/material/Button"

function App() {
  // テーマモードの状態管理（lightかdarkか）
  // ここでは、簡単のために直接'string'を使用していますが、
  // 実際にはstateやcontextから取得することが一般的です。
  const themeMode = "light"

  return (
    <ThemeProvider theme={themeMode === "light" ? lightTheme : darkTheme}>
      <Button>My Button</Button>
      {/* その他のコンポーネント */}
    </ThemeProvider>
  )
}

export default App
```

このようにして、`theme.ts`で定義したテーマに基づいて、Button コンポーネントのスタイルが自動的に切り替わります。これにより、コンポーネントのスタイルをテーマに依存させることができ、より一貫性のある UI デザインを実現できます。

---

## Storybookへの導入

ここでは長くなるので、Storybookの詳細については割愛します。
詳細は[公式ドキュメント](https://storybook.js.org/docs/react/get-started/introduction)を参照してください。

次の機会に、Storybookの導入方法について説明させていただくかと思います。
