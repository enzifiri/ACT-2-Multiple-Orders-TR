# Place multiple Long/Short orders in one transaction (bundled order placement) in any market on Vortex. Currently this needs to be done via CLI
<a href="https://3pgv.notion.site/b7a73a18ef444b9483b5601bf833bae8?v=9111c2c97f2842c5aa75b8d5e5b00a1e">Tüm Sei Görevleri</a>
<a href="https://docs.google.com/forms/d/1qxpIL-ATe1HMX87w1P7BjMqpjXExlKyo1_btEJi00JM/viewform?edit_requested=true">Sei Formu</a>

# 1- Öncelikle TX Gövdesi Oluşturuyoruz.
Creator ve Account karşısındaki "seiadresiniz" kısmına kendi sei cüzdanınızı yazın.
Kodu 1 seferde girin ve tırnakları kaldırmayın!!
ContractAddr kısmında değişiklik yapmayın orası olduğu gibi kalsın.

```
echo '{
  "body": {
    "messages": [
      {
        "@type": "/seiprotocol.seichain.dex.MsgPlaceOrders",
        "creator": "seiadresiniz",
        "orders": [
          {
            "id": "0",
            "status": "PLACED",
            "account": "seiadresiniz",
            "contractAddr": "sei14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9sh9m79m",
            "price": "1.000000000000000000",
            "quantity": "0.000010000000000000",
            "priceDenom": "USDC",
            "assetDenom": "ATOM",
            "orderType": "LIMIT",
            "positionDirection": "LONG",
            "data": "{\"position_effect\":\"Open\",\"leverage\":\"1\"}",
            "statusDescription": ""
          }
        ],
        "contractAddr": "sei14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9sh9m79m",
        "funds": [
          {
            "denom": "uusdc",
            "amount": "10"
          }
        ],
        "autoCalculateDeposit": false
      },
      {
        "@type": "/seiprotocol.seichain.dex.MsgPlaceOrders",
        "creator": "seiadresiniz",
        "orders": [
          {
            "id": "0",
            "status": "PLACED",
            "account": "seiadresiniz",
            "contractAddr": "sei14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9sh9m79m",
            "price": "1.000000000000000000",
            "quantity": "0.000010000000000000",
            "priceDenom": "USDC",
            "assetDenom": "ATOM",
            "orderType": "LIMIT",
            "positionDirection": "LONG",
            "data": "{\"position_effect\":\"Open\",\"leverage\":\"1\"}",
            "statusDescription": ""
          }
        ],
        "contractAddr": "sei14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9sh9m79m",
        "funds": [
          {
            "denom": "uusdc",
            "amount": "10"
          }
        ],
        "autoCalculateDeposit": false
      }
    ],
    "memo": "",
    "timeout_height": "0",
    "extension_options": [],
    "non_critical_extension_options": []
  },
  "auth_info": {
    "signer_infos": [],
    "fee": {
      "amount": [
        {
          "denom": "usei",
          "amount": "0"
        }
      ],
      "gas_limit": "0",
      "payer": "",
      "granter": ""
    }
  },
  "signatures": []
}' > $HOME/gen_tx.json
```
<H1> 2. TXi imzalıyoruz </H1>
seiadresiniz kısmına adresinizi yazın.

```
ACC=$(seid q account seiadresiniz -o json | jq -r .account_number)
```
```
seq=$(seid q account seiadresiniz -o json | jq -r .sequence)
```
From kısmına cüzdan adınızı yazın. Kodu tek bir seferde yazabilirsiniz.
```
seid tx sign $HOME/gen_tx.json -s $seq -a $ACC --offline \
--from walletisminiz --chain-id atlantic-1 \
--output-document $HOME/txs.json
```
<h1>3. Tx yayını </h1>

```
seid tx broadcast $HOME/txs.json
```
<h1> Başarılı olursa, code: 0 çıktısı alacaksınız </h1>

```
code: 0
codespace: ""
data: ""
events: []
gas_used: "0"
gas_wanted: "0"
height: "0"
info: ""
logs: []
raw_log: '[]'
timestamp: ""
tx: null
txhash: 5BA641A155C054BB51A709AA09D703FF98FBEBF214415A186788B78B048DC29C
```

İngilizce kaynak ve hata çözümleri;
https://craving-for-knowledge.gitbook.io/craving_for_knowledge/proekty/sei/act-2-missions/place-multiple-orders-in-one-transaction
