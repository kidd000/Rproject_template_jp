# Rproject_template_jp



<div style="text-align: right;">
  2021/05/20 本間祥吾
</div>




## 概要



このリポジトリは、研究プロジェクトのテンプレートフォルダです。

ゼミ内で分析のやり方、プロジェクト管理の仕方をシェアすることを主な目的としています。

実験、シミュレーション、データ分析を行うことを想定したフォルダ構成です。

既にいくつかのサンプルコードを用意しており、以下のプロセスを実行することができます。

- シミュレーションによるダミーデータの発生
- Rによるデータの分析 & 可視化
- stanによるモデルのフィッティング & フィッティング結果の整理

シミュレーションはRかPython、分析はRで行うことを想定しています。

シミュレーション & フィッティングのモデルは、強化学習（Q学習）モデルを用意しています（※ 拡散過程モデルも現在準備中です…）。



「このやり方でやれ」という絶対のルールではなく、各自柔軟に分析の仕方やフォルダの構成を変えてください。特に、RやPythonでの分析のやり方については日進月歩なので、「この方がわかりやすい」と思ったら、どんどん自分なりにアレンジ、取り入れてください（私もなるべくアップデートしていくようにします）。



## 大まかなフォルダの構成

プロジェクトディレクトリ直下のフォルダのみ表示。詳細は、「フォルダの詳細」を参照。


```
Rproject_template_jp
├ README.md
├ Rproject_template_jp.Rproj
├ Analysis_Script
├ Data
├ Document
├ Experiment
├ Output
├ Simulation_Code
```



- README.md：本ファイルです
- Rproject_template_jp.Rproj
  - Rプロジェクトファイルです。これをクリックすると、RStudioが起動されます。
  - 自分の分析を行う際には、このファイルを削除して、自分の.Rprojを作成してください（詳しくは、「分析のやり方について」を参照）
- Analysis_Script
  - 分析用の.Rファイル、.Rmdファイル、.pyファイルを置くフォルダです。
  - 分析に使う、自作関数もここに置きます。
  - モデルフィッティングで使う.stanファイル
- Data
  - 分析対象のデータを置くフォルダです。シミュレーション結果や、新しく整形したcsvファイルもここに置いておきます。
  - 実験のローデータは、この中に「RawData」というフォルダを作成して、その中に置きましょう（そして、<u>**絶対に変更しない！**</u>）。
- Document
  - Optionalです。プロジェクトに関係する文書を雑多に置いておきます。
  - 書いている論文の原稿とか、引用論文のpdfとかを置くといいかもしれません。
- Experiment
  - 実験で使ったすべてのファイル（プログラム、マテリアル、同意書 etc）を置いておく場所です。
- Output
  - 分析の出力結果を保存しておく場所です。
  - 特に、png形式で出力したFigureを保存することを想定しています。
- Simulation_Code
  - シミュレーション用のコードを置く場所です。





## フォルダの詳細



```
Rproject_template_jp
├ README.md
├ Rproject_template_jp.Rproj
│
├ Analysis_Script
│  ├ _functions_common
│     ├ ...
│
│  ├ _functions_project
│     ├ ...
│ 
│  ├ _functions_ModelBasedAnalysis 
│     ├ ...
│
│  ├ Models_Stan
│     ├ basic_RL.stan
│
│  ├ Rproject_template.Rmd
│  ├ Run_check_rhat.R
│  ├ Run_csv_generator.R
│  ├ Run_mcmc_sampling.R
│  ├ Run_posterior_traceplot_generator.R
│  
├ Data
│  ├ DummyData_RL
│     ├ ...
│
│  ├ Models_Results
│     ├ basic_RL
│
│  ├ PGG_Evo
│     ├ ...
│
├ Document
├ Experiment
├ Output
├ Simulation_Code
│  ├ PGG_Evolution.py
│  ├ generate_DummyData_RL.R
│  ├ generate_DummyData_RL.py
```




### Rproject_template_jp.Rproj

- Rで分析を行う際には、プロジェクトディレクトリ直下に、.Rprojファイルを置くことをおすすめします。
- これをクリックすると、RStudioが起動されます。
- 自分の分析を行う際には、このファイルを削除して、自分の.Rprojを作成してください。



### Analysis_Script

- データ分析用の各種.Rファイルや.Rmdファイルを置く場所です。
- 分析で使用する自作関数も、_functionsというフォルダの中にまとめて置いています。



\_functions_common

- 他のプロジェクトでも共通で使う関数群をここに置きます。



\_functions_project

- プロジェクトで使う、分析用の関数群をここに置きます。



\_functions_ModelBasedAnalysis

- モデルフィッティングで使う関数群をここに置いています。
- Run_\*\*.R という関数で実行されます（後述）。



Models_Stan

- .stanファイルを置く場所です。
  - basicRL.stan：強化学習（Q学習）をフィッティングするためのstanファイルです。パラメータは、学習率$\alpha$と逆温度$\beta$です。



Rproject_template.Rmd

- 分析で使う.Rmdのサンプルです。
- 詳しい内容については「分析のやり方について（案）」を参照してください。



Run_check_rhat.R

- stanオブジェクトを読み込んで、Rhatが1.1以上のパラメータを抜き出し、csvで保存します。
- 保存先は、「Data/Models_Results/モデル名」フォルダです。



Run_csv_generator.R

- stanオブジェクトを読み込んで、推定結果をcsvファイルとして保存します。
- summary(fit)$summaryとほぼ同じ出力が、そのままcsvとして保存されます。
- 保存先は、「Data/Models_Results/モデル名」フォルダです。



Run_mcmc_sampling.R

- rstanでMCMCを実行し、結果をstanオブジェクトとして、「Data/Models_Results/モデル名」フォルダに保存します。



Run_posterior_traceplot_generator.R

- stanオブジェクトを読み込んで、事後分布とトレースプロットをpng形式で保存します。
- 今のところ、参加者ごとに1つのpngファイルが出力されるように設定されています。ここは各自で関数を書いて、柔軟に対応してください。
- 保存先は、「Data/Models_Results/モデル名」フォルダです。



### Data

- 分析対象のデータを置く場所です。シミュレーション結果や、新しく整形したcsvファイルもここに置いておきます。
- 実験のローデータは、「RawData」というフォルダを作成して、その中に置きましょう
- そして、<u>**ローデータは絶対に変更しないこと**</u>。基本的には、RやPythonで読み込んで、その中で処理していくこと。どうしても、直接ファイルをいじりたい場合は、「RawData」を丸ごとコピーして、コピーした方のファイルをいじること。



DummyData_RL

- generate_DummyData_RL.Rを実行すると生成されます。
- 強化学習のシミュレーション結果が、csvファイルとして保存されます。



Models_Results

- stanのモデルフィッティングの結果を保存するフォルダです。

- Run_\*\*.R を実行すると、「Data/Models_Results/モデル名」フォルダが作成され、その下に各種結果が生成されます。



PGG_Evo

- PGG_Evolution.pyを実行すると生成されます。



### Document

- Optionalです。プロジェクトに関係する文書を雑多に置いておきます。
- 書いている論文の原稿とか、引用論文のpdfとかを置くといいかもしれません。



### Experiment

- 実験で使ったすべてのファイル（プログラム、マテリアル、同意書 etc）を置いておく場所です。

  ※ 個人情報が書かれたものは、パスワードつきzipファイルにして保管すること。



### Output

- 分析の出力結果を保存しておく場所です。
- 特に、png形式で出力したFigureを置くことを想定しています。



### Simulation_Code

- シミュレーション用のコードを置く場所です。



PGG_Evolution.py

- 公共財問題ゲームの最もベーシックな進化シミュレーションを実行するファイルです。PythonのClassを使って進化シミュレーションを書いた例です。
  - 集団形成、one-shotの公共財問題ゲーム、自然選択、突然変異が組み込まれています。



generate_DummyData_RL.R

- 強化学習（Q学習）のシミュレーションを実行するファイルです。
- Data/DummyData_RLフォルダに結果が生成されます。



 generate_DummyData_RL.py 

- 強化学習（Q学習）のシミュレーションを実行するファイルです。
- 中身は、generate_DummyData_RL.Rと同じです。PythonのClassを使ってシミュレーションを書いた例です。



## 分析のやり方について（案）



分析はRで行うことを想定しています。また、これまで私が「こう書くとわかりやすい、効率的だ」と感じた書き方をしています（本で勉強したというわけでもないので、ほぼ我流です）。もっと良いやり方があったら、ご自身で書き換えてください & そのやり方を教えて下さい。

以下、サンプルコードの使い方も合わせて、基本的な分析の手順案を述べていきます。



### 基本的な発想

- Tidyverseのパッケージを使う
  - Tidyverse … 整然データ (tidy data) を扱うためにデザインされたパッケージ群です。直感的でわかりやすく（人によりますが）、同じ機能をもつRの基本関数に比べて高速です。
    - Tidyverseについて https://heavywatal.github.io/rstats/programming.html
    - 整然データについて https://speakerdeck.com/fnshr/zheng-ran-detatutenani
  - デメリットとしては、開発が激しいのでバージョン管理が難しいことが挙げられます。アップデートで昔使えた関数が使えなくなる…なんてこともそのうち起こるかもしれない（今のところ、非推奨になった関数はあっても、使用できなくなった関数はほとんど見当たらない）。
  - 毎回以下を宣言して、パッケージを読み込む



```r
library(tidyverse)
```



- パスの作成では、hereパッケージを使う

  - hereパッケージについて https://uribo.hatenablog.com/entry/2018/01/25/082000

  - .Rprojファイルがあるディレクトリを起点にしたパスを作成してくれます。相対パスと絶対パスの中間みたいな機能です。
  - hereパッケージを使う2つのメリット
    1. OS間でのパスの区切り文字問題を解決（Windowsなら"\\", UNIXなら "/"で互換性がないことが多い）
    2. Rmarkdownのワーキングディレクトリ問題を解決

    - 普通は.Rprojファイルが置かれているディレクトリがワーキングディレクトリになるが、Rmarkdownはknit時に「そのRmarkdownファイルが置かれている場所」がワーキングディレクトリになってしまう。
    - そうすると、Rmarkdownファイルと.Rファイルで、パスの書き方を変えなければならないので、面倒くさい。
    - そのため、毎回here()関数で、.Rprojを起点にしたパスを作成する。



- 処理のコピペを避けるため、なるべく関数化する。

  - 3回以上同じ処理を書くなら、関数化したほうがいいらしいです（出典は忘れましたがどっかで見ました）。実際、コピペはヒューマンエラーが入り込む余地ができる上、コードも冗長になります。
  - 関数をどこで定義するか
    - 同じ関数を複数のファイル間で使いまわすことも多いです。この際、関数の定義を毎回コピペしていたら本末転倒です。
    - そのため、別のディレクトリに関数を別ファイルとして定義して、それらを冒頭で読み込むことを推奨します。
      - 基本的に、1つの関数を1つの.Rファイルで保存するとよいです（ファイル名と関数名を一致させましょう）。
      - 1つのファイルに複数の関数を書くこともできますが、時間が経つとどのファイルに書いていたかが混乱するので、ファイル数が増えるのは気にせず、
    - このディレクトリでは、以下の3つに分けて保存しています。
      - Analysis_Script/_functions_common
      - Analysis_Script/\_functions_project
      - Analysis_Script/\_functions_ModelBasedAnalysis

  - とはいっても関数化は難しいです。何を引数にするか、汎用関数にするのか、処理をいくつの関数に分けるか…など決めないといけないことがたくさんあり、それだけで認知負荷が高いので、時間がかかりそうなら関数化は一旦止めておきましょう。
  - むやみやたらに関数化すると可読性が下がるという懸念もありますが、以下のように対処します。
    - RStudioを使っているなら、関数にカーソルをあわせて、Macでは「command + クリック」（Windowsなら「ctrl + クリック」？）で、関数を定義している.Rファイルをすぐに開けます。
    - Rmarkdownで関数の定義を表示したい場合、Rチャンクを以下のように設定すれば、knitしたときに表示されます。
    
    

```r
​```{r, code = readLines(関数のパス)}
​```
```



- 画像はなるべくpng形式で、Outputフォルダに保存する。
  - 学会発表や論文などですぐに使えるように外部に保存しておくとよいです。



### シミュレーションを実行する

- シミュレーションで使用するコードは、Simulation_Codeフォルダに置く。
- サンプルコード：generate_DummyData_RL.R or generate_DummyData_RL.py
  - 二肢バンディット課題を行う。選択したときの結果は1 or 0の2値。
  - 設定するパラメータ
    - trial_N：試行数
    - Option1_p_reward：選択肢1の報酬の発生確率
    - Option2_p_reward：選択肢2の報酬の発生確率
    - alpha：ベクトル。エージェントの学習率
    - beta：ベクトル。エージェントの逆温度

- シミュレーション結果は、Data/DummyData_RLに保存されます。
  - 「パラメータの設定_実行日時」の命名規則でフォルダが生成されます。
  - この命名規則が良いかどうかは別途相談です。
  - その中に、実行した.Rスクリプトのコピーと、シミュレーション結果のcsvファイルが保存されます。
- その他、サーバーなどでシミュレーションを実行した場合も、Dataフォルダに、適宜整理して、置いておきましょう。



### データを分析する

- .Rファイル、または.Rmdファイルで分析していく。
- RawDataは絶対に変更しない。
  - 基本的には、Rで読み込んでその中で処理していきましょう。どうしても、直接ファイルをいじりたい場合は、「RawData」を丸ごとコピーして、コピーした方のファイルをいじること。
  - もしRawDataがあまり整理されていない場合には、整形用のRスクリプトを別途用意して、Rの中でデータを整形しましょう。そして、その結果を新しいcsvファイルとして ./Data/に保存し、それを読み込み直すのがよいです。整形コードは、Rmarkdownで書かない方がよいです。

- 同じ処理は関数化 → purrr::map()で繰り返し処理
  - 例えば、（横軸縦軸も含めて）同じグラフだがデータだけが違う場合、グラフを作成する関数 original_plot() を定義し、purrr::map() でまとめて作成しておくと綺麗です。
  - purrr::map(list, function) は、list (or vector) を順番にfunctionに適用し、その結果をlist形式で返す関数です。
  - そのため、データは事前にリストに分割しておく必要があります。

```r
data_list <- 
	data %>%
	dplyr::group_split(iter_group) # 繰り返したいグループで分割し、リストにする

g <- purrr::map(data_list, ~original_plot(.x))

g[[1]] # 1つ目の画像を表示する
```



- 画像の保存もまとめてできる

```r
name_vector <- c(1, 2, 3, 4, 5)
purrr::walk2(name_vector, g, ~ggsave(filename = paste0("plot", .x, ".png")), plot = .y)
# walkはmapの返り値がないバージョン
# walk2は、引数を2つ指定できるwalk
# name_vectorの1つ目が.xに、gの1つ目が.yに入力されて関数が実行される、次にname_vectorの2つが.xに、gの2つ目が.yに入力されて…以下、繰り返す。
# 結果、plot1.png, plot2.png, ..., plot5.pngという画像が保存される
```



Rmarkdownファイルの基本的な構成について

- 冒頭に書くこと（#セットアップと書いてある部分）
  - ライブラリーの読み込み
  - 関数の読み込み
  - knit時の設定などメタ情報の設定（Optional）
  - データの読み込み
    - .Rmdで使用するすべてのデータファイルをここでデータフレームとして読み込んでおくのが良いです。その方が後で見返したときに、どこでデータフレームが作られたのかわかりやすいです。
      - 分析1の直前に分析1で使用するデータを読み込み、分析2の直前に分析2で使用するデータを読みこむ…というのはあまりオススメしません。
      - ただし、分析対象のオブジェクトの容量があまりにも大きいため、複数のオブジェクトを保持したくないという場合もあるので、ケースバイケースで対応する。
    
  - 分析の目的、概要を書くこと

- 末尾に書くこと
  - SessionInfo … 使用したRのバージョン、パッケージのバージョンを載せます。
  - 以下の関数を書いておけばオーケー。



```r
sessionInfo()
```



### モデルをフィッティングする

- Stanでrstanパッケージを使ってフィッティングしていきます (そのうちcmdstanrに対応させるかもしれない…)。



手順

- mcmcの実行：Run_mcmc_sampling.R
- 結果をcsvに保存：Run_csv_generator.R
- 事後分布・トレースプロットの画像を保存：Run_posterior_traceplot_generator.R
- Rhatのチェック：Run_check_rhat.R

- 以上の結果は、すべて「Data/Models_Results/モデル名」フォルダに生成されます。

※ 予測分布の作成：Run_model_prediction.R は現在作成中



各Run_\** .R ファイルでは、モデルごとに1つのセクションが設けられている

```r
# ------ basic_RL model ----------

## 上のようにセクションを区切る。Rstudioでは目次が生成される。

```



注意

- Run_mcmc_sampling.R, Run_csv_generator.R, Run_posterior_traceplot_generator.Rの中で実行されている各関数（e.g., fit_basicRL）はすべてのモデルで適用できるような関数ではありません。サンプルモデルであるbasicRLモデルでしか使わないことを想定しています。
- これは、パラメータの数や次元、渡すデータが、モデルによって大きく異なるため、それらを包括的に処理できて、同じフォーマットで出力する関数を作成するのは難しいからです。
- そのため、みなさんが自分のモデルをフィッティングする際には、関数を自分でハンドメイドする必要があります。
- サンプルコードを参考にして、自分のモデル用の関数を作成してみてください。

