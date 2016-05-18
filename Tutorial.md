# MSON Tutorial
# MSON 教程

MSON is short for Markdown Syntax for Object Notation, and it's a way to represent data structures in a human readable plain text form. This tutorial will take you though the basics of MSON and how you can use MSON to describe a data structure.

MSON 是 Markdown 语法子集用于描述对象符号，用纯文本格式表示数据结构的方法可轻松让人类阅读。本教程入门将告知如何使用MSON来描述数据结构。

> **NOTE:** **Additional MSON Resources**
> **注意:** **额外 MSON 资源**
>
> + [MSON Specification](https://github.com/apiaryio/mson/blob/master/MSON%20Specification.md)
> + [MSON 规范](https://github.com/apiaryio/mson/blob/master/MSON%20Specification.md)
> + [Examples](https://github.com/apiaryio/mson#notational-conventions)
> + [例子](https://github.com/apiaryio/mson#notational-conventions)

## Data structures in MSON
## MSON 中的数据结构

To get started, we're going to create a data structure in MSON to represent a Person which has a name.

在开始之前，我们要创建一个 MSON 数据结构来表示一个具有名称的人。

A data structure to store a Person could be represented in MSON using the following:

存储一个人的数据结构可以在MSON使用如下方法表示：

```apib
# Person

+ name
```

Here we've declared our own named type called "Person". A heading is one or more `#` symbols followed by a string representing the name of our data structure. By default, named types like `Person` are object types.

在这里，我们定义我们自己命名的类型名为“Person”。一个或多个 `#` 符号后面的字符串标题代表我们定义的数据结构的名称。默认的，像 `Person` 这样命名的类型是对象类型。

An object is constructed with properties, and in this case we've listed them below the heading in a list. Lists are created by putting each list item on its own line and preceding each line with either a `+`, `*` or `-`.

一个对象通过属性构建，在这种情况下，我们在标题下面罗列属性列表。列表是通过每一行列表项加前缀 `+`， `*` 或 `-` 创建的。

In our `Person` data structure, we have a single property called `name`. Similarly to our Person definition, we can declare the type that our property is, with round brackets. For example, we can declare that our name is a string using `+ name (string)`. By default, properties on objects are string's unless specified to another type, as in our above example we have omitted the string type definition.

在我们的 `Person` 数据结构中，有一个命名了一个属性 `name` 。同样我们的Person定义，我们可以通过小括号声明对象属性的类型。例如，我们声明name的类型为string `+ name (string)` 。 默认的，对象中没有明确指定其他类型的属性是字符串类型，正如上面的例子中，我们省略了字符串类型定义。

We can attach a description for our name property by following the type definition with a dash (`-`) followed by the description.

我们可以通过连接符(`-`)连接类定义和描述。

```apib
+ name (string) - The Person's name
```

We may also specify a sample value for the person's name by preceding the property name by a colon (`:`) and then the value.

我们也可以用一个冒号(`:`)，在该属性名称后面指定person name的样本值。

```apib
+ name: Kyle (string) - The Person's name
```

**NOTE**: *It's important to note, that if a sample value contains reserved characters such as `:`, `(`,`)`, `<`, `>`, `{`, `}`, `[`, `]`, `_`, <code>&ast;</code>, `-`, `+`, `` ` `` then the sample value must be wrapped in a code-block using back-ticks:*

**NOTE**: *非常重要，如果一个样本值包含保留字符，如`:`, `(`,`)`, `<`, `>`, `{`, `}`, `[`, `]`, `_`, `<code>&ast;</code>`, `-`, `+`, `` ` `` 那么样本值必须被包裹在一个码块中*

```apib
+ name: `Spencer-Churchill` (string) - The Person's name
```

So far we have used the `object` and `string` types. MSON includes a total of 6 base types. Three of these base types are primitive types such as `boolean`, `string` and `number`. There are also three structure types called `array`, `enum` and `object`. Let's use some of these new types to create another data structure.

到目前为止，我们已经使用的 `object` 和 `string` 类型。MSON 包含6种基本类型。其中三种基本类型，如 `boolean` ， `string` 和 `number` 。其他3中结构类型 `array` ， `enum` 和 `object` 。让我们使用这些新的类型创建其他数据结构。

```apib
# Company

+ name: Apiary
+ founder (Person)
+ founded: 2011 (number) - The year in which the company was founded
```

### Inheritance
### 继承

When declaring a named type, you may also inherit from another type. For example, we could declare a data structure called "Administrator" which inherits from the `Person` type.

声明命名类型，你也可以从另一个类型继承。例如，我们声明一个数据结构称为“Administrator”它是继承自 `Person` 类型的。

```apib
# Administrator (Person)

+ role (string) - The administrators role
```

When inheriting from another data structure, all of the parents properties will be inherited. For example, our `Administrator` structure will contain the `name` property from our previous definition.

当继承自其他数据结构时，所有的父级属性将被继承。例如，我们的 `Administrator` 结构将包含 `name` 属性而其定义来自之前的Person。

#### Nesting
#### 嵌套

It's also possible to nest other data structures directly without a data structure instead of referencing another type as we have done above between our `Company` and `Person`.

也可以直接嵌套其他数据结构，而不是引用其他结构，像 `Company` 引用 `Person` 一样。

```apib
# Company

+ name: Apiary
+ founder (Person)
+ founded: 2011 (number) - The year in which the company was founded
+ address
    + street: 235 Ninth Street
    + city: San Francisco
    + state: California
```

In this example, we've declared a property called `address` which is a nested structure within our `Company`.

在这个例子中，我们已经声明了一个名为 `address` 的属性嵌套在 `Company` 结构中。

**NOTE**: *In this case, since we have inline properties within our address property, the default type for the address is object instead of string.*

**注意**：*在这种情况下，因为地址属性中内嵌其他属性，默认类型为对象，而不是字符串。*

## Additional Learning
## 其他学习

You can find more [examples](https://github.com/apiaryio/mson#example-1) of MSON, along with additional information from the [MSON Specification](https://github.com/apiaryio/mson/blob/master/MSON%20Specification.md).

你可以通过MSON [例子](https://github.com/apiaryio/mson#example-1) ，补充附加 [MSON 规范](https://github.com/apiaryio/mson/blob/master/MSON%20Specification.md) 。
