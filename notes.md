# Steps to Reproduce the Conversion

1. Create anaconda environment (install transformers in there to get all dependencies)
- conda create --name transformers
- conda activate transformers
- pip install torch
- pip install wrapt --upgrade --ignore-installed
- pip install tensorflow
- pip install transformers 

2. Prepare transformers code
- git clone https://github.com/huggingface/transformers.git
- Adapt code as described [here](https://github.com/huggingface/transformers/issues/438#issuecomment-479405364), that is,  import and use BertForTokenClassification instead of BertForPreTraining in transformers/convert_bert_original_tf_checkpoint_to_pytorch.py.

3. Download the TensorFlow BioBERT weights

4. Convert
- cd transformers/src/transformers
- export BERT_BASE_DIR=$YOUR_PATH/biobert_v1.1_pubmed
- python convert_bert_original_tf_checkpoint_to_pytorch.py --tf_checkpoint_path $BERT_BASE_DIR/model.ckpt-1000000 --bert_config_file $BERT_BASE_DIR/bert_config.json --pytorch_dump_path $BERT_BASE_DIR/pytorch_model.bin
- cd $YOUR_PATH/biobert_v1.1_pubmed
- cp bert_config.json config.json
- NOTE: for the v1.0 BioBERT models, in the above command, it's model.ckpt instead of model.ckpt-1000000
