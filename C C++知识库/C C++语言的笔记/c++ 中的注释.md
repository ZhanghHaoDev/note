# c++ 中的注释

这个工具，可以帮助我们更好的编写注释，还可以使用他来生成HTML文档，还可以生成文件包含和过程调用等关系

1. 安装

[https://www.doxygen.nl/index.html](https://www.doxygen.nl/index.html)

vscode 插件推荐：Doxygen Documentation Generator

1. 使用

我们安装这个工具主要是用于生成文档，但如果不安装他也是可以的

比如在编写函数的时候，我们编写完成函数的声明以后，也可以自定义或借助插件的帮助，来生成注释

1. 注释规范：

文件的注释

**代码**

---

/******************************************************************************  OpenST Basic tool library                                                 **  Copyright (C) 2014 Henry.Wen  renhuabest@163.com.                         **                                                                            **  This file is part of OST.                                                 **                                                                            **  This program is free software; you can redistribute it and/or modify      **  it under the terms of the GNU General Public License version 3 as         **  published by the Free Software Foundation.                                **                                                                            **  You should have received a copy of the GNU General Public License         **  along with OST. If not, see < [http://www.gnu.org/licenses/](http://www.gnu.org/licenses/)>.               **                                                                            **  Unless required by applicable law or agreed to in writing, software       **  distributed under the License is distributed on an "AS IS" BASIS,         **  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  **  See the License for the specific language governing permissions and       **  limitations under the License.                                            **                                                                            **  @file     Example.h                                                       **  @brief    对文件的简述                                                      **  Details.                                                                  **                                                                            **  @author   Henry.Wen                                                       **  @email    renhuabest@163.com                                              **  @version  1.0.0.1(版本号)                                                  **  @date     renhuabest@163.com                                              **  @license  GNU General Public License (GPL)                                **                                                                            **----------------------------------------------------------------------------**  Remark         : Description                                              **----------------------------------------------------------------------------**  Change History :                                                          **  <Date>     | <Version> | <Author>       | <Description>                   **----------------------------------------------------------------------------**  2014/01/24 | 1.0.0.1   | Henry.Wen      | Create file                     **----------------------------------------------------------------------------**                                                                            ******************************************************************************/

---

命名空间的注释

**代码**

---

/**   * @brief 命名空间的简单概述 \n(换行)   * 命名空间的详细概述    */     namespace OST    {    }

---

类的注释

**代码**

---

/**    * @brief 类的简单概述 \n(换行)    * 类的详细概述    */    class Example    {    };        枚举类型定义、结构体类型定义注释风格类似    /**     * @brief 简要说明文字    */    typedef struct 结构体名字    {       成员1, /*!< 简要说明文字 */ or ///<说明， /**<说明 */ 如果不加<，则会认为是成员2的注释       成员2, /*!< 简要说明文字 */ or ///<说明， /**<说明 */        成员3, /*!< 简要说明文字 */ or ///<说明， /**<说明 */     }结构体别名；

---

函数的注释

**代码**

---

/**     * @brief 函数简要说明-测试函数    * @param index    参数1    * @param t            参数2 @see CTest    *    * @return 返回说明    *        -<em>false</em> fail    *        -<em>true</em> succeed    */    bool Test(int index, const CTest& t);        note：指定函数注意项事或重要的注解指令操作符    note格式如下：            @note 简要说明

retval：指定函数返回值说明指令操作符。(注:更前面的return有点不同.这里是返回值说明)    retval格式如下：            @retval 返回值 简要说明                pre：指定函数前置条件指令操作符    pre格式如下：            @pre 简要说明                       par：指定扩展性说明指令操作符讲。（它一般跟code、endcode一起使用 ）    par格式如下：          @par 扩展名字              code、endcode：指定    code、endcode格式如下：

@code                简要说明(内容)            @endcode

see：指定参考信息。

see格式如下：

@see 简要参考内容

deprecated：指定函数过时指令操作符。

deprecated格式如下：

@deprecated 简要说明

---

1. 常用的指令

| **指令** | **说明** |
| --- | --- |
| @file | 档案的批注说明 |
| @author | 作者 |
| @brief | 类或函数的简单说明 |
| @param | 函数说明，后面跟参数的名字，然后是关于该参数的说明 |
| @return | 返回值的说明 |
| @retval | 返回值类型 |
| @note | 注解 |
| @attention | 注意 |
| @warning | 警告信息 |
| @enum | 枚举值，文档会产生链接 |
| @var | 引用的某个变量，文档产生链接 |
| @class | 类说明 |
| @exception | 异常描述 |