# collections
よく使いそうなやつこれくしょん．


# ファイルの前にディレクトリがなければ作成する関数

`
to_file = "./sentence_kouho_text/above_" + str(above_num) + "/only_" + str(hindo) + "_kouho_20.txt"

def write(filename):
    file_path = os.path.dirname(filename)
    if not os.path.exists(file_path):
        os.makedirs(file_path)

write(to_file)

`

