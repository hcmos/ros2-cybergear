## 説明
ROS2からSocketCANを通じてcybergearに命令を送るパッケージ群．

### 動作確認環境
| 項目 | 値 |
| --- | --- |
| ROS2 | humble,foxy |

### main_executor
全ノードの起動，及びパラメータの一括設定．  
main_params.yamlから起動するノードのパラメータを設定できる．

#### 起動
```bash
$ ros2 launch main_executor main_exec.launch.py
```

### cybergear_interface
受け取ったトピックからcybergear用の命令を生成し，ROS2内のSocketCANのメッセージを出版する．

#### 購読トピック
- "cybergear/pos"：std_msgs::msg::Float64  
目標位置
- "cybergear/reset"：std_msgs::msg::Empty  
cybergearの零点設定
- "stop"：std_msgs::msg::Empty  
停止命令(再起動するまで命令を受け付けない)
-  "restart"：std_msgs::msg::Empty  
再起動命令

#### 出版トピック
- cybergear/can_tx：socketcan_interface_msg::msg::SocketcanIF  
ROS2内のSocketCANメッセージ

### socketcan_interface
SocketCANとROS2トピックの通信．

### socketcan_interface_msg
Classic CANのROS2内でのメッセージ型．

## 使用したCANデバイス
- [SH-C30A](https://www.deshide.com/product-details.html?pid=384242&_t=1671089557)  
amazonで3千円ほど

WSL環境で開発する場合は，
- [WSLでCAN-USBを使う](https://blog.hcmos.jp/posts/can_with_wsl)

## 参考
- https://github.com/project-sternbergia/cybergear_m5
- [Xiaomi Cybergear 微电机使用说明书](https://web.vip.miui.com/page/info/mio/mio/detail?postId=40233100) (公式説明)
