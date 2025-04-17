# docker desktop
windowsでdockerを使う場合には、WSL2が推奨されている。
## 手順
docker desktopをインストールして起動する。

```bash
WSL2 は、現在のマシン構成ではサポートされていません。
WSL2 を使用するには、"Linux 用 Windows サブシステム" オプション コンポーネントを有効にしてください。
"仮想マシン プラットフォーム" オプション コンポーネントを有効にし、さらに、BIOS で仮想化を有効にしてください。
"仮想マシン プラットフォーム" を有効にするには、次のコマンドを実行します: wsl.exe --install --no-distribution
詳細については、https://aka.ms/enablevirtualization をご覧ください。
```
このエラーメッセージが出たら下記の **#1** と **#2**を実行することで、docker desktopが使用できるようなる。


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


#DockerでVite + React + TypeScript を動かす構成

## 📁プロジェクト構成
```bash
task-tool/
├── Dockerfile
├── docker-compose.yml
├── vite.config.ts
├── package.json
├── tsconfig.json
├── public/
└── src/
    └── App.tsx
```
## 🐳Dockerfile
```bash
# Node.jsの公式イメージを使用
FROM node:20

# 作業ディレクトリ作成
WORKDIR /app

# 依存ファイルをコピー
COPY package*.json ./
COPY tsconfig.json ./
COPY vite.config.ts ./

# 依存関係をインストール
RUN npm install

# ソースコードをコピー
COPY . .

# 開発サーバーを起動（ポートはViteのデフォルト：5173）
CMD ["npm", "run", "dev"]
```

## 🐳docker-compose.yml
```bash
version: '3.9'

services:
  vite-app:
    build: .
    ports:
      - "5173:5173"
    volumes:
      - .:/app
      - /app/node_modules
    environment:
      - HOST=0.0.0.0
```
## 🛠️package.json の dev スクリプトに --host を追加（重要）
ViteをDockerで動かすにはホストを 0.0.0.0 に指定する必要があります：
```bash
"scripts": {
  "dev": "vite --host"
}
```
##  🚀Dockerで起動
```bash
docker-compose up --build
```
その後、ブラウザで
👉 http://localhost:5173 を開いて、Reactアプリが動いているか確認！

## 補足ポイント
volumes を使ってるので、ホスト側のコードを編集すると 即時反映（ホットリロード） されます。
コンテナ上で node_modules を分離してるので、パーミッション問題を避けられます。

# 別のパソコンでVite + React + Docker環境を再現する方法
## プロジェクト一式をコピー（またはGitでクローン）
```bash
git clone https://github.com/your-username/your-repo.git
cd your-repo
```

##  新しいPCに必要なものをインストール
Docker Desktop をインストール（Windows/macOS）

## プロジェクトフォルダに移動
```bash
cd tsk-tool
```

## Dockerで起動！
```bash
docker-compose up --build
```





