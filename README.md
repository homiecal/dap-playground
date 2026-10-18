- performance of weakly grounding method, sufferes when multiple diseases and small disease sizes, DAP paper highlights this but doesn't confirm if their method improves on these metrics, would be interesting to see if it does
- quick experiment using a subset of the padchest-gr dataset (129 records, 76 with disease findings)
  - chexzero weights used
  - chefer interpretability method used
- trends of dice score across disease count and disease size was found for the padchest-gr subset
- multiple qualitative examples were investigated

- Example: **101354916913099012081924155376991837012_81ss65.png**
    - Has a single disease "**Left** pleural fusion", though interpretability map shows localisation entirely in the **right** lung area, with a dice score of 0 (at thresholds of 0.3, 0.4, 0.5) with the ground truth. This example would likely improve under the DAP method - and is a likely example where BG tokens are associated with the global text token.
    - What is interesting, is just how poor the localisation is - it is also interesting (and not necessarily suprising) that the interpretability map does not change much with the change of text, for example referring to morphological descriptions of the disease does not improve the grounding.
    - Additionally, the model correctly predicts the original text description very confidently (99% using scaled logits after softmax from ChexZero), despite interpretability map being in the opposite lung with a dice of 0.5.

- Example: **101120174235725780234709445792984239056_2oib6d.png**
    - 7 findings, poor dice
    - some very small disease patches, and large patches, model is overall quite poor, and there is a highly salient area "hiatal hernia"


- Example: **101126299944644944835561376898203180176_2_o5vjuy.png**
    - 5 findings, poor dice
    - highly salient area (relating to "retrocardiac alecstasis") across all the findings - is the model unable to differentiate based on diseases??



- Did DAP improve on the multiple disease grounding
  - things to distinguish between, when diseases are correlated, or independent does the model behave differently - the reason for this is the model might improve when diseases have lower correlation, because there's enough training samples of each disease (when it is the only disease in the image) - which is why when diseases are correlated it may be harder to improve the grounding
    - i.e. example of one diseas that often presents with the other in a different spatial region
    - vs
    - two independent diseases
