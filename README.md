# solar_intensity_prediction
This repository is used to predict the intensity of the solar irradiation
```
step 4 find nocloud day
步骤4 找出无云遮挡的某一天

clear;
sun= xlsread('train.xlsx');
strength=sun(:,1);
sunny=reshape(strength,[24,1461]);
for i=1:1461
    value=sunny(:,i);
    for n=1:23
        if value(n+1)-value(n)>0
            calculation(n)=1;
        else calculation(n)=0;
        end
    end
    cal(:,i)=calculation';
     xlswrite('calculation.xlsx',cal);
end

num=0;   %此为连续的1的段数
numjudge=0;
for n=1:1461
    a=cal(:,n);
    for i=1:length(a)
    if a(i)==1
        numjudge=numjudge+1;
    elseif numjudge>=1
        num=num+1;
        numjudge=0;
    else
        numjudge=0;
    end
    end  
    number(n)=num;
     xlswrite('number.xlsx',number);
    num=0;
end
    
sunrise=xlsread('number.xlsx');
sunrise=sunrise';
one_index=find(sunrise==1);
%找出数据当中无显云影响的具体天数及具体天
```
