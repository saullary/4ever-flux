在 TypeScript 中，`type` 和 `interface` 都可以用来定义对象类型，但它们在语法、能力和使用场景上有显著差异。

## 核心区别对比

| 特性         | `interface`           | `type`                             |
| ------------ | --------------------- | ---------------------------------- |
| **定义方式** | 声明式（declaration） | 别名式（alias）                    |
| **扩展方式** | `extends` 继承        | `&` 交叉类型                       |
| **重复声明** | ✅ 支持声明合并       | ❌ 不支持重复定义                  |
| **适用类型** | 仅对象/函数/类        | 任意类型（联合、元组、基本类型等） |
| **性能**     | 稍快（缓存友好）      | 稍慢（复杂类型计算）               |
| **错误提示** | 更友好（显示继承链）  | 可能显示交叉类型展开               |

## 详细示例

### 1. 基本定义

```typescript
// interface - 声明对象结构
interface User {
  name: string;
  age: number;
}

// type - 类型别名
type UserType = {
  name: string;
  age: number;
};
```

### 2. 扩展方式对比

```typescript
// interface 使用 extends
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}

// type 使用 & 交叉类型
type AnimalType = {
  name: string;
};

type DogType = AnimalType & {
  breed: string;
};

// interface 还可以 extends type
interface Cat extends AnimalType {
  color: string;
}
```

### 3. 声明合并（Declaration Merging）

```typescript
// interface 支持多次声明自动合并
interface Window {
  myLib: any;
}
interface Window {
  myApp: any;
}
// 最终 Window 包含 myLib 和 myApp

// type 不支持，会报错
type MyType = { a: string };
type MyType = { b: string }; // ❌ Error: 重复标识符
```

### 4. type 独有的能力

```typescript
// 1. 联合类型
type Status = "pending" | "success" | "error";
type ID = string | number;

// 2. 元组类型
type Point = [number, number];

// 3. 映射类型
type ReadonlyUser = Readonly<User>;

// 4. 条件类型
type IsString<T> = T extends string ? true : false;

// 5. 工具类型组合
type Nullable<T> = T | null;
type UserKeys = keyof User; // "name" | "age"
```

### 5. 实现类时的差异

```typescript
// 两者都可被类实现
interface IUser {
  name: string;
  greet(): void;
}

type IUserType = {
  name: string;
  greet(): void;
};

// 都可以使用 implements
class Person implements IUser {
  /* ... */
}
class Person2 implements IUserType {
  /* ... */
}
```

## 选择建议

| 场景                           | 推荐        | 理由                 |
| ------------------------------ | ----------- | -------------------- |
| 定义对象/类的结构              | `interface` | 可扩展、支持声明合并 |
| 需要声明合并（如扩展第三方库） | `interface` | 唯一选择             |
| 联合类型、元组、条件类型       | `type`      | interface 无法实现   |
| 复杂类型运算、工具类型         | `type`      | 表达能力更强         |
| 公共 API 类型定义              | `interface` | 错误信息更清晰       |

## 最佳实践

```typescript
// 默认优先使用 interface
interface Props {
  title: string;
}

// 需要联合类型或复杂运算时用 type
type ButtonVariant = "primary" | "secondary" | "danger";

// 组合使用：interface 定义结构，type 定义变体
interface BaseConfig {
  timeout: number;
  retries: number;
}

type StrictConfig = BaseConfig & {
  validate: true;
  schema: object;
};
```

**总结**：`interface` 更适合面向对象的声明式场景，`type` 更适合函数式编程中的类型运算。现代 TypeScript 中两者差距在缩小，但上述差异仍然是选择的关键依据。
