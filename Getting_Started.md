原文は[こちら](https://docs.julialang.org/en/v1.1/manual/getting-started/)

## Getting Started / さあ、はじめよう

| 原文（英語） | 訳文（日本語） |
|---|---|
| Julia installation is straightforward, whether using precompiled binaries or compiling from source. | Juliaのインストールはいたって単純です。プリコンパイルされたバイナリを使うかソースからコンパイルするかのいずれかの方法で行います。 |
| Download and install Julia by following the instructions at https://julialang.org/downloads/. | https://julialang.org/downloads/ に記載の指示に従い、Juliaのダウンロードとインストールを行ってください。|
| The easiest way to learn and experiment with Julia is by starting an interactive session (also known as a read-eval-print loop or "REPL") by double-clicking the Julia executable or running `julia` from the command line: | Juliaを学習したり試しに動かしたりするのに最も簡単な方法は、Juliaの実行ファイルをダブルクリックするかコマンドライン上で`julia`を実行してインタラクティブセッション（読み込み・評価・出力[read-eval-print] ループや「REPL」としても知られている）を開始することです:|

```julia
$ julia

               _
   _       _ _(_)_     |  Documentation: https://docs.julialang.org
  (_)     | (_) (_)    |
   _ _   _| |_  __ _   |  Type "?" for help, "]?" for Pkg help.
  | | | | | | |/ _` |  |
  | | |_| | | | (_| |  |  Version 1.1.1 (2019-05-16)
 _/ |\__'_|_|_|\__'_|  |  
|__/                   |


julia> 1 + 2
3

julia> ans
3
```

| 原文（英語） | 訳文（日本語） |
|---|---|
| To exit the interactive session, type `CTRL-D` (press the Control/`^` key together with the `d` key), or type `exit()`.  | インタラクティブセッションを終了するには、`Ctrl-D`とタイプする（コントロールキーか`^`キーと`d`キーを同時に押す）か、`exit()`をタイプします。|
| When run in interactive mode, `julia` displays a banner and prompts the user for input. | インタラクティブモードの場合、`julia`はバナーとユーザが入力するためのプロンプトを表示します。|
| Once the user has entered a complete expression, such as `1 + 2`, and hits enter, the interactive session evaluates the expression and shows its value. | ユーザが `1 + 2` のような完全形の式を入力しエンターキーを押すと、インタラクティブセッションは式を評価し値を示します。|
| If an expression is entered into an interactive session with a trailing semicolon, its value is not shown. | 末尾にセミコロンをつけた式をインタラクティブセッションに入力した場合は式の値を示しません。|
| The variable `ans` is bound to the value of the last evaluated expression whether it is shown or not. | 変数`ans`には、その値が示されているかどうかにかかわらず最後に評価された式の値が代入されます。|
| The `ans` variable is only bound in interactive sessions, not when Julia code is run in other ways. | 変数`ans`にはインタラクティブセッションでのみ代入され、Juliaのコードが他の手段で実行される場合には代入されません。|
| * | * |
| To evaluate expressions written in a source file `file.jl`, write `include("file.jl")`. | ソースファイル`file.jl`に書かれた式を評価するには、`include("file.jl")`と書きます。|
| * | * |
| To run code in a file non-interactively, you can give it as the first argument to the `julia` command: | ファイル内のコードを非対話型で実行する際は、`julia`コマンドの第一引数にファイルを指定することができます。|

```julia
$ julia script.jl arg1 arg2...
```

| 原文（英語） | 訳文（日本語） |
|---|---|
| As the example implies, the following command-line arguments to `julia` are interpreted as command-line arguments to the program `script.jl`, passed in the global constant `ARGS`. | 上記の例が示すように、`julia`に続くコマンドライン引数は`script.jl`プログラムに対するコマンドライン引数として解釈され、グローバル定数`ARGS`に渡されます。|
| The name of the script itself is passed in as the global `PROGRAM_FILE`. | スクリプト自体の名前はグローバル定数`PROGRAM_FILE`に引き継がれます。|
| Note that `ARGS` is also set when a Julia expression is given using the `-e` option on the command line (see the `julia` help output below) but `PROGRAM_FILE` will be empty. | また、コマンドライン上で`-e`オプションを使用した（`julia`ヘルプ参照）juliaの式が与えられたときも`ARGS`の値が設定されますが、`PROGRAM_FILE`は値なしということに留意ください。|
| For example, to just print the arguments given to a script, you could do this: | 例えば、あるスクリプトに付与された引数を出力するには、こうすればいいのです: |

```julia
$ julia -e 'println(PROGRAM_FILE); for x in ARGS; println(x); end' foo bar

foo
bar
```

| 原文（英語） | 訳文（日本語） |
|---|---|
| Or you could put that code into a script and run it: | あるいは、そのコードをスクリプトにして実行します。|

```julia
$ echo 'println(PROGRAM_FILE); for x in ARGS; println(x); end' > script.jl
$ julia script.jl foo bar
script.jl
foo
bar
```
| 原文（英語） | 訳文（日本語） |
|---|---|
| The`--`delimiter can be used to separate command-line arguments intended for the script file from arguments intended for Julia: | 区切り文字`--`はスクリプトファイルのコマンドライン引数とJuliaの引数を分けるために使います。|

```julia
$ julia --color=yes -O -- foo.jl arg1 arg2..
```

| 原文（英語） | 訳文（日本語） |
|---|---|
| See also [Scripting](https://docs.julialang.org/en/v1/manual/faq/#man-scripting-1) for more information on writing Julia scripts. | Juliaのスクリプティングについての詳細は[スクリプティング](https://docs.julialang.org/en/v1/manual/faq/#man-scripting-1)（訳注：未翻訳）の項も参照してください。|
| Julia can be started in parallel mode with either the -p or the `--machine-file` options. | `-p`か`--machine-file file`のいずれかのオプションを使用することでJuliaをパラレルモードで起動することができます。|
| `-p n` will launch an additional n worker processes, while`--machine-file file` will launch a worker for each line in file `file`. | `-p n`は追加のワーカプロセスを実行します。一方、`--machine-file file`は`file`ファイル内の各行のワーカを実行します。|
| The machines defined in `file` must be accessible via a password-less `ssh` login, with Julia installed at the same location as the current host. | ファイル内で定義されたマシンには、Juliaを現在のホストと同じ場所にインストールした状態で、パスワードのない`ssh`ログインを経由してアクセスできるようにする必要があります。 |
| Each machine definition takes the form `[count*] [user@]host[:port] [bind_addr[:port]]`. | それぞれのマシンの定義は`[count*] [user@]host[:port] [bind_addr[:port]]`の形をとります。 |
| `user` defaults to current user, `port` to the standard ssh port. | `user`のデフォルトは現在のユーザ、`port`は標準sshポートです。|
| `count` is the number of workers to spawn on the node, and defaults to 1. | `count`はノードにスポーンするワーカの数で、デフォルトは1です。|
| The optional bind-to bind_addr[:port] specifies the IP address and port that other workers should use to connect to this worker. | 任意の`bind-to bind_addr[:port]`では、他のワーカがこのワーカに接続するために使用する必要のあるIPアドレスとポートを指定します。|
| If you have code that you want executed whenever Julia is run, you can put it in ~/.julia/config/startup.jl: | Juliaを動かすたびに実行したいコードがある場合、そこに`~/.julia/config/startup.jl`を指定します。|

```julia
$ echo 'println("Greetings! 你好! 안녕하세요?")' > ~/.julia/config/startup.jl
$ julia
Greetings! 你好! 안녕하세요?

...
```
| 原文（英語） | 訳文（日本語） |
|---|---|
| There are various ways to run Julia code and provide options, similar to those available for the perl and ruby programs: | Juliaコードを実行したり、オプションを提供したりするには様々な方法がありますが、それはperlやrubyのプログラムでもその方法を利用できるのに似ています。|

```julia
julia [switches] -- [programfile] [args...]
```


| Switch <br> スイッチ | Description <br> 説明 |
----|---- 
| `-v`, `--version`	| Display version information <br> バージョン情報の表示 |
| `-h`, `--help` | Print this message <br> このメッセージを出力 |
| `--project[={<dir>\|@.}]` | Set `<dir>` as the home project/environment. The default `@.` option will search through parent directories until a `Project.toml` or `JuliaProject.toml` file is found. <br> `<dir>`をホームのプロジェクトおよび環境に設定。デフォルトの `@.` オプションを使うと`Project.toml`か`JuliaProject.toml`ファイルが見つかるまで親フォルダに遡って検索。|
| `-J`, `--sysimage <file>`	| Start up with the given system image file <br> システムイメージファイルを使用して起動 |
| `-H`, `--home <dir>` | Set location of julia executable <br> juliaの実行ファイルの位置を設定 |
| `--startup-file={yes\|no}` | Load `~/.julia/config/startup.jl` <br> ~/.julia/config/startup.jlのロード |
| `--handle-signals={yes\|no}` | Enable or disable Julia's default signal handlers <br> Juliaのデフォルトのシグナルハンドラを有効/無効に設定|
| `--sysimage-native-code={yes\|no}`	| Use native code from system image if available <br> システム画像からのネイティブコードを使用（利用可能な場合）|
| `--compiled-modules={yes\|no}` | Enable or disable incremental precompilation of modules <br> モジュールのインクリメンタルプリコンパイルを有効/無効に設定 |
| `-e`, `--eval <expr>`	| Evaluate `<expr>` <br> `<expr>`を評価 |
| `-E, --print <expr>` | Evaluate `<expr>` and display the result <br> 式を評価し結果を表示 |
| `-L, --load <file>`	| Load `<file>` immediately on all processors <br> すべてのプロセッサにおける`<file>`を即時にロード |
| `-p, --procs {N\|auto}` | Integer value `N` launches N additional local worker processes; auto launches as many workers as the number of local CPU threads (logical cores) <br> 整数値Nの場合はNの数だけ追加されたローカルのワーカプロセスを実行; autoの場合はローカルのCPUスレッド（論理コア）の数と同じ数のワーカを実行 |
| `--machine-file <file>`	| Run processes on hosts listed in `<file>` <br> `<file>`にリストされたホスト上でプロセスを実行 |
| `-i` | Interactive mode; REPL runs and `isinteractive()` is true <br> インタラクティブモード; REPLでの実行や`isinteractive()`と同様 |
| `-q, --quiet` | Quiet startup: no banner, suppress REPL warnings <br> 静かなスタートアップ（バナーなし、REPLの警告を抑制）
| `--banner={yes\|no\|auto}` | Enable or disable startup banner <br> スタートアップ時のバナーを有効/無効に設定 |
| `--color={yes\|no\|auto}`	| Enable or disable color text <br> テキストのカラー表示を有効/無効に設定 |
| `--history-file={yes\|no}`	| Load or save history <br> 履歴のロード/セーブ|
| `--depwarn={yes\|no\|error}` | Enable or disable syntax and method deprecation warnings (`error` turns warnings into errors) <br> 構文およびメソッド違反の警告を有効/無効に設定（`error`にすると警告がエラーとなる）|
| `--warn-overwrite={yes\|no}`	| Enable or disable method overwrite warnings <br> メソッドの上書き警告を有効/無効に設定|
| `-C, --cpu-target <target>`	| Limit usage of CPU features up to `<target>`; set to help to see the available options <br> CPU featuresの使用を`<target>`を上限に設定（利用可能なオプションはヘルプを参照）|
| `-O, --optimize={0,1,2,3}` | Set the optimization level (default level is 2 if unspecified or 3 if used without a level) <br> 最適化レベルを設定（このスイッチを指定しない場合、デフォルトの最適化レベルは2。レベルを指定せずにこのスイッチを使用する場合、デフォルトの最適化レベルは3）|
| `-g, -g <level>` | Enable / Set the level of debug info generation (default level is 1 if unspecified or 2 if used without a level) <br> デバッグ情報生成レベルの設定（このスイッチを指定しない場合、デフォルトのレベルは1。レベルを指定せずにこのスイッチを使用する場合、デフォルトのレベルは2）|
| `--inline={yes\|no}`	| Control whether inlining is permitted, including overriding `@inline` declarations <br> インライン化の許可を制御（`@inline`での定義のオーバーライドを含む）|
| `--check-bounds={yes\|no}`	| Emit bounds checks always or never (ignoring declarations) <br> 境界チェックを常に実行する/しない（定義を無視）|
| `--math-mode={ieee,fast}`	| Disallow or enable unsafe floating point optimizations (overrides `@fastmath` declaration) <br> 不安定な浮動小数点の最適化を許可する/しない（`@fastmath`での定義をオーバーライド）|
| `--code-coverage={none\|user\|all}`	| Count executions of source lines <br> ソースコード行の実行数をカウント |
| `--code-coverage`	| equivalent to `--code-coverage=user` <br> `--code-coverage=user`と同様 |
| `--track-allocation={none\|user\|all}` | Count bytes allocated by each source line <br> 各ソースコード行でアロケートされたバイト数をカウント |
| `--track-allocation` | equivalent to `--track-allocation=user` <br> `--track-allocation=user`と同様 |


### ! Julia 1.1
| 原文（英語） | 訳文（日本語） |
|---|---|
| In Julia 1.0, the default --project=@. option did not search up from the root directory of a Git repository for the Project.toml file. From Julia 1.1 forward, it does. | Julia 1.0ではデフォルトの`--project=@.`オプションは`Project.toml`ファイルを検索する際Gitのレポジトリのルートディレクトリからは検索しません。Julia 1.1以降はそのような仕様になっています。|

## Resources / リソース
| 原文（英語） | 訳文（日本語） |
|---|---|
| A curated list of useful learning resources to help new users get started can be found on the learning page of the main Julia web site. | 新規ユーザが始める助けとなるような役に立つラーニングリソースのコンテンツをまとめたリストがメインのJuliaウェブサイト上の[learning](https://julialang.org/learning/)（訳注：未翻訳）にあります。|

| 原文（英語） | 訳文（日本語） |
|---|---|
| Previous: Julia v1.1 Release Notes | 前: Julia v1.1 リリースノート |
| Next: Variables | 次: 変数 |
 

