# д����ʷK�ߵ�csv�ļ�

## 1.����ģ��

�����������Ҫ��ģ��

```python
from PT_QuantBaseApi import PT_QuantBaseApi_Python35,GetDataCallBack,TradeDataCallBack
import csv
import time
```

## 2.��������ص���

����ص��࣬�̳и���Ļص����������ڽ��ն�Ӧ�����Ļص���Ϣ������������ʷK����Ϣ�����K����Ϣ�ص���

```python
class MDCallBack(GetDataCallBack):
	def __init__(self):
		super(MDCallBack, self).__init__()
         #����K��csv�ļ�
		self.KLinefile = open('KLine.csv', 'w+',newline='')
		self.klinewriter=csv.writer(self.KLinefile)
		self.klinewriter.writerow(['��������','��������','֤ȯ����', '���ں�ʱ��', '���̼�', '��߼�', '��ͼ�', '������', '�������̼�', '��ͣ��', '��ͣ��', '�ɽ�����','�ɽ��ܶ�'])
	
    #���ػص�
	def OnRecvCodes(self, codes, optionCodes):#�û���¼�ص���������ȡ
		print('Enter MDCallBack OnRecvCodes')
		pass
    
    def OnRecvKLine(self, kLine):#K�߻ص�
		print('Enter MDCallBack OnRecvKLine')
		writedata = [kLine['szType'], kLine['szCycType'], kLine['szWindCode'], kLine['szDatetime'],kLine['nOpen'], kLine['nHigh'], kLine['nLow'], kLine['nClose'], kLine['nPreClose'], kLine['nHighLimit'],kLine['nLowLimit'], kLine['nVolume'], kLine['nTurover']]
		self.klinewriter.writerow(writedata)
		pass
    
    def OnRecvOver(self):
		print('Enter MDCallBack OnRecvOver')
		self.KLinefile.close()
		pass
```

## 3.�������Ӷ���ʵ��

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

ͨ������3�����Ӷ���ʵ�������õ�¼�������û���¼�������У���û����Լ��û�����ĺϷ��ԡ���¼�ɹ����û�����Լ���������������API�������û���¼��API�ڲ������û���¼�ص�������2���û���¼�ص���������Ի�ȡ�������

```python
retLog = ()
retLog = m.Login("BXF", "BXF")#��һ������Ϊ�û������ڶ�������Ϊ����
print("Market Login=", retLog)#��ӡ��¼������
```

## 5.����ĳ��ֻ��ƱK������

��ϵͳ����������ʷK���������ϵͳ����󴥷�K�����ݻص�����������2��K�����ݻص�����������յ���Ӧ�Ļص���Ϣ��

```python
subCodes = ["600000.SH", "000001.SZ"]
m.ReqHistoryKline("day", "2016-04-03 00:00:00", "2016-05-03 00:00:00", subCodes, False)
```

