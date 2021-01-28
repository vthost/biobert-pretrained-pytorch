# BioBERT Pre-trained Weights for PyTorch
This repository provides a PyTorch version of the pre-trained weights of BioBERT, a language representation model for the biomedical domain, proposed in [(Lee et al. 2019)](https://arxiv.org/abs/1901.08746). 

Please go to the [release section](https://github.com/vthost/biobert-pytorch/releases) to download the models. The original TensorFlow models can be found [here](https://github.com/naver/biobert-pretrained).

The [DMIS GitHub repository for BioBERT](https://github.com/dmis-lab/biobert) provides details about BioBERT.

## Application

You should be able to run the models using the code from [Hugging Face](https://github.com/huggingface/transformers). I used [version 2.2.1](https://github.com/huggingface/transformers/tree/v2.2.1/transformers) and only adapted the code as follows:

[run_squad.py](https://github.com/huggingface/transformers/blob/734a28a767e94d0273d7130db21a2ed5c113c51f/examples/question-answering/run_squad.py):
  >     global_step = 0
  
  def evaluate
  >     # Evaluate with the official SQuAD script
  >     # evaluate_options = EVAL_OPTS(data_file=args.predict_file,
  >     #                              pred_file=output_prediction_file,
  >     #                              na_prob_file=output_null_log_odds_file)
  >     # results = evaluate_on_squad(evaluate_options)
  >     # return results
  
  def main
  >     # Evaluate
  >     # result =
  >     evaluate(args, model, tokenizer, prefix=global_step)  

  >     # result = dict((k + ('_{}'.format(global_step) if global_step else ''), v) for k, v in result.items())
  >     # results.update(result)

  >     logger.info("FINISHED!")#"Results: {}.format(results))

  >     #return results  
  
[modeling_bert.py](https://github.com/huggingface/transformers/blob/734a28a767e94d0273d7130db21a2ed5c113c51f/src/transformers/modeling_bert.py):
  
  def __init__ (in BertForQuestionAnswering)
  >     # name needs to correspond to variable in pretrained tf model to get weights correctly initialized
  >     self.classifier = nn.Linear(config.hidden_size, config.num_labels)
  >     self.activation = nn.Sigmoid()
  
  def forward
  >     logits = self.classifier(sequence_output)


## License and Disclaimer
Please see the LICENSE file for details. Downloading the weights indicates your acceptance of our disclaimer.

## Contact information
For help or issues using the pre-trained weights, please submit a GitHub issue. We only used our pre-trained models for question answering so far, so we most likely cannot help with other tasks. For more general questions about BioBERT, please refer to the [DMIS GitHub repository for BioBERT](https://github.com/dmis-lab/biobert).
