# Apex简介

Apex 是一种强类型、面向对象的编程语言，允许开发人员在 Salesforce 平台上执行流程和事务控制语句（allows developers to execute flow and transaction control statements on the Salesforce platform.）。

## 创建一个类

1. 打开org，Click the **setup gear** ![Gear icon to access Setup in Lightning Experience.](https://res.cloudinary.com/hy4kyit2a/f_auto,fl_lossy,q_70/learn/projects/quickstart-apex/quickstart-apex-1/images/8edeaa88035e90a5b5390fea7536fe3d_image-1.png) and select **Developer Console**.
2. 从新打开的页面左上角点击File，select **New | Apex Class**.
3. For the class name, enter `OlderAccountsUtility` and then click **OK**.

这样就创建了一个名为`OlderAccountsUtility`的Apex类。

```apex
public class OlderAccountsUtility {
	
}
```

## 创建一个方法

如同Java一样，一个类可以有多个方法，下面创建一个方法，将创建 `updateOlderAccounts` 方法，该方法获取按创建日期排序的前五条 `Account` 记录。然后更新描述字段，说明这是一个“遗产帐户（`Heritage Account`）”，即比其他帐户更早的帐户。

```apex
public class OlderAccountsUtility {
    public static void updateOlderAccounts() {
      // Get the 5 oldest accounts
      // 执行sql语句，获取最早的accounts记录
      Account[] oldAccounts = [SELECT Id, Description FROM Account ORDER BY CreatedDate ASC LIMIT 5];
      // loop through them and update the Description field
      // 遍历它们并更新Description字段
      for (Account acct : oldAccounts) {
          acct.Description = 'Heritage Account';
      }
      // save the change you made
      // 使用 Apex 数据操作语言 (DML) 更新客户记录。
      update oldAccounts;
    }
    
}
```

## 调用和测试代码

### 运行代码

要运行上列代码的`updateOlderAccounts`方法，可以In the Developer Console, select **Debug | Open Execute Anonymous Window**.然后在弹出的窗口内输入`OlderAccountsUtility.updateOlderAccounts();`，这个代码的意思是执行`OlderAccountsUtility`类的静态方法`updateOlderAccounts()`。然后在右下角点击**Execute**即可运行`OlderAccountsUtility.updateOlderAccounts();`

![](https://suyuesheng-biaozhun-blog-tupian.oss-cn-qingdao.aliyuncs.com/blogimg/20220326155747.png)

## 验证代码运行的结果

1. 打开org，点击**App Launcher** ![](https://suyuesheng-biaozhun-blog-tupian.oss-cn-qingdao.aliyuncs.com/blogimg/20220326162431.jfif) ，点击**Sales** 。
2. 点击**Accounts** 标签。
3. 点击齿轮图标 ![List Settings icon](https://res.cloudinary.com/hy4kyit2a/f_auto,fl_lossy,q_70/learn/projects/quickstart-apex/quickstart-apex-4/images/47389bdcef232e05c2fb1ccff7758953_image-4.png) ，选择**Select Fields to Display**，将**Last Modified Date**移动到Visible Fields column。
4. 按**Last Modified Date**降序排名，点击前五个中的一个，查看**Details**，将会发现Description字段为**Heritage Account**

![](https://suyuesheng-biaozhun-blog-tupian.oss-cn-qingdao.aliyuncs.com/blogimg/20220326162643.png)

# Apex 管理员基础知识

## 开始使用Apex

### Apex 代码存储在哪里？

代码存储在文件中。这些文件可以在本地（在您的 PC 或 Mac 上）、在云中（您的 Salesforce 组织），或者它们可以保存在本地并自动同步到云中。

开发者控制台（Developer Console）是开发者用来创建和编辑代码文件的工具，在trailhead的教程中使用Developer Console在 Salesforce 组织（org）中存储和执行（运行）代码。

打开Developer Console的方法是👉打开org，Click the **setup gear** ![Gear icon to access Setup in Lightning Experience.](https://res.cloudinary.com/hy4kyit2a/f_auto,fl_lossy,q_70/learn/projects/quickstart-apex/quickstart-apex-1/images/8edeaa88035e90a5b5390fea7536fe3d_image-1.png) and select **Developer Console**.

### 注释

如同java一样

```apex
/*
	多行注释
*/

// 单行注释
```

## Apex基础

### 变量

| ata Type             | Description and Example                                      |
| :------------------- | :----------------------------------------------------------- |
| `Integer`            | A positive or negative number that doesn’t have a decimal point.  `Integer num = 12;` |
| `Decimal`            | A positive or negative number that has a decimal point.  `Decimal num = 12.22222;` |
| `String`             | A series of characters surrounded by single quotes. This can include any text as short as one letter to sentences.  `String whatAmI = 'A String';` |
| `Boolean`            | Typically either true or false. In Apex, null (empty) is also a valid value. Boolean is commonly used with checkboxes.  `Boolean doSomething = False;` |
| `Id` (Salesforce ID) | Any valid 18-character Salesforce record ID.  `Id contactId = '00300000003T2PGAA0';` |

Apex 是一种强类型语言，这意味着每次您声明（创建）一个变量时，您都需要设置它的数据类型、名称以及可选的初始值。

初始化变量（为其分配初始值）时，您分配的值必须与变量的数据类型匹配。**如果您选择不在变量声明语句中赋值，则变量的值为空。**

![](https://suyuesheng-biaozhun-blog-tupian.oss-cn-qingdao.aliyuncs.com/blogimg/20220329092245.png)

![](https://suyuesheng-biaozhun-blog-tupian.oss-cn-qingdao.aliyuncs.com/blogimg/20220329092309.png)

System.debug 在调试日志中显示其括号的内容。**类似于java的打印。**

### System.debug

System.debug 在调试日志中显示其括号的内容。**类似于java的打印。**

```apex
Integer numberOfSpoons;
System.debug('The variable numberOfSpoons is: ' + numberOfSpoons);
  
numberOfSpoons = 1;
System.debug('The variable numberOfSpoons is: ' + numberOfSpoons);
```

结果：

![](https://suyuesheng-biaozhun-blog-tupian.oss-cn-qingdao.aliyuncs.com/blogimg/20220329092622.png)

### 基本语法

**排列文本和标点以创建编程语言的方式称为语法。**

1.  Apex 语句以分号`;`结尾。

2. Apex 字符串使用单引号将文字文本与周围的代码分开。

   ```apex
   String whatTimeIsIt = 'It is Tea Time!';
   Integer sugarCount = 2;
   Boolean needsSugar = false;
   ```

## 集合

集合是一种可以存储多个项的变量类型。

![](https://suyuesheng-biaozhun-blog-tupian.oss-cn-qingdao.aliyuncs.com/blogimg/20220329093539.png)



Apex 集合分为三种类型（list, set, and map）

### List

Apex 列表是一组有序的相同类型的项目。

声明类表的方式如下：

![](https://suyuesheng-biaozhun-blog-tupian.oss-cn-qingdao.aliyuncs.com/blogimg/20220329093848.png)

1. 声明一个空列表

   ```apex
   //Declare the groceries list
   List<String> groceries = new List<String>();
     
   //The output for this statement is an empty list, ().
   System.debug('Groceries Value: ' + groceries);
   ```

2. 声明一个数组(可以理解为固定长度的列表)

   ```apex
   String[] cc = new String[3];
   System.debug('数组'+cc);
   ```

   1. 从数组中取值和赋值

      ```apex
      cc[0]='swd';
      System.debug(cc[0]);
      ```

   2. 声明一个初始化的数组

      ```apex
      String[] strArr =new String[]{'张三','李四','王二麻'};
      ```

3. 初始化一个List

   1. 初始化一个空List，**并添加值**。`add`方法适用于数组

      ```apex
      List<String> groceries = new List<String>();
      groceries.add('Tea');
      ```

   2. 初始化一个不为空的List

      ```apex
      //Sets the first item in the list to 'Tea'
      List<String> groceries = new List<String>{'Tea'}; 
      ```

   3. 特定索引（位置）中插入item，适用于数组

      ```apex
      groceries.add(2, 'Milk');
      ```

      4.    从List取值

            ```apex
            System.debug(groceries[0]);
            ```

#### 提示

1. 与java不同，**apex中数组是List的一种**。
2. **apex的数组的长度是可变的，也就是说虽然规定了长度为4，却可以无限使用`add`方法增加。**
3. 与java相同，List的长度是从0开始计算。



# License

本文已将所有引用其他文章之内容清楚明白地标注，其他部分皆为作者劳动成果。对作者劳动成果做以下声明：

copyright © 2021 苏月晟，版权所有。

[![知识共享许可协议](https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-nc-sa/4.0/)
本作品由苏月晟采用[知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc-sa/4.0/)进行许可。不可以商业目的转载和引用此文章，在非商业转载时请注明来源和作者信息，并采用相同的许可协议。如需商业转载需联系作者并取得作者本人同意。

``
