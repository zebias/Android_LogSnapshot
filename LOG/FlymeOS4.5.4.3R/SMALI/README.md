#Smali 基本语法
```smali
.field private isFlag:z　　定义变量

.method　　方法

.parameter　　方法参数

.prologue　　方法开始

.line 12　　此方法位于第12行

invoke-super　　调用父函数

const/high16  v0, 0x7fo3　　把0x7fo3赋值给v0

invoke-direct　　调用函数

return-void　　函数返回void

.end method　　函数结束

new-instance　　创建实例

iput-object　　对象赋值

iget-object　　调用对象

invoke-static　　调用静态函数
```
条件跳转分支：

* "if-eq vA, vB, :cond_**"   如果vA等于vB则跳转到:cond_**
* "if-ne vA, vB, :cond_**"   如果vA不等于vB则跳转到:cond_**
* "if-lt vA, vB, :cond_**"    如果vA小于vB则跳转到:cond_**
* "if-ge vA, vB, :cond_**"   如果vA大于等于vB则跳转到:cond_**
* "if-gt vA, vB, :cond_**"   如果vA大于vB则跳转到:cond_**
* "if-le vA, vB, :cond_**"    如果vA小于等于vB则跳转到:cond_**
* "if-eqz vA, :cond_**"   如果vA等于0则跳转到:cond_**
* "if-nez vA, :cond_**"   如果vA不等于0则跳转到:cond_**
* "if-ltz vA, :cond_**"    如果vA小于0则跳转到:cond_**
* "if-gez vA, :cond_**"   如果vA大于等于0则跳转到:cond_**
* "if-gtz vA, :cond_**"   如果vA大于0则跳转到:cond_**
* "if-lez vA, :cond_**"    如果vA小于等于0则跳转到:cond_**

if函数的java代码：
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
    const/4 v0, 0x1     // v0赋值为1

    .line 24
    .local v0, tempFlag:Z
    if-eqz v0, :cond_0            // 判断v0是否等于0, 不符合条件向下走, 符合条件执行cond_0分支

    .line 25
    const/4 v1, 0x1            // 符合条件分支

    .line 27
    :goto_0
    return v1

    :cond_0
    const/4 v1, 0x0            // cond_0分支

    goto :goto_0
.end method
```
###文字描述：如果符合if分支则程序往下走，最终return ; 而如果条件不符合则会走到 :cond_0分支 , 最终执行 goto :goto_0走回 :goto_0返回


for函数java代码：
```java
private void forSense(){
    listStr = new ArrayList<String>(COUNT);
    for (int i = 0; i < COUNT; i++) {
        listStr.add("现在轮到我上场乐");
    }
}
```
```smali
.line 40
    const/4 v0, 0x0

    .local v0, i:I
    :goto_0
    if-lt v0, v3, :cond_0            //  if-lt判断数值v0小于v3 ,    如不符合往下走, 符合执行分支 :cond_0

    .line 43
    return-void

    .line 41
    :cond_0                // 标签
    iget-object v1, p0, Lcom/example/smalidemo/MainActivity;->listStr:Ljava/util/List;                // 引用对象

    const-string v2, "\u73b0\u5728\u8f6e\u5230\u6211\u4e0a\u573a\u4e50"

    invoke-interface {v1, v2}, Ljava/util/List;->add(Ljava/lang/Object;)Z        // List是接口, 所以执行接口方法add

    .line 40
    add-int/lit8 v0, v0, 0x1　　　　// 将第二个v0寄存器中的值，加上0x1的值放入第一个寄存器中, 实现自增长

    goto :goto_0                // 回去:goto_0标签
```
###文字描述：设定一个标签goto_0, 判断v0小于v3, 符合执行分支:cond_0 ,然后又跑回:goto_0做继续判断

参考自：http://www.cnblogs.com/lee0oo0/p/3728271.html