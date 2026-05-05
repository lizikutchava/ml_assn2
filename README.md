# ml_assn2

# IEEE-CIS Fraud Detection
Kaggle-ის კონკურსის მიზანია ონლაინ საბანკო ტრანზაქციებზე თაღლითობის პროგნოზირება. ამისათვის დათად მოცემული გვაქვს Vesta Corporation-ის მონაცემები. პრობლემის გადასაჭრელად შეფასების მეტრიკად ვიყენებთ ROC_AUC-ს.

# რეპოზიტორიის სტრუქტურა
/model-experiment-logistic-regression.ipynb
Logistic Regression-ის ექსპერიმენტი
/model-experiment-random-forest.ipynb
Random Forest-ის ექსპერიმენტი
/model-experiment-xgboost.ipynb
XGBoost-ის ექსპერიმენტი, რომელიც წარმოადგენს საუკეთესო მოდელს
/model-inference.ipynb
საუკეთესო მოდელის საშუალებით ვაკეთებთ პროგნოზს test set-ზე და ვაგენერირებთ შესაბამის ფაილს.

# Feature Engineering
კატეგორიული ცვლადების რიცხვითში გადაყვანისთვის სამივე მოდელი იყენებს LabelEncoder-ს.
NaN მნიშვნელობებს Logistic Regression-სა და Random Forest-ში კატეგორიულებს ვცვლით 'missing'-ით, ხოლო რიცხვითებს მედიანით. XGBoost-ში კი ვცვლით -999-ით.
სვეტებს, რომელშიც 85%-ზე მეტი გამოტოვებული მნიშვნელობაა ვშლით.
ვამატებთ რამდენიმე ახალ feature-ს.

# Feature Selection
Random Forest და XGBoost-ში ვიყენებთ train-ის და test set-ის ყველა საერთო სვეტს target-ისა ID-ს გამოკლებით. Logistic Regression-ში დამატებით ვფილტრავთ საერთო სვეტებს. ასევე დამატებით ვიყენებთ VarianceThreshold-სა და ნორმალიზაციას.

# Training
გავტესტეთ სამი სხვადასხვა მოდელი: Logistic Regression, Random Forest, XGBoost.
Logistic Regression გამოვიყენეთ baseline-ად, Random Forest-მა გააუმჯობესა წინა შედეგი, ხოლო XGBoost აღმოჩნდა საუკეთესო.
Hyperparameter ოპტიმიზაციის მიდგომა:
scale_pos_weight - ავტომატურად ითვლის negative/positive თანაფარდობას
early_stopping_rounds - overfitting-ს ვიცილებთ თავიდან
class_weight="balanced" - კლასების დაუბალანსებლობას ვაკომპენსირებთ
საბოლოოდ, XGBoost შეირჩა საუკეთესო მოდელად შედეგიდან გამომდინარე, რადგან უმკლავდება დაუბალანსებელ კლასებს და უზრუნველყოფს overfitting-ის კონტროლს.

# MLflow Tracking
MLflow ექსპერიმენტების ბმული: https://dagshub.com/lkuch23/ml_assn2
XGBoost შედეგად იძლევა AUC=0.97
