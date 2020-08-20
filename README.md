# solar_intensity_prediction
This repository is used to predict the intensity of the solar irradiation
```
step 2 data clearness
步骤二 数据清洗

clear;
[numsun,txtsun,rawsun] = xlsread('train（南非约翰内斯堡日照强度数据） - 副本.xlsx');
sun=numsun;
sun(:,1)=[];
n=0:1460;
sunny=cell2mat(arrayfun(@(n) sun((8+24*n):(18+24*n),1),0:1460,'un',0))';
%将35064*2的矩阵sun依照有日照强度的时间节点进行数据提取，变成1461*11的矩阵sunny
suu=sunny';
%转置变成11*1461的矩阵suu，其中11是每天当中8时至18时的日照强度，1461为
%2009.1.1的0点至2013.1.1的0点共计1461天的时间
su=(suu(:));
zero_index=find((su)==0) ;
reg = mod(zero_index,11); 
%排除数据中突然出现的零点

i=find(isnan(sun));
training=sun;
training(:,2)=[];
input=training(9247:9260,1);
T=6:19;
t=T';
[p,S]=polyfit(t,input,9);
y1=polyval(p,t);
plot(t,input,'k.',t,y1,'g');
legend('训练样本','拟合曲线'),grid;
% xlabel(sprintf('多项式:y=%.2fx^2+%.2fx+%.2f',p(1),p(2),p(3)));
% pretty(poly2sym(p))
 xlabel(sprintf('多项式:%s',poly2str(p,'x')));
title('最小二乘法的多项式拟合'); 
sun(9271:9284,1)=y1;
sun(9295:9308,1)=y1;
sun(9319:9332,1)=y1;
j=find(isnan(sun(1:9336,1)));
sun(j,1)=0; 
sun(9337:9348,1)=sun(9265:9276,1);
%用拟合补足数据中出现大量空值的地方

b=sun(31406:31431,1);  
times=1:length(b);
mask=~isnan(b); 
c=b;  
c(~mask)=interp1(times(mask),b(mask),times(~mask));
sun(31406:31431,1)=c;
%用差值补足数据中出行少数空值的地方
 
sun(:,1)=round(sun(:,1));
%经过数据清洗之后的数据

xlswrite('train.xlsx',sun);
```
