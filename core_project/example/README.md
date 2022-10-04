# Motoko bootcamp : NFT minter. 

Basic NFT minter inspired by the DIP 721 standard (implementation not guarantee, consider this example as an educational ressource. For a production project with DIP721, please take a look at the official DIP721 repo).

DIP721規格にインスパイアされた基本的なNFT minter (実装は保証しません。この例は教育用リソースとして考えてください。DIP721を用いたプロダクションプロジェクトについては、DIP721の公式レポを参照してください）。

## Running the project locally プロジェクトをローカルで実行する

If you want to test your project locally, you can use the following commands:

プロジェクトをローカルにテストしたい場合は、次のコマンドを使用します。

```bash
# Install dependencies
# 依存関係のインストール
npm run start

# Starts the replica
# レプリカを起動する
dfx start 

# Deploys your canisters to the replica and generates your candid interface
# キャニスターをレプリカに配備し、candid インターフェイスを生成します。
dfx deploy --argument '("<NAME OF YOUR COLLECTION>","<SYMBOL OF YOUR COLLECTION>")'
```

Once the job completes, your application will be available at `http://localhost:8000?canisterId={asset_canister_id}`.
Additionally, if you are making frontend changes, you can start a development server with

ジョブが完了すると、あなたのアプリケーションは `http://localhost:8000?canisterId={asset_canister_id}` で利用可能になります。
さらに、フロントエンドを変更する場合、開発用サーバーを起動する際には
```bash
npm start
```


Thanks to https://github.com/torates/testMinter for the inspiration.

インスピレーションを与えてくれたことに感謝します。 https://github.com/torates/testMinter
