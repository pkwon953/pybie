# **1. 데이터 전처리**

```python
import numpy as np
import pandas as pd

#범죄율
crime = pd.read_excel('./data/Report.xls')
#crime에서 column들을 drop시킬때, column_name보다 편리한 방법 사용.
crime.drop(crime.columns[3::2],axis=1,inplace=True)
display(crime)
#dateframe 내 자치구 칼럼에서 합계 문자열 포함한 행 제거 리스트 컴프리헨션
crime = crime[~crime['자치구'].str.contains('합계')]
#0 인덱스는 다음 작업에서 불필요하므로 제거
crime.drop([0],axis=0,inplace=True)
crime['기간']=crime['기간'].astype(int)#int 타입으로 바꿔주는 이유는 아래 데이터와 합칠때 다르다고 인식하는것을 방지하기 위해 작업함.
crime = crime.pivot_table(index = ['기간','자치구'],aggfunc='first')#non numeric value 연산 넘길때 aggfunc ='first' 사용한다.

crime

#CCTV 지역별 설치 개수
cctv = pd.read_excel('./data/CCTV통계.xlsx')
cctv = cctv.drop(cctv.columns[1:5],axis=1)
cctv.columns = ['자치구',2014,2015,2016,2017,2018]
cctv['자치구']=cctv1['자치구'].str.replace(" ","")
cctv = cctv.set_index('자치구')
cctv = cctv.unstack(level=0)
display(cctv)

#서울시 지역별 인구 수
pop = pd.read_excel('./data/서울시 주민등록인구 (구별) 통계(2014년~2018년).xls',header=1)
pop.set_index('기간',inplace=True)
#불필요한 데이터 칼럼 삭제
pop.drop(pop.columns[3::4],axis=1,inplace=True)
pop.drop(pop.columns[3::2],axis=1,inplace=True)
pop.drop(pop.columns[5:],axis=1,inplace=True)

# pop.set_index('기간',inplace=True)
pop = pop[~pop['자치구'].str.contains('합계')]
pop = pop.drop(pop.index[0])

pop = pop.pivot_table(index = ['기간','자치구'],aggfunc='first')
display(pop)

#3가지 concat으로 데이터 통합
merged = pd.concat([cctv,pop,crime],axis=1)
merged1=merged.to_excel('./data/merged1.xlsx') #통합데이터 엑셀파일로 우선 저장

merged = pd.read_excel('./data/merged3.xlsx',index_col=[0,1])

merged.rename(columns={0:'CCTV'},inplace=True)
merged['10만명당 범죄 수']=merged['범죄합']/merged['합계']*100000
merged['10만명당 CCTV 수']=merged['CCTV']/merged['합계']*100000
merged[['10만명당 범죄 수','10만명당 CCTV 수']]=merged[['10만명당 범죄 수','10만명당 CCTV 수']].astype(int)

```

# **2. 그래프 시각화**

```python

```



# **3. 예측 프로그래밍**

```python

```





