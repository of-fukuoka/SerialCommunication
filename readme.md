# シリアル通信をしたいときに使えそうなもの群

## Arduino

### LeonardAsInput
Arduino Leonardの全てのピンを入力ピンとして使用する。(analog:6, digital:14)  
アナログピンとデジタルピンへの入力をシリアルで送る。  

- 1バイト目にインデックス(0-19)  
- 2バイト目に入力値(0-255)  
- ※必ず2バイトセットで送る  

(ってことは下記が正しい？)

	unsigned char data[] = {index, map(analogRead(pin), 0, 1023, 0, 255)};
	Serial.write(data, 2);

##oF

### SerialServer
シリアル入力を受け取ってOSCでlocalhostにとばす、サーバー的なもの。  
ポート選択のダイアログのためにOSX専用になってるので必要あれば誰か他プラットフォームにも対応させてください。。  
シリアルデータのフォーマットは下記を想定

- 1バイト目にインデックス  
- 2バイト目に入力値(0-255)  

OSCメッセージのフォーマットは下記  

- address: "/serial"  
- arg[0]: インデックス  
- arg[1]: 値(0-255)  

### SimpleReceiver
SerialServerから値を受け取るサンプル。