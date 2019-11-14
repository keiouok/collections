# collections
よく使いそうなやつこれくしょん．


## ファイルの前にディレクトリがなければ作成する関数

```
to_file = "./sentence_kouho_text/above_" + str(above_num) + "/only_" + str(hindo) + "_kouho_20.txt"

def write(filename):
    file_path = os.path.dirname(filename)
    if not os.path.exists(file_path):
        os.makedirs(file_path)

write(to_file)

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



