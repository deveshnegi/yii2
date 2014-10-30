Yii2 コアフレームワークのコードスタイル
=======================================

下記のコードスタイルが Yii 2.x コアと公式エクステンションの開発に用いられています。
コアに対してプルリクエストをしたいときは、これを使用することを考慮してください。
私たちは、あなたが自分のアプリケーションにこのコードスタイルを使うことを強制するものではありません。
あなたにとってより良いコードスタイルを自由に選んでください。

なお、CodeSniffer のための設定をここで入手できます: https://github.com/yiisoft/yii2-coding-standards

1. 概要
-------

全体として、私たちは [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md) 互換のスタイルを使っていますので、
[PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md) に適用されることは、すべて私たちのコードスタイルにも適用されます。

- ファイルは `<?php` または `<?=` のタグを使わなければならない。
- ファイルの末尾には一個の改行があるべきである。
- ファイルは PHP コードに対して BOM 無しの UTF-8 だけを使わなければならない。
- コードはインデントに、タブではなく、4個の空白を使わなければならない。
- クラス名は `StudlyCaps` で宣言されなくてはならない。
- クラス内の定数はアンダースコアで区切られた大文字だけで宣言されなければならない。
- メソッド名は `camelCase` で宣言されなければならない。
- プロパティ名は `camelCase` で宣言されなければならない。
- プロパティ名は private である場合はアンダースコアで開始しなければならない。
- `else if` ではなく常に `elseif` を使用すること。

2. ファイル
-----------

### 2.1. PHP タグ

- PHP コードは `<?php ?>` または `<?=` タグを使わなければなりません。他のタグ、例えば `<?` は使ってはなりません。
- ファイルが PHP コードのみを含む場合は、末尾の `?>` を含むべきではありません。
- 各行の末尾に空白を追加しないこと。
- PHP コードを含む全てのファイルの名前は `.php` という拡張子で終るべきです。

### 2.2. 文字エンコーディング

PHP コードは BOM 無しの UTF-8 のみを使わなければなりません。

3. クラス名
-----------

クラス名は `StudlyCaps` で宣言されなければなりません。例えば、`Controller`、`Model`。

4. クラス
---------

ここで "クラス" という用語はあらゆるクラスとインタフェイスを指すものとします。

- クラスは `CamelCase` で命名されなければなりません。
- 中括弧は常にクラス名の下の行に書かれるべきです。
- 全てのクラスは PHPDoc に従ったドキュメンテーションブロックを持たなければなりません。
- クラス内のすべてのコードは単一のタブによってインデントされなければなりません。
- 単一の PHP ファイルにはクラスが一つだけあるべきです。
- 全てのクラスは名前空間に属すべきです。
- クラス名はファイル名と一致すべきです。クラスの名前空間はディレクトリ構造と一致すべきです。

```php
/**
 * ドキュメンテーション
 */
class MyClass extends \yii\Object implements MyInterface
{
    // code
}
```

### 4.1. 定数

クラスの定数はアンダースコアで区切られた大文字だけで宣言されなければなりません。
例えば:

```php
<?php
class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```
### 4.2. プロパティ

- Public なクラスメンバーを宣言するときは `public` キーワードを明示的に指定します。
- Public および protected な変数はクラスの冒頭で、すべてのメソッドの宣言に先立って宣言されるべきです。
  Private な変数もまたクラスの冒頭で宣言されるべきですが、
  変数がクラスのメソッドのごく一部分にのみ関係する場合は、変数を扱う一群のメソッドの直前に追加してもかまいません。
- クラスにおけるプロパティの宣言の順序は public から始まり、protected、private と続くべきです。
- より読みやすいように、プロパティの宣言は空行を挟まずに続け、プロパティ宣言とメソッド宣言のブロック間には2行の空行を挟むべきです。
- Private 変数は `$_varName` のように名付けるべきです。
- Public なクラスメンバーとスタンドアロンな変数は、先頭を小文字にした `$camelCase` で名付けるべきです。
- 説明的な名前を使うこと。`$i` や `$j` のような変数は使わないようにしましょう。

例えば:

```php
<?php
class Foo
{
    public $publicProp;
    protected $protectedProp;
    private $_privateProp;
}
```

### 4.3. メソッド

- 関数およびメソッドは、先頭を小文字にした `camelCase` で名付けるべきです。
Functions and methods should be named using `camelCase` with first letter lowercase.
- 名前は、関数の目的を示す自己説明的なものであるべきです。
- クラスのメソッドは常に `private`、`protected` または `public` を使って、可視性を宣言すべきです。`var` は許可されません。
- 関数の開始の中括弧は関数宣言の次の行に置くべきです。

~~~
/**
 * ドキュメンテーション
 */
class Foo
{
    /**
     * ドキュメンテーション
     */
    public function bar()
    {
        // コード
        return $value;
    }
}
~~~

### 4.4 Doc ブロック

`@param`、`@var`、`@property` および `@return` は `boolean`、`integer`、`string`、`array` または `null` として型を宣言しなければなりません。
`Model` または `ActiveRecord` のようなクラス名を使うことも出来ます。
型付きの配列に対しては `ClassName[]` を使います。

### 4.5 コンストラクタ

- PHP 4 スタイルのコンストラクタの代りに、`__construct` が使われるべきです。

## 5 PHP

### 5.1 型

- PHP の全ての型と値には小文字を使うべきです。このことは、`true`、`false`、`null` および `array` にも当てはまります。

連想配列に対しては次の書式を使います:

```php
$config = [
    'name'  => 'Yii',
    'options' => ['usePHP' => true],
];
```

既存の変数の型を変えることは悪い慣行であるとみなされます。本当に必要でない限り、そのようなコードを書かないように努めましょう。


```php
public function save(Transaction $transaction, $argument2 = 100)
{
    $transaction = new Connection; // 駄目
    $argument2 = 200; // 良い
}
```

### 5.2 文字列

- 変数およびシングルクォーツを含まない文字列には、シングルクォーツを使います。

```php
$str = 'Like this.';
```

- 文字列がシングルクォーツを含む場合は、余分なエスケープを避けるためにダブルクォーツを使ってもかまいません。

#### 変数置換

```php
$str1 = "Hello $username!";
$str2 = "Hello {$username}!";
```

下記は許可されません:

```php
$str3 = "Hello ${username}!";
```

#### 連結

文字列を連結するときは、ドットの周囲に空白を追加します:

```php
$name = 'Yii' . ' Framework';
```

文字列が長い場合、書式は以下のようにします:

```php
$sql = "SELECT *"
    . "FROM `post` "
    . "WHERE `id` = 121 ";
```

### 5.3 配列

配列には、開発者は PHP 5.4 の短縮構文を使用しています。

#### 添え字配列

- 負の数を配列のインデックスに使わないこと。

配列を宣言するときは、下記の書式を使います:

```php
$arr = [3, 14, 15, 'Yii', 'Framework'];
```

一つの行に多すぎる要素がある場合は:

```php
$arr = [
    3, 14, 15,
    92, 6, $test,
    'Yii', 'Framework',
];
```

#### 連想配列

連想配列には下記の書式を使います:

```php
$config = [
    'name'  => 'Yii',
    'options' => ['usePHP' => true],
];
```

### 5.4 制御文

- 制御文の条件は括弧の前と後に一つの空白を持たなければなりません。
- 括弧の中の演算子は空白によって区切られるべきです。
- 開始の括弧は同じ行に置きます。
- 終了の括弧は新しい行に置きます。
- 単一行の文に対しても、常に括弧を使用します。

```php
if ($event === null) {
    return new Event();
} elseif ($event instanceof CoolEvent) {
    return $event->instance();
} else {
    return null;
}

// 下記は許容されません:
if (!$model && null === $event)
    throw new Exception('test');
```

#### switch

switch には下記の書式を使用します:

```php
switch ($this->phpType) {
    case 'string':
        $a = (string)$value;
        break;
    case 'integer':
    case 'int':
        $a = (integer)$value;
        break;
    case 'boolean':
        $a = (boolean)$value;
        break;
    default:
        $a = null;
}
```

### 5.5 関数呼び出し

```php
doIt(2, 3);

doIt(['a' => 'b']);

doIt('a', [
    'a' => 'b',
    'c' => 'd',
]);
```

### 5.6 無名関数 (lambda) の宣言

`function`/`use` トークンと開始括弧の間の空白に注意:

```php
// 良い
$n = 100;
$sum = array_reduce($numbers, function ($r, $x) use ($n) {
    $this->doMagic();
    $r += $x * $n;
    return $r;
});

// bad
$n = 100;
$mul = array_reduce($numbers, function($r, $x) use($n) {
    $this->doMagic();
    $r *= $x * $n;
    return $r;
});
```

ドキュメンテーション
--------------------

- ドキュメンテーションの文法については [phpDoc](http://phpdoc.org/) を参照してください。
- ドキュメンテーションの無いコードは許容されません。
- 全てのクラスファイルは、ファイルレベルの doc ブロックを各ファイルの先頭に持ち、
  クラスレベルの doc ブロックを各クラスの直前に持たなければなりません。
- メソッドが何も返さないときは `@return` を使う必要はありません。
- `yii\base\Object` から派生するクラスのすべての仮想プロパティは、クラスの doc ブロックで `@property` タグでドキュメントされます。
  これらの注釈は、`build` ディレクトリで `./build php-doc` コマンドを走らせることにより、
  対応する getter や setter の `@return` や `@param` タグから自動的に生成されます。
  getter や setter によって導入されるプロパティに対してドキュメンテーションのメッセージを
  明示的に与えるために `@property` タグを追加することが出来ます。
  これは `@return` において記述されているのとは違う説明を与えたい場合に有用です。
  例えば:

  ```php
    <?php
    /**
     * 全ての属性または一つの属性についてエラーを返す。
     * @param string $attribute 属性の名前。全ての属性についてエラーを取得するためには null を使う。
     * @property array 全ての属性に対するエラーの配列。エラーが無い場合は空の配列が返される。
     * 結果は二次元の配列である。詳細な説明は [[getErrors()]] を参照。
     * @return array 全ての属性または特定の属性に対するエラー。エラーが無い場合は空の配列が返される。
     * 全ての属性に対する配列を返す場合、結果は、下記のように、二次元の配列である:
     * ...
     */
    public function getErrors($attribute = null)
  ```

>Note|注意: これ以降、読みやすさを考慮してドキュメンテーションの内容を日本語に翻訳していますが、
コアコードや公式エクステンションに対して寄稿する場合は、当然ながら、コメントは英語だけを
使わなければなりません。

#### ファイル

```php
<?php
/**
 * @link http://www.yiiframework.com/
 * @copyright Copyright (c) 2008 Yii Software LLC
 * @license http://www.yiiframework.com/license/
 */
```

#### クラス

```php
/**
 * Component は *property*、*event* および *behavior* の機能を提供する基底クラスである。
 *
 * @include @yii/docs/base-Component.md
 *
 * @author Qiang Xue <qiang.xue@gmail.com>
 * @since 2.0
 */
class Component extends \yii\base\Object
```


#### 関数 / メソッド

```php
/**
 * イベントに対してアタッチされたイベントハンドラのリストを返す。
 * 返された [[Vector]] オブジェクトを操作して、ハンドラを追加したり削除したり出来る。
 * 例えば、
 *
 * ~~~
 * $component->getEventHandlers($eventName)->insertAt(0, $eventHandler);
 * ~~~
 *
 * @param string $name イベントの名前
 * @return Vector イベントにアタッチされたハンドラのリスト
 * @throws Exception イベントが定義されていない場合
 */
public function getEventHandlers($name)
{
    if (!isset($this->_e[$name])) {
        $this->_e[$name] = new Vector;
    }
    $this->ensureBehaviors();
    return $this->_e[$name];
}
```

#### Markdown

上記の例に見られるように、phpDoc コメントの書式設定には markdown を使っています。

ドキュメンテーションの中でクラス、メソッド、プロパティをクロスリンクするために使う追加の文法があります:

- `'[[canSetProperty]] ` は、同じクラス内の `canSetProperty` メソッドまたはプロパティへのクロスリンクを生成します。
- `'[[Component::canSetProperty]]` は、同じ名前空間内の `Component` クラスの `canSetProperty` メソッドへのクロスリンクを生成します。
- `'[[yii\base\Component::canSetProperty]]` は、`yii\base` 名前空間の`Component` クラスの `canSetProperty` メソッドへのクロスリンクを生成します。
- `'[[Component]]` は、同じ名前空間内の `Component` クラスへのクロスリンクを生成します。ここでも、クラス名に名前空間を追加することが可能です。

上記のリンクにクラス名やメソッド名以外のラベルを付けるために、次の例で示されている書式を使うことが出来ます:

```
... [[header|ヘッダセル]] に表示されているように
```

`|` の前の部分がメソッド、プロパティ、クラスへの参照であり、`|` の後ろの部分がリンクのラベルです。

下記の書式を使って公式ガイドにリンクすることも可能です:

```markdown
[ガイドへのリンク](guide:file-name.md)
[ガイドへのリンク](guide:file-name.md#subsection)
```


#### コメント

- 一行コメントは `//` で開始されるべきです。`#` は使いません。
- 一行コメントはそれ自身の行に置くべきです。

追加の規則
----------

### `=== []` 対 `empty()`

かの名時は `empty()` を使います。

### 複数の return ポイント

条件のネストが込み入ってきた場合は、早期の return を使います。メソッドが短いものである場合は、特に問題にしません。

### `self` 対 `static`

以下の場合を除いて、常に `static` を使います:

- 定数へのアクセスには `self` を使わなければなりません: `self::MY_CONSTANT`
- private な静的プロパティへのアクセスには `self` を使わなければなりません: `self::$_events`
- 再帰呼出しにおいて、拡張クラスの実装ではなく、現在のクラスの実装を再び呼び出したいときには、`self` を使うことが許可されます。

### 「何かをするな」を示す値

コンポーネントに対して「何かをしない」という設定を許可するプロパティは `false` の値を受け入れるべきです。`null`、`''`、または `[]` は、そのような値として受け取られるべきではありません。

### ディレクトリ/名前空間の名前

- 小文字を使います。
- オブジェクトを表すものには複数形の名詞を使います (例えば、validators)
- 機能や特徴を表す名前には単数形を使います (例えば、web)