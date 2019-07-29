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
