# ��ȡ��ϸ��K��_������csv�ļ�(Python 3.5)

## 1.����ģ��

�����������Ҫ��ģ��

```python
from PT_QuantBaseApi import PT_QuantBaseApi_Python35,GetDataCallBack,TradeDataCallBack
import csv
```

## 2.��������ص���

����ص��࣬�̳и���Ļص����������ڽ��ն�Ӧ�����Ļص���Ϣ��

```python

class MDCallBack(GetDataCallBack):
	def __init__(self):
		super(MDCallBack, self).__init__()
	#���ػص�
	def OnRecvCodes(self, codes, optionCodes):#�û���¼�ص���������ȡ
		print('Enter MDCallBack OnRecvCodes')
		pass
```

## 3.�����������Ӷ���ʵ��

�ɲ���2�д�������ص��࣬�������Ӷ���ʵ����ͨ�����Ӷ���ʵ������API������

```python
PT_QuantBaseApi_Python35.enableLog()#������־
tspi = TradeDataCallBack()#�����������ݻص�����ʵ��
t = PT_QuantBaseApi_Python35.TradeDataApi(tspi, True)#�����������Ӷ���,��һ������Ϊ�������ݻص�����ʵ�����ڶ�������Ϊ�Ƿ񴴽�ģ���Ͻ������Ӷ���
#��Ҫ���������Ӷ�����Ϊ�����������Ӷ���ʵ���Ĳ�������ڶ�����������ΪTrue
mspi = MDCallBack()#�����������ݻص�����ʵ��
m = PT_QuantBaseApi_Python35.GetDataApi(mspi, t)#�����������Ӷ���ʵ������һ������Ϊ�������ݻص�����ʵ�����ڶ�������Ϊ�������Ӷ������Ϊ�ա�
#���ڶ�������Ϊ�������Ӷ���������ģ���Ͻ���
```

## 4.�û���¼

ͨ������2�����Ӷ���ʵ�������õ�¼�������û���¼�������У���û����Լ��û�����ĺϷ��ԡ���¼�ɹ����û�����Լ���������������API��������¼�ɹ����û�����Լ���������������API�������û���¼��API�ڲ������û���¼�ص�������2���û���¼�ص���������Ի�ȡ�������

```python
retLog = ()
retLog = m.Login("BXF", "BXF")#��һ������Ϊ�û������ڶ�������Ϊ����
print("Market Login=", retLog)#��ӡ��¼������
```

## 5.��ȡ��ϸ��K��

��ȡĳ��ʱ����ϸ��K�ߣ�д��csv�ļ���

```python
#����csv�ļ�
Detailfile = open('DetailKLine.csv', 'w+',newline='')
detailewriter=csv.writer(Detailfile)
#д����ͷ
detailewriter.writerow(['֤ȯ����','������', '֤ȯ������', '��Ȩǰ���̼�' ,'ʵ��������', '����', '��߼�', '��ͼ�', '������', '�ɽ���', '�ɽ����', '�ɽ�����', '�ջ�����','�ۼ�ǰ��Ȩ����','��ͨ��ֵ', '����ֵ', '�ǵ���', '�Ƿ���'])
listKline=[]#����list���ͱ���
#���û�ȡ��ϸ��K�ߺ���
listKline=m.GetDayKline("300012", "2017-02-21 09:30:00", "2017-04-06 15:00:00")
#ѭ�������д��ָ����Χ����ϸ��K������
for i in list(range(len(listKline))):
	writedata=[listKline[i]["szWindCode"],listKline[i ]["szTradeDate"],listKline[i ]["szCodeCNName"],listKline[i]["nPreClose"],listKline[i ]["nActPreClose"],listKline[i ]["nOpen"],listKline[i]["nHigh"],listKline[i]["nLow"],listKline [i]["nClose"],listKline[i]["nVolume"],listKline[i ]["nTurover"],listKline[i][ "nDealAmount"],listKline[i]["nTurnoverRate"],listKline[i][ "nAccumRestorationFactor"],listKline[i]["nNegMarketValue"],listKline[i][ "nMarketValue"],listKline[ i]["nChgPct"],listKline[i]["bIsOpen"]]
	print(writedata)#��ӡ
	detailewriter.writerow(writedata)#д���ļ�
Detailfile.close()#�ر��ļ�
```


