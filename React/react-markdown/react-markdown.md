# react-markdown

## ソースコードのハイライト対応

1. react-syntax-highlighter をインストール

```sh
npm i -D react-syntax-highlighter @types/react-syntax-highlighter
```

2. CodeBlock.tsx(src/components/CodeBlock.tsx)を作成

```ts
import { Prism as SyntaxHighlighter } from "react-syntax-highlighter";
import { okaidia } from "react-syntax-highlighter/dist/cjs/styles/prism";

const CodeBlock = ({ inline, className, children }) => {
  if (inline) {
    return <code className={className}>{children}</code>;
  }
  const match = /language-(\w+)/.exec(className || "");
  const lang = match && match[1] ? match[1] : "";
  return (
    <SyntaxHighlighter
      style={okaidia}
      language={lang}
      children={String(children).replace(/\n$/, "")}
    />
  );
};

export default CodeBlock;
```

3. ReactMarkdown の code に CodeBlock のコンポーネントを設定

```ts
return (
  <ReactMarkdown
    children={markdown}
    components={{
      code: CodeBlock,
    }}
  />
);
```

[参考サイト](https://goodlife.tech/posts/react-markdown-code-highlight.html)

## ソースコードのファイル名を表示する

ソースコードのハイライト対応の続き

1. styled-components を使うのでインストール

```sh
npm install --save styled-components
```

[styled-components の分かりやすいサイト](https://zenn.dev/syu/articles/0f92abf7f0b5c5)

2. コードブロックを囲む枠とファイル名のスタイルを定義

```ts
import styled from "styled-components";

const CodeBlockWrapper = styled.div`
  position: relative;
  margin: 40px 0;
`;

const CodeBlockTitle = styled.div`
  display: inline-block;
  position: absolute;
  top: -2.1em;
  left: 0;
  background: #323e52;
  padding: 0.8em;
  color: #ffffffe6;
  border-radius: 6px 6px 0 0;
  font-size: 0.8rem;
`;
```

3. 上記のラッパで囲む

```ts:src/components/CodeBlock.tsx
  const match = /language-(\w+)(:.+)/.exec(className || '');
  const lang = match && match[1] ? match[1] : '';
  const name = match && match[2] ? match[2].slice(1) : '';
  return (
    <CodeBlockWrapper>
      <CodeBlockTitle>{name}</CodeBlockTitle>
      <SyntaxHighlighter
        style={dark}
        language={lang}
        children={String(children).replace(/\n$/, '')}
      />
    </CodeBlockWrapper>
  );
```

参考サイト
https://goodlife.tech/posts/react-markdown-code-highlight.html#%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E5%90%8D%E3%82%92%E8%A1%A8%E7%A4%BA%E3%81%99%E3%82%8B

## TODO

下記のサイトの diff もできるようにしたい
https://goodlife.tech/posts/react-markdown-code-highlight.html#diff%E3%82%B7%E3%83%B3%E3%82%BF%E3%83%83%E3%82%AF%E3%82%B9%E3%83%8F%E3%82%A4%E3%83%A9%E3%82%A4%E3%83%88
