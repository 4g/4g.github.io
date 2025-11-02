## Time series transformers

### Existing work

1. [**Timesfm**](https://arxiv.org/pdf/2310.10688) : (Google) tokens are embeddings coming from another network. Fed to a decoder only transformer. Output is converted to time series with another network. Mse loss over final time series. Input patch and output patch have different sizes.   
2. [**Universal Time Series Forecasting Transformer**](https://arxiv.org/pdf/2402.02592) **:** (SalesForce) same as above, multivariate. 

### Experiments

1. **Reimplement timesfm / utsft and train on lotsa data.** 

2. **Discrete tokenization** : Timesfm directly feeds timeseries patches into a network and trains this ‘tokenizer’ end to end. There are no discrete tokens. Loss comes by MSE on timeseries output. This is different from traditional discrete tokens / codebooks.  **Train audio like tokenizers and a a downstream model.** Unlike audio there are no frequency features and the input is coming from a highly stochastic process and created with no intent of consumption. In natural modalities data is created to be consumed and hence has less randomness. Check if the timesfm embeddings can be quantized into codebooks. Also code a tokenizer that converts these embeddings into codebooks. 

3. **Image based prediction :** Standard transformer but input is an image of stocks and task is defined in text.

4. **Physics based modelling :** We can *Feel* the market falling and rising. Both are continuous and hence predictable on small timescales. It will continue to fall unless there is a resisting force. It is a system where many actors together make a decision. It is a physical control system and should be like modelling one. 