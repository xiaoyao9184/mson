# Markdown Syntax for Object Notation
# Markdown 对象表示语法
This document provides an introduction to Markdown Syntax for Object Notation (MSON), a Markdown syntax
compatible with describing JSON and JSON Schema.

本文档介绍了 Markdown 语法对象表示法（MSON），Markdown语法描述是兼容 JSON 和 JSON Schema 。

## What?
## 是什么？
MSON is a plain-text, human and machine readable, description format for describing data structures in common markup
formats such as JSON, XML or YAML.

MSON 是纯文本的，机器/人类阅读友好的，是通用的描述数据格式的标记语言，就如 JSON XML YAML 一样。

## What for?
## 干什么？
The aim of this description format is to facilitate the discussion (and thus validation) of data structures. The format,
being agnostic to the common markup formats, is well suited for "resource & representations" and "content negotiation"
scenarios.

这种描述格式的目标是促进数据结构的讨论（和验证）。与通用标记格式无关，是非常适合用于“资源与表示”和“内容协商”的场景。

In addition, this format also offers (limited) serialization functionality.

此外，这种格式也提供了（有限）序列化功能。

Similar to the original Markdown to HTML (markup) conversion, MSON enables conversion to other markup formats.

类似原生Markdown到HTML（标记）转换，MSON也可以轻松转到其他标记格式。

## Who & Why?
## 谁 & 为什么？
This format is being developed by [Apiary][] as a part of the [API Blueprint][] syntax to provide a means
for description and validation of HTTP payloads and DRY, media-type agnostic, resource descriptions and to simplify
content-negotiation.

这种格式是由 [Apiary][] 开发作为 [API Blueprint][] 语法的一部分，为描述和校验HTTP payloads和DRY，无关媒体类型，简化资源描述和内容协商。

> **NOTE**: While this document focuses primarily on JSON and JSON Schema examples, the underlying specification will
> ultimately allow producing XML or YAML representations from MSON.

> **注意**：此文档主要关注 JSON 和 JSON Schema 示例，最终规范将允许 MSON 生成 XML 或 YAML 表示。

## Notational Conventions
## 符号约定
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described in [RFC2119][].

这个文档中关键字 “必须”，“必须不”，“要求”，“将要”，“不将要”，“应该”，“不应该”，“推荐”，“可以”，和“可选”的解释在 [RFC2119文档][]中。

## Example 1
## 例子1
A simple `object` structure and its associated JSON expression.

一个基本的 `object` 型结构和它的 JSON 呈现。

#### MSON
#### MSON

```
- id: 1
- name: A green door
- price: 12.50
- tags: home, green
```

#### Rendered Markdown
#### Markdown 呈现

- id: 1
- name: A green door
- price: 12.50
- tags: home, green

#### JSON
#### JSON

```json
{
    "id": "1",
    "name": "A green door",
    "price": "12.50",
    "tags": [ "home", "green" ]
}
```

>**NOTE:** By default, a Markdown list item is considered to be a `string` type.

>**注意：** 默认的，Markdown列表项是 `string` 类型。

---

## Example 2
## 例子2
A Named Type with its associated JSON expression and JSON Schema.

命名类型的相关 JSON 和 JSON Schema 展示。

#### MSON
#### MSON

```
# Product
A product from Acme's catalog

## Properties

- id: 1 (number, required) - The unique identifier for a product
- name: A green door (string, required) - Name of the product
- price: 12.50 (number, required)
- tags: home, green (array[string])
```

#### Rendered Markdown
#### Markdown 呈现

##### Product
##### 产品
A product from Acme's catalog

一个来自Acme目录的产品。

###### Properties
###### 属性

- id: 1 (number, required) - The unique identifier for a product
- name: A green door (string, required) - Name of the product
- price: 12.50 (number, required)
- tags: home, green (array[string])

#### JSON
#### JSON

```json
{
    "id": 1,
    "name": "A green door",
    "price": 12.50,
    "tags": [ "home", "green" ]
}
```

>**NOTE:** The `id` and `price` sample values are numbers given the explicit declaration of their base type of `number`
> vs. the default of `string` as in [Example 1](#example-1).

>**注意：** `id` 和 `price` 样本值是明确被定义为 `number` 类型，默认的 `string` 类型在[例子 1](#例子-1).

#### JSON Schema
#### JSON Schema

```json
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "title": "Product",
    "description": "A product from Acme's catalog",
    "type": "object",
    "properties": {
        "id": {
            "description": "The unique identifier for a product",
            "type": "number"
        },
        "name": {
            "description": "Name of the product",
            "type": "string"
        },
        "price": {
            "type": "number"
        },
        "tags": {
            "type": "array",
            "items": {
                "type": "string"
            }
        }
    },
    "required": ["id", "name", "price"]
}
```

> **NOTE:** This proposal covers only basic features of JSON Schema. At this moment, it is out of the scope of this
> syntax to support all the JSON Schema keywords (such as `uniqueItems`, `exclusiveMinimum`, etc.).

> **注意：** 这项提案仅仅涵盖 JSON Schema 的基本功能。目前为止，还未支持所有的 JSON Schema 关键字（例如 `uniqueItems` ， `exclusiveMinimum` 等）。

---

## MSON Language Specification
## MSON 语法规范
The rest of this document covers some advanced syntax examples. Refer to the [MSON Language Specification][] for the
complete MSON Grammar Reference.

本文档的其余部分介绍了一些高级语法示例。请参阅完整的MSON语法参考 [MSON 语法规范][] 。

## Quick Links

- [MSON Language Specification][]
- [MSON 语法规范][]
- [Objects & Arrays](#objects--arrays)
- [对象 & 数组](#对象--数组)
- [Advanced Objects](#advanced-objects)
- [高级对象](#高级对象)
- [Advanced Arrays](#advanced-arrays)
- [高级数组](#高级数组)
- [Escaping](#escaping)
- [转义](#转义)
- [Multi-line Descriptions](#multi-line-descriptions)
- [多行描述](#多行描述)
- [Variable Property Name](#variable-property-name)
- [变量属性名](#变量属性名)
- [Type Definition](#type-definition)
- [类型定义](#类型定义)
- [Referencing](#referencing)
- [引用](#引用)
- [Mixins](#mixins)
- [混合](#混合)

## Objects & Arrays
## 对象 & 数组
By default, a Markdown list item with a nested Markdown list is considered to be an `object` structure:

默认的， Markdown列表嵌套了列表项的结构是 `object` ：

#### MSON
#### MSON
```
- address
    - street
    - city
    - state
```

#### JSON
#### JSON
```json
{
    "address" : {
        "street": "",
        "city": "",
        "state": ""
    }
}
```

If a Markdown list's items are intended to be literals (represent array values), the type of the parent list item MUST
be explicitly set to `array`:

如果Markdown列表项的本意是文字（代表数组值），父级列表项的类型必须明确设置为`array`：

#### MSON
#### MSON
```
- address (array)
    - street
    - city
    - state
```

Or, alternately:

或者, 代替为:

```
- address: street, city, state (array)
```

In this latter case, using a comma-separated list of values, the type `(array)` is implied and thus MAY be omitted.

在后一种情况下，用逗号分隔的值列表，类型`(array)`是隐含的因而“可以”被省略。

#### JSON
```json
{
    "address": [ "street", "city", "state" ]
}
```

> **NOTE:** The values "street", "city", and "state" are solely sample values of the `address` array in this example.
> No constraints are implied on the quantity or types of values in such an array other than that they MAY be `string`
> literals.

> **注意：** 本例中 `address` 数组中"street", "city", and "state"是单独的样本值。
> 由于没有约束，隐含意味着数组中的元素数量“可以”任意，值类型则是 `string` 文本值。

## Advanced Objects
## 高级对象

### Non-uniform Property
### 非严格属性
A Property whose value can be of different types is defined by the `enum` structure type:

`enum` 结构类型的属性值可以是不同类型：

#### MSON
#### MSON

```
- tag (enum)
    - green (string)
    - (object)
        - tag_id: 1
        - label: green
```

#### Rendered Markdown
#### Markdown 呈现

- tag (enum)
    - green (string)
    - (object)
        - tag_id: 1
        - label: green

#### JSON
#### JSON

```json
{
    "tag": "green"
}
```

**or**

**或者**

```json
{
    "tag": {
        "tag_id": "1",
        "label": "green"
    }
}
```

>**NOTE:** In an `enum` structure, in contrast to an `array` type structure, a value like "green" is a fully-qualified
>value of the enumeration vs. being a sample value.

>**注意：** `enum` 结构，相对于 `array` 类型结构，枚举类型中的值是完全限定的，例如样本值"green"。

---

### Mutually Exclusive Properties
### 互斥属性
By default, all properties are optional and may or may not be included in the object. If there is a choice of
mutually exclusive properties available MSON defines a `One Of` type:

默认的，所有属性是可选的，可以包含也可以不包含在对象中。如果有互斥属性请使用MSON `One Of` 定义类型：

#### MSON
#### MSON
```
- city
- One Of
    - state
    - province
- country
```

#### Rendered Markdown
#### Markdown 呈现

- city
- One Of
    - province
    - state
- country

#### JSON
#### JSON
```json
{
    "street": "",
    "province": "",
    "country": ""
}
```

**or**

**或**

```json
{
    "street": "",
    "state": "",
    "country": ""
}
```

>**NOTE:** Because an `enum` type MUST define a list of types vs. properties and by default an un-nested Markdown list
defines properties of an implied `object` structure, the `One Of` type declaration MUST only be used to indicate
mutually exclusive properties in an `object` structure.

>**注意：** 因为 `enum` “必须”定义一个列表。而默认的非嵌套 Markdown 列表隐含定义一个 `object` 对象结构的，
> `One Of` 类型声明“必须”只能用于表示 `object` 结构中的互斥属性。

---

## Advanced Arrays
## 高级数组

### Array of Mixed Types
### 混合型数组

#### MSON
#### MSON

```
- tags (array)
    - hello (string)
    - 42 (number)
```

#### Rendered Markdown
#### Markdown 呈现

- tags (array)
    - hello (string)
    - 42 (number)

#### JSON
#### JSON

```json
{
    "tags": [ "hello", 42 ]
}
```

---

#### MSON
#### MSON

```
- (array)
    - (object)
        - name: snow (string)
        - description (string)
    - 42 (number)
```

#### Rendered Markdown
#### Markdown 呈现

- (array)
    - (object)
        - name: snow (string)
        - description (string)
    - 42 (number)

#### JSON
#### JSON

```json
[
    {
        "name": "snow",
        "description": ""
    },
    42
]
```

---

### Array of Arrays
### 数组嵌套

#### MSON
#### MSON

```
- (array)
    - 1, 2, 3, 4 (array[number])
```

#### Rendered Markdown
#### Markdown 呈现

- (array)
    - 1, 2, 3, 4 (array[number])

#### JSON
#### JSON

```json
[
    [ 1, 2, 3, 4 ]
]
```

---

## Multi-line Descriptions
## 多行描述
In the case where a one-liner description is not sufficient, a multi-paragraph text block is the way to go.

在单行描述是不满足的情况下，多段落文本块是更好的方法。

#### MSON
#### MSON

```
- id: 1 (number, required) - The unique identifier for a product
- name: A green door (string, required)

    Lorem ipsum dolor sit amet, consectetur adipiscing elit.

    Sed sed lacus a arcu vehicula ultricies sed vel nibh. Mauris id cursus felis.

    Interdum et malesuada fames ac ante ipsum primis in faucibus.

    - unus
    - duo
    - tres
    - quattuor

- price: 12.50 (number, required)
- tags: home, green (array)
```

For a multi-line description of a structure type, an `Items`, `Members` , or `Properties` keyword MUST be used to avoid
conflict with potential list item values that are part of the description:

对于包含多行描述的结构类型，“必须”使用 `Items` ， `Members` ，或者 `Properties` 关键字来避免与描述中潜在列表项冲突：

```
- tags (array)

    Lorem ipsum dolor sit amet, consectetur adipiscing elit.

    Sed sed lacus a arcu vehicula ultricies sed vel nibh. Mauris id cursus felis.

    Interdum et malesuada fames ac ante ipsum primis in faucibus.

    - unus
    - duo
    - tres
    - quattuor

    - Items
        - home
        - green
```

>**NOTE:** Unus ... quattuor are considered part of the text block vs. defining items of the array.

>**注意：** Unus 到 quattuor 被视为文本块的一部分与数组项区分开。

## Escaping
## 转义
Markdown [code span][] element syntax (`` ` ` ``) is used to escape reserved Keywords that should just be interpretted
as literals as well as other constructs that may be erroneously interpreted by an MSON parser as meaningful.

Markdown [code span][] 元素语法(`` ` ` ``) 用来转义保留关键字，被包含的关键字只会被解析为文字，这样不会被MSON解析器错误地解释为其他有意义的元素。

For non-Keywords, a [code span][] can be used for formatting Markdown as an aesthetic preference.

对于非关键字，[code span][] 可用于格式化 Markdown 作为审美偏好。

#### MSON
#### MSON

```
- listing (object)

    Our real estate listing has different properties available.

    - `Properties`
        - This one.
        - That one.

    - Properties
        - description (string)
        - date_listed (string)
        - `some:location`: local (string)
```

#### Rendered Markdown
#### Markdown 呈现

- listing (object)

    Our real estate listing has different properties available.

    - `Properties`
        - This one.
        - That one.

    - Properties
        - description
        - date_listed
        - `some:location`: local (string)

>**NOTE:** In this example, the first "Properties" string is part of the multi-line block description whereas the second
> defines the properties of the `listing` object.

>**注意：** 这个例子中，第一"Properties"字符串是多行块描述的一部分，而第二个"Properties"定义是 `listing` 的属性。

---

## Variable Property Name
## 变量属性名
Variable property name (key) is defined using *italics*. Note that a variable property cannot be required.

变量属性名（键）采用 *斜体* 定义​的。注意，变量属性名不是必须项。

#### MSON
#### MSON

```
- _links
    - *self*
        - href: a URI
```

#### Rendered Markdown
#### Markdown 呈现

- _links
    - *self*
        - href: a URI

#### JSON
#### JSON

```json
{
    "_links": {
        "self": {
            "href": "..."
        },
        "users": {
            "href": "..."
        }
    }
}
```

---

## Type Definition
## 类型定义
Additional Named Types can be defined using a Markdown header:

其他命名的类型可以使用 Markdown 头进行定义：

#### MSON
#### MSON

```
# Address (object)
Description is here! Properties to follow.

## Properties
- street
- state
- zip
```

The same entity defined as an `address` property:

相同实体 `address` 的属性定义方法:

```
- address (object)

    Description is here! Properties to follow.

    - Properties
        - street
        - state
        - zip
```

The same `address` property referencing the previously Named type:

 `address` 属性引用先前定义的命名类型:

```
- address (Address)
```

## Referencing
## 引用
Anywhere a type is expected, a top-level MSON Named Type can be referenced.

在类型的任何地方，都可以引用顶层 MSON 命名类型。

#### MSON
#### MSON

```
# Address (object)
- street
- city
- state
- zip

# User (object)
- first_name
- last_name
- address (Address)
```

#### Rendered Markdown
#### Markdown 呈现

##### Address (object)
- street
- city
- state
- zip

##### User (object)
- first_name
- last_name
- address (Address)

#### JSON

```json
{
    "first_name": "",
    "last_name": "",
    "address": {
        "street": "",
        "city": "",
        "state": "",
        "zip": ""
    }
}
```

---

## Mixins
## 混合
To include (mixin) values or properties in another Named Type use the `Include` keyword followed by a reference to the  
MSON Named Type.

要在其他命名类型（混入）值或属性，请使用 `Include` 关键字连接 MSON 命名类型。

#### MSON
#### MSON

```
# Address Object
- street
- city
- state
- zip

# User Object
- first_name
- last_name
- Include Address
```

#### Rendered Markdown
#### Markdown 呈现

##### Address Object
- street
- city
- state
- zip

##### User Object
- first_name
- last_name
- Include Address

#### JSON
#### JSON

```json
{
    "first_name": "",
    "last_name": "",
    "street": "",
    "city": "",
    "state": "",
    "zip": ""
}
```

>**NOTE:** A mixin can only use a Named Type that is derived from the same type of structure including the mixin.
> Further, the parent structure inherits all the members of the included Named Type and maintains the order the
> members were originally defined.

>**注意：** 一个混合类型只能使用派生自相同类型结构的混合类型。
> 进一步讲，使用混合类型的结构继承了包括命名类型在内的所有成员，并保持最初定义的成员的顺序。

[API Blueprint]: https://github.com/apiaryio/api-blueprint
[code span]: http://daringfireball.net/projects/markdown/syntax#code
[@zdne]: https://github.com/zdne
[Apiary]: http://apiary.io
[RFC2119]: https://www.ietf.org/rfc/rfc2119
[RFC2119文档]: https://www.ietf.org/rfc/rfc2119
[MSON Language Specification]: MSON%20Specification.md
[MSON 语法规范]: MSON%20Specification.md
