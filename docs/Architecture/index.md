# システムアーキテクチャ

## Launch
**Zenoh**ライブラリを用いたプロセス間通信を主としています。

ノードは各パッケージで非同期関数で宣言されていてそれを以下のようなLaunchパッケージで呼び出すことで実行します。

|repository name|build status|Link|
|:--:|:--:|:--:|
|zenoh_launch|[![Rust](https://github.com/PureRustRobot/zenoh_launch/actions/workflows/rust.yml/badge.svg)](https://github.com/PureRustRobot/zenoh_launch/actions/workflows/rust.yml)|https://github.com/PureRustRobot/zenoh_launch|

## メッセージ通信
**serde**を用いたシリアライズ、デシリアライズをderiveしたメッセージ通信をしています。
メッセージ構造体を定義した[prr_msgs](../Libraries/prr_msgs.md)を使用しています。
以下はメッセージのひとつの例です。

```
#[derive(Serialize, Deserialize)]
pub struct Wheel{
    pub  front_left:f32,
    pub  front_right:f32,
    pub  rear_left:f32,
    pub  rear_right:f32,
}

pub fn serialize_wheel(value:&Wheel)->String
{
    serde_json::to_string(value).unwrap()
}
pub fn deserialize_wheel(str_value:String)->Wheel
{
    let result:Wheel = serde_json::from_str(&str_value).unwrap();
    result
}
```

また、[メッセージ構造体ライブラリを生成するツール](../Libraries/zenoh_msg_generator.md)を使い.msgファイルから、メッセージパッケージを
容易に作成することができます。