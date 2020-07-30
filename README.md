# solar_intensity_prediction
This repository is used to predict the intensity of the solar irradiation
```
%x是当地的地理纬度
%y是当日的太阳赤纬
%t是当日的太阳时角
x=26.1.*pi./180;

n=1:366;

b=2.*pi.*(n-1)./366;
y=0.006918-0.399912.*cos(b)+0.070257.*sin(b)-0.006758.*cos(2.*b)+0.000907.*sin(2.*b)-0.002697.*cos(3.*b)+0.00148.*sin(3.*b);

T=0:pi/12:(23./12)*pi;
t=T';

h=sin(x).*sin(y)+(cos(x).*cos(y)).*cos(t);
H=asin(h).*180./pi;
d=(H(:));
```
