Title: "FPSカメラにOculus回転を仕込んだ"
Published: 2013-6-26
Tags: []
---

FPSカメラにOculus回転を仕込んだ
IrrlichtのCSceneNodeAnimatorCameraFPSにOculusを合体した。
Irrlichtのカメラが思ったよりいろいろやっていたのと
ビュー行列を直接扱っていないのに手間取ったがとりあえず当初の目的を達成。
どうにも都合が悪かったので本体をちょっと拡張した。
class CSCameraSceneNode
{
    core::marix4 LeftAffector;
};

レンダリング直前にビュー行列に乗算する行列をセットできるのだが
これが右からの乗算なので、
左からの乗算を追加してこれにOculusの回転を表す行列をセットできるようにした。
これを踏まえてCSceneNodeAnimatorCameraFPSをコピーしてCSceneNodeAnimatorCameraOculusOnFPSを作った。
こいつはFPSカメラのマウスの上下移動を無視するのとlibOVRからの回転値取得と左行列を追加する機能をもつ。
コードはこれなのだけど
https://github.com/ousttrue/onibi/blob/master/irrlicht/examples/HMDIrrlicht/CSceneNodeAnimatorCameraOculusOnFPS.cpp
日記に全部書くには長いし、サンプルが改造版のIrrlichtに依存するので紹介し辛い感じだなぁ。
オフスクリーンレンダリングとシェーダーをサポートした今風のglutみたいなフレームワークがあるとよいのだけど。
今度はmmd表示周りに着手して表示途中までできた。
しかしIrrlicht界のスケーリングの基準がよくわからず。cmのような気もするがなんかもっと適当な値のような気もする。
画像右側の身切れているのはIrrlichtサイズのDwarfである。
mmd界はミクさんの身長20を基準とする統一単位なのだが何かしら基準を決めねばならぬ。
物理の挙動の都合上スケーリングしたくないなーという事情がありどうしたものか。

スカイボックスもOculusで見ると見違えるものがあるなー。
テクスチャとライティングを解決する。 あとpmx。
