## 1. �ַ���

>  ��ȡ�ַ����ĳ���
>
> ```shell
> name="abcd"
> echo ${#name} #��� 4
> ```
>
> ��ȡ���ַ���
>
> ```shell
> str="runoob is a great site"
> echo ${str:1:4} # ��� unoo
> ```

## 2. ���� ( )

���ű�ʾ���飬����Ԫ���� ���ո� ���ŷֿ�

```shell
# ��������
array_name=(value0 value1 value2 value3)
# ��ȡ����: ${������[�±�]}
echo ${array_name[n]}
# ��ȡ�����е�����Ԫ��: @����
echo ${array_name[@]}
# ��ȡ����ĳ���
echo ${#array_name[@]}
```

## 3. ������ / ˫����

### 1.1.1. �����Ƿ��ʧЧ

����������κ��ַ�����`ԭ�����`���������ַ����е�`��������Ч��`

```shell
name="Tom"
echo "${name}"  # ˫����, ��� Tom, ������Ч
echo '${name}'  # ������, ��� ${name}, ����ʧЧ
```

### 1.1.2. �ܷ�ת�� ?

```shell
echo "aa\'aa"   # aa\'aa  ������', ���ܱ�ת�� \'
echo "aa\"aa"   # aa"aa   ˫����", ���Ա�ת�� \"
```

### 1.1.3. ��������ƴ���ַ���

```shell
name="Tom"
# ʹ��˫����ƴ��
new_name_1=" hello, "${name}" "
echo ${new_name_1}  # ��� hello, Tom
# ʹ�õ�����ƴ��
new_name_2=' hello, '${name}' '
echo ${new_name_2}  # ��� hello, Tom
```

---



## 4. ���̿���

if����

```shell
if condition1
then
    command1
elif condition2 
then 
    command2
else
    commandN
fi
```

forѭ��

```shell
for var in ${var_list}
do
    echo ${var}   
done
```

whileѭ��

```shell
i=10
while [ $i -gt 0 ];do
	echo ${i}
	i=`expr ${i} - 1`  # i=$[${i}-1]
done
```

case��ѡ��

```shell
read aNum
case $aNum in
    1)  echo '��ѡ���� 1'
    ;;
    2)  echo '��ѡ���� 2'
    *)  echo '��û������ 1 �� 2 ֮�������'
    ;;
esac
```

## 5. ����

```shell
# ���庯��
function run()
{
	local var1=$1
	local var2=$2
	return 0  # 0 ��ʾ�ɹ�, 1 ��ʾʧ��
}

# ʹ�ú���
run "param1" "param2" 
res=$?   # ��ȡ��һ�������ִ�н��
if [ $res -ne 0 ]; then
	log_error "error: func run, res: ${res}"
fi
```

