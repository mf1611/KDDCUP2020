## KDD Cup 2020

- タスクは、テキストクエリに対応する画像を引っ張ってくること

- 与えられているデータは、テキストのクエリと、画像内で検知された物体のboxの位置座標(4角)と、box内のfeatures



- 最初思ったのは、boxの中でも大きいものの寄与が高いのでは？
    - けど、人とかが着ているものの場合は、違う？
    - 例えば、クエリもしくは探索画像の中で、分類器にかけてから、対象絞って、検索掛ける方がいい？




- fashion corpusを収集すること
- word2vec + ELMOが良いのでは？




- NNで学習させようとする場合、入力の形が一定ではないので、どうするか？
    - 検出された物体数だけある
    - 例えば、画像サイズと、各物体のサイズも分かっている


    - まずは、boxの位置や大きさは無視してやってみる？



- 同一空間に飛ばすが、どのような形で損失関数を設計するのがよいか？
    - https://www.anlp.jp/proceedings/annual_meeting/2019/pdf_dir/P8-8.pdf
    - https://cs.stanford.edu/people/karpathy/cvpr2015.pdf

    - 基本的には、内積が大きくなるように学習
        - けっこう使われているのが、hinge loss


- metric learningを使いたい
    - https://techblog.zozo.com/entry/metric_learning
    - https://gombru.github.io/2019/04/03/ranking_loss/
    - positive pairとnegative pairを作りたい
    - そのために、ラベル付けをやりたい
        - 例えば、シャツカテゴリなら、negativeはズボンとかにするなど


    - なので、query自体をまず分類したいが、、、



- class labelのグルーピング
    - 




- triplet lossを使うのはあり
    - この場合、1つのクエリと画像に対して、positiveとnegative(とても似ている、似ていない)ものを用意する必要がある



- metric learningのライブラリ
    - https://github.com/KevinMusgrave/pytorch-metric-learning


- word2vecの事前学習モデル
    - https://qiita.com/Hironsan/items/8f7d35f0a36e0f99752c


- パラメータごとの最適化パラメータの調節
    - https://pytorch.org/docs/stable/optim.html


- DCG(Discounted Cumulative Gain)
    - 順位を含めて正解データのランキングをどれだけ再現できるのかの評価の指標。つまり、「推薦、検索などでランキングされたデータがどれだけ適切か」を示すものである。


    - sklearn.metrics.ndcg_score(y_true, y_score, k=None, sample_weight=None, ignore_ties=False)
