<p align="center"><img src="https://github.com/deltaxflux/fluxion/blob/master/logos/logo1.jpg?raw=true" /></p>
#Fluxion 是 MITM WPA 攻击的未来趋势
Fluxion是一个无线破解工具，这个工具有点像是Linset的翻版。但是与Linset比较起来，它有着更多有趣的功能。目前这个工具在Kali Linux上可以完美运行。

##一些问题

#### "Clients are not automatically connected to the fake access point"
This is a social engineering attack and it's pointless to drag clients in automatically. The script relies on the fact that a user should be present in order to enter the wireless credentials.

#### "There's no Internet connectivity in the fake access point"
There shouldn't be one. All of the traffic is being sinkholed to the built in captive portal via a fake DNS responder in order to capture the credentials.

#### "伪造的Wi-Fi不能访问页面"
那可能是 lighttpd 服务器问题. 测试版 lighttpd 1.439-1, 如果有问题请使用稳定版. 更多bug点击 [fix] (https://github.com/deltaxflux/fluxion/wiki/fix) out.

#### "Experimental menu is not responsive"
In the experimental version it will automatically check the handshake. I will fix the menu shortly. If you need a GUI, use the stable version (which doesn't automatically control handshakes).

#### "I need to sign in (on Android)"
This is how the script works. The fake captive portal is set up by the script itself to collect the credentials. Don't freak, it's al okay.

#### "The MAC address of the fake access point differs from the original"
The MAC address of the fake access point differs by one octet from the original in order to prevent fluxion deauthenticating clients from itself during the session. 

### "HTTPS 网站重定向问题"
HTTPS 网站暂时不支持

## 工作原理
* 1.扫描能够接收到的WIFI信号
* 2.抓取握手包（这一步的目的是为了验证WiFi密码是否正确）
* 3.使用WEB接口
* 4.启动一个假的AP实例来模拟原本的接入点
* 5.然后会生成一个MDK3进程。如果普通用户已经连接到这个WiFi，也会输入WiFi密码
* 6.随后启动一个模拟的DNS服务器并且抓取所有的DNS请求，并且会把这些请求重新定向到一个含有恶意脚本的HOST地址
* 7.随后会弹出一个窗口提示用户输入正确的WiFi密码
* 8.用户输入的密码将和第二步抓到的握手包做比较来核实密码是否正确
* 9.这个程序是自动化运行的，并且能够很快的抓取到WiFi密码

## 使用步骤

* 1.使用 `kali Linux` 2016版，确保联网
* 2.下载，命令行执行
```
git clone https://github.com/jeeinn/fluxion
```
<p align="center"><img src="https://camo.githubusercontent.com/b8f731d08542e0ac9a18c3bbe3794c642085b507/68747470733a2f2f342e62702e626c6f6773706f742e636f6d2f2d5442422d4d4a46383379342f563737594c304156564e492f41414141414141414271302f705061392d2d73666f53494a6f356a5a78733261536e666c514939326168464e51434c63422f73313630302f466c7578696f6e2532424769746875622e706e67" /></p>

* 3.检测依赖
```
cd fluxion; sudo ./fluxion
```
<p align="center"><img src="https://camo.githubusercontent.com/20f0cddf1b64213b1f194416ded7f6350e15d607/68747470733a2f2f312e62702e626c6f6773706f742e636f6d2f2d506a5a4c7a4737725641552f563737582d5a48465a47492f41414141414141414271772f485a78516e305035714f383762754b55674b666b5250784f4578544e3635774377434c63422f73313630302f466c7578696f6e253242636865636b253242646570656e64656e636965732e706e67" /></p>

* 4.安装依赖
```
sudo ./Installer.sh
```
<p align="center"><img src="https://camo.githubusercontent.com/3e8d792d4fe1c491d286b158c7169b63b86d14b7/68747470733a2f2f312e62702e626c6f6773706f742e636f6d2f2d39457858502d67643478732f563737596e6939654a47492f41414141414141414272412f2d5f666c41704a6866466356673947464e4a6354456d7161353736574935785251434c63422f73313630302f466c7578696f6e25324242756767792532426170742d676574253242322e706e67" /></p>

* 5.启动脚本，选择网卡 输入：1
```
sudo ./fluxion
```
<p align="center"><img src="https://camo.githubusercontent.com/cd9b9adb4c12e51bb26e2f710fb56e33134c5635/68747470733a2f2f342e62702e626c6f6773706f742e636f6d2f2d616e5974766f53575a44552f563737747973316f3774492f41414141414141414272772f6c383461747838376f4f346c5742636a70746d63764b4c356769474b79624a5451434c63422f73313630302f312532422d25324243686f6f73652532426e6574776f726b253242416461707465722e706e67" /></p>

* 6.自动扫描Wi-Fi，选择要复制的Wi-Fi序号，前面带 `*` 号表示当前有客户端连接
<p align="center"><img src="https://camo.githubusercontent.com/990af93e08db4bdf3011797a1c00100b0336ad0c/68747470733a2f2f322e62702e626c6f6773706f742e636f6d2f2d637850574c4631425663552f563737747a5576565066492f41414141414141414272302f62696b4e6174667962436f526b6e30304933446a37634952364c2d647743695277434c63422f73313630302f332532422d25324243686f6f73652532427468652532427461726765742e706e67" /></p>

* 7.选择一个攻击方式，输入：1）FakeAP
<p align="center"><img src="https://camo.githubusercontent.com/d4957428ebb1c3576292ffbe68598944ea63418c/68747470733a2f2f322e62702e626c6f6773706f742e636f6d2f2d7262616f45736d494a50302f56373774304434463554492f41414141414141414273412f345065716c49545a7754672d472d336a7948635035336b346833685f41526f7241434c63422f73313630302f342d53656c65637425324261747461636b2e706e67" /></p>

* 8.选择本地握手包，不输入直接回车则开始自动抓包；
输入路径为绝对路径，如：/home/cap/some_wifi_mac.cap
<p align="center"><img src="https://camo.githubusercontent.com/2b7f894cfb7b532c7d2bbe3fef5d29d62a774e49/68747470733a2f2f332e62702e626c6f6773706f742e636f6d2f2d794a52777559785f454a772f563737743050426e4949492f41414141414141414273492f4a444a774658624a6f4c67795562797155466c416a37386d51334b416a714b7241434c63422f73313630302f352d48616e647368616b65253242537465702e706e67" /></p>

* 9.选择握手包检测模式；
建议选择为2 Pyrit
<p align="center"><img src="https://camo.githubusercontent.com/43bb8d83ed5a59c22fc00ad4a8ae1461809509fb/68747470733a2f2f342e62702e626c6f6773706f742e636f6d2f2d554e546d4b6a722d4a354d2f56373774304752775a34492f41414141414141414273452f496b3648306f306c4259596a664e557a3376565358674a41354d434b6430423667434c63422f73313630302f362532422d25324253656c656374253242746f6f6c253242616972637261636b2d6e672e706e67" /></p>

* 10.捕获握手包；
捕获之后，在弹出的窗口顶部会有显示，之后进行下一步
<p align="center"><img src="https://camo.githubusercontent.com/c10cf5201c511d3885dfc8045c41e23f454f3eb4/68747470733a2f2f342e62702e626c6f6773706f742e636f6d2f2d67354375746d50367137552f56373774306768554458492f414141414141414142734d2f5435793577345268797041526a347a644978346c546a7a30743237355a6c386241434c63422f73313630302f372532422d25324248616e647368616b652532426361707475726564253235324325324263686f6f7365253242636865636b25324268616e647368616b652e706e67" /></p>

* 11.选择钓鱼方式；
这里选择1）Webinterface
<p align="center"><img src="https://camo.githubusercontent.com/aca0d9c96ec6c888fea54d4fcef78c5f689ad5ab/68747470733a2f2f342e62702e626c6f6773706f742e636f6d2f2d5f6f4f70634445413831592f56373774303742564641492f41414141414141414273512f434f437954315a2d574b67787235495053485845536d414d313175516d62667a77434c63422f73313630302f382532422d253242416674657225324268616e647368616b65253235324325324263686f6f736525324261747461636b2e706e67" /></p>

* 12.选择语言，发起攻击；
这里找到"Chinese"
<p align="center"><img src="https://camo.githubusercontent.com/5fec95df198928da9a9b4434641e50c351ec7d0a/68747470733a2f2f332e62702e626c6f6773706f742e636f6d2f2d7871455a713175474b51412f56373774796771346e2d492f41414141414141414272732f75616c744a6b494b44767349434959647934594675676868426e68663148557667434c63422f73313630302f31302532422d25324246616b6525324241502532426372656174656425324225323533412532424d756c7469706c6525324270726f6365737365732532426174253242776f726b2e706e67" /></p>

* 13.客户端连接后界面
<p align="center"><img src="https://camo.githubusercontent.com/5fec95df198928da9a9b4434641e50c351ec7d0a/68747470733a2f2f332e62702e626c6f6773706f742e636f6d2f2d7871455a713175474b51412f56373774796771346e2d492f41414141414141414272732f75616c744a6b494b44767349434959647934594675676868426e68663148557667434c63422f73313630302f31302532422d25324246616b6525324241502532426372656174656425324225323533412532424d756c7469706c6525324270726f6365737365732532426174253242776f726b2e706e67" /></p>

* 14.成功后界面
<p align="center"><img src="https://camo.githubusercontent.com/bcd7c85bb4608a4df124bc88783f24f410742bbd/68747470733a2f2f332e62702e626c6f6773706f742e636f6d2f2d5261635f31754f43665f4d2f563737747a5247524e74492f41414141414141414272342f3554775948377843744d63716352485574515a3476366632544157505436476a51434c63422f73313630302f31322532422d253242446f6e652e706e67" /></p>

## 依赖版本
1. Aircrack : 1:1.2-0~rc4-0parrot0
2. Lighttpd : 1.439-1
3. Hostapd  : 1:2.3-2.3 _If you want to compare this type `dpkg -l | grep "name"`_

## 升级日志
Fluxion 几乎每周更新 [更新日志] (https://github.com/deltaxflux/fluxion).

## 支持!
Fluxion 比特币账户: 1EL4asZh5bsdtt7ECwLQmypeyC2e1TqvmW


## :octocat: Credits
1. Deltax - Fluxion main developer
2. Strasharo - contributor
3. l3op - contributor
4. dlinkproto - contributor
5. vk496 - developer of linset
6. ApatheticEuphoria - @WPS-SLAUGHTER,Bruteforce Script,Help with Fluxion
7. Derv82 - @Wifite/2
8. Princeofguilty - @webpages
9. Photos for wiki @http://www.kalitutorials.net
10. Ons Ali @wallpaper

## Useful links
 1. [Wifislax] (http://www.wifislax.com/)
 2. [Kali Linux] (https://www.kali.org/)
 3. [linset] (https://github.com/vk496/linset)
 4. [ares] (https://github.com/deltaxflux/ares)
 5. [Closeme] (https://github.com/rad4day/GithubScripts)

## Disclaimer

***Fluxion is intended to be used for legal security purposes only, and you should only use it to protect networks/hosts you own or have permission to test. Any other use is not the responsibility of the developer(s).  Be sure that you understand and are complying with the Fluxion licenses and laws in your area.  In other words, don't be stupid, don't be an asshole, and use this tool responsibly and legally.***
