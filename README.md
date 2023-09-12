# Analog-Design-of-Dynamic-Comparator
This project is about building a Clocked Comparator to be used in a 4-bit Flash ADC &amp; minimize the ADC Figure of Merit given by FoM = Power / (fs*2ENOB).

### 1) PreAmp Stage:
![Preamp](https://user-images.githubusercontent.com/27668656/61270953-025b2880-a758-11e9-81d2-4219565702db.png)<br/>
- The focus in the preamp design was to be fast, more than to have a very high gain, since the regenerative latch provides the huge gain.<br/>
- The ideal current source & Mcx are used to provide the biasing for Mc (current mirror) so the overdrive voltage of Mc won’t take much of the headroom, while providing good gain & speed.<br/>

### 2) Regenerative Latch Stage:
![latch](https://user-images.githubusercontent.com/27668656/61271066-6da4fa80-a758-11e9-9729-42b8279ea556.png)<br/>
- Cc1 & Cc2 are coupling capacitors that can be used for offset cancellation & blocks the DC level from the Preamp stage.<br/>
- The transmission gates cause the inputs & outputs of the back-to-back inverters to reset to VDD/2 during the latch-reset phase. This speeds up the regeneration during the latch-regenerating phase.<br/>

### 3) RS Latch Stage:
![rslatch](https://user-images.githubusercontent.com/27668656/61271258-f328aa80-a758-11e9-98cf-6db5de6dfc62.png)<br/>
- The RS latch stage is for the comparator to maintain the sampled & regenerated value when the latch output is reset.<br/>
- The input-inverters of the RS latch block are sized to move the inverters’ switching threshold point such that an input of 0.9V (during latch-reset phase) is considered high, thus causing the output-inverters to maintain the received information.<br/>


## Clocked Comparator
![DynamicComparator](https://user-images.githubusercontent.com/27668656/61270452-93c99b00-a756-11e9-9196-5da9eb5d4369.png)

Ideally, How the switches & the coupling capacitors work:<br/> <pre/>
During clk = 1:	<pre/>   𝑉_𝐶𝑎𝑝 = 𝑉_𝐶𝑀  − 𝑉_𝐼𝑁  <br/>   𝑉_𝑔 = 𝑉_𝐶𝑀 </pre> 
During clk = 0:	<pre/>  𝑉_𝑔  =  𝑉_𝐶𝑎𝑝 + 𝑉_𝑅𝑒𝑓 = 𝑽_𝑪𝑴 − (𝑽_𝑰𝑵  − 𝑽_𝑹𝒆𝒇) <br/> 
𝑉_𝑔n  = 𝑽_𝑪𝑴 − (𝑽_𝑰𝑵n  − 𝑽_𝑹𝒆𝒇n) <br/> 
𝑉_𝑔p  = 𝑽_𝑪𝑴 − (𝑽_𝑰𝑵p  − 𝑽_𝑹𝒆𝒇p) <br/>
𝑉in(to_Preamp)  =  𝑉_𝑔p - 𝑉_𝑔n  =  − (𝑽_𝑰𝑵p  − 𝑽_𝑹𝒆𝒇p) + (𝑽_𝑰𝑵n  − 𝑽_𝑹𝒆𝒇n) = 2 * (𝑽_𝑰𝑵n  − 𝑽_𝑹𝒆𝒇n) <br/>
</pre> <br/> </pre>
*****************
## **_Overdrive test_**:
### Testbench:
![testbench](https://user-images.githubusercontent.com/27668656/61345219-190d8800-a809-11e9-875e-82018d5c8e6c.png)<br/>
In this test, We want to find the smallest difference between Vin_p & Vin_n that the Comparator can detect (give the right output value), & this tells us the resolution of this comparator at this frequency.<br/>
![testbench](https://user-images.githubusercontent.com/27668656/61346229-be762b00-a80c-11e9-839a-d46364ac2afa.png)

*****************
## **_4-bit Differential Flash ADC_**:
![flash ADC](https://user-images.githubusercontent.com/27668656/61346320-190f8700-a80d-11e9-8da7-23e72b3fd2d1.png)

## Whole System Testbench:
![wholesystem](https://user-images.githubusercontent.com/27668656/61346632-6fc99080-a80e-11e9-9e35-75b61bcdee1e.png)

![wholesystem](https://user-images.githubusercontent.com/27668656/61346665-91c31300-a80e-11e9-85c4-183adbb95ab2.png)

*****************
### References:
-> My project on google drive:<br/>
https://drive.google.com/drive/folders/1W9ip4MpMZNf3IQsoFQkhgg6QaUya4Yp4 <br/>
-> EE288 Lecture Notes:<br/>
https://drive.google.com/drive/folders/12Qqfw_TX1i7dvVVYXksaSdHV4gth1OD5 <br/><br/>
-> Check our paper:<br/>
M. Aldacher, M. Nasrollahpour, S. Hamedi-Hagh, **__“A low-power, high-resolution, 1 GHz differential comparator with low-offset and low-kickback”__**, 24th IEEE International Conference on Electronics, Circuits and Systems (ICECS), Year: 2017, Pages: 310 – 313. <br/><br/>

-> Video: "How Clocked Comparators work?"<br/>
https://www.youtube.com/watch?v=u1_9_BL5NjI
