# MSON Specification
# MSON 规范
Markdown Syntax for Object Notation (MSON) is a plain-text syntax for the description and validation of data structures.

Markdown 语法表示对象(MSON) 是一种用纯文本语法描述、验证数据结构的规范。

## Quick Links
## 快速导航

- 1 [How to Read the Grammar][] [如何阅读这个语法手册][]
    - 1.1 [Markdown Syntax][] [Markdown 语法][]
    - 1.2 [Notational Conventions][] [符号约定][]
    - 1.3 [Promises][] [承诺][]
- 2 [Types][] [类型][]
    - 2.1 [Base Types][] [基本类型][]
        - 2.1.1 [Primitive Types][] [原始类型][]
        - 2.1.2 [Structure Types][] [结构类型][]
    - 2.2 [Named Types][] [命名类型][]
    - 2.3 [Member Types][] [成员类型][]
        - 2.3.1 [Property Member Types][] [属性成员类型][]
        - 2.3.2 [Value Member Types][] [值成员类型][]
- 3 [Type Declaration][] [类型声明][]
    - 3.1 [Named Declaration][] [命名声明][]
        - 3.1.1 [Generic Named Declaration][] [泛型命名声明][]
    - 3.2 [Property Member Declaration][] [属性成员声明][]
        - 3.2.1 [Property Name][] [属性名][]
        - 3.2.2 [Variable Property Name][] [可变属性名][]
    - 3.3 [Value Member Declaration][] [值成员声明][]
    - 3.4 [Value Definition][] [值定义][]
        - 3.4.1 [Value][] [值][]
        - 3.4.2 [Literal Value][] [文字值][]
        - 3.4.3 [Variable Value][] [可变值][]
    - 3.5 [Type Definition][] [类型定义][]
        - 3.5.1 [Type Specification][] [类型规范][]
            - 3.5.1.1 [Variable Type Specification][] [可变类型规范][]
        - 3.5.2 [Type Name][] [类型名][]
            - 3.5.2.1 [Variable Type Name][] [可变类型名][]
            - 3.5.2.2 [Wildcard Type Name][] [通配符类型名][]
        - 3.5.3 [Type Attribute][] [类型属性][]
    - 3.6 [Description][] [描述][]
- 4 [Type Sections][] [类型片段][]
    - 4.1 [Block Description][] [描述块][]
    - 4.2 [Member Type Group][] [成员类型分组][]
        - 4.2.1 [Member Type Separator][] [成员类型分离器][]
    - 4.3 [Nested Member Type][] [嵌套成员类型][]
    - 4.4 [Sample][] [样本][]
    - 4.5 [Default][] [默认][]
    - 4.6 [Validations][] [验证][]
- 5 [Type Inheritance][] [类型继承][]
    - 5.1 [Mixin Type][] [混合类型][]
    - 5.2 [One Of Type][] [单一类型][]
    - 5.3 [Generic Named Type][] [泛型命名类型][]
    - 5.4 [Member Type Precedence][] [成员类型优先级][]
- 6 [Reserved Characters & Keywords][] [保留字符和关键字][]
    - 6.1 [Characters][] [字符][]
    - 6.2 [Keywords][] [关键字][]
    - 6.3 [Additional Keywords][] [其他关键字][]

## 1 How to Read the Grammar
## 1 如何阅读这个语法手册
- An arrow (→) mark grammar productions that can be read as "is defined by|is defined by a(n)"
- 单箭头(→)标记的语法可以读成"被 a(n) 定义|由 a(n) 定义"
- A double arrow (⇒) marks grammar productions that can be read as "contains|contains a(n)"
- 双箭头(⇒)标记的语法可以读成"包含|包含 a(n)"
- _Italic_ text indicates syntactic categories
- _斜体_ 文本表示语法范畴
- A `code span` indicates literal characters, words and punctuations
- `代码块` 表示字符串、文字和标点
- A pipe character (|) separates alternative grammar productions
- 管道字符(|)分割代表二选一
- A following _[opt]_ indicates optional syntactic categories and literals
- 被 _[opt]_ 跟随（在opt之前的）的选项表示可选的语法或文字

### 1.1 Markdown Syntax
### 1.1 Markdown 语法
Note this reference is using ATX-style headers (#) and hyphen-style lists (-) exclusively. However you MAY use
Setext-style headers and/or asterisk (*) or plus (+) style lists if you prefer.

注意这个参考文档使用 ATX 风格标题(#)和连字符风格列表(-)。当然如果你喜欢也“可以”使用 Setext 风格标题配合星号(*)或者加号(+)风格列表。

### 1.2 Notational Conventions
### 1.2 符号约定
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described in [RFC2119][].

这个文档中关键字 “必须”，“必须不”，“要求”，“将要”，“不将要”，“应该”，“不应该”，“推荐”，“可以”，和“可选”的解释在 [RFC2119文档][]中。

### 1.3 Promises
### 1.3 承诺
By default, MSON explicitly defines data structures and the meaning of their members without making any assertion to the
exclusivity of structures or their members. Further, no assertion is made concerning the presence of defined
structures or members. Rather, MSON describes structures that MAY be observed versus what MUST be observed.

默认情况下，MSON明确定义数据结构及其成员含义，无须通过任何断言建立结构及成员的排他性。进一步讲，没有断言造就了结构或成员的限定存在。相反，MSON描述了“可以”观察与“必须”遵守的结构。（PS：我理解的意思是，相对于不能出现什么值、不能出现什么类型这种反向定义，MSON是正向定义）

However, much like JSON Schema being able to restrict "additionalProperties", MSON allows annotating structures to
indicate when they are strictly defined to preclude other structures and members and when they have strict ordering.

然而，就像 JSON Schema 能够限制“additionalProperties”一样，MSON 允许通过在结构上注释，来表明结构的严格排他性和成员的严格顺序性（PS：additionalProperties是在JSON Schema中对额外属性做限定用的）。

## 2 Types
## 2 类型
In MSON, data structures are described by header-defined and/or list-defined _Types_ and/or combinations thereof built
from a limited set of _[Base Types][]_. A particular _Type_ is defined by its _[Type Declaration][]_ and combination of
optional _[Type Sections][]_.

在 MSON 中，数据格式通过标题头、列表声明 _类型_ 或者两者组合，从有限的 _[基本类型][]_ 来构建。
特定 _类型_ 是由 _[类型声明][]_ 和 可选 _[类型片段][]_ 组合定义的。

_Type_ → _[Type Declaration][]_
_类型_ → _[类型声明][]_

_Type_ ⇒ _[Type Sections][]_ _[opt]_
_类型_ ⇒ _[类型片段][]_ _[可选项]_

More specifically:

更多：

_Type_ → _[Type Declaration][]_
_类型_ → _[类型声明][]_

_Type_ ⇒ _[Block Description][]_ _[opt]_
_类型_ ⇒ _[描述块][]_ _[可选项]_

_Type_ ⇒ _[Member Type Group][]_ _[opt]_ |  _[Nested Member Types][]_ _[opt]_
_类型_ ⇒ _[成员类型分组][]_ _[可选项]_ |  _[嵌套成员类型][]_ _[可选项]_

_Type_ ⇒ _[Sample][]_ _[opt]_
_类型_ ⇒ _[样本][]_ _[可选项]_

_Type_ ⇒ _[Validations][]_ _[opt]_
_类型_ ⇒ _[验证][]_ _[可选项]_

- Header-defined _[Named Type][]_
- 标题头定义 _[命名类型][]_

    ```
    # Person (object)
    A person.

    ## Properties
    - `first_name`
    - `last_name`
    - address
        - city
        - street
    ```

- List-defined _[Member Type][]_
- 列表定义 _[成员类型][]_

    ```
    - person (object) - A person
        - `first_name`
        - `last_name`
        - address
            - city
            - street
    ```

    or, equivalently:

    等效：

    ```
    - person (Person) - A person
    ```

### 2.1 Base Types
### 2.1 基本类型
MSON defines a number of distinct base, case-insensitive _[Primitive][]_ and _[Structure Types][]_ from which all data
structures are built (sub-typed).

MSON定义了许多独特的、基本的、大小写友好的 _[原始类型][]_ 和 _[结构类型][]_ ，他们是用来构建（子类型）数据结构的基础。

#### 2.1.1 Primitive Types
#### 2.1.1 原始类型
Applies to basic data structure and type definitions. _[Types][]_ that are sub-typed from _Primitive Types_ MUST NOT
contain a _[Member Type Group][]_ or _[Nested Member Types][]_.

适用于基本数据结构和类型定义。自定义 _[类型][]_ 是 _原始类型_ 的子类型，原始类型“必须不”能包含 _[成员类型分组][]_ 或 _[嵌套成员类型][]_ 。

- `boolean`

    Specifies a type with allowed values of `true` or `false`.

    只能允许`true` 或 `false`作为值。

- `string`

    Specifies any string.

    任何字符串。

- `number`

    Specifies any number.

    任何数字。

#### 2.1.2 Structure Types
#### 2.1.2 结构类型
Applies to recursive, composite data structure and type definitions. _[Types][]_ that are sub-typed from
_Structure Types_ MAY contain a _[Member Type Group][]_ or _[Nested Member Types][]_.

适用于递归，复合数据结构和类型定义。自定义 _[类型][]_ 是 _结构类型_ 的子类型，结构类型“可以”包含一个 _[成员类型分组][]_ 或 _[嵌套成员类型][]_ 。

Structure Types may directly or indirectly contain recursive references to
themselves.

结构类型可以直接或间接地包含对自身的递归引用。

- `array`

    Specifies a list of items for values.

    拥有值项的列表。

- `enum`

    Specifies an exclusive list of possible _[Values][]_ or _[Types][]_ for values.

    有限可能值或类型的独占列表。

- `object`

    Specifies a structure that contains properties as members.

    包含属性成员的结构体。

### 2.2 Named Types
### 2.2 命名类型
Users may extend _[Base Types][]_ to define new header-defined _Named Types_ that MAY be referenced to build other
_[Types][]_.

用户可以通过标题头扩展 _[基本类型][]_ ，新建 _命名类型_ 从而“可以”构建其他 _[类型][]_ 。

_Named Type_ → _[Named Declaration][]_ | _[Generic Named Declaration][]_
_命名类型_ → _[命名声明][]_ | _[泛型命名声明][]_

_Named Type_ ⇒ _[Type Sections][]_ _[opt]_
_命名类型_ ⇒ _[类型片段][]_ _[可选项]_

```
# Person (object)
- first_name
- last_name
```

### 2.3 Member Types
### 2.3 成员类型
Markdown lists specify MSON _Member Types_, which define the structure and types of individual
members of _[Types][]_ built from _[Structure Types][]_. A _[Member Type][]_ that contains _[Nested Member Types][]_
defines an inner, anonymous type that specifies the structure of values of that particular member.

Markdown 列表可以指定 MSON _成员类型_ ，定义自己的成员 _[类型][]_ 用于构建 _[结构类型][]_ 。一个 _[成员类型][]_ 包含内部 _[嵌套成员类型][]_ 、匿名类型，以用来指定特定成员结构。

#### 2.3.1 Property Member Types
#### 2.3.1 属性成员类型
Define individual members of `object` type structures.

`object`类型结构中各个成员的定义。

_Property Member Type_ → _[Property Member Declaration][]_
_属性成员类型_ → _[属性成员声明][]_

_Property Member Type_ ⇒ _[Type Sections][]_ _[opt]_
_属性成员类型_ ⇒ _[类型片段][]_ _[可选项]_

Any list of _[Property Member Types][]_ collectively MAY define an implied parent `object` type structure.

任何 _[属性成员类型][]_ 的列表集合“可以”隐含定义其父级为`object`类型结构。

```
- person (object) - A person
    - `first_name`
    - `last_name`
    - address
- company (string)
```

Defines a `person` _Property Member Type_ with a value that is an explicit `object` type structure with members
`first_name`, `last_name`, and `address` and, at the same time, is a member together with `company` of another
implied `object` structure.

定义一个结构（未给出），`person` _属性成员类型_ 被显示定义为`object`类型结构，其中包含`first_name`，`last_name`，和`address`子成员，`company`属性成员同时被包含在这个被隐含定义为`object`类型的结构中。

#### 2.3.2 Value Member Types
#### 2.3.2 值成员类型
Define individual members of `array` or `enum` type structures.

`array`或`enum`类型结构的各个成员的定义。

_Value Member Type_ → _[Value Member Declaration][]_
_值成员类型_ → _[值成员声明][]_

_Value Member Type_ ⇒ _[Type Sections][]_ _[opt]_
_值成员类型_ ⇒ _[类型片段][]_ _[可选项]_

```
- (array)
    - red (string) - A sample value
    - green (string)
```

## 3 Type Declaration
## 3 类型声明
Defines a particular MSON _[Type][]_.

特殊 MSON _[类型][]_ 定义。

_Type Declaration_ → _[Named Declaration][]_ | _[Generic Named Declaration][]_ | _[Property Member Declaration][]_  | _[Value Member Declaration][]_

_类型声明_ → _[命名声明][]_ | _[泛型命名声明][]_ | _[属性成员声明][]_  | _[值成员声明][]_


### 3.1 Named Declaration
### 3.1 命名声明
Defines a _[Named Type][]_.

_[命名类型][]_ 定义。

_Named Declaration_ → `#` _[Type Name][]_` `_[Type Definition][]_ _[opt]_

_命名声明_ → `#` _[类型名][]_` `_[类型定义][]_ _[opt]_

```
# Person (object)
```

### 3.1.1 Generic Named Declaration
### 3.1.1 泛型命名声明
Defines a _[Named Type][]_ that allows an italicized _[Variable Type Name][]_ to represent a _[Type Name][]_
at any location in the _[Type Specification][]_ of a _[Variable Type Specification][]_.

_[命名类型][]_ 允许斜体 _[可变类型名][]_ 代表 _[类型名][]_ 在 _[类型规范][]_ 或者 _[可变类型规范][]_ 的任何位置定义。

_Generic Named Declaration_ →  `#` _[Type Name][]_` `_[Variable Type Specification][]_

_泛型命名声明_ →  `#` _[类型名][]_` `_[可变类型规范][]_

```
# One or Many (enum[*T*])
```

### 3.2 Property Member Declaration
### 3.2 属性成员声明
Defines a _[Property Member Type][]_.

_[属性成员类型][]_ 定义。

_Property Member Declaration_ → `-` _[Property Name][]_ `:` _[opt]_ _[Value Definition][]_ _[opt]_ `-` _[opt]_ _[Description][]_ _[opt]_
_属性成员声明_ → `-` _[属性名][]_ `:` _[可选项]_ _[值定义][]_ _[可选项]_ `-` _[可选项]_ _[描述][]_ _[可选项]_

```
- person (object) - A person
```

The optional `:` is only applicable in the case where a _[Value Definition][]_ is present and includes a _[Value][]_.

选项 `:` 只适用 _[值定义][]_ 包含 _[值][]_ 的情况。

```
- company: Apiary (string)
```

#### 3.2.1 Property Name
#### 3.2.1 属性名
Defines the name of a property in an `object` type structure.

`object` 结构中的属性名称定义。

_Property Name_ → _[Literal Value][]_ | _[Variable Property Name][]_
_属性名_ → _[文字值][]_ | _[可变属性名][]_

```
- customer (object)
```

Defines a _[Property Member Declaration][]_ with a _Property Name_ "customer".

一个 _[属性成员声明][]_ 定义了一个叫"customer"的 _属性名_ 。

#### 3.2.2 Variable Property Name
#### 3.2.2 可变属性名
Defines a _[Property Name][]_ that is associated with a specific _[Value Definition][]_ in an `object` type structure
that MAY be any arbitrary name in an actual implementation. The _[Value][]_ of the _Variable Property Name_ serves as
a sample.

实际实现中与`object`类型结构 _[属性名][]_ 关联的具体 _[值定义][]_ “可以”使用任意名称。 _可变属性名_ 的 _[值][]_ 作为一个样本提供。
（TODO：目前理解上有些问题）

_Variable Property Name_ → `*`_[Value Definition][]_`*`
_可变属性名_ → `*`_[值定义][]_`*`

In the case of specifying a _[Variable Property Name][]_, the  _[Value Definition][]_ MAY reference a _[Named Type][]_
that MUST be sub-typed from a `string` _[Primitive Type][]_.

在指定 _[可变属性名][]_ 的情况下，该 _[值定义][]_ “可以”引用一个 _[命名类型][]_ ，并且“必须”是从`string` _[原始类型][]_ 派生的子类型。

```
*rel (Custom String)* (object)
```

Where `rel` is a sample value for the arbitrary _[Property Name][]_ of a _[Property Member Declaration][]_.

其中，`rel` 是一个 _[属性成员定义][]_ 的任意 _[属性名][]_ 的样本值。

### 3.3 Value Member Declaration
### 3.3 值成员声明
Defines a _[Value Member Type][]_. A _Value Member Declaration_ MUST only be used to define structures of `array`
or `enum` _[Member Types][]_.

_[值成员类型][]_ 定义。一个 _值成员声明_ “必须”只能用于`array`或`enum`的 _[成员类型][]_ 结构。

_Value Member Declaration_ → `-` _[Value Definition][]_ `-` _[opt]_ _[Description][]_ _[opt]_
_值成员声明_ → `-` _[值定义][]_ `-` _[可选项]_ _[描述][]_ _[可选项]_

The optional `-` is only applicable in the case where a _[Description][]_ is provided.

可选项 `-` 仅适用于其中  _[描述][]_ 存在的情况。

```
- (array)
```

### 3.4 Value Definition
### 3.4 值定义
Every _[Member Type][]_ MAY specify type information associated with values in a structure or member in a structure.
This includes a _Value Definition_ that may include literal or sample _[Values][]_ and a _[Type Definition]_, including
a _[Type Specification][]_ and/or _[Type Attributes][]_, of associated types.

每个 _[成员类型][]_ “可以”指定值信息或成员信息。_值定义_ 包括文字、样本 _[值][]_ 和 _[类型定义]_ ，类型定义又包括 _[类型规范][]_ 和 _[类型属性][]_。

_Value Definition_ → _[Value][]_ _[opt]_ _[Type Definition][]_ _[opt]_
_值定义_ → _[值][]_ _[可选项]_ _[类型定义][]_ _[可选项]_

A _Value Definition_ MUST include at least a _[Value][]_ or a _[Type Definition][]_. A _Value Definition_ of an
`object` _[Member Type][]_ MUST NOT specify a _[Value][]_.

_值定义_ “必须”至少包含一个 _[值][]_ 或一个 _[类型定义][]_ 。 “不能”给一个 `object` _[成员类型][]_ 指定 _[值][]_ 。

```
5, 6 (array)
```

Defines a _Value Definition_ for an `array` type structure with sample values "5" and "6".

使用样本值“5”和“6” `array` 型结构的 _值定义_ 。

#### 3.4.1 Value
#### 3.4.1 值
Defines either sample or actual value(s) in _[Member Types][]_ based on the associated _[Type Definition][]_ in a
_[Value Definition][]_.

在 _[类型定义][]_ 关联的 _[成员类型][]_ 上定义任意样本值或实际值。

_Value_ → _[Literal Value][]_ | _[Variable Value][]_ | _Values List_
_值_ → _[文字值][]_ | _[可变值][]_ | _值列表_

_Values List_ → _Value_ | _Value_`,` _Values List_
_值列表_ → _值_ | _值_`,` _值列表_

A _Values List_ MUST only be used with `array` or `enum` _[Structure Types][]_ or _[Named Types][]_ derived from them.

_值列表_ “必须” 仅在 `array` `enum` _[结构类型][]_ 或者派生的 _[命名类型][]_ 中使用.

By default:

默认：

- A _Value Definition_ that incorporates a _Values List_ but has no _[Type Definition][]_ implies an
`array` type structure.
- _值定义_ 包含了 _值列表_ ，没有明确 _[类型定义][]_ 的，即隐式意味着为 `array` 类型结构。

```
- list: 1, 2, 3
```

is equivalent to:

相当于：

```
- list: 1, 2, 3 (array)
```

Where "1", "2", and "3" are sample values of the `array` structure.

其中"1", "2", 和 "3" 是 `array` 结构中的样本值。

- A _Value Definition_ that incorporates a _Values List_ defines fully-qualified values of an `enum` type structure.
- _值定义_ 包含限定的 _值列表_ ，即为 `enum` 类型结构。

```
- colors: red, green (enum)
```

Where "red" and "green" are fully-qualified values of the `colors` enumeration.

其中"red"和"green"是 `colors` 枚举的限定值。

#### 3.4.2 Literal Value
#### 3.4.2 文字值
Literal value of a type instance. Some limitations apply (see [Reserved Characters & Keywords][]).

一个类型实例的文本值。一些限制（参见 [保留字符和关键字][]）。

```
5
```

#### 3.4.3 Variable Value
#### 3.4.3 可变值
Defines a _[Value][]_ that is not concrete using Markdown *italics*.

使用 Markdown *斜体* 定义 _[值][]_ 。

_Variable Value_ → `*`_[Literal Value][]_`*`
_可变值_ → `*`_[文字值][]_`*`

A _Variable Value_ MAY be used to indicate a _[Variable Property Name][]_ in a _[Property Member Declaration][]_ or
more generally, a sample value in a _[Value Definition][]_.

_可变值_ 一般地“可以”用来表示 _[属性成员声明][]_ 中的 _[可变属性名][]_ 或 _[值定义][]_ 中的样本值。

```
*rel*
```

#### 3.5 Type Definition
#### 3.5 类型定义
Explicitly specifies the type of a value in an MSON instance.

在 MSON 实例中明确指定值的类型。

_Type Definition_ → `(`_[Type Specification][]_ _[opt]_ `,` _[opt]_ _Type Attributes List_ _[opt]_`)`

_类型定义_ → `(`_[类型规范][]_ _[可选项]_ `,` _[可选项]_ _类型属性列表_ _[可选项]_`)`

_Type Attributes List_ → _[Type Attribute][]_ | _[Type Attribute][]_`,` _Type Attributes List_

_类型属性列表_ → _[类型属性][]_ | _[类型属性][]_`,` _类型属性列表_

A _Type Definition_ MUST separate multiple items with commas and is order-independent.

一个 _类型定义_ “必须”用逗号分隔其中的多个项目，并且顺序无关。

```
(enum, optional)
```

#### 3.5.1 Type Specification
#### 3.5.1 类型规范
Defines sub-typed _[Base Types][]_ or _[Types][]_ for a particular _[Type][]_.

特定 _[类型][]_ 的 _[基本类型][]_ 或自定义 _[类型][]_ 定义。

_Type Specification_ → _[Type Name][]_ | _[Type Name][]_`[`_Nested Type Name List_`]`

_类型规范_ → _[类型名][]_ | _[类型名][]_`[`_嵌套类型名列表_`]`

_Nested Type Name List_ →  _[Type Name][]_ | _[Type Name][]_`,` _Nested Type Name List_

_嵌套类型名列表_ →  _[类型名][]_ | _[类型名][]_`,` _嵌套类型名列表_

An `array` or `enum` _[Value Definition][]_ MAY specify the _Type Specifications_ of implied
_[Nested Member Types][]_ members in-line using `[]` as a _Nested Type Name List_.

`array` 或 `enum` _[值定义][]_ “可以”使用`[]`作为 _嵌套类型名列表_ ，隐含指定 _[嵌套成员类型][]_ 的 _类型规范_。

```
array[number, string]
```

Indicates a `array` type structure MAY include distinct numbers or strings as values.

上面的`array`结构“可以”同时包括数字或字符串的值。

##### 3.5.1.1 Variable Type Specification
##### 3.5.1.1 可变类型规范
Defines a variable _[Type Specification][]_ to indicate generic _[Named Types][]_.

用可变 _[类型规范][]_ 定义泛型 _[命名类型][]_ 的定义。

_Variable Type Specification_ → _[Type Specification][]_

_可变类型规范_ → _[类型规范][]_

A _Variable Type Specification_ MUST include at least one _[Variable Type Name][]_.

一个 _可变类型规范_ “必须”包括至少一个 _[可变类型名][]_ 。

```
# One or Many (enum[*T*])
```

#### 3.5.2 Type Name
#### 3.5.2 类型名
References the name of a type in _[Base Types][]_ or _[Named Types][]_. Some limitations apply (see
[Reserved Characters & Keywords][]).

通过名称引用 _[基本类型][]_ 或 _[命名类型][]_ 。一些限制（参见 [保留字符和关键字][] ）。

_Type Name_ → _[Literal Value][]_ | _[Variable Type Name][]_ | _[Wildcard Type Name][]_ | _Referenced Type Name_

_类型名_ → _[文字值][]_ | _[可变类型名][]_ | _[通配符类型名][]_ | _引用类型名_

_Referenced Type Name_ → *A valid [Markdown-style link][], where the link name MUST be a _[Literal Value][]_*

_引用类型名_ → *一个有效的 [Markdown 风格链接][]，其中的链接名称“必须”是_[文字值][]_*

A _[Variable Type Name][]_ MUST only be used in two situations:
一个 _[可变类型名][]_ “必须”只能用在以下2种情况：
- As a _Type Name_ in a _[Type Definition]_ for a _[Generic Named Type][]_.
- 在 _[类型定义]_ 中作为一个针对 _[泛型命名类型][]_ 的 _类型名_ 。
- As an associated _Type Name_ in _[Nested Member Types][]_ of the _[Generic Named Type][]_.
- 在 _[泛型命名类型][]_ 的 _[嵌套成员类型][]_ 中作为与泛型的关联 _类型名_ 。

A _Referenced Type Name_ MAY be used to link to a _Type Name_ defined in another location in an MSON document
solely as a navigation convenience.

MSON 文档中 _引用类型名_ “可以”方便的用来导航链接到另一个位置定义的 _类型名_ 。

##### 3.5.2.1 Variable Type Name
##### 3.5.2.1 可变类型名
An *italicized* variable that MAY be used in place of a _[Type Name][]_ for a _[Type Definition][]_ in a
_[Generic Named Declaration][]_.

*斜体* 变量“可以”来代替 _[泛型命名声明][]_ 中的 _[类型定义][]_ 的 _[类型名][]_ 。

_Variable Type Name_ → `*`_[Literal Value][]_`*`
_可变类型名_ → `*`_[文字值][]_`*`

##### 3.5.2.2 Wildcard Type Name
##### 3.5.2.2 通配符类型名
Indicates any type MAY be possible.

表示任何“可能”的类型。

_Wildcard Type Name_ → `*`
_通配符类型名_ → `*`

A _Wildcard Type Name_ MAY only be used in a _[Type Specification][]_ for _[Member Types][]_.

一个 _通配符类型名_ 只“可以”用于 _[成员类型][]_ 的 _[类型规范][]_ 。

#### 3.5.3 Type Attribute
#### 3.5.3 类型属性
Defines extra attributes associated with the implementation of a type.

一个类型实现的相关附加属性定义。

- `required` - instance of this type is required
- `required` - 类型实例必要
- `optional` - instance of this type is optional (default)
- `optional` - （默认）类型实例可选
- `fixed`    - instance of this type structure and values are fixed
- `fixed`    - 类型实例结构和值固定
- `nullable` - instance of this type *Value* MAY be unset (e.g. `null` or `nil`)
- `nullable` - 类型实例 *值* “可以” 不设置（`null` 或者 `nil`）
- `sample`   - Alternate way to indicate a _[Value][]_ is a sample. See _[Sample][]_.
- `sample`   - 另一种方式来表示实例 _[值][]_ 是一个样本。见 _[样本][]_ 。
- `default`  - Alternate way to indicate a _[Value][]_ is a default. See _[Default][]_.
- `default`  - 另一种方式来表示实例 _[值][]_ 是一个默认。见 _[默认][]_ 。

A `sample` _Type Attribute_ is mutually exclusive with `default`.

`sample` 和 `default` 是互斥的 _类型属性_ 。

### 3.6 Description
### 3.6 描述
Describes a _[Member Type][]_ in-line.

用连接符来描述 _[成员类型][]_ 。

_Description_ → `-` _Markdown-formatted text_
_描述_ → `-` _Markdown-格式文本_

```
- name: Andrew (string) - A Description
```

## 4 Type Sections
## 4 类型片段
_[Types][]_ MAY contain any _[Block Description][]_, _[Member Type Group][]_, _[Nested Member Types][]_,
_[Sample][]_, _[Default][]_ and/or _[Validations][]_ _Type Sections_. Apart from a _[Block Description][]_, multiple
_[Type Sections][]_ MAY be specified and MAY have any order.

_[类型][]_ “可以”包含 _[描述块][]_ ， _[成员类型分组][]_，_[嵌套成员类型][]_，_[样本][]_ , _[默认值][]_， _[验证][]_ 中的任何 _类型片段_。
除了一个 _[描述块][]_ ，“可以”指定多个 _[类型片段][]_ ，并且顺序“可以”任意。

```
# Person (object)
An additional
multi-line description

- here
- there

## Sample
...

## Properties
- `first_name`
- `last_name`

## Validations
...

## Sample
Another ...
```

In general, _Type Sections_ nested under:
一般情况下，_类型片段_ 嵌套的元素如下：
- A _[Named Declaration][]_ MUST use header-defined (`##`) variations.
- 对于 _[命名声明][]_ 类型片段“必须”使用标题头定义（`##`）。
- A _[Property Member Declaration][]_ or _[Value Member Declaration][]_ MUST use list-defined (`-`) variations.
- 对于 _[属性成员声明][]_ 或 _[值成员声明][]_ 类型片段“必须”使用列表定义（`-`）。

### 4.1 Block Description
### 4.1 描述块
Describes a _[Type][]_ using a nested (multi-line) Markdown text block.

_[类型][]_ 描述使用（多行）嵌套的 Markdown 文本块。

_Block Description_ → _Markdown-formatted text_
_描述块_ → _Markdown-格式文本_

A _Block Description_ MUST be located directly under a _[Type Declaration][]_ and MUST start with text. Markdown lists
MAY be included in a _Block Description_ after initial text content and are considered part of the block text.

一个 _描述块_ “必须”直接在 _[类型声明][]_ 下定义，并且“必须”使用文本开头。
Markdown 列表“可以”包含在 _描述块_ 初始文本内容之后，这样将被认为是块文本的一部分。

```
- name: Andrew (string) - A Description

    An additional
    multi-line description.

    - here
    - there

    More text.
```

Note that `here` and `there` are NOT _[Nested Member Types][]_ but rather are part of a Markdown list in the
_Block Description_.

请注意，在 `here` 和 `there` “不是” _[嵌套成员类型][]_ ，而是 _描述块_ 中 Markdown 列表的一部分。

A _[Member Types][]_ _Block Description_ MUST escape _[Member Type Separator][]_ _[Keywords][]_ as a `code span`
when used in a Markdown list.

_描述块_ 中的描述 _[成员类型][]_ 的 Markdown 列表，“必须”使用`code span`转义 _[成员类型分离器][]_ _[关键字][]_ 。

```
- person (object)
    This person does not have:

    - `Properties`
        - first_name
        - last_name

    - Properties
        - `given_name`
        - surname
```

### 4.2 Member Type Group
### 4.2 成员类型分组
A _Member Type Group_ delineates _[Nested Member Types][]_ and MUST be used when other _[Type Sections][]_ are present.

描述 _[嵌套成员类型][]_ 的 _成员类型分组_ “必须”在其他 _[类型片段][]_ 存在的情况下使用。

_Member Type Group_ → `-` _[Member Type Separator][]_ | `##` _[Member Type Separator][]_
_成员类型分组__ → `-` _[成员类型分离器][]_ | `##` _[成员类型分离器][]_

_Member Type Group_ ⇒ _Nested Member Types_
_成员类型分组_ ⇒ _嵌套成员类型_

In order to specify _[Nested Member Types][]_ after a _Block Description_, _[Types][]_ MUST use an appropriate
_[Member Type Group][]_ to indicate the end of the _Block Description_ and the beginning of a
_[Nested Member Types][]_ list.

为了在 _描述块_ 后指定 _[嵌套成员类型][]_ ，_[类型][]_ “必须”使用适当的 _[成员类型分组][]_ 指示 _描述块_ 的结束和 _[嵌套成员类型][]_ 列表的开始。

- Named Type
- 命名类型

    A header-defined (`##`) _[Member Type Group][]_ SHOULD be nested one additional header level under the associated
    _[Named Type][]_, when required.

    标题头定义的（`##`）_[成员类型分组][]_ ，在需要时，“应该”被嵌套在另外一个与 _[命名类型][]_ 相关联的标题头等级下。

    ```
    # Person (object)
    An additional
    multi-line description

    - here
    - there

    ## Properties
    - `first_name`
    - `last_name`
    ```

- Member Type
- 成员类型

    A list-defined (`-`) _[Member Type Group][]_ SHOULD be nested one indentation level under the associated
    _[Member Type][]_.

    列表定义的（`-`） _[成员类型分组][]_ “应该”被嵌套在相关联的 _[成员类型][]_ 下并增加一个缩进级别。

    ```
    - person (object)

        An additional
        multi-line description

        - here
        - there

        - Properties
            - `first_name`
            - `last_name`
    ```

A _Member Type Group_ of an appropriate type MUST be used to define _[Nested Member Types][]_ whenever any other
_[Type Section][]_ is specified at the same level.

当同级别指定了其他 _[类型片段][]_ ，“必须”使用适当的 _成员类型分组_ 定义类型的 _[嵌套成员类型][]_ 。

- Without a _[Block Description][]_
- 不使用 _[描述块][]_

    - _[Nested Member Types][]_ SHOULD be nested directly under a _[Type Declaration][]_ whenever possible.
    - _[嵌套成员类型][]_ “应该”尽可能直接嵌套在 _[类型声明][]_ 下。
    - _[Nested Member Types][]_ MAY be used without a _Member Type Group_ in a _[Named Type][]_, even if other
    _[Type Sections][]_ are present, if they are nested directly under the _[Type Declaration][]_.
    - _[嵌套成员类型][]_ “可以”直接嵌套在 _[命名类型][]_ 下而不使用 _成员类型分组_ ，即使存在其他 _[类型片段][]_ 。


    ```
    # Person (object)
    - `first_name`
    - `last_name`

    ## Sample
    ...
    ```
- With a _[Block Description][]_
- 使用 _[描述块][]_

    A _Member Type Group_ MUST be used to define _[Nested Member Types][]_.

    _[嵌套成员类型][]_ “必须”由 _成员类型分组_ 来定义。

    ```
    # Person (object)
    Just an ordinary person

    ## Properties
    - `first_name`
    - `last_name`
    ```

#### 4.2.1 Member Type Separator
#### 4.2.1 成员类型分离器
Defines the names of separators to indicate the beginning of a section of _[Nested Member Types][]_.

使用分离器名称来指示 _[嵌套成员类型][]_ 片段的开头。

_Member Type Separator_ →  `Items` | `Members` | `Properties`
_成员类型分离器_ →  `Items` | `Members` | `Properties`

- Array Structures - MUST use `Items` for a _Member Type Separator_
- 数组结构 - “必须”使用`Items`标识 _成员类型分离器_

- Enum Structures - MUST use `Members` for a _Member Type Separator_
- 枚举结构 - “必须”使用`Members`标识 _成员类型分离器_

- Object Structures - MUST use `Properties` for a _Member Type Separator_
- 对象结构 - “必须”使用`Properties`标识 _成员类型分离器_


### 4.3 Nested Member Types
### 4.3 嵌套成员类型
_[Types][]_ built from _[Structure Types][]_ MAY contain _Nested Member Types_, which are defined using nested Markdown
lists of allowed _[Member Types][]_.

从 _[结构类型][]_ 构建的 _[类型][]_ “可以”包含 _嵌套成员类型_ ，允许 _[成员类型][]_ 使用嵌套的 Markdown 列表定义。（PS：这种允许是有限的）

A _[Member Type][]_ that contains _Nested Member Types_ defines an inner, anonymous type that specifies the structure
of values of that particular member.

内部的匿名类型可以通过在 _成员类型_ 中再包含 _[嵌套成员类型][]_ 来定义，可以指定特定结构的成员值。

_Nested Member Types_ → _[Member Types][]_
_嵌套成员类型_ → _[成员类型][]_

By Default:

默认：

- Un-nested Member Types
- 非嵌套成员类型

    A _[Member Type][]_ that does not contain _Nested Member Types_ and does not contain a _[Type Definition][]_
    implies a `string` _[Type Specification][]_.

    一个 _[成员类型][]_ 不包含 _嵌套成员类型_ ，也不包含 _[类型定义][]_ ，这意味着 _[类型规范][]_ 是`string`字符串。

    ```
    - count: 1
    ```

    Implies:

    意味着：

    ```
    - count: 1 (string)
    ```

- Object Structures
- 对象结构

    A _[Property Member Type][]_ without a _[Type Definition][]_ that contains _[Nested Member Types][]_ implies
    an `object` type structure.

    一个 _[属性成员类型][]_ 不包含 _[类型定义][]_ 但包含 _[嵌套成员类型][]_ ，这意味着是`object`对象类型结构。

    ```
    - address
        - city
        - state
    ```

    Implies:

    意味着：

    ```
    - address (object)
        - city
        - state
    ```

- Array Structures
- 数组结构

    A _[Member Type][]_ with an `array` _[Type Definition][]_ that contains _[Nested Member Types][]_
    specifies an `array` type structure that MAY contain items of the specified type and
    sample values per the particular _[Value Definition][]_.

    一个 _[成员类型][]_ 包含 _[嵌套成员类型][]_ 并使用`array`数组 _[类型定义][]_ 指定`array`数组类型结构，
    “可以”包含明确指定了类型和样本值的详细 _[值定义][]_ 子项。

    ```
    - colors (array)
        - red (string)
        - 5 (number)
    ```

    Implies an `array` structure whose individual items MAY be strings or numbers with sample values "red" and "5",
    respectively.

    意味着一个`array`数组结构，其子项“可以”分别是字符串“red”和数字“5”这2个样本值。

- Enum Structures
- 枚举结构

    A _[Member Type][]_ with an `enum` _[Type Definition][]_ that contains _[Nested Member Types][]_
    specifies an `enum` type structure that MUST only contain items of the specified type and
    values per the particular _[Value Definition][]_.

    一个 _[成员类型][]_ 包含 _[嵌套成员类型][]_ 并使用`enum`枚举 _[类型声明][]_ 指定`enum`枚举类型结构，
    “必须”只能包含明确指定了类型和值的详细 _[值定义][]_ 子项。

    ```
    - colors (enum)
        - red (string)
        - 5 (number)
    ```

    Implies a `colors` _[Property Member Type][]_ that MUST only have a value of the string "red" or the number 5.

    意味着`colors` _[属性成员类型][]_ “必须”只能包含字符串“red”和数字“5”。

    A _[Variable Value][]_ in a _[Nested Member Type][]_ under a `enum` type structure indicates an allowed type
    with an associated sample value.

    在`enum`枚举类型结构下， _[嵌套成员类型][]_ 的 _[可变值][]_ 允许设置样本值。

    ```
    - colors (enum)
        - red (string)
        - *5* (number)
    ```

    Implies a `colors` _[Property Member Type][]_ that MUST have either the string "red" or any number as
    a value, where "5" is a sample of a `number` value.

    意味着`colors` _[属性成员类型][]_ “必须”有字符串“red”或任何数字，其中“5”是一个数值的样本。

- Named Types
- 命名类型

    _[Nested Member Types][]_ MAY be nested directly under a _[Named Declaration][]_ when there are no other
    _[Type Sections][]_ present.

    当不存在其他 _[类型片段][]_ 时， _[嵌套成员类型][]_ “可以”直接在 _[命名声明][]_ 下嵌套。

    ```
    # Person (object)
    - `first_name`
    - `last_name`
    ```

With a `fixed` _[Type Attribute][]_:
`fixed`固定的 _[类型属性][]_ ：

- If a _[Named Type][]_ or _[Member Type][]_ annotates its type as `fixed`, all _[Nested Member Types][]_ inherit
the `fixed` attribute as well.
- 如果一个 _[命名类型][]_ 或 _[成员类型][]_ 被诠释为`fixed`固定，所有 _[嵌套成员类型][]_ 继承`fixed`固定属性。

    ```
    - person (object, fixed)
        - name
    ```

    Implies:

    意味着：

    ```
    - person (object, fixed)
        - name (fixed)
    ```

- An `array` based _[Named Type][]_ or _[Member Type][]_ MAY specify `fixed` to indicate the structure is a
"fixed ordered list" of only the specified values and/or types, if any, of its _[Nested Member Types][]_.
- 一个基于`array`的 _[命名类型][]_ 或 _[成员类型][]_ “可以”指定`fixed`固定属性，表示结构是“固定有序列表”，只有指定的值和/或类型，如果有值，它是 _[嵌套成员类型][]_ 。

    ```
    - colors (array, fixed)
        - red
        - green
    ```

    Implies a fixed-list `array` structure that MUST only contain the two items "red" and "green" in that order.

    意味着一个固定列表`array`数组型结构“必须”仅包含2个有序子项“red”和“green”。

    ```
    - components (array, fixed)
        - (object)
        - (string)
    ```

    Implies a fixed-list `array` structure that MUST only contain the two items of an arbitrary `object` and `string`
    in that order.

    意味着固定列`array`数组型结“必须”仅包含2个有序子项`object`型子项和`string`型子项。

- An `object` based _[Named Type][]_ or _[Member Type][]_ MAY specify `fixed` to indicate a "value object" where all
the properties MUST be present and the values of the properties MUST be the values specified, if any, in its
_[Nested Member Types][]_. Further, such an `object` type structure MUST NOT contain any other properties.
- 一个基于`object`的 _[命名类型][]_ 或 _[成员类型][]_ “可以”指定`fixed`固定属性，指示所有属性“必须”存在，如果 _[嵌套成员类型][]_ 有属性值，则值“必须”是规定的值。进一步来讲，`object`型结构类型“必须不”包含其他非法属性。

    ```
    - person (object, fixed)
        - `first_name`: Andrew
        - `last_name`: Smith
    ```

    Implies a "value object" that MUST contain only the properties "first_name" and "last_name" with the values
    "Andrew" and "Smith", respectively.

    意味着“值对象”“必须”只能包含“first_name”和“last_name”属性，而这两个属性的值分别是“Andrew”和“Smith”。

    ```
    - person (object, fixed)
        - `first_name`
        - `last_name`
    ```

    Implies an `object` that MUST contain only the properties "first_name" and "last_name", respectively.

    意味着一个`object`，“必须”只能包含“first_name”和“last_name”属性。

- Individual _[Nested Member Types][]_ MAY override inherited behavior from a `fixed` inherited type
by using an `optional` attribute and/or MAY indicate values are samples using a _[Variable Value][]_.
- 个别 _[嵌套成员类型][]_ “可以”通过使用`optional`可选属性来覆盖继承自`fixed`固定的类型并“可以”使用 _[可变值][]_ 指定样本值。

    ```
    - person (object, fixed)
        - `first_name`
        - `last_name` (optional)
    ```

    Implies a "value object" that MUST contain the property "first_name" and MAY contain the property
    "last_name".

    意味着“值对象”“必须”包含“first_name”属性，“可以”包含“last_name”属性。

    ```
    - colors (array, fixed)
        - red
        - *green*
    ```

    Implies an `array` type structure that MUST contain "red" as an item and MAY contain any other strings, where
    "green" is a sample value.

    意味着`array`型结构“必须”包含“red”子项，“可以”包含其他样本值是“green”的字符串。

### 4.4 Sample
### 4.4 样本
Defines alternate sample _[Values][]_ for _[Member Types][]_ as a nested Markdown list with (multi-line) text.

嵌套在 Markdown 列表中的 _[成员类型][]_ 的备用样本 _[值][]_ 是样本。（TODO：这里理解上有些问题）

_Sample_ → `- Sample` | `- Sample :` _[Value][]_ | `## Sample`
_样本_ → `- Sample` | `- Sample :` _[值][]_ | `## Sample`

_Sample_ ⇒ _Markdown-formatted text_ | _[Value Member Types][]_
_样本_ ⇒ _Markdown-格式文本_ | _[值成员类型][]_

A _[Type][]_ MAY have multiple _Sample_ lists.

一个 _[类型][]_ “可以”有多个 _样本_ 集合。

- Named Types
- 命名类型

    A header-defined (`##`) _[Sample][]_ MUST be nested one additional header level under the associated
    _[Named Type][]_ if a _[Block Description][]_ is used.

    如果使用了 _[描述块][]_ ，标题头定义的（`##`） _[样本][]_ “必须”以额外标题级别嵌套在相关联的 _[命名类型][]_ 下。

    ```
    # Colors (array)
    A list of colors

    ## Sample
    - red

    ## Items
    - (string)

    ## Sample
    - blue
    - green
    ```

    A `sample` _[Type Attribute][]_ MUST NOT be used in the _[Type Definition][]_ of a _[Named Declaration][]_.

    `sample` _[类型属性][]_ “必须不”能在 _[命名声明][]_ 的 _[类型定义][]_ 中使用。

- Member Types
- 成员类型

    A list-defined (`-`) _[Sample][]_ SHOULD be nested one indentation level under the associated
    _[Member Type][]_.

    列表定义的（`-`）_[样本][]_ “应该”被嵌套在相关联的 _[成员类型][]_ 下，并增加一个缩进级别。

    ```
    - colors (array)
      - Sample: red
      - Sample
          - blue
          - green
    ```

    A `sample` _[Type Attribute][]_ MAY be used to indicate a _[Value][]_ in a _[Value Member Type][]_ is a sample
    value.

    `sample` _[类型属性][]_ “可以”用来表示一个  _[值成员类型][]_ 的 _[值][]_ 是一个样本值。

    ```
    - list: 3, 4 (enum, sample)
    ```

    Is equivalent to:

    相当于：

    ```
    - list: *3, 4* (enum)
    ```

    Which, is equivalent to:

    还相当于：

    ```
    - list (enum)
        - Sample
            - 3
            - 4
    ```

    A `default` _[Type Attribute][]_ MUST NOT be used in the _[Type Definition][]_ of a
    _[Property Member Declaration][]_.

    （PS：应该是写错了）
    `sample` _[类型属性][]_ “必须不”能在 _[属性成员声明][]_ 的 _[类型定义][]_ 中使用。（PS：只有object包含属性成员）

### 4.5 Default
### 4.5 默认
Indicates _[Values][]_ for _[Member Types][]_ as a nested Markdown list with (multi-line) text are defaults.

表示嵌套在 Markdown 列表中的 _[成员类型][]_ 的 _[值][]_ 是默认值。

_Default_ → `- Default` | `- Default :` _[Value][]_ | `## Default`
_默认_ → `- Default` | `- Default :` _[值][]_ | `## Default`

_Default_ ⇒ _Markdown-formatted text_ | _[Value Member Types][]_
_默认_ ⇒ _Markdown-格式文本_ | _[值成员类型][]_

A _[Type][]_ MAY have one _Default_ _[Type Section][]_. A _Default_ for a _[Member Type][]_ MAY also indicate a
_[Sample][]_.

一个 _[类型][]_ “可以”有一个 _默认_ 的 _[类型片段][]_ 。一个 _[成员类型][]_ 的 _默认_ 也“可以”用于表明 _[样本][]_。

- Named Types
- 命名类型

    A header-defined (`##`) _[Default][]_ MUST be nested one additional header level under the associated
    _[Named Type][]_ if a _[Block Description][]_ is used.

    如果使用了 _[描述块][]_ ，标题头定义的（`##`） _[默认][]_ “必须”以额外标题级别嵌套在相关联的 _[命名类型][]_ 下。

    ```
    # Colors (array)
    A list of colors

    ## Default
    - red

    ## Items
    - (string)
    ```

     A `default` _[Type Attribute][]_ MUST NOT be used in the _[Type Definition][]_ of a _[Named Declaration][]_.

     `default` _[类型属性][]_ “必须不”能在 _[命名声明][]_ 的 _[类型定义][]_ 中使用。

- Member Types
- 成员类型

    A list-defined (`-`) _[default][]_ SHOULD be nested one indentation level under the associated
    _[Member Type][]_.

    列表定义的（`-`）_[默认][]_ “应该”被嵌套在相关联的 _[成员类型][]_ 下，并增加一个缩进级别。

    ```
    - colors (array)
      - Default: red
    ```

    A `default` _[Type Attribute][]_ MAY be used to indicate a _[Value][]_ in a _[Value Member Type][]_ is a default
    value.

    `default`_[类型属性][]_ “可以”用来表示一个  _[值成员类型][]_ 的 _[值][]_ 是一个默认值。

    ```
    - list: 4 (enum, default)
        - 3
        - 4
    ```

    is equivalent to:

    相当于：

    ```
    - list: 3, 4 (enum)
        - Default: 4
    ```

     A `default` _[Type Attribute][]_ MUST NOT be used in the _[Type Definition][]_ of a
     _[Property Member Declaration][]_.

     `default` _[类型属性][]_ “必须不”能在 _[属性成员声明][]_ 的 _[类型定义][]_ 中使用。
     （PS：只有object包含属性成员，enum和array包含的是值成员）

### 4.6 Validations
### 4.6 验证
Reserved for future use.

未来加入。（PS：应该会使用Validations关键字作为验证分离器）

## 5 Type Inheritance
## 5 类型继承
A _[Member Type][]_ or _[Named Type][]_ that inherits from another _[Named Type][]_ also inherits any
_[Nested Member Types][]_ in the same order they are defined in the inherited _[Named Type][]_ and in order based
on the placement of the _[Mixin Type][]_.

从另一个 _[命名类型][]_ 继承的 _[成员类型][]_ 或 _[命名类型][]_ 同时继承 _[命名类型][]_ 的所有 _[嵌套成员类型][]_ 和顺序。

```
# Person (object)
- `first_name`
- `last_name`
```

And:

和：

```
- person (Person)
    - address
```

Implies the same structure as:

意味与如下结构相同：

```
- person (object)
    - `first_name`
    - `last_name`
    - address
```

Where the inherited _[Member Types][]_ from `Person` _[Named Type][]_ are listed first.

从`Person`继承的 _[成员类型][]_ 会首先列出。

An object may not inherit from itself, either directly or indirectly.

一个对象无法从本身继承，无论是直接或间接。

### 5.1 Mixin Type
### 5.1 混合类型
MSON defines a _Mixin Type_ that supports multiple inheritance from another _[Named Type][]_. The _[Named Type][]_ being inherited MUST be a _[Structure Type][]_ or its sub-type.

MSON _混合类型_ 支持从继承多个 _[命名类型][]_ 。被继承的 _[命名类型][]_ “必须”是一个 _[结构类型][]_ 或结构子类型。

_[Nested Member Types][]_ defined in and inherited from the mixed-in _[Named Type][]_ are added at the same indentation level of the _Mixin Type_.

从 _[命名类型][]_ 混合继承的 _[嵌套成员类型][]_ 在 _混合类型_ 中与其他成员类型具有相同的缩进级别。

_Mixin Type_ → `- Include` _[Type Name][]_ | `- Include` _[Type Definition][]_
_混合类型_ → `- Include` _[类型名][]_ | `- Include` _[类型定义][]_

_Example 1_

_例子 1_

```
# Person (object)
- `first_name`
- `last_name`
```

And:

和：

```
- `formal_person` (object)
    - prefix: Mr
    - Include Person
```

Implies the same structure as:

意味与如下结构相同：

```
- `formal_person` (object)
    - prefix: Mr
    - `first_name`
    - `last_name`
```

_Example 2_
_例子 2_

Alternately:

交替位置：

```
- `formal_person` (object)
    - Include Person
    - prefix: Mr.
```

Implies the same structure as:

意味与如下结构相同：

```
- `formal_person` (object)
    - `first_name`
    - `last_name`
    - prefix: Mr.
```

A _[Mixin Type][]_ MUST use an appropriate _[Member Type Separator][]_ in a _[Member Type Group][]_ in order to specify
_[Nested Member Types][]_ after a _[Block Description][]_.

一个 _[混合类型][]_ 为了在 _[描述块][]_ 之后指定 _[嵌套成员类型][]_ ，“必须”在 _[成员类型分组][]_ 中使用合适的 _[成员类型分离器][]_ 。

```
- address (object)
    An address

    - Properties
        - Include Address
```

### 5.2 One Of Type
### 5.2 单一类型
MSON defines a _One Of Type_ that can be used to describe mutually exclusive sets of _[Nested Member Types][]_. A
_One of Type_ MUST only be used to define _[Property Member Types][]_ for a `object` type structure.

MSON 限定 _单一类型_ 可用于描述互斥的 _[嵌套成员类型][]_ 集。 _单一类型_ “必须”只能用于定义`object`类型结构的 _[属性成员类型][]_ 。

_One of Type_ → `- One Of`
_单一类型_ → `- One Of`

_One of Type_ ⇒ _[Member Type Group][]_
_单一类型_ ⇒ _[成员类型分组][]_

_One of Type_ ⇒ _[Nested Member Types][]_
_单一类型_ ⇒ _[嵌套成员类型][]_

_One of Type_ ⇒ _[Mixin Type][]_
_单一类型_ ⇒  _[混合类型][]_

_One of Type_ ⇒ _One of Type_
_单一类型_ ⇒ _单一类型_

```
- `first_name`
- One Of
    - `last_name`
    - One Of
        - `given_name`: Smith
        - `suffixed_name`: Smith, Sr.
```

Implies values with a structure of:

意味与如下值结构相同：

```
- `first_name`
- `last_name`
```

Or:

或者：

```
- `first_name`
- `given_name`: Smith
```

Or:

或者：

```
- `first_name`
- `suffixed_name`: Smith, Sr.
```

A _One Of Type_ MUST use a `Properties` _[Member Type Separator][]_ in a _[Member Type Group][]_:

一个 _单一类型_ “必须”在 _[成员类型分组][]_ 中的`Properties` _[成员类型分离器][]_ 上使用：
- In order to specify _[Nested Member Types][]_ after a _[Block Description][]_.
- 为了在 _[描述块][]_ 后指定 _[嵌套成员类型][]_ 。

    ```
    - address (object)
        An address

        - Properties
            - One Of
                - state
                - province
    ```

- When it contains a _[Member Type Group][]_.
- 当包含 _[成员类型分组][]_ 。

    ```
    - person (object)
        - One Of
            - `full_name`
            - Properties
                - `first_name`
                - `last_name`
    ```

### 5.3 Generic Named Type
### 5.3 泛型命名类型
Defines a _[Named Type][]_ that allows an italicized _[Variable Type Name][]_ to represent a _[Type Name][]_
at any location in a _[Type Specification][]_.

一个 _[命名类型][]_ 允许在 _[类型规范][]_ 的任何位置使用斜体 _[可变类型名][]_ 代表一个 _[类型名][]_ 。

_Generic Named Type_ → _[Named Type][]_
_泛型命名类型_ → _[命名类型][]_

By default:

默认的：
- A _[Named Type][]_ that contains at least one _[Variable Type Name][]_ is a _Generic Named Type_.
- _[命名类型][]_ 的最后一项类型是 _[可变类型名][]_ 代表类型是 _泛型命名类型_
- A _Variable Type Name_ in a _[Type Specification][]_ MAY only be used in the _[Type Definition][]_ of explicitly
defined _[Nested Member Types][]_ in the _Generic Named Type_ and MUST NOT define any implied _[Nested Member Types][]_.
- _[类型规范][]_ 中的 _可变类型名_ 仅“可以”在明确定义了 _[嵌套成员类型][]_ 的 _泛型命名类型_ _[类型定义][]_ 中使用，并且“必须不”能隐含定义的 _[嵌套成员类型][]_ 。（PS：不太理解）

- Inherited type as a variable
- 继承可变类型

    ```
    # Address Decorator (*T*)
        - address

    # Person (object)
        - `first_name`
        - `last_name`
    ```

    And:

    和:

    ```
    - `decorated_person` (Address Decorator(Person))
    ```

    Implies the same structure as:

    意味与如下结构相同：

    ```
    - decorated_person (object)
        - `first_name`
        - `last_name`
        - address
    ```

- Type passed into explicitly defined _[Member Types][]_
- 传入明确的 _[成员类型][]_ 定义

    ```
    # One or Many (*S*[*T*, string])
    - (*T*)
    - (array[*T*])
    ```

    And:

    和：

    ```
    - rel (One or Many(enum, object))
    ```

    Implies the same structure as:

    意味与如下结构相同：（PS：第二行string是One or Many定义的）

    ```
    - rel (enum)
        - (string)
        - (object)
        - array[object]
    ```

### 5.4 Member Type Precedence
### 5.4 成员类型优先级
Implementers of tooling for MSON structures SHOULD use an inheritance precedence such that the last redundant
_[Member Type][]_ specified in a list at the same indentation level appends or overrides a previously defined
_[Member Type][]_.

MSON 结构实现工具“应该”使用继承优先级，使得在相同缩进级别的列表中，沉余大的 _[成员类型][]_ 应追加或覆盖先前定义的 _[成员类型][]_。

```
# Person (object, fixed)
- `first_name`
- `last_name`
- address (object)
```

- Add/Override Attributes
- 添加/覆盖 属性

    _Example 1_
    _例子 1_

    ```
    - person (Person)
        - `last_name` (optional)
    ```

    Is literally the same as:

    等效于：

    ```
    - person (object)
        - `first_name` (fixed)
        - `last_name` (fixed)
        - address (object, fixed)
        - `last_name` (optional)
    ```

    Which implies a structure the same as:

    意味着与如下结构相同：

    ```
    - person (object)
        - `first_name` (fixed)
        - `last_name` (optional)
        - address (object, fixed)
    ```

    _Example 2_
    _例子 2_

    ```
    - person (object)
        - `first_name` (optional)
        - Include Person
    ```

    Is literally the same as:

    等效于：

    ```
    - person (object)
        - `first_name` (optional)
        - `first_name` (fixed)
        - `last_name` (fixed)
        - address (object, fixed)
    ```

    Which implies a structure the same as:

    意味着与如下结构相同：

    ```
    - person (object)
        - `first_name` (fixed)
        - `last_name` (fixed)
        - address (object, fixed)
    ```

    _Example 3_
    _例子 3_

    ```
    - person (object)
        - Include Person
        - `first_name` (optional)

    ```

    Is literally the same as:

    等效于：

    ```
    - person (object)
        - `first_name` (fixed)
        - `last_name` (fixed)
        - address (object, fixed)
        - `first_name` (optional)
    ```

    Implies a structure the same as:

    意味与如下结构相同：

    ```
    - person (object)
        - `first_name` (optional)
        - `last_name` (fixed)
        - address (object, fixed)
    ```

- Add New Member Types
- 添加新成员类型

    ```
    - person (Person)
        - citizenship
    ```

    Implies a structure the same as:

    意味与如下结构相同：

    ```
    - person (object, fixed)
        - `first_name`
        - `last_name`
        - address (object)
        - citizenship
    ```

- Override Member Types
- 重写成员类型

    ```
    - person (object)
        - Include Person
        - address (string)
    ```

    Is literally the same as:

    等效于：

    ```
    - person (object)
        - `first_name` (fixed)
        - `last_name` (fixed)
        - address (object, fixed)
        - address (string)
    ```

    Implies a structure the same as:

    意味与如下结构相同：

    ```
    - person (object)
        - `first_name` (fixed)
        - `last_name` (fixed)
        - address (string)
    ```

## 6 Reserved Characters & Keywords
## 6 保留字符和关键字
When using following characters or keywords in a _[Property Name][]_, _[Literal Value][]_ or _[Type Name][]_ the name
or literal MUST be escaped in backticks `` ` ``. Otherwise, a `code span` MAY be used for any arbitrary formatting
and has no specific meaning in an MSON document.

当在 _[属性名][]_, _[文字值][]_ 或者 _[类型名][]_ 或者文字中使用以下字符和关键字时，“必须”通过反引号进行转义 `` ` `` 。
否则，在 MSON 文档中使用 `code span` 处理没有任何特殊含义的任意格式文本。

### 6.1 Characters
### 6.1 字符

`:`, `(`,`)`, `<`, `>`, `{`, `}`, `[`, `]`, `_`, `*`, `-`, `+`, `` ` ``

### 6.2 Keywords
### 6.2 关键字

`Property`, `Properties`, `Item`, `Items`, `Member`, `Members`, `Include`, `One of`, `Sample`

Note keywords are case-insensitive.

注意关键字区分大小写。

### 6.3 Additional Keywords
### 6.3 其他关键字
Following keywords are reserved for future use:

以下关键字为将来保留：

`Trait`, `Traits`, `Parameter`, `Parameters`, `Attribute`, `Attributes`, `Filter`, `Validation`, `Choice`, `Choices`,
`Enumeration`, `Enum`, `Object`, `Array`, `Element`, `Elements`, `Description`

[RFC2119]: https://www.ietf.org/rfc/rfc2119
[RFC2119文档]: https://www.ietf.org/rfc/rfc2119
[Markdown-style link]: http://daringfireball.net/projects/markdown/syntax#link
[Markdown 风格链接]: http://daringfireball.net/projects/markdown/syntax#link
[How to Read the Grammar]: #1-how-to-read-the-grammar
[如何阅读这个语法手册]: #1-如何阅读这个语法手册
[Markdown Syntax]: #11-markdown-syntax
[Markdown 语法]: #11-Markdown语法
[Notational Conventions]: #12-notational-conventions
[符号约定]: #12-符号约定
[Promises]: #13-promises
[承诺]: #13-承诺
[Type]: #2-types
[Types]: #2-types
[类型]: #2-类型
[Base Type]: #21-base-types
[Base Types]: #21-base-types
[基本类型]: #21-基本类型
[Primitive]: #211-primitive-types
[Primitive Type]: #211-primitive-types
[Primitive Types]: #211-primitive-types
[原始类型]: #211-原始类型
[Structure Type]: #212-structure-types
[Structure Types]: #212-structure-types
[结构类型]: #212-结构类型
[Named Type]: #22-named-types
[Named Types]: #22-named-types
[命名类型]: #22-命名类型
[Member Type]: #23-member-types
[Member Types]: #23-member-types
[成员类型]: #23-成员类型
[Property Member Type]: #231-property-member-types
[Property Member Types]: #231-property-member-types
[属性成员类型]: #231-属性成员类型
[Value Member Type]: #232-value-member-types
[Value Member Types]: #232-value-member-types
[值成员类型]: #232-值成员类型

[Type Declaration]: #3-type-declaration
[类型声明]: #3-类型声明
[Named Declaration]: #31-named-declaration
[命名声明]: #31-命名声明
[Generic Named Declaration]: #311-generic-named-declaration
[泛型命名声明]: #311-泛型命名声明
[Property Member Declaration]: #32-property-member-declaration
[属性成员声明]: #32-属性成员声明
[Property Name]: #321-property-name
[属性名]: #321-属性名
[Variable Property Name]: #322-variable-property-name
[可变属性名]: #322-可变属性名
[Value Member Declaration]: #33-value-member-declaration
[值成员声明]: #33-值成员声明
[Value Definition]: #34-value-definition
[Value Definitions]: #34-value-definition
[值定义]: #34-值定义
[Value]: #341-value
[Values]: #341-value
[值]: #341-值
[Literal Value]: #342-literal-value
[文字值]: #342-文字值
[Variable Value]: #343-variable-value
[可变值]: #343-可变值
[Type Definition]: #35-type-definition
[Type Definitions]: #35-type-definition
[类型定义]: #35-type-definition
[Type Specification]: #351-type-specification
[Type Specifications]: #351-type-specification
[类型规范]: #351-type-specification
[Variable Type Specification]: #3511-variable-type-specification
[可变类型规范]: #3511-variable-type-specification
[Type Name]: #352-type-name
[Type Names]: #352-type-name
[类型名]: #352-type-name
[Variable Type Name]: #3521-variable-type-name
[可变类型名]: #3521-可变类型名
[Wildcard Type Name]: #3522-wildcard-type-name
[通配符类型名]: #3522-通配符类型名
[Type Attribute]: #353-type-attribute
[Type Attributes]: #353-type-attribute
[类型属性]: #353-type-attribute
[Description]: #36-description
[Descriptions]: #36-description
[描述]: #36-描述

[Type Section]: #4-type-sections
[Type Sections]: #4-type-sections
[类型片段]: #4-类型片段
[Block Description]: #41-block-description
[Block Descriptions]: #41-block-description
[描述块]: #41-描述块
[Member Type Group]: #42-member-type-group
[成员类型分组]: #42-成员类型分组
[Member Type Separator]: #421-member-type-separator
[成员类型分离器]: #421-成员类型分离器
[Nested Member Type]: #43-nested-member-types
[Nested Member Types]: #43-nested-member-types
[嵌套成员类型]: #43-嵌套成员类型
[Sample]: #44-sample
[Samples]: #44-sample
[样本]: #44-样本
[Default]: #45-default
[Defaults]: #45-default
[默认]: #45-默认
[Validation]: #46-validations
[Validations]: #46-validations
[验证]: #46-验证


[Type Inheritance]: #5-type-inheritance
[类型继承]: #5-类型继承
[Mixin Type]: #51-mixin-type
[混合类型]: #51-单一类型
[One Of Type]: #52-one-of-type
[单一类型]: #52-单一类型
[Generic Named Type]: #53-generic-named-type
[泛型命名类型]: #53-泛型命名类型
[Member Type Precedence]: #54-member-type-precedence
[成员类型优先级]: #54-成员类型优先级

[Reserved Characters & Keywords]: #6-reserved-characters--keywords
[保留字符和关键字]: #6-保留字符和关键字
[Characters]: #61-characters
[字符]: #61-字符
[Keywords]: #62-keywords
[关键字]: #62-关键字
[Additional Keywords]: #63-additional-keywords
[其他关键字]: #63-其他关键字
