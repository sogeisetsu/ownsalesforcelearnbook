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

**每个 DML 语句接受单个 sObject 或 sObject 的列表（或数组）。**每个 Apex 事务有 **150** 条语句的 DML 限制，对 sObject 列表执行 DML 操作算作一个 DML 语句，而不是每个 sObject 一个语句。**对 sObject 列表进行操作是处理记录更有效的方法。**

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

**插入记录时，系统会为每条记录分配一个 ID。除了将 ID 值保留在数据库之外，ID 值还会自动填充到您在 DML 调用中用作参数的 sObject 变量上。**

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

- **同步 Apex 为 100 个 SOQL 查询，异步 Apex 为 200 个。**
- **每次查询最多查询200个记录**

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

*SearchQuery* 表示要搜索的文本（单个单词或短语）。搜索词可以与逻辑运算符（AND、OR）和括号组合。此外，搜索词可以包含通配符（`*`、`?`）。通配符 `*` 在搜索词的中间或结尾匹配零个或多个字符。通配符 `?` 只匹配搜索词中间或结尾的一个字符。

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

**触发器执行完毕后，系统保存 `before` 触发器的触发记录。如果对这些记录执行 DML 语句，则会出现错误。**

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

### 使用触发器异常

您有时需要对某些数据库操作添加限制，例如在满足某些条件时防止保存记录。要防止在触发器中保存记录，请对相关 sObject 调用 addError() 方法。addError() 方法在触发器内部抛出一个致命错误。用户界面将显示并记录该错误提示。

```apex
trigger AccountDeletion on Account (before delete) {
   
    // Prevent the deletion of accounts if they have related opportunities.
    for (Account a : [SELECT Id FROM Account
                     WHERE Id IN (SELECT AccountId FROM Opportunity) AND
                     Id IN :Trigger.old]) {
        Trigger.oldMap.get(a.Id).addError(
            'Cannot delete account with related opportunities.');
    }
    
}
```

除非批量 DML 调用时部分成功，否则**在触发器中调用 addError() 会导致整个操作集回滚。**

- 如果 Apex 中的 DML 语句生成了触发器，则任何错误都会回滚整个操作。但是，运行时引擎仍会处理操作中的每条记录以编译完整的错误列表。
- 如果 Lightning 平台 API 中的批量 DML 调用生成了触发器，则运行时引擎会将不良记录放在一边。然后，运行时引擎尝试保存部分未生成错误的记录。

## 禁用触发器

假设有一个触发器名为`AccountDeletion`，禁用该触发器方法如下：

1. 在 Setup（设置）中，搜索 Apex Triggers（Apex 触发器）。
2. 在 Apex Triggers（Apex 触发器）页面中，单击 AccountDeletion 触发器旁边的 **Edit（编辑）**。
3. 取消选择 **Is Active（有效）**。
4. 单击**保存**。

### 借助vscode

[Disable a Salesforce Trigger in Production with VS Code - Spinning Code](https://spinningcode.org/2022/02/disable-a-salesforce-trigger-in-production-with-vs-code/)

1. 首先，默认vscode中有一个salesforce project并且连接正常。

2. 将需要禁用的trigger所属的xml文件的`status`更改为`Inactive`（**Update the trigger’s XML file to change the status**. All project code files in SFDX are accompanied by an XML file of class metadata. Open the file and change the status to “Inactive”.）

   ```xml
   <?xml version='1.0' encoding='UTF-8'?>
   <ApexTrigger xmlns="http://soap.sforce.com/2006/04/metadata">
     <apiVersion>54.0</apiVersion>
     <status>Inactive</status>
   </ApexTrigger>
   ```

3. 如果需要的话（一般情况下不会需要），在`sfdx-project.json`文件的`packageDirectories`节点加入trigger所在的文件夹（**一般是triggers文件夹已经包含在force-app文件夹里，所以不用单独设置**）

4. 在triggers文件夹右键点击deploy source to org。

## 批量触发

[批量 Apex 触发器 单元 | Salesforce Trailhead](https://trailhead.salesforce.com/zh-CN/content/learn/modules/apex_triggers/apex_triggers_bulk)

总是会需要一些对记录集进行整体操作。

salesforce是有查询限制的：

- 每个 Apex 事务有 **150** 条语句的 DML 限制
- 同步 Apex 为 100 个 SOQL 查询，异步 Apex 为 200 个。

为了更好使用触发器，有下面几种方式：

- 对记录集进行for循环，原因是要对完整记录集起作用

  ```apex
  trigger MyTriggerBulk on Account(before insert) {
      for(Account a : Trigger.New) {
          a.Description = 'New description';
      }
  }
  ```

- 执行批量 SOQL,防止大量的循环进行soql操作

  - 通过一步查询获取记录

    ```apex
    trigger SoqlTriggerBulk on Account(after update) {  
        // Perform SOQL query once.    
        // Get the accounts and their related opportunities.
        List<Account> acctsWithOpps = 
            [SELECT Id,(SELECT Id,Name,CloseDate FROM Opportunities) 
             FROM Account WHERE Id IN :Trigger.New];
      
        // Iterate over the returned accounts    
        for(Account a : acctsWithOpps) { 
            Opportunity[] relatedOpps = a.Opportunities;  
            // Do some other processing
        }
    }
    ```

  - SOQL for 循环(推荐)，既防止soql查询限制，又代码整洁

    ```apex
    trigger SoqlTriggerBulk on Account(after update) {  
        // Perform SOQL query once.    
        // Get the related opportunities for the accounts in this trigger,
        // and iterate over those records.
        for(Opportunity opp : [SELECT Id,Name,CloseDate FROM Opportunity
            WHERE AccountId IN :Trigger.New]) {
      
            // Do some other processing
        }
    }
    ```

- 批量DML

  ```apex
  trigger AddRelatedRecord on Account(after insert, after update) {
      List<Opportunity> oppList = new List<Opportunity>();
      
      // Add an opportunity for each account if it doesn't already have one.
      // Iterate over accounts that are in this trigger but that don't have opportunities.
      for (Account a : [SELECT Id,Name FROM Account
                       WHERE Id IN :Trigger.New AND
                       Id NOT IN (SELECT AccountId FROM Opportunity)]) {
          // Add a default opportunity for this account
          oppList.add(new Opportunity(Name=a.Name + ' Opportunity',
                                     StageName='Prospecting',
                                     CloseDate=System.today().addMonths(1),
                                     AccountId=a.Id)); 
      }
      
      if (oppList.size() > 0) {
          insert oppList;
      }
  }
  ```

  

# Asynchronous Apex（异步APEX）

Asynchronous 发音：[eɪˈsɪŋkrənəs]

## 简介

简而言之，异步 Apex 用于稍后在单独的线程中运行进程。

An asynchronous process is a process or function that executes a task "**in the background**" without the user having to wait for the task to finish.

有以下特点：

- 效率

  无需等待就可以进行下一个进程，可以在做其他事情的同时等待完成，而不是等着上一个进程完成浪费时间。

- 可扩展性

  通过允许平台的某些功能在未来某个时间资源可用时执行，可以快速管理和扩展资源。这允许平台使用并行处理来处理更多作业。

- 更高的limit

  异步进程在新线程中启动，具有更高的调控器和执行限制。

异步 Apex 有多种不同的风格。我们将很快详细介绍每一个，但这里是一个高级概述。

| 类型           | 概述                                                         | 常见场景                            |
| :------------- | :----------------------------------------------------------- | :---------------------------------- |
| Future Methods | 在自己的线程中运行，并且**在资源可用之前不要启动**。         | Web 服务标注。                      |
| Batch Apex     | 运行超出正常处理限制的大型作业。                             | 数据清理或记录归档。                |
| Queueable Apex | 类似于Future Methods，但提供额外的作业链接并允许使用更复杂的数据类型。 | 使用外部 Web 服务执行顺序处理操作。 |
| Scheduled Apex | 安排 Apex 在指定时间运行。                                   | 每日或每周任务。                    |

这些不同类型的异步操作并不相互排斥。 For instance, a common pattern is to kick off a Batch Apex job from a Scheduled Apex job.

处理异步请求有下面三个过程：

**入队**（**Enqueue**）

请求被放入队列。这可能是 Apex 批处理请求、未来 Apex 请求或许多其他请求之一。该平台将请求与适当的数据一起排队以处理该请求。

**持久性**（**Persistence**）

排队的请求被保留。请求存储在持久存储中，用于故障恢复并提供事务功能。

**出队**（**Dequeue**）

入队的请求将从队列中移除并进行处理。如果处理失败，事务控制确保请求不会丢失。

**异步处理的优先级低于通过浏览器和 API 实现的实时交互，不能保证处理时间，但总会完成。**

## Future Apex

Future Apex is used to run processes in a separate thread, at a later time when system resources become available.

Future Methods 的本质是用@future 注解标识的方法。

### 语法

未来的方法必须是**静态方法**，并且只能返回一个 **`void` 类型**。指定的**参数必须是基础数据类型、基础数据类型数组或基础数据类型集合**。值得注意的是，未来的方法不能使用标准或自定义对象作为参数。**一个常见的模式是向方法传递一个要异步处理的记录 id 列表**。

```apex
public class SomeClass {
  @future
  public static void someFutureMethod(List<Id> recordIds) {
    List<Account> accounts = [Select Id, Name from Account Where Id IN :recordIds];
    // process account records to do awesome stuff
  }
}
```

**future methods不能保证按照它们被调用的顺序执行。**当使用 future methods时，两个 future methods也可能同时运行，如果这两个方法更新同一条记录，这可能会导致记录锁定和令人讨厌的运行时错误。

考虑使用 Batch Apex 而不是future methods来异步处理大量记录。这比为每条记录创建future请求更有效。

## Batch Apex

Batch Apex 用于运行超出正常处理限制的大型作业（想想数千或数百万条记录！）。使用 Batch Apex，可以批量异步处理记录（因此得名“Batch Apex”）以保持在平台限制内。

![](https://suyuesheng-biaozhun-blog-tupian.oss-cn-qingdao.aliyuncs.com/blogimg/20220405145307.png)



## Queueable 

利用future method的简单性和 Batch Apex 的强大功能，将它们混合在一起形成 Queueable Apex！它提供了平台序列化的类结构、没有start和stop方法的简化接口，**甚至允许使用的不仅仅是原始参数！它由一个简单的 `System.enqueueJob()` 方法调用，该方法返回一个可以监控的作业 ID。**

Queueable Apex allows you to submit jobs for asynchronous processing similar to future methods with the following additional benefits:

- 非原始类型：Queueable 类可以包含非原始数据类型的成员变量，例如 sObjects 或自定义 Apex 类型。作业执行时可以访问这些对象
- 可监控：the method returns the ID of the AsyncApexJob record.
- Chaining（链接） jobs: You can chain one job to another job by starting a second job from a running job. Chaining jobs is useful if you need to do some sequential（顺序的） processing.

### 语法

要使用 Queueable Apex，只需实现 Queueable 接口。

```apex
public class SomeClass implements Queueable {
    public void execute(QueueableContext context) {
        // awesome code here
    }
}
```

#### 示例代码

```apex
public class UpdateParentAccount implements Queueable {
    private List<Account> accounts;
    private ID parent;
    public UpdateParentAccount(List<Account> records, ID id) {
        this.accounts = records;
        this.parent = id;
    }
    public void execute(QueueableContext context) {
        for (Account account : accounts) {
          account.parentId = parent;
          // perform other processing or callout
        }
        update accounts;
    }
}
```

#### 调用

```apex
// find all accounts in ‘NY’
List<Account> accounts = [select id from account where billingstate = ‘NY’];
// find a specific parent account for all records
Id parentId = [select id from account where name = 'ACME Corp'][0].Id;
// instantiate a new instance of the Queueable class
UpdateParentAccount updateJob = new UpdateParentAccount(accounts, parentId);
// enqueue the job for processing
ID jobID = System.enqueueJob(updateJob);
```

### 链接作业

Queueable Apex 的最佳功能之一是作业链接。要将作业链接到另一个作业，从可排队类的 execute() 方法提交第二个作业。只能从正在执行的作业中添加一个作业，这意味着每个父作业只能存在一个子作业。例如，如果您有一个名为 SecondJob 的第二个类实现了 Queueable 接口，可以在 execute() 方法中将该类添加到队列中，如下所示：

```apex
public class FirstJob implements Queueable {
    public void execute(QueueableContext context) {
        // Awesome processing logic here
        // Chain this job to next job by submitting the next job
        System.enqueueJob(new SecondJob());
    }
}
```

### 要记住的事情

Queueable Apex 是一个很棒的新工具，但有几点需要注意：

- 您可以在**单个事务**中使用 System.enqueueJob 将多达 50 个作业添加到队列中。
- 链接作业时，您可以使用 System.enqueueJob 从正在执行的作业中添加一个作业，这意味着每个父队列作业只能存在一个子作业。从同一个可排队作业启动多个子作业是不允许的。
- 对链接作业的深度没有限制，这意味着您可以将一个作业链接到另一个作业，并对每个新的子作业重复此过程以将其链接到新的子作业。但是，对于 Developer Edition 和 Trial 组织，链接作业的最大堆栈深度为 5，这意味着您可以链接作业四次，并且链中的最大作业数为 5，包括初始父队列作业。

也就是说Queueable Apex的Chaining必须是一条线。

## Scheduled Apex

The Apex Scheduler lets you delay execution so that you can run Apex classes at a specified time. This is ideal for daily or weekly maintenance tasks using Batch Apex. To take advantage of the scheduler, write an Apex class that implements the Schedulable interface, and then schedule it for execution on a specific schedule.

### 语法

要调用 Apex 类以在特定时间运行，首先为该类实现 Schedulable 接口。然后，**使用 `System.schedule` 方法安排类的实例在特定时间运行。**

```apex
public class SomeClass implements Schedulable {
    public void execute(SchedulableContext ctx) {
        // awesome code here
    }
}
```

该方法的参数是一个 SchedulableContext 对象。在计划了一个类之后，将创建一个表示计划作业的 CronTrigger（定时触发） 对象。它提供了一个 getTriggerId 方法，该方法返回 CronTrigger API 对象的 ID。

### 使用 System.Schedule 方法

System.Schedule 方法接受三个参数：作业的名称、用于表示作业计划运行的时间和日期的 CRON 表达式，以及实现 Schedulable 接口的类的实例。

```apex
RemindOpptyOwners reminder = new RemindOpptyOwners();
// Seconds Minutes Hours Day_of_month Month Day_of_week optional_year
String sch = '20 30 8 10 2 ?';
String jobID = System.schedule('Remind Opp Owners', sch, reminder);
```

#### 用于表示作业时间和日期的表达式

语法如下：

```apex
Seconds Minutes Hours Day_of_month Month Day_of_week Optional_year
```

```apex
秒 分 时 月的某一天 月 周的某一天 年（可选）
```

以下是表达式的值：

| Name          | Values                                                       | Special Characters |
| :------------ | :----------------------------------------------------------- | :----------------- |
| Seconds       | 0–59                                                         | None               |
| Minutes       | 0–59                                                         | None               |
| Hours         | 0–23                                                         | None               |
| Day_of_month  | 1–31                                                         | `, - * ? / L W`    |
| Month         | 1–12 or the following:`JAN`、`FEB`、`MAR`、`APR`、`MAY`、`JUN`、`JUL`、`AUG`、`SEP`、`OCT`、`NOV`、`DEC`。 | `, - * /`          |
| Day_of_week   | 1–7 or the following:SUN、MON、TUE、WED、THU、FRI、SAT（注意每周的第一天是周日） | `, - * ? / L #`    |
| optional_year | null or 1970–2099                                            | `, - * /`          |

The special characters are defined as follows:

| Special Character | Description                                                  |
| :---------------- | :----------------------------------------------------------- |
| ,                 | 分隔值。例如，使用`JAN, MAR, APR` 指定超过一个月。           |
| -                 | 指定范围。例如，使用 `JAN-MAR` 指定超过一个月。              |
| *                 | 指定所有值。例如，如果将 Month 指定为 `*`，则每月安排作业。  |
| ?                 | 不指定具体值。这仅适用于 Day_of_month 和 Day_of_week，通常用于指定一个值而不是另一个值时。 |
| /                 | 指定增量。斜线前的数字指定间隔的开始时间，斜线后的数字是间隔量。例如，如果您为 Day_of_month 指定 `1/5`，则 Apex 类从每月的第一天开始每五天运行一次。 |
| L                 | 指定范围的结尾（最后一个）。这仅适用于 Day_of_month 和 Day_of_week。与 Day of month 一起使用时，L 始终表示该月的最后一天，例如 1 月 31 日，闰年的 2 月 29 日，等等。当单独与 Day_of_week 一起使用时，它始终表示 7 或 SAT。**当与 Day_of_week 值一起使用时，它表示该月中该类型日期的最后一天。**例如，如果您指定 2L，则您指定的是该月的最后一个星期一。不要使用 L 的值范围，因为结果可能出乎意料。 |
| W                 | 指定给定日期最近的工作日（周一至周五）。这仅适用于 Day_of_month。例如，如果您指定 `20W`，并且 20 日是星期六，则课程将在 19 日进行。如果您指定 `1W`，并且第一个是星期六，则该类不会在上个月运行，而是在第三个，即下一个星期一运行。**一起使用 L 和 W 可以来指定该月的最后一个工作日。** |
| #                 | 指定月份的第 n 天，格式为 weekday#day_of_month。这仅适用于 Day_of_week。 `#` 前面的数字指定工作日 (SUN-SAT)。 `#` 后面的数字指定月份中的日期。例如，指定 2#2 表示班级在每个月的第二个星期一上课。 |

以下是如何使用表达式的一些示例：

再回顾一遍表示日期的语法：

```apex
Seconds Minutes Hours Day_of_month Month Day_of_week Optional_year
```

| Expression         | Description                                         |
| :----------------- | :-------------------------------------------------- |
| 0 0 13 * * ?       | Class runs every day at 1 PM.                       |
| 0 0 22 ? * 6L      | Class runs the last Friday of every month at 10 PM. |
| 0 0 10 ? * MON-FRI | Class runs Monday through Friday at 10 AM.          |
| 0 0 20 * * ? 2010  | Class runs every day at 8 PM during the year 2010.  |

### 注意

**您一次只能有 100 个计划的 Apex 作业（You can only have 100 scheduled Apex jobs at one time）也就是说在一个事务或者方法里面schedule apex只能有最多100个**

# 测试

在您为 Lightning 平台 AppExchange 部署或打包代码之前，必须测试至少 75% 的 Apex 代码，并且所有这些测试都必须通过。

测试类和方法使用 isTest 注释定义，语义如下：

```apex
@isTest
private class MyTestClass {
    @isTest static void myTest() {
        // code_block
    }
}
```

**测试类可以是专用或公用。**如果您仅将测试类用于单元测试，请将其声明为专用。公用测试类通常用于测试数据工厂类，稍后会介绍。

测试方法的可见性并不重要，因此将测试方法声明为公用或专用没有区别，因为测试框架始终能够访问测试方法。基于这个原因，语法中省略了访问修饰符。

```apex
@isTest
private class TestVerifyDate{
    @isTest static void in30Days(){
        Date d1 = Date.newInstance(2022, 3, 1);
        Date d2 = d1.addDays(2);
        VerifyDate.CheckDates(d1, d2);
    }

    @isTest static void over30Days(){
        Date d1 = Date.newInstance(2022, 3, 1);
        Date d2 = d1.addDays(31);
        VerifyDate.CheckDates(d1, d2);
    }
}
```

**在测试方法中创建的 Salesforce 记录不会提交到数据库。**测试执行完成后，回滚 Salesforce 记录。回滚行为对测试而言很方便，原因是您不必在测试执行后清理测试数据。

默认情况下，**Apex 测试除拥有访问设置和元数据对象（例如用户或配置文件对象）权限以外，无权访问组织中“预先存在(pre-existing)”的数据。**

> Starting with Apex code saved using Salesforce API version 24.0 and later, test methods don’t have access by default to pre-existing data in the organization, such as **standard objects, custom objects, and custom settings data**, and **can only access data that they create.** However, objects that are used to manage your organization or metadata objects can still be accessed in your tests.
>
> ---
>
> 也就是说，**虽然不能访问standard objects，但是可以访问自己创建的数据。比如说在测试中无法访问某个已经存在的Account object的record，但是自己可以创建一个新的Account object的record，然后访问它。**

 

有时测试方法需要访问预先存在的数据。要访问组织数据，可以使用 `@isTest(SeeAllData=true)` 注释测试方法。

## 建立数据和测试数据分离

可以使用`Test.startTest()`和`Test.stopTest()`来将测试过程中建立数据和测试数据分离。

**为什么要建立数据和测试数据分离？**

首先必须了解一件事情就是在一个事务中，salesforce对数据库操作是有限制的：

- 每个 Apex 事务有 **150** 条语句的 DML 限制
- 同步 Apex 为 100 个 SOQL 查询，异步 Apex 为 200 个。

有可能在测试过程中就已经接近达到了salesforce的限制，所以就无法验证要测试的代码是否接近了salesforce的限制。

salesforce在`Test.startTest()`和`Test.stopTest()`之间的代码分配了一个全新的调速器限制，也就是说如果在在`Test.startTest()`之前浪费了99条DML语句，那么在`Test.startTest()`和`Test.stopTest()`之间是全新的150个DML语句限制，在`Test.stopTest()`之后，数据库限制将会继承`Test.startTest()`之前的状况，也就是还剩下*150-99=51*个DML语句可以执行。

还有一个原因就是使用了建立数据和测试数据分离之后，代码会更加规范。

下面是在测试trigger的过程中，使用了`Test.startTest()`和`Test.stopTest()`：

```apex
// TODO 测试触发器
@isTest
private class TestAccountDeletion {
    @isTest static void TestDeleteAccountWithOneOpportunity() {
        // Test data setup
        // Create an account with an opportunity, and then try to delete it
        Account acct = new Account(Name='Test Account');
        insert acct;
        Opportunity opp = new Opportunity(Name=acct.Name + ' Opportunity',
                                       StageName='Prospecting',
                                       CloseDate=System.today().addMonths(1),
                                       AccountId=acct.Id);
        insert opp;
        // Perform test
        Test.startTest();
        Database.DeleteResult result = Database.delete(acct, false);
        Test.stopTest();
        // Verify 
        // In this case the deletion should have been stopped by the trigger,
        // so verify that we got back an error.
        System.assert(!result.isSuccess());
        System.assert(result.getErrors().size() > 0);
        System.assertEquals('Cannot delete account with related opportunities.',
                             result.getErrors()[0].getMessage());
                             
    }
}
```

## 为 Apex 测试创建测试数据

测试实用程序类包含测试方法可以调用的方法，用来执行实用的任务，例如建立测试数据。

```apex
// TODO 测试实用程序类包含测试方法可以调用的方法，用来执行实用的任务，例如建立测试数据。
/*
    TestDataFactory 类是一种特殊的类 — 它是一个用 isTest 注释的公共类，
    只能从正在运行的测试中访问。测试实用程序类包含测试方法可以调用的方法，
    用来执行实用的任务，例如建立测试数据。测试实用程序类不受组织的代码大小限制。
 */
@isTest
// TODO 用来创建测试数据的测试类要用public修饰
public class TestDataFactory {
    public static List<Account> createAccountsWithOpps(Integer numAccts, Integer numOppsPerAcct) {
        List<Account> accts = new List<Account>();
        for(Integer i=0;i<numAccts;i++) {
            Account a = new Account(Name='TestAccount' + i);
            accts.add(a);
        }
        insert accts;
        List<Opportunity> opps = new List<Opportunity>();
        for (Integer j=0;j<numAccts;j++) {
            Account acct = accts[j];
            // For each account just inserted, add opportunities
            for (Integer k=0;k<numOppsPerAcct;k++) {
                opps.add(new Opportunity(Name=acct.Name + ' Opportunity ' + k,
                                       StageName='Prospecting',
                                       CloseDate=System.today().addMonths(1),
                                       AccountId=acct.Id));
            }
        }
        // Insert all opportunities for all accounts.
        insert opps;
        return accts;
    }
}
```

然后在测试类中调用测试实用程序类来获取测试数据。

# 限制

[Execution Governors and Limits | Apex Developer Guide | Salesforce Developers](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_gov_limits.htm)



# License

本文已将所有引用其他文章之内容清楚明白地标注，其他部分皆为作者劳动成果。对作者劳动成果做以下声明：

copyright © 2021 苏月晟，版权所有。

[![知识共享许可协议](https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-nc-sa/4.0/)
本作品由苏月晟采用[知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc-sa/4.0/)进行许可。不可以商业目的转载和引用此文章，在非商业转载时请注明来源和作者信息，并采用相同的许可协议。如需商业转载需联系作者并取得作者本人同意。

