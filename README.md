clc;

clear all;

%given specifications

Ap=1.25;As=15;

fpb=200; fsb=300; fs = 2000;

%to find Order(N) and cutoff frequency (fc)

fpbn = fpb /(fs/2); fsbn = fsb /(fs/2);

[N,fc]=buttord(fpbn,fsbn,Ap,As); 

disp('order of the filter is ='); 

disp(N);

disp('cutoff frequency is = '); 

disp(fc*fs/2);

%to compute frequency response of an IIR digital filter

[b,a]=butter(N,fc);

[H,f] = freqz(b,a,256,fs); 

subplot(3,1,1);

plot(f,abs(H));

title('frequency response of Low Pass Filter'); 

xlabel('------->frequency in Hz');

ylabel('------->Magnitude');

%filtering operation on input singal having frequency 10Hz,100Hz,500Hz

n = 0:1/fs:0.1; 

s1=5*sin(2*pi*10*n); 

s2=5*sin(2*pi*100*n); 

s3=5*sin(2*pi*500*n);

x = [s1 s2 s3]; 

subplot(3,1,2); 

plot(x);

title('input signal'); 

xlabel('----------> n');

ylabel('---------->amplitude');

y = filter(b,a,x);

subplot(3,1,3); plot(y);

title('filterd output signal'); 

xlabel('----------> n');

ylabel('---------->amplitude')
