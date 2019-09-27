import random 

import numpy as np

import matplotlib.pyplot as plt

 

#+추가한 부분
def inputa(a,b,c,string): 
    #인풋 받는 함수
    a, b, c = map(float, input(string +'번째 일차부등식의 x의 계수, y의 계수, 상수항을 입력해주세요! (우변은 0으로, 부등호는 좌변이 더 큰 상태를 맞춰주세요!) : ').split())
    
inputa(a_1,b_1,c_1,'첫'); inputa(a_2,b_2,c_2,'두'); inputa(a_3,b_3,c_3,'첫'); temp = True

while temp: #평행하지 않은 함수 거르기
    if a_1 == a_2 and b_1 == b_2:
        print('1번 2번 함수를 다시 입력해주시기 바랍니다')
        inputa(a_1,b_1,c_1,'첫'); inputa(a_2,b_2,c_2,'두');
    if a_2 == a_3 and b_2 == b_3:
        print('2번 3번 함수를 다시 입력해주시기 바랍니다')
        inputa(a_2,b_2,c_2,'두'); inputa(a_3,b_3,c_3,'셋');
    if a_1 == a_3 and b_1 == b_3:
        print('1번 3번 함수를 다시 입력해주시기 바랍니다')
        inputa(a_1,b_1,c_1,'첫'); inputa(a_3,b_3,c_3,'셋');
    else:
        temp = False


#일차연립방정식의 해 구하기

x_1 = (b_1*c_2 - b_2*c_1)/(b_2*a_1 - a_2*b_1)

y_1 = (c_2*a_1 - c_1*a_2)/(a_2*b_1 - a_1*b_2)

 

#1,3번 방정식의 해

x_2 =(b_1*c_3 - b_3*c_1)/(b_3*a_1 - a_3*b_1)

y_2 =(c_3*a_1 - c_1*a_3)/(a_3*b_1 - a_1*b_3)

 

#2,3번 방정식의 해

x_3=(b_3*c_2 - b_2*c_3)/(b_2*a_3 - a_2*b_3)

y_3=(c_2*a_3 - c_3*a_2)/(a_2*b_3 - a_3*b_2)

 

 
print(x_1,y_1, x_2, y_2, x_3, y_3)
#랜덤하게 뿌린 점을 담을 리스트와 그 중에서 영역 안에 포함된 점을 담을 리스트 설정

randompoint=[]

conditionpoint=[]

 

#세 방정식으로 만들어진 도형(삼각형)을 포함하는 최소의 직사각형 안에 랜덤하게 점을 뿌리기

a=max(x_1,x_2,x_3)

b=min(x_1,x_2,x_3)

c=max(y_1,y_2,y_3)

d=min(y_1,y_2,y_3)

 

for i in range(100000):

    randompoint += [[0.01*random.randint(100*int(b),100*(int(a)+1)), 0.01*random.randint(100*int(d),100*(int(c)+1))]]

 

# 이 중 조건을 만족하는 점들을 다른 리스트에 담기

for i in range(len(randompoint)):

    if a_1*randompoint[i][0]+b_1*randompoint[i][1]+c_1>0 and a_2*randompoint[i][0]+b_2*randompoint[i][1]+c_2>0 and a_3*randompoint[i][0]+b_3*randompoint[i][1]+c_3>0:

        conditionpoint.append(randompoint[i])

 

#그래프 그리기

list_x=[]

list_y=[]

 

for i in range(len(conditionpoint)):

    list_x = list_x + [conditionpoint[i][0]]

    list_y = list_y + [conditionpoint[i][1]]

    
 

plt.scatter(list_x ,list_y)

plt.show()