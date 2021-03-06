# movie_review 

## 目的 
映画レビューの内容が肯定的か、否定的かを分類するモデルをつくる

## データセット 
(https://ai.stanford.edu/~amaas/data/sentiment/) に公開されているLarge Movie Review Dataset v1.0を用いた。

## データの中身 
    trainフォルダー
        posフォルダー：ポジティブレヴュー（1万2500件  
        negフォルダー：ネガティブレヴュー（1万2500件)  
    testフォルダー  
        posフォルダー： ポジティブレヴュー（1万2500件)  
        negフォルダー： ネガティブレヴュー（1万2500件)  

　 合計で5万件のレヴュー(言語は英語)
  
 

## 前処理 
1.HTMLマークアップや句読点を正規表現ライブラリをつかって削除  
2.レヴュー文をトークン化する  
以下の2パターンを試した  
・空白文字で区切る  
(例) he earns enough credits to graduate.  
　→[‘he’, ‘earns’, ‘enough’, ‘credits’, ‘to’, ‘graduate’ ]  
・ワードステミング(単語を原型にして区切る)  
(例) he earns enough credits to graduate.  
    →[‘he’, ‘earn’, ‘enough’, ‘credit’, ‘to’, ‘graduate’ ]  


## 特徴量抽出
1.BoW  
単純に各単語の出現回数で重みづけをする  

2.TF-IDF  
複数の文書で頻繁に出現する単語の重みを減らすことができる  

2パターン試して結果を比較  

## 学習手法 
学習手法  
　ーロジスティクス回帰  

グリッドサーチのパラメタ候補値  
　ーL1正則化 or L2正則化(過学習防止)  
　ー正則化の強さ(強さを示すパラメータを1.0, 10.0, 100.0の3通り試す)  
　ー文書のトークン化の手法(空白文字で区切る or ワードステミング)  

性能指標が最も良くなったパラメータ　(BoW,TF-IDFどちらも同じ結果だった)  
　ーL2最適化  
　ー正則化の強さを示すパラメータ　10.0  
　ー単に空白文字で区切る  


## 結果 
BoWでの特徴量抽出  
訓練データでの3分割交差検証の平均	accuracy 0.874  
テストデータ				accuracy 0.880  

TF-IDFでの特徴量抽出  
訓練データでの3分割交差検証の平均 	accuracy 0.895  
テストデータ				accuracy 0.899  

BoWと比較してTF-IDFの方が約2％ほど正解率が高い  



## 参考文献
Sebastian Raschka 「第3版Python機械学習プログラミング」(https://www.amazon.co.jp/dp/B08LYWFPQ9/ref=dp-kindle-redirect?_encoding=UTF8&btkr=1)
