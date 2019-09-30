---
categories: [RL]
tags: [RL, bidding]
title: Paper Review - Optimizing Budget Constrained Spend in Search Advertising
---
Google 검색광고 플랫폼 관점에서 제한된 예산 내에서 Sponsored Search의 bidding에 대한 최적화를 다룬 논문

- Google Research
- Optimized budget allocation problem: 지정한 목표를 최적화하면서 예산 제한이 충족되도록 광고주를 쿼리에 할당
- 사용자가 저품질 광고를 본다면 광고를 무시하고, 이는 (광고플랫폼의) 수익을 감소시킨다.
광고주의 ROI가 낮다면 광고주는 입찰가와 예산을 감소시키고 이는 (광고플랫폼의) 수익 감소로 이어진다.
- 논문의 목표
    - 광고 품질(CTR 최대화)
    - 광고주 cost-per-click 감소(클릭 수 최대화)(CPC광고가 아닌 듯)
    - 광고주 ROI 증대
- $$ctr_{(a,q)}$$은 position-independent로 모델링.
- Generalized second price auction(GSP): $$ cpc_(a_j) = bid_{(a_{j+1},q)} ctr_{(a_{j+1},q)}/ctr_{(a_j,q)}$$
- Rank 별 CTR 차이는 고려하지 않음.

## 4.1 Optimized Throttling

* **Optimized Throttling** algorithm:  
>* For each arriving query q:  
>    * For each budget constrained advertiser a:  
>        * If $$B_{\theta,a}(\theta(i))\le B_a / T_a$$, then a participates in the auction.
* 이 알고리즘은 모든 광고주에게 공정한 해결책이다.
* 특정한 제약조건 하에서는 최적의 해결책이다. 제약조건이 유지되지 않는 많은 사례가 있지만, 현실적으로는 최적에서 크게 벗어나지 않을 만큼 충분히 제약조건이 유지된다. 
* 우리는 질의어 공간으로부터 나온 도메인을 질의어들의 어떤 속성 분포로 변환한다. 꼬리 쪽의 질의어 빈도 예측은 어렵지만, (우리 알고리즘에서 다루는) 질의어 속성의 분포 예측은 매우 다루기 쉽다.
* 측정법의 선택으로 넓은 범위의 목표나 목표들의 조합을 최적화할 수 있다.

||Objective|$$\theta(i)$$|
|---|---|---|
|OT-CTR|Ad quality|$$\textbf{ctr}_i$$|
|OT-Clicks|Clicks|$$1/\textbf{cpc}_i$$|
|OT-Profit|Profit|$$(\textbf{bid}_i - \textbf{cpc}_i)/\textbf{cpc}_i$$|
|OT-Conversions|Conversions|$$\textbf{cvr}_i \textbf{val}_i / \textbf{cpc}_i$$|
|OT-CTR-Profit|Blend|$$\textbf{ctr}_i (\textbf{bid}_i - \textbf{cpc}_i ) / \textbf{cpc}_i$$|

## 4.2 System design and implementation
* Primary components
  * estimating $$B_a / T_a$$
  * estimating and cmpressing $$R_{\theta,a}$$, and
  * using the estimates at serving time.
