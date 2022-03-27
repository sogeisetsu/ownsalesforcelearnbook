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

```java
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

