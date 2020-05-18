## 1 Junit单元测试

* Junit使用：白盒测试
* 步骤：
  1. 定义一个测试类(测试用例)
    * 测试类名：被测试的类名Test		CalculatorTest
    * 包名：xxx.xxx.xx.test		cn.itcast.test

  2. 定义测试方法：可以独立运行
    - 方法名：test测试的方法名		testAdd()  

    * 返回值：void
    * 参数列表：空参

  3. 给方法加@Test
  4. 导入junit依赖环境

* 判定结果：
  * 红色：失败
  * 绿色：成功
  * 一般我们会使用断言操作来处理结果
    * Assert.assertEquals(期望的结果,运算的结果);

* 补充：
  * @Before：修饰的方法会在测试方法之前被自动执行
  * @After：修饰的方法会在测试方法执行之后自动被执行

# 2 BeanUtils

## 2.1 BeanUtils概述

- BeanUtils类的功能是把一个Map集合中的数据, 封装到一个 JavaBean上
- 使用BeanUtils工具类中的populate方法就可以把Map集合中的数据封装到指定的bean上
- Map中的key名称必须和bean对象的属性名称保持一致
- Request 请求 -> getParameter -> getParameterMap(); -> populate 填充 -> JavaBean 类的对象.

## 2.2 BeanUtils方法

|                          方法                           |                             描述                             |
| :-----------------------------------------------------: | :----------------------------------------------------------: |
| populate(Object bean,Map<String,String[]>   properties) | 将Map数据封装到指定Javabean中，一般用于将表单的所有数据封装到javabean |
|   setProperty(Object obj,String name,Object   value)    |                          设置属性值                          |
|           getProperty(Object obj,String name)           |                          获得属性值                          |