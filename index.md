# 自作RDBMSやろうぜ!
## このサイトの目的
- RDBMS（いわゆるリレーショナルデータベース）というものはプログラミング言語の処理系や、OSなどと同様に、世の中で広く使われているソフトウェアであるにも関わらず、自作してみようと思うと日本語で記述されたサイトで、必要な情報・情報源がまとまったサイトがないことに気づきました
- そこで、管理人他が開発を進めている自作RDBMSである [SamehadaDB](https://github.com/ryogrid/SamehadaDB) が軌道に乗るまでの経験をベースに、自作RDBMSに関する情報をある程度分かりやすくまとめてみようと思った次第です
  - 各々の情報・情報源はあいかわらず英語などが多くなるとは思います
- なお、技術的な解説を管理者が行うつもりはなく、あくまで適切と思われる情報源をポイントするに留めます
- GitHub Pagesで構築したWebページですので、Pull Requestなど送っていただければ可能な限り反映しますし、集合知的なやり方で良いものにしていければと考えています

## ハードコース
- 英語スラスラ読めるし、とっかかりさえあれば自分でどうにかできるという方はこちら
- 以下のページに Database System について学ぶための情報源がリストされているので、適宜参照しながら進められると良いでしょう
  - [awesome-database-learning](https://github.com/pingcap/awesome-database-learning)

## 段階的に進んでいこうコース（= おおむね管理人が歩んだ道）
- いきなり英語とか辛いので日本語の書籍などで基本を押さえてから段階的に進んでいきます
- これがベストと言うつもりはないので、こういう世界線もあるよ、という方はよろしくサイト内リンクで飛べるような形でまとめてPR送っていただければ幸い

### 日本語の書籍でデータベースシステムの基本について押さえよう
- [北川 博之著 『データベースシステム 改訂2版』](https://www.amazon.co.jp/%E3%83%87%E3%83%BC%E3%82%BF%E3%83%99%E3%83%BC%E3%82%B9%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0-%E6%94%B9%E8%A8%822%E7%89%88-%E5%8C%97%E5%B7%9D%E5%8D%9A%E4%B9%8B-ebook/dp/B08BNXFRL3/)
  - 大学の情報系の講義などで用いられる教科書といった感じの書籍です
  - 実装寄りかと言えばそうでもないですが、基本を押さえておけば英語の情報にあたった時もなんとかなります
  - なお、管理人は後述の日本語な情報源の存在を知ったタイミングの関係から、本書の実装に必要な所に目を通したところで次のステップに進みました
- [KOBA789著 『WEB+DB PRESS Vol. 122 "特集3 作って学ぶ RDBMS のしくみ"』](https://www.amazon.co.jp/WEB-DB-PRESS-Vol-122-PRESS%E7%B7%A8%E9%9B%86%E9%83%A8-ebook/dp/B092Q8SKDB)
  - 特集のタイトルの通り実装を追いながらRDBMSについて解説しています
  - rellyというシンプルなRDBMS実装について解説しており、コードはGitHubにあります
    - [KOBA789/relly](https://github.com/KOBA789/relly)
  - 日本語で書かれているという点で、大変貴重な記事なのですが、実装がRustなため、Rust経験者でない場合、コードの読解は少し苦労するかもしれません 
  - WEB+DB PRESSは上のリンクから vol.122 だけのKindle版が購入できます
- 管理人が自作RDBMSするにあたっていろいろとアドバイスをいただいている方の一人が[kumagi](https://github.com/kumagi)氏ですが、以下のようなものを執筆しているので、読んでおくと、後でああ、あの話かーという感じで役に立つかもしれません
  - [一人トランザクション技術 Advent Calendar 2016 - Qiita](https://qiita.com/advent-calendar/2016/transaction)
  - 次のセクションのオープンコースウェアな講義で良く分からなかったときに参照する、というのでもよい気はします

### オープンコースウェアで本格的なデータベースシステムの実装について学ぼう
- ここについては以下のGitHubリポジトリにまとめておいたので、ひとまずそちらをご参照下さい
  - [ryogrid/CMU_lecture_DATABASE_SYSTEMS_materials](https://github.com/ryogrid/CMU_lecture_DATABASE_SYSTEMS_materials)
- 管理人および他のコミッタは、前出ですが、自作RDBMSとして [SamehadaDB](https://github.com/ryogrid/SamehadaDB) というものをちまちまと開発していますが、これは現状、上記のCMUの講義で扱っている教育用RDBMS実装 BusTubを C++ から Go言語にポーティングすることが主な作業となっています
  - bruncalza氏が先だって [brunocalza/go-bustub](https://github.com/brunocalza/go-bustub) というプロジェクトを進めていたため、全てのポーティングを管理人が行ったわけではありません
  - なお、brunocalza氏は、時間が取れなくなったそうで、go-bustub プロジェクトは管理人が fork するしばらく前から更新されておらず、今後更新できる見込みも無いとのこと
    - 現状、やっている作業がgo-bustubのやろうとしていたことに類似しているだけであって、プロジェクトを引き継いだわけではありません
  - 本家BusTubは講義の課題として実装の穴埋めをさせるように作られているため、歯抜けになっていますが、brunocalza氏及び管理人他はそれらの部分を埋める形でポーティングを行ったため、全てではないですが一応、一通り実装が行われています
  - 従って、手前味噌ですが、BusTub相当の機能までであれば、SamehadaDBのコードベースを参考にしていただくのも良いのではないかと思います
    - 更新しきれていない部分も多いですが、[なんちゃってクラスダイアグラム](https://github.com/ryogrid/SamehadaDB/wiki/class_diagram_of_samehadaDB) も go-bustub読解の時点で作成したので、ご活用ください
  - (Go言語にポーティングしているのは写経的な意味と、個人的にC++のまま拡張していくの辛いな・・・と思ったためです)

### アドバンスドなところも実装していこう
- BusTubには残念ながら planner/optimizer に相当するところの実装やフロントエンドの実装がありません
- [awesome-database-learning](https://github.com/pingcap/awesome-database-learning) を参照して気合で実装するのも良いかもしれませんが、なかなか大変らしいです（管理人らもまだそこまで達していない）
- というわけで、英語ではありますが以下の書籍を参考に実装するとよいらしいです
  - [ Edward Sciore 『Database Design and Implementation (Second Edition) 』](https://link.springer.com/book/10.1007/978-3-030-33836-7)
  - 通称、SimpleDB本とも呼ばれたりするらしく、SimpleDBというRDBMS実装（Java）をフロントエンドからストレージエンジンのところまで丸っと実装しています
  - SimpleDBのソースコードは著者のWebページから入手可能です
    - [The SimpleDB Database System](http://www.cs.bc.edu/~sciore/simpledb/)
  - 同書を読みながらSimpleDBをC++で実装したという方がいて、GitHubにコードがあったりもします
    - [yutaroyamanaka/SimpleDB](https://github.com/yutaroyamanaka/SimpleDB)  
    - なお、本家SimpleDBの全てをカバーしているわけではないようです

### 戦いはさらに続く
- ここまでに挙げたものは基本的なところを、比較的一般的かつ、さほど難度の高くない手法で実装している認識ですが、RDBMSをより良いものにしようと思えば、やれることは際限なくあります
- 例えば、logging/recoveryにおけるsnapshotにARIESなどを採用するというのもよいでしょう
- そのあたりは [awesome-database-learning](https://github.com/pingcap/awesome-database-learning) など参照して各自追求していきましょう（一緒に）
- あと、自作 (R)DBMSの世界で定番？なコンテンツとして通称redbook（赤本）と呼ばれる 『Readings in Database Systems』というものがありまして、その内容は押さえておくとよいのだろうと思います
  - [Peter Bailis, Joseph M. Hellerstein, Michael Stonebraker, editors『Readings in Database Systems, 5th Edition』](https://www.redbook.io/)

## その他の自作RDBMSに関連するトピック
- 何か載せたいものがあれば Pull Requestお願いします
- 下の"ほげほげ"のような感じで並べていければと思います
  - 必要であれば、https://github.com/dbms-jisaku の中にmdファイルなりhtmlファイルなり置いてもらって構いません
- [ほげほげ](https://ryogrid.github.io/dbms-jisaku)
