# solar_intensity_prediction
This repository is used to predict the intensity of the solar irradiation
'''
clear;
sun= xlsread('train(经过数据清洗之后的训练集).xlsx');
strength=sun(:,1);
height=sun(:,2);
strength(end,:)=[];
height(end,:)=[];
sunny=reshape(strength,[24,1461]);
high=reshape(height,[24,1461]);
targetsunny=sunny;
targethigh=high;

x1 =5:20;
i=1:1461;
v1 = targetsunny(6:21,i);
xq1 = 5:1/6:20;
vq1 = interp1(x1,v1,xq1);
subplot(121), plot(x1,v1,'o',xq1,vq1,':.');
xlim([5 20]);
title('(Default) Linear Interpolation');

x2=5:20;
i=1:1461;
v2 = targethigh(6:21,i);
xq2 = 5:1/6:20;
vq2 = interp1(x2,v2,xq2);
 subplot(122),plot(x2,v2,'o',xq2,vq2,':.');
xlim([5 20]);
title('Spline Interpolation'); 

targetsunny_10min=vq1;
targethigh_10min=vq2;
%xlswrite('targetsunny_10min.xlsx',targetsunny_10min);
%xlswrite('targethigh_10min.xlsx',targethigh_10min);

%利用线性插值和光滑插值充实日照强度和太阳高度角的数据量，并作图比较
'''
