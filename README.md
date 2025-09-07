# Barrage Storm

# 特徴

Unity 風クラス設計のコンポーネント指向エンジン  
Photon SDKを利用したオンラインマルチプレイ機能

# 設計概要

### ComponentEngine

エンジンの基礎部分です。基本的なオブジェクトはこの名前空間に入っています。  
transformを除き、基本的にライブラリに依存しないよう意識して設計しています。インターフェース部分を差し替えれば DirectX 等に変更できることも想定した作りになっています。

### SivComponent

名前空間ではComponentEngine::Sivになっています。  
Siv3Dに関するコンポーネントの機能はここで実装しています。

### PhotonComponent

Photonを使ったオンライン機能をコンポーネントにまとめたものです。  
設計がまだ練りきれていませんが、機能的には必要なものが整っています。

# 利用方法概要  

SceneManager -> Scene -> GameObject -> Component　のような保持関係になっています。上位オブジェクトは Get[Hoge]().lock() で取得することができます。(シーン遷移するためにはSceneManagerまで辿って呼ぶ必要があります。かなり深いですが、あまり頻繁に書く機能ではないので許容しています)

1. ComponentEngine::ISceneを継承したクラスを作ります。
1. ComponentEngine::AttachbleComponentを継承したクラスを作り、Start()やUpdate()に処理を書いていきます。
1. void IScene::Setup() override にてゲームオブジェクトを生成していきます。生成と同時にオブジェクトのポインタを受け取れる、CreateAndGetGameObject()がおすすめです。オブジェクトにはAddComponentでコンポーネントをくっつけていきます。
1. シーンマネージャーを作り、クラスを登録します。シーン登録周りについては、Siv3Dのシーンマネージャーに寄せています。
1. SceneManager.UpdateCurrentScene()をゲームループで毎フレーム呼びます。


# ライブラリ
ビルドする場合はそれぞれインストールを行い、パス等を通す必要があります

boost 1.72.0  


Photon Realtime SDK v4.1.15.2  
<https://www.photonengine.com/ja/sdks>

OpenSiv3D v0.4.2  
Copyright (c) 2008-2019 Ryo Suzuki  
Copyright (c) 2016-2019 OpenSiv3D Project  
<https://github.com/Siv3D/OpenSiv3D>



~~ICU  
Copyright © 1991-2020 Unicode, Inc.~~  