# 方法一
``` javascript

timea='2019-06-12 16:13:97'
sql = '''
SELECT
b.patient_id,
  b.patient_name,
  b.GENDER,
  b.age,
b.DEPARTMENT,
b.PATIENT_TYPE,
b.ORDER_DATE,
b.SOURCE_DOCTOR as '送检医生',
b.TEST_DOCTOR as '检验医生',
  a.CURRENT_RESULT,
  a.report_limit,
  c.ITEM_NAME,
  a.ITEM_CODE,
  a.SAMPLE_DATE,
  a.INSTRUMENT,
  a.SAMPLE_NO,
  b.barcode,
  b.SAMPLE_TYPE,
c.unit,
c.REPORT_LIMIT
FROM
  [dbo].[TB_CURRENT_ITEM_RESULT] a
LEFT JOIN TB_CURRENT_SAMPLE_INFO b ON a.SAMPLE_DATE = b.SAMPLE_DATE
AND a.SAMPLE_NO = b.SAMPLE_NO
AND a.INSTRUMENT = b.INSTRUMENT
LEFT JOIN TB_ITEM_PROPERTY c ON c.ITEM_CODE = a.ITEM_CODE
AND REPLACE(a.INSTRUMENT, '@#@', '') = c.INSTRUMENT
WHERE
  b.ORDER_DATE >= %s
AND LEFT (a.INSTRUMENT, 3) <> '@#@'
AND a.INSTRUMENT = '7060'
AND b.PATIENT_TYPE != '门诊'--包括体检与住院
'''
print(sql % (timea))
```

# 方法2
``` javascript   <!-- javascript改成python没颜色 -->
b.ORDER_DATE >= %(bb)s
print(sql % dict(bb=变量))
```
2019-12-22 18:03:24
--------------------------------------------------

# mysql查询日期转换用DATE_FORMAT函数
select * FROM tjzyinfo where  DATE_FORMAT(print_date,'%Y-%m-%d')='2019-12-30'
2019-12-30 18:47:10
--------------------------------------------------