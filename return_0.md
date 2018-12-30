# “华为杯”极客出发XMan冬令营资格赛wp

## by return 0;

### mobile

#### 签到题

![](https://i.imgur.com/QtoiJMJ.png)
在这里看到字符串"=kFBUShIf5IBT9GHfCEy"
![](https://i.imgur.com/hi4FTv9.png)
然后在这里发现是base64编码，不过base64密码表的字母顺序进行了调整  
于是写了一个exp.c来变成正常的base64编码，再进行base64解码得到flag:e4sY_bAs3_XmAN，然后加上xman{}就是最后的结果xman{e4sY_bAs3_XmAN}了  

```c
#include<stdio.h>
#include<string.h>
int main()
{
	char a[]="=kFBUShIf5IBT9GHfCEy";
	int i,j;
	char base64[]="ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/";
	char base[]={'v', 'w', 'x', 'r', 's', 't', 'u', 'o', 'p', 'q', '3', '4', '5', '6', '7', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'y', 'z', '0', '1', '2', 'P', 'Q', 'R', 'S', 'T', 'K', 'L', 'M', 'N', 'O', 'Z', 'a', 'b', 'c', 'd', 'U', 'V', 'W', 'X', 'Y', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', '8', '9', '+', '/'};
	for(i=0;i<=strlen(a);i++)
		for(j=0;j<64;j++)
			if(a[i]==base[j])
			{
				a[i]=base64[j];
				break;
			}
	for(i=0;i<strlen(a);i++)
		printf("%c",a[strlen(a)-i-1]);
	return 0;
}
```

#### EASY-APK1

![](https://i.imgur.com/NswACYp.png)
先根据内容求出praseLong的数值  

praseLong=0x3070336E  
praseLong2=0x59307552  
praseLong3=0x786D346E  
然后根据加密算法两位一截根据ascii码得到前三段flag:0p3n_Y0uR_xm4n_  
```c
#include<stdio.h>
#include<stdlib.h>

FILE *fp;

int main()
{
	int a[12]={0x30,0x70,0x33,0x6e,0x59,0x30,0x75,0x52,0x78,0x6d,0x34,0x6e};
	int i;
	for(i=0;i<12;i++)
	{
		printf("%c",a[i]);
		if(i%4==3)printf("_");
	}
	return 0;
}
```  
然后再将那段md5码进行解码得到最后一段flag:t0Ur  
![](https://i.imgur.com/rXc1fpy.png)

再将flag连起来并加上头xman{}得到xman{0p3n_Y0uR_xm4n_t0Ur}