# Precision & recall

정답\예측결과 |  Positive | Negative
---- | ---------- | ---- 
Positive | TP(true positive) | FN(false negative) 
Negative | FP(false positve) | TN(true negative)


### Precision(정밀도) : positive로 예측된 것 증에, 진짜로 옳은 검출인 비율

![precision](http://latex.codecogs.com/gif.latex?Precision%20%3D%20%5Cfrac%7BTP%7D%7BTP&plus;FP%7D)



### Recall(재현율) : 실제 positive인 검출 중에, 제대로 positive라고 검출 된 것의 비율

![Recall](http://latex.codecogs.com/gif.latex?Precision%20%3D%20%5Cfrac%7BTP%7D%7BTP&plus;FN%7D)

obejct detection 알고리즘의 성능을  둘 중 하나로만 평가하는 것은 옳지 않다.
 한 예로, 실제로 검출되어야 하는 객체는 100개인데, 알고리즘이 검출한 객체는 10개이다.
알고리즘이 검출한 객체 10개중 9개가 정답이라고 해보자. Precision은 9/10=0.9 이지만, Recall은 10/100=0.1이다. 이처럼 precision과 recall은 서로 trade-off 관계에 있다. 그렇기 때문에, 두 가지를 모두 종합하여 성능을 평가해야만 한다. 이를 나타낸 것이 AP, 즉, precision-recall 곡선이다. 

object detection에서 어떻게 TP와 FP를 판단할까? IoU(Intersection over Union)를 통해 판단한다. 정답인 박스와, 예측된 박스간의 교집합을 합집합의 면적으로 나누어 준다. 이 비율이 (threshold) 이상이면 TP로, (threshold) 미만이면 FP로 판단한다.

threshold= 0.5라고 가정하자.
우선 클래스 종류가 하나인 경우부터 살펴보자. 
다음은 얼굴 검출 실험결과의 일부를 가지고 온 것이다. 10개의 정답이 존재하고 검출된 얼굴은 다음과 같디 7개이다.

검출 index |  confidence score | 판별 | precison | recall
---- | ----------  | ---------- | ---------- | ----------
1 | 88%  | TP | 1/1=1 | 1/10=0.1 
2 | 90%  | TP | 2/2=1 | 2/10
3 | 98%  | TP | 3/3=1 | 3/10
4 | 67%  | TP | 4/4=1 | 4/10
5 | 23%  | FP | 4/5 | 4/10
6 | 87%  | TP | 5/6 | 5/10
7 | 46%  | FP | 5/7 | 5/10

다음과 같이 precision 과 recall을 판별해서 그래프를 나타내보면 다음과 같은 형태를 띤다.


![image](https://user-images.githubusercontent.com/44438752/62420609-02ec3c80-b6d0-11e9-82d9-cd677d2452d5.png)


AP 면적을 구해서 AP값을 구하게된다. 면적이 클 수록 성능이 더 좋은 것으로 판별할 것이다. 이를 확장시켜 클래스가 여러 개인 경우에는 클래스 별 AP를 구한 다음 평균을 계산하여 성능을 평가한다.(mAP: mean average precision)
