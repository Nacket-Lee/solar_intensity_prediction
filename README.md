# solar_intensity_prediction
This repository is used to predict the intensity of the solar irradiation
```
step 5 targetdata nocloud
步骤5 无云日数据写入

clear;
number=xlsread('number.xlsx'); 
number = number';
one_index=find(number==1);
xlswrite('one_index.xlsx',one_index);
sun=xlsread('train.xlsx');
strength=sun(:,1);
height=sun(:,2);
sunny=reshape(strength,[24,1461]);
high=reshape(height,[24,1461]);
targetsunny=sunny(:,one_index(:));
targethigh=high(:,one_index(:));
xlswrite('targetsunny.xlsx',targetsunny);
xlswrite('targethigh.xlsx',targethigh);
%无显云影响的天数的日照强度和太阳高度角（3min）
```
