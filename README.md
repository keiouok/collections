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

## ついついWindows上で一般的なファイル保存のショートカット（「Ctrl」＋「S」キー）に手が伸びてしまい、キー入力がまったく受け付けられなくなってしまった。これは、Linuxのコンソール上で「Ctrl」＋「S」キーを押すとターミナルへの出力がロックされるためだ。この場合には、焦らずに「Ctrl」＋「Q」キーを押せば解除される。混乱を避けるためにこの機能そのものを無効にさせたい場合、次のように指定しよう。


## 素数列挙 O(NloglogN) (by tonnnura)
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
## ABC035D ダイクストラ法
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
上記のLinuxコマンドを実行すると、file1のあとにfile2の内容が追加されたnewfileというファイルが完成します。追加するファイルの指定では、ワイルドカードも使うことができます。

``` 
cat file2.txt >> file1.txt
```
これで、file1の末尾にfile2の文字列が追加されます。>ひとつのリダイレクションでは、元となるファイルと、作成するファイルに同じファイルを指定することができないので、>>が必要になる場面もでてくるはずです。

## 空行を削除するvim
```
 :v/./d
 :g/^$/d
```

## ctrl+s <-> ctrl+q

def load_pickle(file_path):
    with open(file_path, "rb") as f:
        obj = pickle.load(f)
        return obj
  
def save_pickle(file_path, obj):
 20     with open(file_path, "wb") as f:
 21         pickle.dump(obj, f)
 22  
 23 def str_sent_to_list(str_sent):
 24     # str_sent = "ほぼ 無関係 です \n"
 25     str_sent = str_sent.strip()
 26     str_sent_list = str_sent.split()
 27     print(str_sent_list)
 28  









syntax on
"colorscheme molokai"
colorscheme molokai
"colorscheme industry"
""colorscheme torte

"yank save on clickboard"

set clipboard=unnamedplus

set t_Co=256

" setting
"文字コードをUFT-8に設定
set fenc=utf-8
" バックアップファイルを作らない
set nobackup
" スワップファイルを作らない
set noswapfile
" 編集中のファイルが変更されたら自動で読み直す
set autoread
" バッファが編集中でもその他のファイルを開けるように
set hidden
" 入力中のコマンドをステータスに表示する
set showcmd


" 見た目系
" 行番号を表示
set number
" 現在の行を強調表示
set cursorline
" 現在の行を強調表示（縦）
set cursorcolumn
" 行末の1文字先までカーソルを移動できるように
set virtualedit=onemore
" インデントはスマートインデント
set smartindent
" ビープ音を可視化
set visualbell
" 括弧入力時の対応する括弧を表示
set showmatch
" ステータスラインを常に表示
set laststatus=2
" コマンドラインの補完
set wildmode=list:longest
" 折り返し時に表示行単位での移動できるようにする
nnoremap j gj
nnoremap k gk
" シンタックスハイライトの有効化
syntax enable


" Tab系
" 不可視文字を可視化(タブが「▸-」と表示される)
set list listchars=tab:\▸\-
" Tab文字を半角スペースにする
set expandtab
" 行頭以外のTab文字の表示幅（スペースいくつ分）
set tabstop=4
" 行頭でのTab文字の表示幅
set shiftwidth=4

" 検索系
" 検索文字列が小文字の場合は大文字小文字を区別なく検索する
set ignorecase
" 検索文字列に大文字が含まれている場合は区別して検索する
set smartcase
" 検索文字列入力時に順次対象文字列にヒットさせる
set incsearch
" 検索時に最後まで行ったら最初に戻る
set wrapscan
" 検索語をハイライト表示
set hlsearch
" ESC連打でハイライト解除
nmap <Esc><Esc> :nohlsearch<CR><Esc>

"https://teratail.com/questions/124520"
"{}片方消したらもう片方も消したい"


noremap [ []<LEFT>
inoremap ( ()<LEFT>
inoremap " ""<LEFT>
inoremap ' ''<LEFT>inoremap { {}<LEFT>
inoremap [ []<LEFT>
inoremap ( ()<LEFT>
inoremap " ""<LEFT>
inoremap ' ''<LEFT>

augroup vimrcEx
  autocmd!
    autocmd BufReadPost *
        \ if line("'\"") > 1 && line("'\"") <= line('$') |
            \   exe "normal! g`\"" |
                \ endif
                augroup END

autocmd FileType python setl autoindent
autocmd FileType python setl smartindent cinwords=if,elif,else,for,while,try,except,finally,def,class,with
autocmd FileType python setl tabstop=8 expandtab shiftwidth=4 softtabstop=4

inoremap jj <Esc>


"https://qiita.com/ahiruman5/items/4f3c845500c172a02935"
set wildmenu " コマンドモードの補完
set history=5000 " 保存するコマンド履歴の数

"mouse"
if has('mouse')
    set mouse=a
    if has('mouse_sgr')
        set ttymouse=sgr
    elseif v:version > 703 || v:version is 703 && has('patch632')
        set ttymouse=sgr
    else
        set ttymouse=xterm2
    endif
endif

if &term =~ "xterm"
    let &t_SI .= "\e[?2004h"
    let &t_EI .= "\e[?2004l"
    let &pastetoggle = "\e[201~"

    function XTermPasteBegin(ret)
        set paste
        return a:ret
    endfunction

    inoremap <special> <expr> <Esc>[200~ XTermPasteBegin("")
endif

"https://sy-base.com/myrobotics/vim/vim-transparent/"
"highlight Normal ctermbg=none"
"highlight NonText ctermbg=none"
"highlight LineNr ctermbg=none"
"highlight Folded ctermbg=none"
"highlight EndOfBuffer ctermbg=none"





"from yamamoto"
"fzf setting 

""set rtp+=~/.fzf
""
""" [START] Vundle.vim
""set nocompatible              " be iMproved, required
""filetype off                  " required
""set rtp+=~/.vim/bundle/Vundle.vim
""call vundle#begin()
""set clipboard=unnamed 
""
""Plugin 'scrooloose/syntastic'
""Plugin 'valloric/youcompleteme'
""Plugin 'altercation/vim-colors-solarized'
""Plugin 'vim-airline/vim-airline'
""Plugin 'tpope/vim-surround'
""Plugin 'junegunn/fzf.vim'
""Plugin 'tpope/vim-eunuch'
""
""call vundle#end()            " required
""filetype plugin indent on    " required
""" [END] Vundle.vim
