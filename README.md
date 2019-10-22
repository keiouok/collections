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

## 20191022 
## 昼：餃子 これで自分一人でも作れそう
皮は厚め．うどんが作れそうなのでそれもあり．今日の感触を覚えておくこと．

薄力粉＋水   こねて炊飯器のに入れて10分間置く．薄力粉が水を吸って均等に滑らかな記事になるという．塩は我が家は入れない．

豚肉300～400g＋醤油，酒，砂糖，酢    ミキサーで先に細かくする．

セロリ1，2本 そのあと肉と分けてミキサーに入れて細かくする．今日はセロリが多めであったが，ちゃんと肉はバラバラでなく固まったので問題ない．

セロリはミキサーで細かくした後，水気を手で絞って捨てること．これ忘れて肉と一緒にミキサーに入れないように．

生地を数分こねこねする．

ちゃんと丸くした後に，真ん中に穴をあけて，ドーナツ状にする．その後，小麦粉をまぶした台の上に置き，均等な太さになるようにコロコロする．

終わったら，餃子づくりにおいて最難関の秘伝業であるちぎり技によって気持ち小さめに記事を切っていく．これを習得するにはまだ時間がかかるようだ．生地をつぶして平らにしてしまった．

薄力粉上で丸めるように生地をなでる．最後に軽めに上から掌で力をかけて平らにする．

7，8回転加えて親指の付け根部分に力を入れ，棒で平らにする．

包む，最後に両手の親指でギュっとする．

## 夜：冷麺
麺   4分ゆでる

きゅうり 2個    あの切り方で切る．切るときは上下に力を入れて小刻みに．今日よりもっと薄く切れるように．

トマト     適当

ハム      きゅうりと違って柔軟性があるので，上下だけでなくある程度の左右運動も必要．

にんにく    包丁の掌で力を入れてつぶし，細かく切る．にんにくおいしい．

卵   2個  フライパンに油をしき，最大限に広げ，余った分は他の鍋に入れる．油少なくて大丈夫．半分に分けて入れながら，薄く延ばす．すぐに出す．これを2回．

あとは盛り付けて完成．














# aiserv
# LDAP
LDAPを通した後に

```
sudo apt update
sudo apt upgrade
```
すると，LDAP入れた後にぶっ壊れなかった．



pyenvとanacondaの導入の所が古いようなので，今回やった内容に即して追加記入します．思い出しながら書いているので，間違いや追加事項あれば適宜訂正をお願いします．ちなみに，導入の際のコマンドのほとんどは，sudoを必要としました．

## pyenvの導入
LDAPを通すと，/home/の下にuser_nameの他にsettingができるはずなので，
/home/setting/に移動し，setting下でpyenvとanacondaを導入する．
ssh setting@<user_name>.sspnetで飛んでからやると，管理者権限に引っ掛かり，sudoを付けても導入ができないっぽいので，基本的にuser_name<ai,ironなど>から見て，/home/setting/で導入を行う．

以下内容の参考文献：https://qiita.com/aical/items/126128c3e8916ad1988f

まず，pyenv環境を設定する．

以下コマンドを実行する．
```
sudo curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash
```
実行したら，/home/setting/下に/home/setting/.pyenvが存在しているか確認すること．存在していなければ，/home/user_name/の下にできてしまっていることがあるので，丸ごと/home/setting/下に移動してくればよい．
```
sudo mv /home/user_name/.pyenv /home/user_name/.pyenv

```


コマンドを実行すると以下のような警告が出てくる．

```
WARNING: seems you still have not added 'pyenv' to the load path.

# Load pyenv automatically by adding
# the following to ~/.bashrc:

export PATH="/home/user_name/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```
参考文献のように，個人のパソコンにpyenvを導入する場合は/home/user_name/.bashrcに直接以下の内容を書き込むが，今回はみんなが使うサーバーなので，/etc/profile.d/にpyenv.shを新規作成し，そこに書き込む．参考文献で言われた書き方ではなく(virtualenv-initは導入不要，導入してない上で呼び出されるとterminal上でエラーメッセージが出てきてしまうため)，以下の内容を/etc/profile.d/pyenv.shに書き込む．anaconda3-2019.10の部分は，今からやるanacondaの導入で得られたパッケージ名を入力すること(ver.は最新のものが望ましい) ．

```
export PYENV_ROOT="/home/setting/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
export PATH="$PYENV_ROOT/versions/anaconda3-2019.10/bin:$PATH"

```

できたシェルファイルを実行し，パスを通す．

```
sudo sh /etc/profile.d/pyenv.sh
```
いったんシェルを再起動する．
```
exec $SHELL -l

```

再度ターミナルを起動した際に，
```
pyenv versions
pyenv --version
```
などと打ってpyenvが起動すればOK．通したつもりでもパスが通ってないといわれた場合は，再度確認，もしくは，シェルを再起動したりrebootをかけてみる．個人のパソコンからsshでアクセスした際にエラーメッセージ発生するか同時に見てみてもよい．


# anaconda(Python)の導入
pyenvでインストールできるanacondaのパッケージを確認する．

```
pyenv instal -l | grep anaconda
```

その中で最新のパッケージを導入する．例では，anaconda3-2019.10．
(anacondaなので数分時間がかかる)

```
pyenv install anaconda3-2019.10
pyenv global anaconda3-2019.10

```
Pythonが動くか確認する
```
python --version
```
と入力した際に，

```
Python 3.7.4
```

などと出ればOK.

# tensorflow_gpuの導入
pipが叩けるようになったので，tensorflow_gpuを導入する．

```
pip install tensorflow_gpu
```

tensorflow_gpuが使えるかどうか確認する．

以下内容の参考文献：https://qiita.com/sho8e69/items/66c1662c49ac89a024be

メモリの使用率をみるとよい．以下の内容のdousa.pyを作成して実行させる．
```

import tensorflow as tf

while 1:
    tf.test.gpu_device_name()

```
プログラムを実行している間に，もう一つterminalを開き，

```
nvidia-smi
ps aux | grep python
```
でプロセスが実行しているかどうかを確認する．実行されていればOK．プロセス番号が特定できれば殺してプログラムが止まるか確認するとわかりやすい．
```
kill <ID>
```

