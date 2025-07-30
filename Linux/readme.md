# 目次

- [Linuxディストリビューション](#linuxディストリビューション)
- [特色](#特色)
- [系統](#系統)
- [パッケージ管理システム](#パッケージ管理システム)
- [RedHad系のパッケージ管理](#redhad系のパッケージ管理)

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
|RedHat,CentOS|RPM(.rpm)|rpm,yum,dnf|
|Debian,Ubuntu|DEB(.deb)|dpkg,apt|


## RedHad系のパッケージ管理

- rpmコマンドの特徴
  - パッケージを個別に管理する
  - 依存関係や競合関係の解決は**手動で行う必要がある**

- yum(yellowdog updater modified)コマンドの特徴
  - リポジトリからパッケージを取得する
  - 依存関係や競合関係は**自力で解決する**
  - 一部の処理はバックグラウンドでrpmコマンドが使用される
  - 開発は終了しており、現在はdnfに置き換えられる

- dnf(Dandifiel Yum)コマンドの特徴
  - yumの後継で、パフォーマンス向上やメモリ使用量削減などの改善が加えられている
  - 依存関係や競合関係の管理やトランザクション処理がより効率的になっている

yumやdnfは依存管理などが自動のため、これらを使用することが一般的  

