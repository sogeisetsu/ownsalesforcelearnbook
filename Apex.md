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

## 控制数据流

### 比较运算符

| Operator | Description              | Syntax           | Result |
| :------- | :----------------------- | :--------------- | :----- |
| <        | Less than                | 1 < 2            | TRUE   |
| <=       | Less than or equal to    | 1 <= 2 3 <= 3    | TRUE   |
| ==       | Equal to                 | 10 == 10         | TRUE   |
| != <>    | Not equal to             | 10 != 0 10 <> 11 | TRUE   |
| >        | Greater than             | 11 > 10          | TRUE   |
| >=       | Greater than or equal to | 40 >=10 40 >= 40 | TRUE   |

### 逻辑运算符

| **Operator**        | OR                                        | AND                                       |
| ------------------- | ----------------------------------------- | ----------------------------------------- |
| **Operator symbol** | \|\|                                      | &&                                        |
| **Pseudocode**      | If X or Y, do this. Otherwise, do that.   | If X and Y, do this. Otherwise, do that.  |
| **Apex code**       | `if(X || Y) {//do this} else {//do this}` | `if(X && Y) {//do this} else {//do this}` |

### 条件语句

1. if else

   ```apex
   String waterLevel = 'full'; /*This variable keeps track of the water level status: full or empty*/
     
   if(waterLevel == 'empty') {
       System.debug('Fill the tea kettle');
       waterLevel = 'full'; /*Once the tea kettle is filled the variable is changed to full*/
   } else {
       System.debug('The tea kettle is full');
   }
   ```

2. if-else if

   ```apex
   String waterLevel = 'half';
     
   if(waterLevel == 'empty') {
       System.debug('Fill the tea kettle');
       waterLevel = 'full';
   } else if(waterLevel == 'half') {
       System.debug('Fill the tea kettle');
       waterLevel = 'full';
   } else { /*This statement only runs if line 3 and line 6 result in false.*/
       System.debug('The tea kettle is full');
   }
   ```

3. **Switch** 

   ```apex
   String waterLevel = 'empty';
   
   switch on waterLevel {
       when 'empty', 'half' { //when waterLevel is either empty or half
           System.debug('Fill the tea kettle');
       }
       when 'full' {
           System.debug('The tea kettle is full');
       }
       when else {
           System.debug('Error!');
       }
   }
   ```

## 循环

while 和 do while循环和java一致，不再阐述。

# Apex 基础知识和数据库

这次将会比较深入地讲解基础知识。

**Apex 是不区分大小写的语言**

## 使用 Visual Studio Code

[Make Visual Studio Code Salesforce Ready Unit | Salesforce Trailhead](https://trailhead.salesforce.com/en/content/learn/projects/quickstart-vscode-salesforce/vscode-salesforce-ready#)

## sObject

类似于java中的pijo（Plain Old Java Objects）层。

**每条 Salesforce 记录在插入 Salesforce 之前，都表示为一个 sObject。同样，当从 Salesforce 检索持久化记录时，这些记录将存储在 sObject 变量中。**

以下示例创建了类型为 Account、名称为 Acme 的 sObject 并将其分配给了 `acct` 变量。

```apex
Account acct = new Account(Name='Acme');
```

Apex 引用标准或自定义 sObject，字段用它们的唯一 API 名称。

对于**自定义对象和自定义字段，API 名称始终以 `__c` 后缀结尾。对于自定义关系字段，API 名称以 `__r` 后缀结尾。**例如：

- 标签为 Merchandise 的自定义对象的 API 名称为 Merchandise__c。
- 标签为 Description 的自定义字段的 API 名称为 Description__c。
- 标签为 Items 的自定义关系字段的 API 名称为 Items__r。

### 创建 sObject 并添加字段

与实例化一个对象的方式没有显著差异。

- 点记法为 sObject 添加字段

  ```apex
  Account acct = new Account();
  acct.Name = 'Acme';
  acct.Phone = '(415)555-1212';
  acct.NumberOfEmployees = 100;
  ```

- 构造器填充

  ```apex
  Account acct = new Account(Name='Acme', Phone='(415)555-1212', NumberOfEmployees=100);
  ```

在填充的时候，必须先填充必填字段，才能插入新记录。

### 泛型

此泛型并非一般面向对象的编程语言的泛型，而是父类型的继承关系，也就是说`sObject`类是所有`sObject`子类的父类。

当不知道正在处理的 `sObject` 类型方法时，您可以使用泛型 `sObject` 数据类型。

```apex
sObject sobj1 = new Account(Name='Trailhead');
sObject sobj2 = new Book__c(Name='Workbook 1');
```

**特定 sObject 类型支持使用点记法访问字段，而泛型 sObject 却不支持。**由于 **`sObject` 是所有特定 `sObject` 类型的父类型**，因此您可以将泛型 sObject 转换为特定 sObject。

```apex
// Cast a generic sObject to an Account
Account acct = (Account)myGenericSObject;
// Now, you can use the dot notation to access fields on Account
String name = acct.Name;
String phone = acct.Phone;
```

**只能通过 `put()` 和 `get()` 方法访问泛型 sObject 的字段。**

## 通过 DML 操作记录

[通过 DML 操作记录 单元 | Salesforce Trailhead](https://trailhead.salesforce.com/zh-CN/content/learn/modules/apex_database/apex_database_dml)

使用 Data Manipulation Language（简称 DML）在 Salesforce 中创建和修改记录。DML 提供简单语句用于插入、更新、合并、删除和恢复记录操作，方便您以简单直接的方式来管理记录。

类似于SSM的Mybatis或者java的jdbc。

此示例将 Acme 客户添加到 Salesforce。首先创建一个客户 sObject，然后将其作为参数传递给 insertstatement，insertstatement 会将记录保留在 Salesforce 中。

```apex
// Create the account sObject 
Account acct = new Account(Name='Acme', Phone='(415)555-1212', NumberOfEmployees=100);
// Insert the account by using DML
insert acct;
```

**每个 DML 语句接受单个 sObject 或 sObject 的列表（或数组）。**每个 Apex 事务有 150 条语句的 DML 限制，对 sObject 列表执行 DML 操作算作一个 DML 语句，而不是每个 sObject 一个语句。**对 sObject 列表进行操作是处理记录更有效的方法。**

以下是可用的 DML 语句。

- `insert`
- `update`
- `upsert`
- `delete`
- `undelete`
- `merge`

通过 `upsert` DML 操作在单个语句中创建新记录并更新 sObject 记录，使用指定字段来确定现有对象的存在，如果没有指定字段，则使用 ID 字段。也就是说如果比对的字段值已经存在就`update`，若不存在就`insert`，若存在多个，就报错。

- 如果主键不匹配，则创建新对象记录。
- 如果主键匹配一次，则更新已有对象记录。
- 如果主键匹配多次，则会产生错误，并且不插入也不更新对象记录。

使用的方式如下：

- `upsert sObject | sObject[]  field`

- `upsert sObject | sObject[]`

可选字段是字段令牌。例如，要指定 MyExternalID 字段，语句是：

```apex
upsert sObjectList Account.Fields.MyExternalId;
```

`Merge` 语句将最多三个相同 sObject 类型的记录合并到其中一个记录中，同时删除其他记录，并重新设置关联记录的父级。

### **自动分配给新记录的 ID 字段**

插入记录时，系统会为每条记录分配一个 ID。除了将 ID 值保留在数据库之外，ID 值还会自动填充到您在 DML 调用中用作参数的 sObject 变量上。

sObject 变量包含 DML 调用后的 ID，您可以重用 sObject 变量来执行其他 DML 操作，例如更新操作，**因为系统能够通过匹配 ID 的方式将 sObject 变量映射到其对应的记录上。**

您可以从数据库中检索记录以获取其字段，包括 ID 字段，**但这不能通过 DML 来完成。需要使用 SOQL 编写查询语句**。

### 删除记录

通过 `delete` 语句删除永久记录。已删除的记录不会从 Lightning 平台永久删除，而是在回收站中保存 15 天，您可以从回收站中恢复记录。

### 异常

如果 DML 操作失败，将返回 `DmlException` 类型的异常。您可以在代码中捕获异常以处理错误情况。

```apex
try {
    // This causes an exception because 
    //   the required Name field is not provided.
    Account acct = new Account();
    // Insert the account 
    insert acct;
} catch (DmlException e) {
    System.debug('A DML exception has occurred: ' +
                e.getMessage());
}
```

### 数据库方法

Apex 包含了内置的数据库类，该类提供执行 DML 操作和镜像 DML 语句对应项的方法。

数据库方法是**静态的，并在类名上调用。**

- `Database.insert()`
- `Database.update()`
- `Database.upsert()`
- `Database.delete()`
- `Database.undelete()`
- `Database.merge()`

数据库方法返回包含每个记录的成功或失败信息的结果对象。

**`insert` 和 `update` 操作都会返回 `Database.SaveResult` 对象数组。`upsert` 操作返回 `Database.UpsertResult` 对象，delete 操作返回 `Database.DeleteResult` 对象。**

[Database Class | Apex Developer Guide | Salesforce Developers](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_methods_system_database.htm)

数据库方法有两个好处

- 一个是数据库方法有一个可选的 allOrNone 参数（默认为true），它允许您指定操作是否可以部分成功。当该参数设置为 `false` 时，如果部分记录集发生错误，将提交成功的记录，并为失败的记录返回错误。另外，部分成功选项不会抛出异常。
- 另一个是可以记录错误信息

```apex
/*

To pass this challenge, create an Apex class that inserts a new account named after 
an incoming parameter. If the account is successfully inserted, the method should 
return the account record. If a DML exception occurs, the method should return null.
 */

public class AccountHandler {
    // 参数是客户名称
    public static Account insertNewAccount(String name){
        Account a= new Account(Name=name);
        // allOrNone参数为false,不会抛出错误,会记录错误类型
        Database.SaveResult result= Database.insert(a,false);
        if(result.isSuccess()){
            // 插入记录时，系统会为每条记录分配一个 ID
            System.debug(a.Id);
            return a;
        }else{
            System.debug(result.getErrors().size());
            for(Database.Error error:result.getErrors()){
                System.debug('影响的字段'+error.getFields());
                System.debug('错误消息'+error.getMessage());
            }
            return null;
        }
    }
}

```

### 处理相关记录

可以通过为一个记录指定相关联的外键ID来指定相关记录，但是如果更新相关记录需要执行单独调用 DML 操作。

```apex
// Query for the contact, which has been associated with an account.
Contact queriedContact = [SELECT Account.Name 
                          FROM Contact 
                          WHERE FirstName = 'Mario' AND LastName='Ruiz'
                          LIMIT 1];
// Update the contact's phone number
queriedContact.Phone = '(415)555-1213';
// Update the related account industry
queriedContact.Account.Industry = 'Technology';
// Make two separate calls 
// 1. This call is to update the contact's phone.
update queriedContact;
// 2. This call is to update the related account's Industry field.
update queriedContact.Account; 
```

`Delete` 操作支持级联删除。在每条子记录都允许删除的情况下删除父对象，其子对象也会自动删除。

## SOQL（未完）

[编写 SOQL 查询 单元 | Salesforce Trailhead](https://trailhead.salesforce.com/zh-CN/content/learn/modules/apex_database/apex_database_soql)

从数据库中检索记录以获取其字段，包括 ID 字段，**但这不能通过 DML 来完成。需要使用 SOQL 编写查询语句**。

SOQL与常规的mysql基本一致。

与其他 SQL 语言不同，您不能为所有字段指定 *。您必须指定想要明确获取的每个字段。如果您尝试访问 SELECT 子句中未指定的字段，则会出现错误，原因是未检索到该字段。

您不需要在查询中指定 Id 字段，因为无论是否在查询中指定 Id 字段，它都会在 Apex 查询中返回。例如：`SELECT Id,Phone FROM Account` 和 `SELECT Phone FROM Account` 是等效的语句。如果 Id 字段是您要检索的唯一字段，那么您可能需要指定该字段，因为必须至少列出一个字段：`SELECT Id FROM Account`。在查询编辑器中运行查询时，您可能也需要指定 Id 字段，如果不指定，Id 字段将不会在查询结果中显示。

字符串比较不区分大小写。

## SOSL（未完）

Salesforce 对象搜索语言 (SOSL) 是一种 Salesforce 搜索语言，用于在记录中执行文本搜索。使用 SOSL 在 Salesforce 中跨多个标准和自定义对象记录搜索字段。SOSL 类似于 Apache Lucene。

另一个区别是 SOSL 基于单词匹配的方式来匹配字段，而默认情况下即便不使用通配符，SOQL 仍然执行精确匹配。例如，在 SOSL 中搜索 "Digital" 会返回字段值为 "Digital" 或 "The Digital Company" 的记录，但 SOQL 只返回字段值为 "Digital" 的记录。

SOQL 和 SOSL 是两种不同语法的独立语言。每种语言都有一个独特的用例：

- 使用 SOQL 检索单个对象的记录。
- 使用 SOSL 跨多个对象搜索字段。SOSL 查询可以搜索对象上的大多数文本字段。

[编写 SOSL 查询 单元 | Salesforce Trailhead](https://trailhead.salesforce.com/zh-CN/content/learn/modules/apex_database/apex_database_sosl)

### 语法

```apex
FIND 'SearchQuery' [IN SearchGroup] [RETURNING ObjectsAndFields]
```

*SearchGroup* 是可选的。它表示要搜索的字段范围。如果未指定，则默认搜索范围是所有字段。*SearchGroup* 可以取以下值之一。

- `ALL FIELDS`
- `NAME FIELDS`
- `EMAIL FIELDS`
- `PHONE FIELDS`
- `SIDEBAR FIELDS`



# 触发器（trigger）（未完）

[Apex 触发器入门教程 单元 | Salesforce Trailhead](https://trailhead.salesforce.com/zh-CN/content/learn/modules/apex_triggers/apex_triggers_intro)

Apex 触发器使您能够在事件之前或之后对 Salesforce 中的记录执行自定义操作，例如添加、更新或删除。就像数据库系统支持触发器一样，Apex 为管理记录也提供了触发器支持。

触发器定义的语法与类定义的语法不同。触发器定义以 trigger 关键字开头。然后是触发器的名称、触发器关联的 Salesforce 对象以及触发条件。触发器包含以下语法：

```java
trigger TriggerName on ObjectName (trigger_events) {
   code_block
}
```

要在插入、更新、删除和取消删除操作之前或之后执行触发器，请在逗号分隔列表中指定多个触发器事件。可指定事件（trigger_events）如下：

- `before insert`
- `before update`
- `before delete`
- `after insert`
- `after update`
- `after delete`
- `after undelete`

## 第一次编写

编写一个trigger：

```apex
trigger HelloWorldTrigger on Account (before insert) {
    System.debug('触发器开始');
	System.debug('Hello World!');
    System.debug('触发器结束');
}
```

运行下列**Anonymous** 代码：

```apex
Account a = new Account(Name='Test Trigger');
insert a;
```

日志：

```
17:07:22.37 (208907128)|USER_DEBUG|[2]|DEBUG|触发器开始
17:07:22.37 (208926372)|USER_DEBUG|[3]|DEBUG|Hello World!
17:07:22.37 (208938148)|USER_DEBUG|[4]|DEBUG|触发器结束
```

## 触发器类型

- Before 触发器通常用于在记录被保存到数据库之前更新或者校验记录值。
- After 触发器用于访问系统设置的字段值（例如记录的 Id 或者 LastModifiedDate 字段），并影响其他记录中的更改。对触发 *after 触发器*的记录拥有只读权限。

要访问导致触发器触发的记录，请使用上下文变量。例如，**`Trigger.New` 包含插入或更新触发器中插入的所有记录。`Trigger.Old` 提供在更新触发器中更新之前的旧版本 `sObject`，或删除触发器中已删除的 `sObject` 列表。**当插入一条记录或通过 API 或 Apex 批量插入记录时，会触发触发器。因此，诸如 `Trigger.New` 之类的上下文变量只能包含一条或多条记录。您可以遍历 `Trigger.New` 来获取每个独立的 `sObject`。

```apex
trigger HelloWorldTrigger on Account (before insert) {
    for(Account a : Trigger.New) {
        a.Description = 'New description';
    }   
}
```

**触发器执行完毕后，系统保存 before 触发器的触发记录。如果对这些记录执行 DML 语句，则会出现错误。**

### 触发上下文变量

| 变量          | 使用情况                                                     |
| :------------ | :----------------------------------------------------------- |
| isExecuting   | 如果 Apex 代码的当前上下文是触发器，而不是 Visualforce 页面、Web 服务或 executeanonymous() API 调用，则返回 true。 |
| isInsert      | 如果此触发器由于插入操作，并从 Salesforce 用户界面、Apex 或 API 触发，则返回 true。 |
| isUpdate      | 如果此触发器由于更新操作，并从 Salesforce 用户界面、Apex 或 API 触发，则返回 true。 |
| isDelete      | 如果此触发器由于删除操作，并从 Salesforce 用户界面、Apex 或 API 触发，则返回 true。 |
| isBefore      | 如果在保存任何记录之前触发此触发器，则返回 true。            |
| isAfter       | 如果在保存任何记录之后触发此触发器，则返回 true。            |
| isUndelete    | 如果在从回收站恢复记录后触发此触发器，则返回 true。从 Salesforce 用户界面、Apex 或 API 执行取消删除操作后，会出现恢复记录的情况。 |
| new           | 返回 sObject 记录的新版本列表。此 sObject 列表仅在 insert、update 和 undelete 触发器中可用，并且只能在 before 触发器中修改记录。 |
| newMap        | ID 到 sObject 新版本记录的映射。此映射仅在 before update、after insert、after update 以及 after undelete 触发器中可用。 |
| old           | 返回 sObject 记录的旧版本列表。此 sObject 列表仅在 update 和 delete 触发器中可用。 |
| oldMap        | ID 到 sObject 旧版本记录的映射。此映射仅在 update 和 delete 触发器中可用。 |
| operationType | 返回与当前操作对应的 System.TriggerOperation 类型的枚举。System.TriggerOperation 枚举的可能值包括：BEFORE_INSERT、BEFORE_UPDATE、BEFORE_DELETE、AFTER_INSERT、AFTER_UPDATE、AFTER_DELETE 和 AFTER_UNDELETE。如果您根据不同的触发器类型改变编程逻辑，请考虑使用 switch 语句，该语句具有独特触发器执行枚举状态的不同排列。 |
| size          | 触发器调用中包含的新旧记录总数。                             |

部分上下文变量返回一个布尔值，以指示触发器是由于更新还是其他事件引起的触发。当触发器组合多个事件时，这些变量有很大的用处。例如：

```apex
trigger ContextExampleTrigger on Account (before insert, after insert, after delete) {
    if (Trigger.isInsert) {
        if (Trigger.isBefore) {
            // Process before insert
        } else if (Trigger.isAfter) {
            // Process after insert
        }        
    }
    else if (Trigger.isDelete) {
        // Process after delete
    }
}
```



# License

本文已将所有引用其他文章之内容清楚明白地标注，其他部分皆为作者劳动成果。对作者劳动成果做以下声明：

copyright © 2021 苏月晟，版权所有。

[![知识共享许可协议](https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-nc-sa/4.0/)
本作品由苏月晟采用[知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc-sa/4.0/)进行许可。不可以商业目的转载和引用此文章，在非商业转载时请注明来源和作者信息，并采用相同的许可协议。如需商业转载需联系作者并取得作者本人同意。

