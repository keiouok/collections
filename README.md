# collections
よく使いそうなやつこれくしょん．

## texコンパイル(tex.sh)

```
platex *.tex                                         
dvipdfmx *
evince *.pdf
```

## ファイルの前にディレクトリがなければ作成する関数

```
to_file = "./sentence_kouho_text/above_" + str(above_num) + "/only_" + str(hindo) + "_kouho_20.txt"

def write(filename):
    file_path = os.path.dirname(filename)
    if not os.path.exists(file_path):
        os.makedirs(file_path)


```


## リストの間にblank(空欄)を入れる関数

```
def insert_blank(line):
    line_with_blank = []
    length = len(line)
    for word in line:
        if word != "\n":
            line_with_blank.append(word)
            line_with_blank.append(" ")
        else:
            line_with_blank.append(word)
    
    return line_with_blank
```

## 実行時間を表示
```
import time
start = time.time()

elapsed_time = time.time() - start

print("elapsed_time:{0}".format(elapsed_time)+"[sec]")
```

## デバッグ

```
import pdb
pdb.set_trace()
```

## 辞書でも使えるenumerate
```
for i key in enumerate(dict):
```

## pickleにして保存する
```
import pickle
L = ['未経験転職', 'Pythonで人工知能エンジニア', 123456, {'Pyhon': '機械学習'}]
with open('*.textfile', 'wb') as f:
  pickle.dump(L , f)
```


## pickleにして保存したものを読み込む
```
import pickle
with open('*.textfile', 'rb') as f:
  target = pickle.load(f)
  print(target)
```
## cos_similarity
```
def cos_sim(v1, v2):    
    c_s = np.dot(v1, v2) / (np.linalg.norm(v1) * np.linalg.norm(v2))
    # if c_s <= 0.3:
    #     return 0
    # else:
    return c_s
```

## 文を受け取って言い換えた文候補のリストを返す関数
```
def para_sent(low_word, low_high_dict, sentence):
	# sentenceのどこにwordがあるのかのindexを作成
	# 言い換えるべきlow_word
	# sentenceは一文を入力とする
	kouho_thre = 20
	sentence_kouho_list = []
	# default 原文も含む状態
	sentence_kouho_list.append(sentence)
	word_index_in_sent = []

	for i in range(len(sentence)):
		if sentence[i] == low_word:
			word_index_in_sent.append(i)
	high_word_list = low_high_dict[low_word]
	high_word_list = high_word_list[:kouho_thre]
	for high_word in high_word_list:
		n_sentence = []
		for j in range(len(sentence)):
			if j not in word_index_in_sent: 
				n_sentence.append(sentence[j])
			else: # if j in word_index_in_sent
				n_sentence.append(high_word)
		sentence_kouho_list.append(n_sentence)
	
	return sentence_kouho_list
```

## 20191115
「Python3」完全に理解しよう

## 剰余を返す関数
```
divmod(9, 5)
# (1, 4)
```

## 文字列はimmutableなので，直接挿入や，指定位置の言い換えはできない．なので，replaceかsliceを使いましょう．

## 末尾から先頭まで取り出す
```
letter = "abcdefghijklmnop"
letter[-1::-1]
letter[::-1]
```
## 組み込み文字列関数split()は何も言わなければ空白文字のシーケンスを使う．

## join()はsplit()関数の逆．指定するのは，「糊として挟む文字列」．

## 先頭文字列がそれかどうか，trueか
```
poem.startswith("All")
poem.endswith("All")
```
## 素数列挙 O(NloglogN) (by tonnn*)
```
def primes_for(n):
  is_prime = [True] * (n + 1)
  is_prime[0] = False
  is_prime[1] = False
  for i in range(2, n + 1):
      for j in range(i * 2, n + 1, i):
          is_prime[j] = False
  return [i for i in range(n + 1) if is_prime[i]]
```
## ダイクストラ法
```
def dijkstra(E, start):
    N_d = len(E)
    dist = [INF] * N_d
    dist[start] = 0
    q = [(0, start)]
    while q:
        dist_v, v = heappop(q)
        if dist[v] != dist_v:
            continue
        for u, dist_vu in E[v]:
            dist_u = dist_v + dist_vu
            if dist_u < dist[u]:
                dist[u] = dist_u
                heappush(q, (dist_u, u))
    return dist
```
E は 連結リスト(多分)
startは始点

E[a].append(b, c)

意味するのは，「a番目のノードがbと繋がっており，コストはc」
これが連結リスト．すべてのノードからダイクストラを求める必要はない．0スタートを逆順にすればよいだけ．大事．
## テキストファイル結合
```
cat file1.txt file2.txt > newfile.txt
```
上記のLinuxコマンドを実行すると、file1のあとにfile2の内容が追加されたnewfileというファイルが完成。追加するファイルの指定では、ワイルドカードも使える。

``` 
cat file2.txt >> file1.txt
```
これで、file1の末尾にfile2の文字列が追加される。>ひとつのリダイレクションでは、元となるファイルと、作成するファイルに同じファイルを指定することができないので、>>が必要になる場面もでてくる。

## 空行を削除するvim
```
 :v/./d
 :g/^$/d
```

## ctrl+s <-> ctrl+q 
vimで癖でctrl+S押したら，ctrl+Qすべし．

## pickle の保存と読み込み
```
def load_pickle(file_path):
    with open(file_path, "rb") as f:
        obj = pickle.load(f)
        return obj
  
def save_pickle(file_path, obj):
    with open(file_path, "wb") as f:
        pickle.dump(obj, f)
```
