#Smali �����﷨
```smali
.field private isFlag:z�����������

.method��������

.parameter������������

.prologue����������ʼ

.line 12�����˷���λ�ڵ�12��

invoke-super�������ø�����

const/high16  v0, 0x7fo3������0x7fo3��ֵ��v0

invoke-direct�������ú���

return-void������������void

.end method������������

new-instance��������ʵ��

iput-object��������ֵ

iget-object�������ö���

invoke-static�������þ�̬����
```
������ת��֧��

* "if-eq vA, vB, :cond_**"   ���vA����vB����ת��:cond_**
* "if-ne vA, vB, :cond_**"   ���vA������vB����ת��:cond_**
* "if-lt vA, vB, :cond_**"    ���vAС��vB����ת��:cond_**
* "if-ge vA, vB, :cond_**"   ���vA���ڵ���vB����ת��:cond_**
* "if-gt vA, vB, :cond_**"   ���vA����vB����ת��:cond_**
* "if-le vA, vB, :cond_**"    ���vAС�ڵ���vB����ת��:cond_**
* "if-eqz vA, :cond_**"   ���vA����0����ת��:cond_**
* "if-nez vA, :cond_**"   ���vA������0����ת��:cond_**
* "if-ltz vA, :cond_**"    ���vAС��0����ת��:cond_**
* "if-gez vA, :cond_**"   ���vA���ڵ���0����ת��:cond_**
* "if-gtz vA, :cond_**"   ���vA����0����ת��:cond_**
* "if-lez vA, :cond_**"    ���vAС�ڵ���0����ת��:cond_**

if������java���룺
```java
private boolean ifSense(){
        boolean tempFlag = ((3-2)==1)? true : false;
        if (tempFlag) {
            return true;
        }else{
            return false;
        }
    }
```
```smali
.method private ifSense()Z
    .locals 2

    .prologue
    .line 22
    const/4 v0, 0x1     // v0��ֵΪ1

    .line 24
    .local v0, tempFlag:Z
    if-eqz v0, :cond_0            // �ж�v0�Ƿ����0, ����������������, ��������ִ��cond_0��֧

    .line 25
    const/4 v1, 0x1            // ����������֧

    .line 27
    :goto_0
    return v1

    :cond_0
    const/4 v1, 0x0            // cond_0��֧

    goto :goto_0
.end method
```
###�����������������if��֧����������ߣ�����return ; �������������������ߵ� :cond_0��֧ , ����ִ�� goto :goto_0�߻� :goto_0����


for����java���룺
```java
private void forSense(){
    listStr = new ArrayList<String>(COUNT);
    for (int i = 0; i < COUNT; i++) {
        listStr.add("�����ֵ����ϳ���");
    }
}
```
```smali
.line 40
    const/4 v0, 0x0

    .local v0, i:I
    :goto_0
    if-lt v0, v3, :cond_0            //  if-lt�ж���ֵv0С��v3 ,    �粻����������, ����ִ�з�֧ :cond_0

    .line 43
    return-void

    .line 41
    :cond_0                // ��ǩ
    iget-object v1, p0, Lcom/example/smalidemo/MainActivity;->listStr:Ljava/util/List;                // ���ö���

    const-string v2, "\u73b0\u5728\u8f6e\u5230\u6211\u4e0a\u573a\u4e50"

    invoke-interface {v1, v2}, Ljava/util/List;->add(Ljava/lang/Object;)Z        // List�ǽӿ�, ����ִ�нӿڷ���add

    .line 40
    add-int/lit8 v0, v0, 0x1��������// ���ڶ���v0�Ĵ����е�ֵ������0x1��ֵ�����һ���Ĵ�����, ʵ��������

    goto :goto_0                // ��ȥ:goto_0��ǩ
```
###�����������趨һ����ǩgoto_0, �ж�v0С��v3, ����ִ�з�֧:cond_0 ,Ȼ�����ܻ�:goto_0�������ж�

�ο��ԣ�http://www.cnblogs.com/lee0oo0/p/3728271.html