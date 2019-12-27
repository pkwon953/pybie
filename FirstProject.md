# **1. 데이터 전처리**

```python
import numpy as np
import pandas as pd

#범죄율
crime = pd.read_excel('./data/Report.xls')
crime.drop(['합계.1','살인.1','강도.1','강간강제추행.1','절도.1','폭력.1'],axis=1,inplace=True)
display(crime)
#crime.set_index('기간',inplace=True)
crime = crime[~crime['자치구'].str.contains('합계')]
#crime.drop('기간',inplace=True)
crime1 = crime.groupby(['기간','자치구']).sum()
crime1
#CCTV 지역별 설치 개수
cctv = pd.read_excel('./data/서울시 자치구 년도별 CCTV 설치 현황(2011년 이전_2018년).xlsx')
display(cctv.head())
cctv1 = cctv.drop(['소계','2011년 이전','2012년','2013년'],axis=1)
cctv1['기관명']=cctv1['기관명'].str.replace(" ","")
cctv = cctv1.set_index('기관명')
display(cctv)
#서울시 지역별 인구 수
pop = pd.read_excel('./data/서울시 주민등록인구 (구별) 통계(2014년~2018년).xls',header=1)
#pop.set_index('기간',inplace=True)
pop.drop(['인구밀도','인구밀도.1','세대당인구','65세이상고령자'],axis=1,inplace=True)
pop['기간']=pop['기간'].astype(str)
# display(pop)

```

