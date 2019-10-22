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

# aiserv

pyenvとanacondaの導入の所が古いようなので，今回やった内容に即して追加記入します．思い出しながら書いているので，間違いや追加事項あれば適宜訂正をお願いします(胡)．
ちなみに，導入の際のコマンドのほとんどは，sudoを必要としました．

## pyenvの導入
LDAPを通すと，/home/の下にaiの他にsettingができるはずなので，
/home/setting/に移動し，setting下でpyenvとanacondaを導入する．
ssh setting@aiserv.sspnetで飛んでからやると，管理者権限に引っ掛かり，sudoを付けても導入ができないっぽい(?)ので，基本的にuser_name<ai,ironなど>から見て，/home/setting/で導入を行う．

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
```

や

```
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



