# **1. 데이터 전처리**

```python
import numpy as np
import pandas as pd

#범죄율
pd.read_table(./)
crime = pd.read_excel('./data/Report.xls')
crime.drop(['합계.1','살인.1','강도.1','강간강제추행.1','절도.1','폭력.1'],axis=1,inplace=True)
display(crime)
#dateframe 내 자치구 칼럼에서 합계 문자열 포함한 행 제거
crime = crime[~crime['자치구'].str.contains('합계')]
#0 인덱스는 다음 작업에서 불필요하므로 제거
crime.drop([0],axis=0,inplace=True)
crime['기간']=crime['기간'].astype(int)
#crime.drop('기간',inplace=True)
crime1 = crime.groupby(['기간','자치구']).sum()
crime1

#CCTV 지역별 설치 개수
cctv = pd.read_excel('./data/CCTV통계.xlsx')
cctv = cctv.drop(['소계','2011년 이전','2012년','2013년'],axis=1)
cctv.columns = ['기관명',2014,2015,2016,2017,2018]
cctv['기관명']=cctv1['기관명'].str.replace(" ","")
cctv = cctv.set_index('기관명')
cctv = cctv.unstack(level=0)
display(cctv)

#서울시 지역별 인구 수
pop = pd.read_excel('./data/인구통계.xls',header=1)
pop.set_index('기간',inplace=True)
pop.drop(['합계.1','합계.2','한국인.1','한국인.2','등록외국인.1','등록외국인.2','인구밀도','인구밀도.1','세대당인구','65세이상고령자'],axis=1,inplace=True)
pop = pop[~pop['자치구'].str.contains('합계')]
pop = pop.drop(pop.index[0])
pop = pop.groupby(['기간','자치구']).sum()/4 #왜 mean은 안되는건지 찾아볼것
pop[['세대','합계','한국인','등록외국인']] = pop[['세대','합계','한국인','등록외국인']].astype(int) #우선 합계를 4로 나눈것이기때문에 float 값을 int 값으로 변환 시켜줘야 함.
display(pop)

#3가지 concat으로 데이터 통합
merged = pd.concat([cctv,pop,crime],axis=1)
merged1=merged.to_excel('./data/merged1.xlsx') #통합데이터 엑셀파일로 우선 저장


```

# **2. 그래프 시각화**

```python

```



# **3. 예측 프로그래밍**

```python

```





