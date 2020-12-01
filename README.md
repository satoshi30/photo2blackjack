# ブラックジャックの世界へ
個人プロジェクト「ブラックジャックの世界へ」のレポジトリです
<p>
<img src="https://github.com/satoshi30/mosaic_art/blob/master/main.png?raw=true" width="200" height="300" align="left">
<br clear="left">
</p>

- GANの⽣成モデルを活⽤して、**実写真をアニメーション**へ変換する︕という試みを行ってみました。
- 著作権の関係で一般で出版されている著作物が使用できないため、**二次利用がフリー化されている「ブラックジャックによろしく」（作者：佐藤秀峰）**を利用し[（リンク）](https://densho810.com/free/)、**本作の主人公・斉藤英二風の画像生成**を行いました
- 課題設定の背景や、結果・考察などはこちらのスライドにまとめております。[（リンク）]()

<img src="./image/data_process/0001.png" width="100" height="100" align="left">
<img src="./image/result/test1.png" width="100" height="100" align="left">
<img src="./image/data_process/0000.png" width="100" height="100" align="left">
<img src="./image/result/test2.png" width="100" height="100" align="left">
<img src="./image/data_process/0002.png" width="100" height="100" align="left">
<img src="./image/result/test3.png" width="100" height="100" align="left">
<br clear="left">

## Start
### Google Colaboratory
<table class="tfo-notebook-buttons" align="left">
  <td>
    <a target="_blank" href="https://colab.research.google.com/#create=true"><img src="https://www.tensorflow.org/images/colab_logo_32px.png" />Run in Google Colab</a>
  </td>
</table>
<br clear="left">

**このレポジトリはGoogle Colaboratoryで動作検証しています**

### Mount
```
from google.colab import drive
drive.mount("/content/drive")
```
```
%cd /content/drive/MyDrive
```

### Clone
```
git clone https://github.com/satoshi30/photo2blackjack.git
cd ./photo2blackjack
```
### Requirements
```
pip install tensorflow==1.14
pip install tensorflow-gpu==1.14
pip install face-alignment
```

### Test
```
python test.py --photo_path ./image/original/test1.jpeg
```

### Train
#### 前処理
- 実際の顔写真のデータをトリミングします
```
python data_process.py --data_path YourPhotoFolderPath --save_path YourSaveFolderPath
```
#### データセット
- 前処理した写真データをA、アニメーションの画像データをBとして以下のようなディレクトリを作成します
```
├── dataset
    └── photo2blackjack
        ├── trainA
            ├── xxx.jpg
            ├── yyy.png
            └── ...
        ├── trainB
            ├── zzz.jpg
            ├── www.png
            └── ...
        ├── testA
            ├── aaa.jpg 
            ├── bbb.png
            └── ...
        └── testB
            ├── ccc.jpg 
            ├── ddd.png
            └── ...
```

#### train
- １から学習させる場合
```
python train.py --dataset photo2blackjack
```
- 学習済みの重みを利用する場合
```
python train.py --dataset photo2blackjack --pretrained_weights models/photo2cartoon_weights.pt
```
- 別環境で複数GPUを利用する場合
```
python train.py --dataset photo2blackjack --batch_size 4 --gpu_ids 0 1 2 3
```
