# 目次

- [ロードバランサー](#ロードバランサー)

## Linuxディストリビューション

まずは言葉の整理から

Linux：厳密にはOSの核となる「カーネル」を指す。（カーネルだけではPCを使えない）  
ディストリビューション：カーネルにプラスして、必要なものをひとまとまりにして配布しているもの。  


## 特色

Linuxディストリビューションには様々存在する。  
- Ubuntu：使いやすさと初心者への配慮を重視  
- CentOS（AlmaLinux/Rocky Linux）：サーバでの安定運用を重視
- Arch Linux：最新性とカスタマイズ性を重視
- Kali Linux：セキュリティテストに特化

## 系統

- RedHat系：Red Hat Enterprise Linuxを中心に派生したディストリビューション  
  fedora、CentOS、AlmaLinux（参考：https://note.com/_chibisuke/n/n0ae85ead39cd）  
  AmazonLinuxもRedHat系

- Debian系：ボランティアによって開発されているDebianを中心に派生したディストリビューション  
  Ubuntu、LinuxMint、elementaryOS  
  Raspberry Pi OSもDebian系  

## パッケージ管理システム

linuxのパッケージ管理システム

|ディストリビューション|分類(拡張子)|管理コマンド|
|-|-|-|
|RedHat,CentOS|RPM(.rpm)|rpm,yum,def|
|Debian,Ubuntu|DEB(.deb)|dpkg,apt|


## RedHad系のパッケージ管理

