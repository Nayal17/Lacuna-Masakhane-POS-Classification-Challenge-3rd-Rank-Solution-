## Team Info:
- Himanshu Nayal
- Ahmed Attia

## Environment info: 

- We have used Kaggle's GPU T4 x2.
- For best reproducibility use similar environment, as in MLM notebook batch size is fixed per device so changing number of gpus may change the batch size and hence results by a slight margin. (Important)

## Dataset and Notebooks NOTE:

- All data(https://zindi.africa/competitions/lacuna-masakhane-parts-of-speech-classification-challenge/data) and notebooks used are provided along with this summary.
- For smooth process we have also provided original kaggle notebook links where with simple run we can reproduce the exact results.

## Solution Summary:

### MLM:
- MLM is done on luo+tsn+pcm+wol languages, where pcm and wol are from train data and luo+tsn data is extracted from NER data of same repo: https://github.com/masakhane-io/lacuna_pos_ner/tree/main/language_corpus
- Use T4x2 GPU to reproduce same mlm model or use this notebook link from kaggle (Version 9 is used from this notebook): https://www.kaggle.com/code/himanshunayal/mlm-on-lm-pos

	
## Training: 
- Training is done on full data (18 languages) using mlm model trained in the last step.
- On full data with mlm we got the score of 0.718 (Use Version 82 of the notebook) : https://www.kaggle.com/code/lastopt/lm-pos-classification-train-model-1
- We have done pseudo labelling iteratively on train+test data 3 times:
	- Round 1: using pseudo labels from best score of 0.718 we trained again on train and test data and got accuracy of 0.721 (version 2 of the notebook mentioned in 4.)
	- Round 2: Now doing it again with test predictions of 0.721 we got 0.723. (version "round 2 pseudo" of the notebook mentioned in 4.)
	- Round 3: In third round we got a score of 0.724. (version "pseudo round 3" of the notebook mentioned in 4.)
		
- Link to the pseudo labelling kaggle notebook: https://www.kaggle.com/code/ahmedattia143/lacuna-pos-train-pseudo-labeling
	
- Inference notebook link: https://www.kaggle.com/code/lastopt/lm-pos-classification-infer
- After each step of pseudo labeling, make sure to run the inference notebook using the new model to get predictions on test so they can be used in the next pseudo labeling round.
