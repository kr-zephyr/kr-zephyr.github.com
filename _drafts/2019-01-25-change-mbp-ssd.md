---
layout: post
title:  "맥북 프로 13인치 2015 SSD 교체하기"
date:   2019-01-25 00:00:00 +0900
categories: etc
tags: ['etc', 'mbp', 'ssd']
---

* content
{:toc}

제가 개인적으로 사용하는 장비는 맥북 프로 13인치 2015 중급형 모델입니다.  
이 녀석은 SSD가 256GB를 가지고 있는데, 이래저래 저장 공간이 부족함을 느끼게 됩니다. 잘 관리하고 사용하려면 사용할 수는 있지만 항상 잔여 용량을 체크하고 파일 정리하는 과정이 즐겁지만은 않죠.  
  
맥북 프로는 SSD를 사용하기는 하지만 표준 규격의 I/O를 가지고 있지 않은데다, OS 레벨에서 하드웨어를 체크하기 때문에 구매 시에 고용량을 선택하거나 일반적인 SSD가 아닌 고가의 맥북 전용 SSD를 사용해야 하는 부담이 있었습니다.  

그.런.데.  

OSX 하이시레라로 OS가 업그레이드되면서 nvme 인터페이스에 대한 규제가 풀어집니다.  
즉! 적절한 I/O 컨버터만 있다면 nvme 규격의 어떤 SSD라도 사용자가 교체할 수 있는 길이 열리게 된 것입니다!  
(물론 모든 조합이 잘 동작하지는 않고 많은 선구자들에 의해 궁합이 잘 맞는 어떠한 조합들이 생겨났습니다.)

### 참고

- [M.2 PCIe nvme Adapter for MACBOOK](https://www.aliexpress.com/item/M-Key-M-2-PCIe-X4-NGFF-AHCI-2280-SSD-12-16Pin-Adapter-Card-as-SSD/32855772670.html?spm=a2g0s.9042311.0.0.8d844c4dhj7dx8)
- [WD Black 1TB High-Performance NVMe PCIe Internal SSD - M.2 2280, 8 Gb/s - WDS100T2X0C](https://www.amazon.com/gp/product/B07BRCLMTS/ref=ppx_yo_dt_b_asin_title_o00__o00_s00?ie=UTF8&psc=1)
- [샤오미 Wiha 정밀 드라이버 세트](http://www.11st.co.kr/product/SellerProductDetail.tmall?method=getSellerProductDetail&prdNo=1883839706&xfrom=&xzone=)
- [MacBook Pro 13" Retina Display Early 2015 Repair](https://www.ifixit.com/Device/MacBook_Pro_13%22_Retina_Display_Early_2015)