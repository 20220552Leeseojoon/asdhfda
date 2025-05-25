# asdhfda

import pandas as pd
import matplotlib.pyplot as plt

# CSV 파일 불러오기
raw_data = pd.read_csv('./survey_results_public.csv')

# 필요한 열만 추출
target_data = raw_data[['Age', 'Country', 'LanguageHaveWorkedWith', 'LearnCode']]

# 'LearnCode' 열에서 복수 선택된 값들을 ';' 기준으로 나눔
methods = target_data['LearnCode'].dropna().str.split(';')

# 각 방법들을 한 행씩 분해
exploded_methods = methods.explode()

# 각 학습 방법별 응답 수 세기
size_by_methods = exploded_methods.value_counts()

# 상위 10개 방법을 파이차트로 시각화
plt.figure(figsize=(5, 5))
size_by_methods.nlargest(10).plot.pie(autopct='%1.0f%%')
plt.ylabel('')  # y축 레이블 제거
plt.title('Top 10 Coding Learning Methods')
plt.tight_layout()
plt.show()


