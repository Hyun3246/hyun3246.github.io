---
title:  "Predict WAR with Classic Stats"
excerpt: "An innovative ensemble model that can predict baseball WAR"

categories:
  - Data Science & ML
tags:
  - [Machine Learning, Deep Learning, Research]

use_math: true
toc: true
toc_sticky: true

date: 2025-01-16
last_modified_at: 2025-01-16

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Predict WAR.png
---
## Full Article
[Predict WAR with Classic Stats](https://github.com/Hyun3246/Predict-WAR-with-Classic-Stats/blob/f267cfc73b9c3ecbdfc01bff730d991aac9f7ac7/Predict%20WAR%20with%20Classic%20Stats.pdf)

## Abstract
Wins Above Replacement (WAR) is a widely used metric in baseball. However, it is too complex to calculate. Therefore, we built a position player’s WAR predicting model only using 12 easily accessible classic stats. The final model is an ensemble stacking model, which consists of two best-performing models, random forest and XGBoost. The two base model was chosen among 8 different algorithms, by hyperparameters random searching. The final model has a strong performance not only in predicting WAR of the season, but also another seasons. By using the model and machine learning methodology we used, there will be an innovative change in baseball.

<br/>

## Structure of Final Model
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/Predict-WAR-with-Classic-Stats@master/Figures/Final Model Graphic.png"
       style="width: 50%; height: auto; margin:10px">
</figure>
<br/>

## References
1. Slowinski, P. What is WAR?, <https://library.fangraphs.com/misc/war/> (2010).
2. Slowinski, P. Replacement Level, <https://library.fangraphs.com/misc/war/replacement-level/>(2010).
3. Slowinski, P. WAR for Position Players, <https://library.fangraphs.com/war/war-position-players/> (2010).
4. Hamilton, M. et al. in Proceedings of the 3rd International Conference on Pattern Recognition Applications and Methods 520-527 (2014).
5. Koseler, K. & Stephan, M. Machine Learning Applications in Baseball: A Systematic Literature Review. Applied Artificial Intelligence 31, 745-763 (2018). https://doi.org/10.1080/08839514.2018.1442991
6. Huang, M.-L. & Li, Y.-Z. Use of Machine Learning and Deep Learning to Predict the Outcomes of Major League Baseball Matches. Applied Sciences 11 (2021). https://doi.org/10.3390/app11104499
7. Yaseen, A. S., Marhoon, A. F. & Saleem, S. A. Multimodal Machine Learning for Major League Baseball Playoff Prediction. Informatica 46 (2022). https://doi.org/10.31449/inf.v46i6.3864
8. Ishii, T. Using Machine Learning Algorithms to Identify Undervalued Baseball Players.(2016).
9. developers, s.-l. SVR, <https://scikit-learn.org/1.5/modules/generated/sklearn.svm.SVR.html> (2025).
10. Louppe, G. & Geurts, P. in Machine Learning and Knowledge Discovery in Databases: European Conference, ECML PKDD 2012, Bristol, UK, September 24-28, 2012. Proceedings, Part I 23. 346-361 (Springer).
11. Géron, A. Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow, 3rd Edition.(O'Reilly Media, Inc, 2022).
12. Freund, Y. & Schapire, R. E. A decision-theoretic generalization of on-line learning and an application to boosting. Journal of Computer and System Sciences 55, 119-139 (1997).
13. Breiman, L. Arcing the edge. (Citeseer, 1997).
14. Friedman, J. H. Greedy function approximation: a gradient boosting machine. Annals of statistics, 1189-1232 (2001).
15. Chen, T. & Guestrin, C. in Proceedings of the 22nd acm sigkdd international conference on knowledge discovery and data mining (2016).
16. Wade, C. Hands-On Gradient Boosting with XGBoost and scikit-learn. (Packt Publishing, 2020).
17. Ke, G. et al. Lightgbm: A highly efficient gradient boosting decision tree. Advances in neural information processing systems 30 (2017).
18. Prokhorenkova, L., Gusev, G., Vorobev, A., Dorogush, A. V. & Gulin, A. CatBoost: unbiased boosting with categorical features. Advances in neural information processing systems 31 (2018).
19. Dorogush, A. V., Ershov, V. & Gulin, A. CatBoost: gradient boosting with categorical features support. arXiv preprint arXiv 1810 (2018).

