# informal-gpt

これは、早稲田大学理工学術院情報理工・情報通信専攻科目「自然言語処理」のグループワークにおいて実装したものです。

## About

OpenAI社よりリリースされているGPT2-mediumを強化学習によってファインチューニングし、インフォーマルな文体で文章を生成するよう調整します。

- 自己回帰テキスト生成モデルに[gpt2-medium](https://huggingface.co/gpt2-medium)を
- 強化学習における報酬モデルに[s-nlp/roberta-base-formality-ranker](https://huggingface.co/s-nlp/roberta-base-formality-ranker)の"informal"クラスに対応するロジット出力を
- データセットに[binhgiangnguyendanh/reddit_casual_conversation_for_alpaca_lora](https://huggingface.co/datasets/binhgiangnguyendanh/reddit_casual_conversation_for_alpaca_lora)(60%)と[wikitext](https://huggingface.co/datasets/wikitext)(40%)を

それぞれ使用します。ただし、ここでは強化学習によってチューニングを行うため、訓練時はデータセットのテキストを全文入力してパラメータを更新するのではなく、データセット（コーパス）の各文の先頭部分を切り出したものを用意してその続きをGPT-2に生成させ、出来上がった文章を報酬モデルによって評価させています。

## implementation

Hugging Faceの[trl](https://huggingface.co/docs/trl/index)を使用します。🤗Accelerateを使用して複数GPUで訓練を行う場合は`how-to-use-accelerate.md`に従ってください。