### 每隔四位插入空格
```javascirpt
str.replace(/\s/g, '').replace(/[^\d]/g, '').replace(/(\d{4})(?=\d)/g, '$1 ');
```
### 银行卡号前部分用 * 代替，仅显示后四位
```javascript
str.replace(/\s/g, '').replace(/(\d{4})\d+(\d{4})$/, "**** **** **** $2");
```
### 去除字符串所有的空格
```javascript
str.replace(/\s|\xA0/g, "");
```