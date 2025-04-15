# Docker

## Docker desktop
windowsでdockerを使う場合には、WSL2が推奨されている。
## 手順
docker desktopをインストールする。
起動してエラー
WSL2 は、現在のマシン構成ではサポートされていません。
WSL2 を使用するには、"Linux 用 Windows サブシステム" オプション コンポーネントを有効にしてください。
"仮想マシン プラットフォーム" オプション コンポーネントを有効にし、さらに、BIOS で仮想化を有効にしてください。
"仮想マシン プラットフォーム" を有効にするには、次のコマンドを実行します: wsl.exe --install --no-distribution
詳細については、https://aka.ms/enablevirtualization をご覧ください。

このエラーメッセージが出たら **#1** と **#2**を実行する
これでdocker desktopが使用できるようなる。


## #1. WSL2を有効にする
設定 -> システム -> オプション機能 -> Windowsのその他機能 -> Linux用のWindowsサブシステムをチェック

## #2. BIOSの設定
パソコンに搭載されているCPUによって有効化する仮想化技術の名称が異なります。
Intel製…Intel Virtualization Technology、Inte-VTなど
AMD製…AMD-Virtualization、AMD-Vなど

 ### 手順
パソコンを起動したときに、ロゴマークが出たときに、F2 か F10 か Del を押すとBIOSが開く。
Advanced Modeにして、詳細を押す。
CPU設定のIntel Virtualization Technologyを有効にする。

## WSL（Windows Subsystem for Linux）
Windows上でLinux環境を実行するためのサブシステムです。
これにより、ユーザーは仮想マシンやデュアルブートを使用せずに、Windows上で直接Linuxアプリケーションを実行できます。
windous上で仮想マシンが動作するホストOS型。
